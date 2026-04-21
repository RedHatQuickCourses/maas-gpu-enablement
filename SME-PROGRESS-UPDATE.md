# MaaS Training Development: Progress Update

**To**: Taylor Smith, James Harmison, Jonathan Zarecki  
**From**: Course Development Team  
**Date**: April 13, 2026  
**Re**: Models-as-a-Service Training - Layered Development Approach

---

## Executive Summary

We are developing the MaaS training using a **bottom-up, layered architecture** that directly follows the reference diagram provided by the SME team. This approach builds foundational infrastructure first, then progressively adds platform and application layers—mirroring how platform engineers actually deploy MaaS in production environments.

**Current Status**: Foundation layer (GPU Enablement) is complete and ready for SME review.

---

## Architectural Approach

Our course structure maps directly to the **MaaS architecture diagram** you provided:

```
┌─────────────────────────────────────────────────────────────┐
│ Layer 5: Developer Integration (PLANNED - Ch6)              │
│ • MaaS API consumption, tokens, DevSpaces integration       │
└─────────────────────────────────────────────────────────────┘
                            ▲
┌─────────────────────────────────────────────────────────────┐
│ Layer 4: MaaS Platform (PLANNED - Ch5)                      │
│ • RHOAI operator config, user tiers, quotas, rate limits    │
└─────────────────────────────────────────────────────────────┘
                            ▲
┌─────────────────────────────────────────────────────────────┐
│ Layer 3: Model Serving (PLANNED - Ch4)                      │
│ • LLM Inference, vLLM, model selection, llm-d API           │
└─────────────────────────────────────────────────────────────┘
                            ▲
┌─────────────────────────────────────────────────────────────┐
│ Layer 2: GPU Quota/Priority (SEPARATE REPO)                 │
│ • Kueue workload management (maas-kueue-enablement)         │
└─────────────────────────────────────────────────────────────┘
                            ▲
┌─────────────────────────────────────────────────────────────┐
│ Layer 1: GPU Enablement ✅ COMPLETE (Ch1-3)                 │
│ • NVIDIA GPU Operator, MIG configuration, HW Observability  │
└─────────────────────────────────────────────────────────────┘
```

This layered approach ensures students understand each infrastructure component before building on it—avoiding the "magic black box" problem where developers don't understand the platform they're using.

---

## Current Progress: Foundation Layer ✅

**Repository**: `maas-gpu-enablement`  
**GitHub**: https://github.com/[org]/maas-gpu-enablement  
**Status**: Chapters 1-3 complete and ready for SME review

### What's Complete

| Chapter | Content | SME Requirement Addressed |
|---------|---------|---------------------------|
| **Ch1: GPU Operator** | • Hardware stack architecture<br>• Operator-based deployment patterns<br>• Hands-on operator deployment lab | • Foundational infrastructure<br>• Addresses "misallocation of expertise" problem |
| **Ch2: Multi-Instance GPU (MIG)** | • MIG slicing concepts<br>• ROI maximization strategies<br>• Hands-on MIG configuration lab | • **Directly addresses GPU under-utilization**<br>• Enables multi-tenant GPU sharing |
| **Ch3: HW Observability** | • Observability stack architecture<br>• GPU metrics exposure<br>• Grafana dashboard creation labs | • Baseline for MaaS-level metrics (Layer 4)<br>• Uses Grafana as per Taylor's guidance |

### Review Access

**Option 1 - View Locally**:
```bash
cd maas-gpu-enablement
npm install
npm run build
open build/site/index.html
```

**Option 2 - Source Files**:
Review AsciiDoc source in `modules/` directory

**Key Reference Page**:
`modules/ch1-gpu-operator/pages/s2-operators-overview.adoc` demonstrates our depth/quality standard (WHY/WHAT/HOW approach with concrete metrics and production guidance)

---

## Mapping to SME Requirements

### ✅ Currently Addressed

| SME Problem Statement | Our Solution (Ch1-3) |
|-----------------------|----------------------|
| GPU under-utilization and over-provisioning | ✅ Ch2: MIG slicing enables multi-tenant GPU sharing |
| Misallocation of engineer expertise (debugging CUDA, K8s) | ✅ Ch1: Operator-managed infrastructure reduces manual config |
| Need for hardware observability baseline | ✅ Ch3: Grafana + GPU metrics foundation |

### ⏳ Planned (Ch4-6)

| SME Requirement | Planned Coverage | Chapter |
|-----------------|------------------|---------|
| **MaaS Architecture** | High-level flow GPU→API, layer breakdown | Ch5 (s1) |
| **Configure MaaS w/ RHOAI** | Operator config, user tiers, rate limits, quotas | Ch5 (s2-3) |
| **Deploy Model for MaaS** | llm-d API, model endpoints, GitOps integration | Ch4 (s3) |
| **Model Selection** | Dense vs sparse, reasoning vs non-reasoning, context length | Ch4 (s1) |
| **Redundant Model Deployments** | Shared model catalog via MaaS | Ch5 (s2) |
| **Security "Black Boxes"** | API gateway, audit logs, PII filtering | Ch6 (s3) |
| **MaaS Metrics & Usage Tracking** | User tier metrics, model usage analytics | Ch5 (s4) |
| **API Integration (Developer)** | Consuming endpoints, tokens, DevSpaces | Ch6 (s1-2) |

