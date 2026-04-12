# Course Terminology Reference

This document maintains canonical definitions for all technical terms used across the course. Use these exact definitions to ensure consistency.

**Last Updated**: 2026-04-11
**Maintainer**: Course authors

---

## How to Use This Document

1. **When writing new content**: Check this document first before defining any technical term
2. **On first use of a term**: Reference the chapter where it was first defined
3. **When introducing new terms**: Add the canonical definition here after the content is approved
4. **When updating definitions**: Update here and note which chapters need updating

---

## Operators and OLM

### Operator
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> A Kubernetes operator combines three essential components: (1) Custom Resource (CR) expressing desired state, (2) Controller software that watches CRs and reconciles cluster state, and (3) Reconciliation Loop that continuously monitors and corrects drift.

**First Defined**: Chapter 1, Section 2 (Understanding Operators and Platform Automation)

**Key Characteristics**:
- Encodes human operational knowledge into software
- Provides self-healing automation
- Uses declarative configuration

### Custom Resource (CR)
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> A Custom Resource is an instance of a Custom Resource Definition (CRD)—your actual configuration that declares desired state for an operator to reconcile.

**First Defined**: Chapter 1, Section 2

**Example**: ClusterPolicy for NVIDIA GPU Operator

### Custom Resource Definition (CRD)
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> A CRD is a schema that defines a new resource type in Kubernetes. It specifies API group, version, resource kind, allowed fields, and validation rules.

**First Defined**: Chapter 1, Section 2

**Relationship**: CRD defines the schema; CR is an instance of that schema

### Controller
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Controller is software that watches for changes to Custom Resources, compares desired state (CR spec) to actual state (cluster resources), and takes actions to reconcile differences. Controllers run in a continuous loop.

**First Defined**: Chapter 1, Section 2

### Reconciliation Loop
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> The reconciliation loop is the continuous cycle where a controller: (1) OBSERVE—read current cluster state, (2) DIFF—compare to desired state in CR, (3) ACT—make changes to align, (4) REPEAT—every ~5 seconds.

**First Defined**: Chapter 1, Section 2

**Visual Reference**: See ASCII diagram in ch1-gpu-operator/s2-operators-overview.adoc

### Operator Lifecycle Manager (OLM)
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> OpenShift's Operator Lifecycle Manager (OLM) is a built-in framework for discovering, installing, and managing operators. It functions as a "package manager for operators" similar to how yum or apt manages system packages.

**First Defined**: Chapter 1, Section 2

### ClusterServiceVersion (CSV)
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> A ClusterServiceVersion (CSV) represents a specific version of an installed operator. It contains operator metadata, deployment specification, CRDs the operator manages, RBAC requirements, and upgrade path information.

**First Defined**: Chapter 1, Section 2

**CSV Phases**: Pending, Installing, Succeeded, Failed, Replacing

### Subscription
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> A Subscription declares your intent to install and maintain an operator. It specifies which operator to install, which catalog contains it, which update channel to track, and whether upgrades should be automatic or manual.

**First Defined**: Chapter 1, Section 2

**Key Fields**: channel, name, source, sourceNamespace, installPlanApproval

### InstallPlan
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> An InstallPlan is OLM's execution plan for installing or upgrading an operator. It lists which CSV version to install, CRDs to create or update, and RBAC resources to configure.

**First Defined**: Chapter 1, Section 2

**Approval Modes**: Automatic (dev/test), Manual (production)

### OperatorGroup
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> An OperatorGroup defines the scope where an operator can manage resources. It configures which namespaces the operator watches (single, multiple, or all) and controls RBAC generation for operator permissions.

**First Defined**: Chapter 1, Section 2

### CatalogSource
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> A CatalogSource represents a repository of available operators. It points to a catalog index container image that OLM queries to discover operators.

**First Defined**: Chapter 1, Section 2

**Default Catalogs**: redhat-operators, certified-operators, community-operators, redhat-marketplace

