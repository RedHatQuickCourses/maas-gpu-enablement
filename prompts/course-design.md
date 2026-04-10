# Red Hat Product and Technical Learning Team
## Nvidia GPU Enablement: Course High Level Design

### COURSE GOAL
To equip architects, engineers, and administrators with the knowledge and skills required to configure, manage, and monitor NVIDIA GPU Accelerators on OpenShift. This course serves as the foundational hardware enablement layer for a Models-as-a-Service (MaaS) architecture, ensuring teams can utilize and support these components as part of a revenue-generating services business. Participants will learn to map the foundational GPU strategy using the NVIDIA GPU Operator stack and comprehensive observability patterns.

*(Note: GPU Quota, Priority, and Job Scheduling via Kueue are covered in a subsequent module within the MaaS learning path).*

### TARGET AUDIENCE
* **Platform Engineers**: Responsible for designing and deploying model serving environments and enabling MaaS.
* **DevOps/SREs**: Focused on observability, operational scale, tracking consumption metrics, and cost allocation.

### PREREQUISITES
* Familiarity with Kubernetes and Red Hat OpenShift Container Platform.
* Basic understanding of machine learning concepts and Red Hat OpenShift AI.
* Basic networking, routing, and understanding of Kubernetes operators.
* Familiarity with REST APIs, Prometheus metrics, and RBAC within OpenShift.

### COURSE DESIGN

| Section | Format | Topics & Activities |
| :--- | :--- | :--- |
| **Learning Objective 1: Understand and Install Foundational Operators** | Presentation | **Deconstructing the Hardware Stack:**<br>Understand the "GPU Silo" crisis and how the NVIDIA GPU Operator automates the management of NVIDIA software components. Define the core components that power the GPU stack:<br>• **Node Feature Discovery (NFD):** Scans the node's hardware (via PCI IDs) and applies Kubernetes labels so the scheduler knows where GPUs physically exist.<br>• **NVIDIA Driver Container:** Deploys the necessary NVIDIA GPU drivers directly via containers, removing the need to manually install kernel modules on the host OS.<br>• **NVIDIA Container Toolkit:** Plugs into the OpenShift container runtime (CRI-O) to ensure pods can securely request and access the underlying GPU hardware.<br>• **GPU Feature Discovery (GFD):** Gathers granular hardware capabilities (GPU model, VRAM size, MIG profiles) and applies them as specific node labels.<br>• **DCGM (Data Center GPU Manager):** A daemon that continuously monitors GPU health, diagnostics, and telemetry.<br>• **DCGM Exporter:** Extracts metrics from DCGM and formats them for Prometheus scraping. |
| | Lab | **Deploying the Base Stack:**<br>Install the NFD Operator. Create the `nvidia-gpu-operator` Namespace, OperatorGroup, and Subscription. Apply a customized `ClusterPolicy` to configure the deployment of the underlying components (Driver, Toolkit, GFD). Verify successful installation by inspecting the daemonset pods. |
| **Learning Objective 2: Configure Multi-Instance GPU (MIG) for MaaS** | Presentation | **Maximizing GPU ROI:**<br>Understand how the Multi-Instance GPU (MIG) feature splits hardware resources into multiple GPU instances, operating completely isolated from each other. Evaluate MIG advertisement strategies: Single (homogeneous) vs. Mixed (heterogeneous) slicing. |
| | Lab | **MIG Slicing:**<br>Update node labels to apply a MIG partitioning profile (e.g., `nvidia.com/mig.config=all-1g.10gb`). Create a custom `mig-parted` config resource file for specific hardware deployments. Verify that the sliced MIG instances are exposed as allocatable resources on the node. |
| **Learning Objective 3: Monitor GPU Telemetry and Health (Grafana Operator)** | Presentation | **The MaaS Observability Stack:**<br>Understand how hardware telemetry flows up to the platform observability plane. Discuss the integration between OpenShift's built-in monitoring (Prometheus/Thanos) and standalone visualization using the Grafana Operator for platform, node, and accelerator metric correlation. |
| | Lab | **Exposing Metrics:**<br>Enable OpenShift user-workload monitoring by modifying the `cluster-monitoring-config` configmap. Label the GPU Operator namespace to expose GPU telemetry for Prometheus via the NVIDIA DCGM Exporter. |
| | Lab | **Deploying the Grafana Operator & Setting Up Access:**<br>Install the community or Red Hat Grafana Operator from OperatorHub and create a Grafana instance Custom Resource (CR). <br><br>Set up secure access to the cluster's metrics by:<br>1. Creating a dedicated ServiceAccount (e.g., `grafana-sa`).<br>2. Granting the ServiceAccount the `cluster-monitoring-view` ClusterRole so it can securely read OpenShift platform metrics.<br>3. Extracting the ServiceAccount token and creating a `GrafanaDatasource` CR that points directly to the OpenShift `thanos-querier` endpoint. |
| | Lab | **Visualizing the Hardware:**<br>Access the custom Grafana instance route. Import and customize the NVIDIA DCGM Exporter Dashboards to view interconnected metrics, mapping standard node resources (CPU/RAM) alongside accelerator metrics (GPU Power Usage, Temperature, Tensor Core Utilization, and MIG instance allocations). |

### VIRTUAL LABS (CLASSROOM) REQUIREMENTS
* **Hardware Acceleration**: This course requires significant hardware acceleration (GPUs) in the lab environment. 
* **Distributed Architecture**: Cluster environments must be capable of supporting distributed inference (llm-d), meaning multi-GPU node availability is required.
* **MIG Capabilities**: To perform the MIG labs, nodes must feature supported Ampere or Hopper architecture cards (e.g., A100, A30, H100).
* **Cluster Version**: The OpenShift Container Platform must be running version 4.10 or higher to support custom Grafana Operator metrics extraction.

### OVERALL COURSE TIMINGS

| Chapter/Section | Estimated Time |
| :--- | :--- |
| **LO 1:** Understand and Install Foundational Operators | 75 minutes |
| **LO 2:** Configure Multi-Instance GPU (MIG) for MaaS | 90 minutes |
| **LO 3:** Monitor GPU Telemetry and Health (Grafana Operator) | 75 minutes |
| **Course Total:** | **4 Hours 0 Minutes** |