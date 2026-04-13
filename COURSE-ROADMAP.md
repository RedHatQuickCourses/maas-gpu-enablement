# MaaS Training Course Roadmap

## Visual Progress Map

```
┌────────────────────────────────────────────────────────────────────┐
│                    MAAS TRAINING ARCHITECTURE                      │
│              (Based on SME-Provided Reference Diagram)             │
└────────────────────────────────────────────────────────────────────┘

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  EXTERNAL: MaaS Consumers (Developers, Apps, Data Scientists)   ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                              │
                              │ OpenAI-compatible API
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ CHAPTER 6: Developer Integration ⏳ PLANNED                     │
├─────────────────────────────────────────────────────────────────┤
│ • API Consumption & Tokens        • Security & Audit Logging   │
│ • DevSpaces Integration           • PII Filtering              │
├─────────────────────────────────────────────────────────────────┤
│ Persona: Developer                                              │
│ Delivery: Weeks 7-8                                             │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ MaaS Gateway API
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ CHAPTER 5: MaaS Platform Configuration ⏳ PLANNED               │
├─────────────────────────────────────────────────────────────────┤
│ • MaaS Architecture Overview      • User Tiers & Quotas        │
│ • RHOAI Operator Configuration    • Rate Limits                │
│ • Model Catalog Management        • Usage Tracking & Metrics   │
│ • Multi-Tenancy & Isolation       • Cost Allocation            │
├─────────────────────────────────────────────────────────────────┤
│ Persona: Platform Engineer                                      │
│ Delivery: Weeks 4-6                                             │
│ SME Addresses: Redundant deployments, security visibility,     │
│                usage tracking problems                          │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ Model Registry + Inference Endpoints
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ CHAPTER 4: Model Serving (LLM Inference) ⏳ PLANNED             │
├─────────────────────────────────────────────────────────────────┤
│ • Model Selection Criteria        • llm-d API Integration      │
│   - Dense vs Sparse               • Model Endpoints            │
│   - Reasoning vs Non-Reasoning    • GitOps Integration         │
│   - Context Length Considerations • Performance Tuning         │
│   - Tool Calling Capabilities     • Model Observability        │
│ • vLLM Inference Engine                                         │
├─────────────────────────────────────────────────────────────────┤
│ Persona: Platform Engineer                                      │
│ Delivery: Weeks 1-3                                             │
│ SME Addresses: Model deployment standardization                │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ Workload Scheduling
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ LAYER 2: GPU Quota/Priority Management 📦 SEPARATE REPO         │
├─────────────────────────────────────────────────────────────────┤
│ Repository: maas-kueue-enablement                               │
│ • Kueue Workload Orchestration    • Fair Resource Sharing      │
│ • Priority Queues                  • Team-based Quotas         │
│ • Preemption Policies              • Multi-Tenant Isolation    │
├─────────────────────────────────────────────────────────────────┤
│ Persona: Platform Engineer                                      │
│ SME Addresses: GPU over-provisioning, workload bottlenecks     │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ GPU Resource Requests
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ CHAPTER 3: Hardware Observability ✅ COMPLETE                   │
├─────────────────────────────────────────────────────────────────┤
│ • Observability Stack             • Grafana Configuration      │
│ • GPU Metrics Exposure            • Dashboard Creation         │
│ • Prometheus Integration          • Alert Configuration        │
├─────────────────────────────────────────────────────────────────┤
│ Sections: 4 sections + 3 hands-on labs                          │
│ Status: Ready for SME review ✅                                 │
└─────────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────────┐
│ CHAPTER 2: Multi-Instance GPU (MIG) ✅ COMPLETE                 │
├─────────────────────────────────────────────────────────────────┤
│ • MIG Architecture & Concepts     • ROI Optimization           │
│ • GPU Slicing Strategies          • Multi-Tenant Sharing       │
│ • Profile Configuration           • Production Best Practices  │
├─────────────────────────────────────────────────────────────────┤
│ Sections: 2 sections + 1 hands-on lab                           │
│ Status: Ready for SME review ✅                                 │
│ SME Addresses: GPU under-utilization problem 🎯                │
└─────────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────────┐
│ CHAPTER 1: GPU Operator & Infrastructure ✅ COMPLETE            │
├─────────────────────────────────────────────────────────────────┤
│ • Hardware Stack Architecture     • Operator Patterns          │
│ • NVIDIA GPU Operator             • Driver Management          │
│ • Node Feature Discovery          • Device Plugin Config       │
│ • Container Toolkit               • Lifecycle Management       │
├─────────────────────────────────────────────────────────────────┤
│ Sections: 3 sections + 1 hands-on lab                           │
│ Status: Ready for SME review ✅                                 │
│ SME Addresses: Misallocation of engineering expertise 🎯       │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃         PHYSICAL: NVIDIA GPU Hardware (A100, H100, etc.)        ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

---

## SME Problem → Solution Mapping

| SME Problem Statement | Current Status | Solution Location |
|----------------------|----------------|-------------------|
| **GPU under-utilization and over-provisioning** | ✅ Addressed | Ch2: MIG slicing<br>⏳ Ch5: MaaS quotas |
| **Misallocation of engineer/DS expertise** <br>(time on CUDA, Docker, K8s vs models) | ✅ Addressed | Ch1: Operator-managed infra<br>Ch4: llm-d API abstraction |
| **Redundant Model Deployments** <br>(5 teams, same model, waste) | ⏳ Planned | Ch5: Shared model catalog |
| **Security "Black Boxes"** <br>(no visibility, audit logs, PII filtering) | ⏳ Planned | Ch5: MaaS gateway<br>Ch6: Audit & governance |
| **No usage tracking or forecast** <br>(can't forecast compute needs) | ⚠️ Partial | ✅ Ch3: Grafana baseline<br>⏳ Ch5: MaaS-level metrics |

---

## Course Learning Progression

### Phase 1: Foundation ✅ (Weeks 0 - Current)
**Chapters 1-3 Complete**

Students learn:
1. How GPU infrastructure is managed via operators (not manual CUDA installs)
2. How to slice GPUs for multi-tenant sharing via MIG
3. How to observe GPU health and performance

**Outcome**: Platform engineers can deploy and monitor GPU infrastructure

---

### Phase 2: Model Layer ⏳ (Weeks 1-3)
**Chapter 4 Planned**

Students learn:
1. How to select appropriate models for use cases
2. How to deploy models with vLLM inference engine
3. How to expose models via llm-d API
4. How to monitor model performance

**Outcome**: Platform engineers can deploy and manage LLM inference services

---

### Phase 3: MaaS Platform ⏳ (Weeks 4-6)
**Chapter 5 Planned**

Students learn:
1. How MaaS architecture works (full stack GPU → API)
2. How to configure RHOAI operator for MaaS
3. How to set up user tiers, quotas, and rate limits
4. How to track usage and allocate costs

**Outcome**: Platform engineers can operate a multi-tenant MaaS platform

---

### Phase 4: Developer Integration ⏳ (Weeks 7-8)
**Chapter 6 Planned**

Students learn:
1. How to consume MaaS endpoints in applications
2. How to manage API tokens and authentication
3. How to use DevSpaces for AI development
4. How to implement security and compliance

**Outcome**: Developers can integrate MaaS into production applications

---

## Repository Structure

```
maas-gpu-enablement/
│
├── antora.yml                          # Course structure definition
├── antora-playbook.yml                 # Build configuration
│
├── modules/
│   ├── ROOT/                           # Course introduction
│   │   └── pages/
│   │       └── index.adoc              # Course goals, audience, prereqs
│   │
│   ├── LABENV/                         # Lab environment setup
│   │   └── pages/
│   │       └── index.adoc
│   │
│   ├── ch1-gpu-operator/               ✅ COMPLETE
│   │   ├── nav.adoc
│   │   └── pages/
│   │       ├── index.adoc
│   │       ├── s1-hardware-stack.adoc
│   │       ├── s2-operators-overview.adoc  ← QUALITY REFERENCE
│   │       └── s3-deploy-operators-lab.adoc
│   │
│   ├── ch2-mig/                        ✅ COMPLETE
│   │   ├── nav.adoc
│   │   └── pages/
│   │       ├── index.adoc
│   │       ├── s1-mig-overview.adoc
│   │       └── s2-mig-slicing-lab.adoc
│   │
│   ├── ch3-observability/              ✅ COMPLETE
│   │   ├── nav.adoc
│   │   └── pages/
│   │       ├── index.adoc
│   │       ├── s1-observability-stack.adoc
│   │       ├── s2-expose-metrics-lab.adoc
│   │       ├── s3-grafana-setup-lab.adoc
│   │       └── s4-dashboards-lab.adoc
│   │
│   ├── ch4-model-serving/              ⏳ PLANNED (Weeks 1-3)
│   │   ├── nav.adoc
│   │   └── pages/
│   │       ├── index.adoc
│   │       ├── s1-model-selection.adoc
│   │       ├── s2-vllm-deployment.adoc
│   │       ├── s3-llm-d-api-lab.adoc
│   │       └── s4-model-observability.adoc
│   │
│   ├── ch5-maas-platform/              ⏳ PLANNED (Weeks 4-6)
│   │   ├── nav.adoc
│   │   └── pages/
│   │       ├── index.adoc
│   │       ├── s1-maas-architecture.adoc
│   │       ├── s2-rhoai-operator-config.adoc
│   │       ├── s3-user-tiers-quotas-lab.adoc
│   │       └── s4-maas-metrics-lab.adoc
│   │
│   └── ch6-developer-integration/      ⏳ PLANNED (Weeks 7-8)
│       ├── nav.adoc
│       └── pages/
│           ├── index.adoc
│           ├── s1-api-consumption.adoc
│           ├── s2-devspaces-integration-lab.adoc
│           └── s3-security-governance.adoc
│
├── SME-PROGRESS-UPDATE.md              # This document
├── SME-EMAIL-SUMMARY.md                # Email version
└── COURSE-ROADMAP.md                   # Visual roadmap
```

---

## Quality Assurance Standards

All content follows the style guide documented in:
- `STYLE-GUIDE.md`
- Reference implementation: `modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