### Cluster Operator
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Cluster operators are core OpenShift platform components managed by the Cluster Version Operator (CVO). They provide essential platform services like authentication, DNS, and ingress. Cluster operators cannot be uninstalled and are automatically upgraded with OpenShift.

**First Defined**: Chapter 1, Section 2

**Examples**: authentication, dns, ingress, network, storage

**Location**: openshift-* namespaces

### Add-on Operator
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Add-on operators extend OpenShift with additional capabilities. They are user-managed through OLM, have user-controlled lifecycle, and are installed in user-created namespaces.

**First Defined**: Chapter 1, Section 2

**Examples**: Node Feature Discovery, NVIDIA GPU Operator, Red Hat OpenShift AI

---

## GPU Components and Stack

### Node Feature Discovery (NFD)
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> Node Feature Discovery scans the node's hardware via PCI IDs and applies Kubernetes labels to nodes where GPU hardware is detected. This enables the OpenShift scheduler to intelligently place GPU workloads on nodes with the appropriate hardware capabilities.

**First Defined**: Chapter 1, Section 1 (Deconstructing the Hardware Stack)

**Namespace**: openshift-nfd
**Catalog**: redhat-operators

### NVIDIA GPU Operator
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> The NVIDIA GPU Operator orchestrates several critical components that work together to enable GPU acceleration in containerized environments. It automates deployment and lifecycle management of GPU drivers, container toolkit, device plugin, and monitoring components.

**First Defined**: Chapter 1, Section 1

**Namespace**: nvidia-gpu-operator
**Catalog**: certified-operators

### ClusterPolicy
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> ClusterPolicy is the Custom Resource for the NVIDIA GPU Operator. It declares the desired state for the entire GPU software stack including driver version, enabled components (DCGM, MIG, GFD), and configuration settings.

**First Defined**: Chapter 1, Section 2

**API**: nvidia.com/v1
**Kind**: ClusterPolicy
**Scope**: Cluster-wide (not namespaced)

### NVIDIA Driver Container
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> The NVIDIA Driver Container deploys necessary GPU drivers directly via containers, eliminating the need to manually install kernel modules on the host operating system. This containerized approach provides simplified driver management, consistent versions across the cluster, and isolation from host OS dependencies.

**First Defined**: Chapter 1, Section 1

### NVIDIA Container Toolkit
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> The NVIDIA Container Toolkit plugs into the OpenShift container runtime (CRI-O) to ensure pods can securely request and access underlying GPU hardware. It provides runtime integration for GPU resource allocation, secure GPU device passthrough to containers, and environment configuration for CUDA applications.

**First Defined**: Chapter 1, Section 1

### GPU Feature Discovery (GFD)
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> GPU Feature Discovery gathers granular hardware capabilities including GPU model, VRAM size, and MIG profiles, then applies them as specific node labels. This detailed hardware inventory enables fine-grained workload placement decisions and MIG-aware scheduling.

**First Defined**: Chapter 1, Section 1

### Data Center GPU Manager (DCGM)
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> DCGM is a daemon that continuously monitors GPU health, diagnostics, and telemetry. It provides real-time GPU health monitoring, performance metrics collection, diagnostic capabilities for troubleshooting, and integration with cluster monitoring systems.

**First Defined**: Chapter 1, Section 1

### DCGM Exporter
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> The DCGM Exporter extracts metrics from DCGM and formats them for Prometheus scraping, enabling integration with OpenShift's monitoring stack. This component bridges GPU telemetry with cloud-native observability platforms.

**First Defined**: Chapter 1, Section 1

### GPU Silo Crisis
**Canonical Definition** (from ch1-gpu-operator/s1-hardware-stack.adoc):
> The "GPU Silo" problem occurs when expensive GPU hardware remains underutilized due to complex manual configuration, dependency management, and operational overhead. It represents the challenge organizations face before operator-based automation.

**First Defined**: Chapter 1, Section 1

**Key Metrics**: 150+ hours manual setup time, 40-60% idle time without automation

---

