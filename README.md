# NVIDIA Accelerator Configuration for Scale

> **Enterprise GPU Infrastructure Enablement for Models-as-a-Service**

A comprehensive Red Hat QuickCourse for platform engineers and SREs who need to deploy, configure, and monitor NVIDIA GPU infrastructure on OpenShift at enterprise scale. This course provides the foundational GPU enablement layer required for building production Models-as-a-Service (MaaS) platforms.

---

## 🎯 Course Overview

Organizations investing in GPU infrastructure face the "GPU Silo" problem—expensive GPU hardware remains underutilized due to complex manual configuration, dependency management, and operational overhead. This course teaches you how to:

- **Automate GPU software stack deployment** using the NVIDIA GPU Operator and OpenShift Operator Lifecycle Manager
- **Maximize GPU ROI** by configuring Multi-Instance GPU (MIG) partitioning for workload isolation
- **Build comprehensive observability** by integrating GPU telemetry with OpenShift monitoring and Grafana

**Business Value**: Transform GPU infrastructure from manually-managed silos into automated, observable, revenue-generating service platforms.

---

## 👥 Target Audience

This course is designed for:

- **Platform Engineers** - Designing and deploying model serving environments and enabling MaaS
- **DevOps/SREs** - Building observability, tracking consumption metrics, and managing operational scale
- **Cloud Architects** - Planning GPU infrastructure for AI/ML workloads at enterprise scale

---

## 📚 What You'll Learn

Upon completing this course, you will be able to:

✅ Understand the operator pattern and how it powers enterprise AI platform automation  
✅ Deploy the complete NVIDIA GPU Operator stack using OpenShift's Operator Lifecycle Manager  
✅ Troubleshoot operator installations and manage GPU driver lifecycle  
✅ Configure Multi-Instance GPU (MIG) partitioning to maximize hardware utilization  
✅ Implement Single and Mixed MIG slicing strategies for heterogeneous workloads  
✅ Build GPU observability stacks integrating DCGM telemetry with OpenShift monitoring  
✅ Create Grafana dashboards for GPU health, performance, and utilization metrics  
✅ Correlate platform, node, and accelerator metrics for effective MaaS operations  

---

## 🔧 Prerequisites

This course assumes you have:

- **OpenShift Experience**: Familiarity with Kubernetes and Red Hat OpenShift Container Platform
- **AI/ML Basics**: Basic understanding of machine learning concepts and Red Hat OpenShift AI
- **Networking & Operators**: Understanding of Kubernetes operators, basic networking, and routing
- **Observability**: Familiarity with REST APIs, Prometheus metrics, and RBAC within OpenShift

---

## 📖 Course Structure

### **Chapter 1: Operator Foundations and GPU Stack Deployment**

Master the operator pattern and deploy the NVIDIA GPU Operator stack.

- **Section 1**: Understanding the GPU Hardware and Software Stack
- **Section 2**: Operator Pattern Deep Dive (3 parts)
  - The Operator Pattern and Lifecycle Management
  - Operator Lifecycle Manager (OLM) Architecture
  - Custom Resources and Reconciliation
- **Section 3**: Deploy GPU Operators Lab (Hands-on)
  - Lab Setup and Operator Installation
  - Configuring GPU Node Discovery
  - Driver Deployment and Validation
  - Troubleshooting Common Issues
  - Performance Verification

### **Chapter 2: Multi-Instance GPU (MIG) Configuration**

Maximize GPU ROI with MIG partitioning for workload isolation.

- **Section 1**: MIG Overview (4 parts)
  - Introduction to Multi-Instance GPU
  - MIG Profiles and Partitioning Strategies
  - Single vs. Mixed Slicing
  - MIG Scheduling and Resource Allocation
- **Section 2**: MIG Slicing Lab (Hands-on)
  - Configuring MIG partitions
  - Applying MIG profiles
  - Testing workload isolation

### **Chapter 3: GPU Telemetry and Observability**

Build comprehensive monitoring for GPU infrastructure health and performance.

- **Section 1**: Observability Stack Architecture
- **Section 2**: Expose GPU Metrics Lab (Hands-on)
- **Section 3**: Grafana Setup Lab (Hands-on)
- **Section 4**: Custom Dashboards Lab (Hands-on)

---

## 🚀 Getting Started

### Local Development

**Prerequisites**:
- Node.js 16+ and npm
- Git

**Clone and Setup**:
```bash
git clone https://github.com/RedHatQuickCourses/maas-gpu-enablement.git
cd maas-gpu-enablement
npm install
```

### Build and View the Course

