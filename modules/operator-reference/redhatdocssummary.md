# OpenShift AI: Monitoring, Observability, and Metrics Reference Guide

## 1. Centralized Observability Stack Overview
Red Hat OpenShift AI provides a centralized platform observability stack that offers an integrated, out-of-the-box solution for monitoring the health and performance of the instance and user workloads. 

The stack architecture utilizes the following OpenShift components:
* **Cluster Observability Operator**: Deploys and manages Prometheus (for metrics collection) and Alertmanager (for monitoring alerts).
* **Tempo Operator**: Provides the Red Hat build of Tempo backend for distributed tracing.
* **Red Hat build of OpenTelemetry**: Deploys the OpenTelemetry Collector (OTC) to standardize data ingestion, collection, and exporting of telemetry data.

### Enabling the Stack
To activate the centralized observability stack, a cluster administrator must configure the `DataScienceClusterInitialization` (DSCI) custom resource. This involves setting `spec.monitoring.managementState` to `Managed`. The observability components are deployed into the `redhat-ods-monitoring` namespace. 

## 2. Collecting Metrics from User Workloads
By default, metric collection is not automatically active for all user-deployed workloads. To gather metrics from specific user workloads (e.g., custom workbench servers, training jobs, or inference services) that expose a `/metrics` endpoint:

* **Label Requirement**: You must add the `monitoring.opendatahub.io/scrape: 'true'` label directly to the pod template in the workload's deployment configuration (`spec.template.metadata.labels`) .
* **Operator Warning**: Do not apply this label to operator-managed workloads, as the managing operator may overwrite or remove the label during reconciliation cycles .

## 3. Model Serving and Inference Metrics
Models deployed on the model serving platform can be monitored for performance and resource usage metrics. 

* **Supported Configurations**: Metrics are supported for models deployed using preinstalled model-serving runtimes or custom runtimes duplicated from preinstalled ones . 
* **Standard Performance Metrics** :
    * **Number of requests**: Succeeded or failed requests for a specific model.
    * **Average response time (ms)**: The average time taken to respond.
    * **CPU utilization (%)**: Percentage of the CPU limit per model replica currently utilized.
    * **Memory utilization (%)**: Percentage of the memory limit per model replica utilized.

### Runtime-Specific Queries
Cluster administrators or users with the `monitoring-rules-view` role can run PromQL queries in the OpenShift web console Developer perspective :
* **vLLM Runtime**: `sum(increase(vllm:request_success_total{namespace=${namespace}, model_name=${model_name}}[${rate_interval}]))` . 
    * *Note: vLLM metrics are only generated and available after an initial inference request is successfully processed by the deployed model* .
* **OpenVINO Model Server (OVMS)**: `sum(increase(ovms_requests_success{namespace=${namespace},name=${model_name}}[${rate_interval}]))` .

## 4. NVIDIA NIM Model Observability
For models deployed via the NVIDIA NIM model serving platform, OpenShift AI provides specific telemetry data out-of-the-box (accessible via the NIM Metrics tab) :
* GPU cache usage over time (ms)
* Current running, waiting, and max requests count
* Tokens count
* Time to first token
* Time per output token
* Request outcomes

## 5. Models-as-a-Service (MaaS) and LLM Governance
When managing LLMs at scale using Models-as-a-Service (MaaS), observability acts as a critical governance layer :
* **Usage Tracking & Cost Control**: MaaS tracks consumption metrics (token consumption and API requests) for cost allocation and billing across different teams/tiers .
* **Observability Insights**: Monitors model access patterns, policy enforcement checks, and resource utilization.
* **Rate Limiting Metrics**: Clients can monitor their API quotas and limits directly through HTTP response headers, which include `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`, and `Retry-After` .

## 6. External Exporters and Distributed Tracing
OpenShift AI can seamlessly integrate with existing enterprise observability tools. 

### Exporting Metrics
Metrics can be exported to external platforms (e.g., Grafana, Prometheus, or OTLP-compatible backends) by modifying the `spec.monitoring.metrics.exporters` field in the DSCI resource [. 
* **Configurations**: You can define the export `type` (`otlp` or `prometheusremotewrite`) and the external `endpoint` URL . 
* The OpenTelemetry Collector automatically reloads and forwards metrics once saved.

### Distributed Tracing (Tempo)
OpenShift AI uses Tempo as the tracing backend.
* **OTLP Ingestion**: Instrumented applications must export traces to the OpenTelemetry Collector service (`data-science-collector`) via gRPC (port 4317) or HTTP (port 4318) .
* **Visualization**: To view traces in tools like Jaeger or Grafana, administrators can port-forward or expose the `tempo-query` or `tempo-query-frontend` service on port 3200 .

## 7. Node, GPU, and Cluster-Level Diagnostics
For physical resources and infrastructure management, observability is heavily reliant on OpenShift cluster tools and Operator logs.

### GPU Verification and Capacity
Administrators can check for GPU availability and node assignment using standard OpenShift CLI tools :
* **NVIDIA GPUs**: Use `oc describe node <node_name>` and verify that `nvidia.com/gpu` appears in the `Capacity` and `Allocatable` blocks .
* **AMD GPUs**: Similarly, verify that `amd.com/gpu` appears in the `Capacity` and `Allocatable` blocks . Furthermore, `lspci | grep -E "MI210|MI250|MI300"` or the `rocminfo` command can provide detailed driver/hardware status .

### Platform Logs and Auditing
* **Operator Logger**: The OpenShift AI Operator log level can be configured at runtime in the DSCI using `.spec.devFlags.logmode`. Values can be set to `development` (plaintext, INFO/WARN levels) or `production` (JSON format, INFO/ERROR levels) .
* **Audit Records**: Administrators can view historical changes made to OpenShift AI configurations (like DSC and DSCI resources) by querying the OpenShift API server audit logs (`kube-apiserver/audit.log`) . Setting the audit log policy to `WriteRequestBodies` allows inspection of the full content of changed custom resources. 
* **Built-in Alerts**: A Prometheus Alertmanager instance provides built-in alerts for OpenShift AI components (e.g., crashing pods, operator downtime) and can be accessed locally by port-forwarding the `data-science-monitoringstack-alertmanager` service on port `9093`.