## Models-as-a-Service (MaaS) Architecture

### Models-as-a-Service (MaaS)
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Models-as-a-Service (MaaS) is an enterprise AI platform pattern where machine learning models are deployed as scalable, managed services with automated infrastructure lifecycle, multi-tenant resource sharing, and production-grade observability.

**First Defined**: Chapter 1, Section 2

**Key Requirements**: GPU automation, workload queuing, inference serving, monitoring

### Three-Layer MaaS Operator Stack
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> The three-layer MaaS operator stack organizes operators into functional layers: Layer 1 (Core & Infrastructure: NFD, GPU Operator), Layer 2 (Inference at Scale: Kueue, KServe, Cert-manager, Kuadrant), and Layer 3 (Orchestration: Red Hat OpenShift AI). Each layer builds on the previous, with Layer 3 coordinating dependencies across all layers.

**First Defined**: Chapter 1, Section 2

**Visual Reference**: See architecture diagram in ch1-gpu-operator/s2-operators-overview.adoc

### Layer 1: Core & Infrastructure Operators
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Layer 1 provides hardware detection and GPU software stack automation through Node Feature Discovery (NFD) and NVIDIA GPU Operator. This layer enables OpenShift to recognize GPU hardware and make it available as schedulable resources.

**First Defined**: Chapter 1, Section 2

**Purpose**: Hardware enablement foundation

### Layer 2: Operators for Inference at Scale
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Layer 2 provides production-grade MaaS capabilities including certificate management (Cert-manager), rate limiting (Kuadrant/Connectivity Link), workload queueing (Kueue), and distributed training (LeaderWorkerSet). This layer transforms basic GPU resources into enterprise-ready inference infrastructure.

**First Defined**: Chapter 1, Section 2

**Purpose**: Production-grade MaaS capabilities

### Layer 3: Red Hat OpenShift AI Orchestration
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Layer 3 coordinates the complete MaaS ecosystem through the Red Hat OpenShift AI Operator. It manages Layer 2 operator dependencies automatically via the DataScienceCluster Custom Resource, providing a single control point for the entire MaaS platform lifecycle.

**First Defined**: Chapter 1, Section 2

**Purpose**: Orchestrate complete MaaS ecosystem

---

## OpenShift AI Components

### Red Hat OpenShift AI
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Red Hat OpenShift AI is an enterprise AI/ML platform built on OpenShift that provides a complete MaaS ecosystem. It orchestrates multiple operators for model serving, distributed training, workload queuing, and observability through a unified DataScienceCluster configuration.

**First Defined**: Chapter 1, Section 2

**Namespace**: redhat-ods-operator
**Catalog**: redhat-operators

### DataScienceCluster
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> DataScienceCluster is the Custom Resource for Red Hat OpenShift AI. It provides unified configuration for the complete MaaS platform, automatically managing dependencies for KServe, Kueue, Dashboard, and other components.

**First Defined**: Chapter 1, Section 2

**API**: datasciencecluster.opendatahub.io/v1
**Kind**: DataScienceCluster

### Kueue
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> Kueue provides workload queueing and quota management for multi-tenant GPU platforms. It enables fair sharing of GPU resources across teams, implements resource quotas, and queues workloads when resources are unavailable.

**First Defined**: Chapter 1, Section 2

**Namespace**: kueue-system
**Purpose**: Multi-tenant resource management

### KServe
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> KServe provides model serving capabilities for deploying ML models as scalable inference services. It supports multiple model formats, auto-scaling, canary rollouts, and integrates with the GPU Operator for GPU-accelerated inference.

**First Defined**: Chapter 1, Section 2

**API**: serving.kserve.io/v1beta1
**Key Resource**: InferenceService

### InferenceService
**Canonical Definition** (from ch1-gpu-operator/s2-operators-overview.adoc):
> InferenceService is the Custom Resource for deploying ML models as managed services. It specifies the model format, runtime, resource requirements (including GPU allocation), and serving configuration.

**First Defined**: Chapter 1, Section 2