**Build the course**:
```bash
npm run build
```

**Serve locally**:
```bash
npm run serve
```

Then open `http://localhost:8080` in your browser.

**Watch mode** (auto-rebuild on changes):
```bash
# Terminal 1: Watch for changes
npm run watch:adoc

# Terminal 2: Serve the site
npm run serve
```

### Using Red Hat DevSpaces

Click to launch in DevSpaces:

[![Contribute](https://www.eclipse.org/che/contribute.svg)](https://devspaces.apps.tools-na100.dev.ole.redhat.com/#https://github.com/RedHatQuickCourses/maas-gpu-enablement)

---

## 🧪 Lab Environment

This course includes hands-on labs that require:

- **OpenShift Cluster**: OpenShift 4.12+ with cluster-admin access
- **GPU Nodes**: At least one node with NVIDIA GPU hardware
  - Recommended: NVIDIA A100, A30, or H100 for MIG support
  - Minimum: NVIDIA T4 or V100 for basic GPU operator functionality
- **Operators**: Access to OperatorHub for installing:
  - NVIDIA GPU Operator
  - Grafana Operator (optional for Chapter 3)
- **Network Access**: Ability to pull container images from registry.redhat.io and nvcr.io

**Lab environment setup is covered in the LABENV module.**

---

## 🛠️ Technology Stack

This course covers:

- **Platform**: Red Hat OpenShift Container Platform 4.12+
- **GPU Stack**: NVIDIA GPU Operator, NVIDIA Device Plugin, DCGM Exporter
- **Operators**: Operator Lifecycle Manager (OLM), NVIDIA GPU Operator
- **Monitoring**: OpenShift Monitoring Stack, Prometheus, Grafana Operator
- **GPU Features**: Multi-Instance GPU (MIG), NVIDIA DCGM
- **Documentation**: Antora 3.1.x, AsciiDoc

---

## 📝 Course Authoring System

This course was developed using the **Red Hat QuickCourse Content Creation System**, which includes:

- **Content Request Templates** - Structured approach for requesting content from Claude Code
- **Style Guide** - Three-layer depth approach (WHY/WHAT/HOW) with production-ready patterns
- **Terminology Management** - Canonical term definitions for consistency
- **Fresh Session Workflow** - Maintaining quality across multiple development sessions

For details on the content creation system, see the companion course: [knox-test-claude](https://github.com/RedHatQuickCourses/knox-test-claude)

---

## 🤝 Contributing

We welcome contributions! To contribute:

1. **Fork this repository**
2. **Create a feature branch**: `git checkout -b feature/new-section`
3. **Follow the style guide**: Read `STYLE-GUIDE.md` and reference existing sections for patterns
4. **Check terminology**: Use `TERMINOLOGY.md` for canonical term definitions
5. **Test your changes**: Run `npm run build` to verify the build succeeds
6. **Submit a pull request**

**Content Quality Standards**:
- All content must include three layers: Conceptual (WHY), Architectural (WHAT), Tactical (HOW)
- Use concrete examples with specific metrics (not "quickly" - use "within 45 seconds")
- Include production guidance (decision matrices, TIP/WARNING callouts)
- Reference prior concepts and prepare for future concepts

---

## 📄 License

Copyright © 2024 Red Hat, Inc.

This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.

---

## 📞 Support and Feedback

- **Issues**: Report issues or request features via [GitHub Issues](https://github.com/RedHatQuickCourses/maas-gpu-enablement/issues)
- **Discussions**: Join the conversation in [GitHub Discussions](https://github.com/RedHatQuickCourses/maas-gpu-enablement/discussions)
- **Questions**: For Red Hat OpenShift AI and GPU-related questions, see [Red Hat Customer Portal](https://access.redhat.com/)

---

## 🔗 Additional Resources

**Product Documentation**:
- [Red Hat OpenShift AI Documentation](https://access.redhat.com/documentation/en-us/red_hat_openshift_ai)
- [NVIDIA GPU Operator Documentation](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/overview.html)
- [NVIDIA Multi-Instance GPU (MIG) User Guide](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/)

**Related Courses**:
- [Red Hat OpenShift AI Fundamentals](https://github.com/RedHatQuickCourses/rhoai-fundamentals)
- [QuickCourse Creation Guide](https://github.com/RedHatQuickCourses/knox-test-claude)

**Community**:
- [Red Hat Developer](https://developers.redhat.com/)
- [NVIDIA Developer](https://developer.nvidia.com/)

---

**Built with ❤️ by Red Hat Training and the QuickCourse community**