### Content Depth Requirements

Every section includes:
1. **WHY (Business Value)**: Problem it solves, ROI, concrete metrics
2. **WHAT (Architecture)**: Components, relationships, how parts work together
3. **HOW (Tactical)**: Configuration, commands, workflows, verification

### Production Readiness

Every section includes:
- Decision matrices for production choices
- TIP/WARNING callouts for production considerations
- Concrete examples with specific timing (e.g., "45 seconds" not "quickly")
- Annotated code with numbered callouts
- Integration with prior and future concepts

---

## SME Feedback Loop

### Review Checkpoints

1. **Now**: Ch1-3 technical accuracy and depth review
2. **Week 1**: Ch4 outline and content approach review
3. **Week 4**: Ch5 outline and MaaS architecture review
4. **Week 7**: Ch6 outline and developer persona review

### Continuous Improvement

- Each chapter reviewed before proceeding to next
- Feedback from early chapters applied to later chapters
- Iterative refinement based on SME technical guidance

---

## Success Metrics

By course completion, students will be able to:

✅ **Deploy** GPU infrastructure using operators (not manual config)  
✅ **Configure** MIG for multi-tenant GPU sharing  
✅ **Monitor** GPU health and performance with Grafana  
⏳ **Select** optimal models for specific use cases  
⏳ **Deploy** models with vLLM and llm-d API  
⏳ **Configure** MaaS platform with RHOAI operator  
⏳ **Manage** user tiers, quotas, and rate limits  
⏳ **Track** usage and allocate costs across teams  
⏳ **Integrate** MaaS endpoints into production applications  
⏳ **Implement** security, governance, and compliance controls  

---

## Contact & Review Access

**Repository**: https://github.com/[org]/maas-gpu-enablement  
**Build Instructions**: `npm install && npm run build`  
**Questions**: Contact course development team

**Next Steps**: Awaiting SME review of Ch1-3 before proceeding to Ch4