**API**: serving.kserve.io/v1beta1
**Kind**: InferenceService

---

## Terms to Define in Future Chapters

### Multi-Instance GPU (MIG)
**Status**: TO BE DEFINED in Chapter 2
**Brief Description**: NVIDIA technology for partitioning single GPU into multiple independent instances

### MIG Profile
**Status**: TO BE DEFINED in Chapter 2
**Brief Description**: Specific GPU partition configuration (e.g., 1g.5gb, 3g.20gb, 7g.40gb)

### Time-Slicing
**Status**: TO BE DEFINED in Chapter 2
**Brief Description**: Alternative to MIG for GPU sharing via temporal multiplexing

### Prometheus
**Status**: TO BE DEFINED in Chapter 3
**Brief Description**: Metrics collection and monitoring system

### Grafana
**Status**: TO BE DEFINED in Chapter 3
**Brief Description**: Metrics visualization and dashboarding platform

---

## Deprecated or Avoided Terms

### ❌ "GPU Operator" (ambiguous)
**Use instead**: "NVIDIA GPU Operator" (specific vendor)
**Reason**: Multiple vendors have GPU operators; be specific

### ❌ "Red Hat OpenShift Data Science" (old name)
**Use instead**: "Red Hat OpenShift AI"
**Reason**: Product was renamed in version 3.x

### ❌ "Community Operators" (in production context)
**Use instead**: "redhat-operators or certified-operators"
**Reason**: Community operators lack support SLAs for production use

---

## Acronym Reference

| Acronym | Full Term | First Defined |
|---------|-----------|---------------|
| AI | Artificial Intelligence | Course title |
| CRD | Custom Resource Definition | Chapter 1, Section 2 |
| CR | Custom Resource | Chapter 1, Section 2 |
| CSV | ClusterServiceVersion | Chapter 1, Section 2 |
| CVO | Cluster Version Operator | Chapter 1, Section 2 |
| DCGM | Data Center GPU Manager | Chapter 1, Section 1 |
| GFD | GPU Feature Discovery | Chapter 1, Section 1 |
| GPU | Graphics Processing Unit | Course title |
| MaaS | Models-as-a-Service | Chapter 1, Section 2 |
| MIG | Multi-Instance GPU | Chapter 2 (TBD) |
| ML | Machine Learning | Chapter 1, Section 2 |
| NFD | Node Feature Discovery | Chapter 1, Section 1 |
| OLM | Operator Lifecycle Manager | Chapter 1, Section 2 |
| RBAC | Role-Based Access Control | Chapter 1, Section 2 |
| ROI | Return on Investment | Chapter 1 index |
| SLA | Service Level Agreement | Chapter 1, Section 2 |
| TLS | Transport Layer Security | Chapter 1, Section 2 |
| VRAM | Video Random Access Memory | Chapter 1, Section 1 |
| YAML | YAML Ain't Markup Language | Course prerequisites |

---

## Usage Guidelines

### When to Reference This Document

**Always reference before**:
- Defining a technical term for the first time in new content
- Writing transitions that reference prior concepts
- Creating cross-references to other chapters
- Updating existing content

### How to Reference Existing Terms

**Pattern for first use in a section**:
```asciidoc
The ClusterPolicy Custom Resource (introduced in Chapter 1, Section 2)
declares the desired state...
```

**Pattern for subsequent uses**:
```asciidoc
Edit the ClusterPolicy to change the driver version...
```

### How to Add New Terms

1. Define the term in your new content
2. After content is approved, add to this document with:
   - Canonical definition (exact text from content)
   - First defined location (chapter, section)
   - Key characteristics or related terms
   - Examples if applicable
3. Commit terminology update with content changes

---

## Maintenance Schedule

**Weekly**: Review new content for terms to add
**Monthly**: Check for deprecated terms or changed product names
**Per Release**: Verify all version-specific information is current

**Maintainer Notes**: 
- Last full review: 2026-04-11
- Next review due: 2026-05-11