---

## Planned Course Expansion

To complete the full SME-specified MaaS training, we propose adding three chapters:

### Chapter 4: Model Serving (NEW)
**Persona**: Platform Engineer  
**Topics**: 
- Model selection criteria (dense/sparse, reasoning/non-reasoning)
- vLLM inference engine deployment
- llm-d API integration
- Model observability and performance tuning

**Labs**:
- Deploy LLM with vLLM
- Configure model endpoint with llm-d API
- Monitor model performance metrics

---

### Chapter 5: MaaS Platform Configuration (NEW)
**Persona**: Platform Engineer  
**Topics**:
- MaaS architecture (full stack from GPU to API)
- OpenShift AI operator configuration
- User groups, tiers, and multi-tenancy
- Rate limits and usage quotas
- MaaS-specific observability (usage tracking, cost allocation)

**Labs**:
- Configure MaaS feature via RHOAI operator
- Set up user tiers and quotas
- Build MaaS metrics dashboards in Grafana
- Track usage across models and user groups

---

### Chapter 6: Developer Integration (NEW)
**Persona**: Developer  
**Topics**:
- Consuming MaaS API endpoints
- Token management and authentication
- OpenShift DevSpaces integration
- Security, governance, and audit logging

**Labs**:
- Integrate MaaS endpoint into sample application
- Use DevSpaces for AI-powered development
- Implement audit logging for compliance

---

## Course Sequencing Strategy

### Modular Design Benefits

1. **Phased Development**: Complete each layer before moving up the stack
2. **Independent Review**: SMEs can review each layer as it's completed
3. **Flexible Consumption**: Organizations can use Layer 1-2 standalone for GPU infrastructure, or complete stack for full MaaS
4. **Parallel Development**: Different team members can work on different layers simultaneously

### Integration with Separate Repositories

- **GPU Quota/Priority** (`maas-kueue-enablement`): Layer 2, separate repository
- **GPU Enablement** (`maas-gpu-enablement`): Layers 1, 3-5, this repository
- **Potential**: Could link as prerequisite courses or merge into single comprehensive training

---

## Quality Standards

All content follows the established quality framework:

- ✅ **Three-layer depth**: WHY (business value) + WHAT (architecture) + HOW (hands-on)
- ✅ **Concrete examples**: Specific metrics, timing, real-world scenarios (not "quickly"—actual seconds)
- ✅ **Production guidance**: Decision matrices, TIP/WARNING callouts for production considerations
- ✅ **Integration**: References prior concepts, prepares for future layers
- ✅ **Annotated code**: YAML/CLI examples with numbered callouts explaining each section

---

## SME Review Request

### Immediate Action Items

1. **Review Ch1-3** (GPU Enablement layer) for technical accuracy and depth
2. **Validate layered approach** against your architectural vision
3. **Confirm Ch4-6 topic coverage** aligns with SME requirements
4. **Provide feedback** on any gaps or adjustments needed

### Specific SME Questions

1. **Model Selection (Ch4)**: Should we include specific model recommendations (e.g., Llama vs Mixtral) or focus on decision criteria?
2. **MaaS Observability (Ch5)**: Beyond Grafana, are there specific RHOAI observability features we should highlight?
3. **Developer Persona (Ch6)**: What level of application development expertise should we assume? (Basic Python? Full-stack?)
4. **GPU Quota/Priority**: Should we merge `maas-kueue-enablement` content into this repo, or maintain as separate prerequisite?

---

## Timeline Considerations

**Current Velocity**: Each chapter (3-4 sections + labs) takes approximately 2-3 weeks at current depth/quality standard.

**Estimated Timeline** (pending SME review cycles):
- Ch4 (Model Serving): 3 weeks
- Ch5 (MaaS Platform): 3 weeks  
- Ch6 (Developer Integration): 2 weeks
- **Total**: 8 weeks to complete full MaaS training stack

This assumes no major architectural changes from SME feedback.

---

## Next Steps

1. **SME Review**: Review Ch1-3 content and provide feedback
2. **Alignment Meeting**: Discuss Ch4-6 scope and any adjustments
3. **Proceed with Ch4**: Begin Model Serving chapter upon approval
4. **Iterative Review**: Each new chapter reviewed before moving to next layer

---

## Contact

For questions or to schedule a review session, please reach out to the course development team.

**Current Content Review**: See repository at `maas-gpu-enablement` or request demo build.
