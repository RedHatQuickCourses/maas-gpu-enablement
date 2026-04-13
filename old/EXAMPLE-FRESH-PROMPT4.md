# Example Fresh Prompt for New Content

This is a complete, ready-to-paste example for your next fresh conversation with Claude.

---

## COPY EVERYTHING BELOW THIS LINE AND PASTE INTO NEW CHAT

---

I'm creating content for the **maas-gpu-enablement** course. This is part of an ongoing content development effort, and I need to maintain consistency with existing materials.

## Course Information

**Course**: Nvidia Accelerator Configuration for Scale (maas-gpu-enablement)
**Working Directory**: `/Users/kaknox/Documents/GitHub/maas-gpu-enablement/`
**Current Chapter**: Chapter 3 - Observability and Monitoring
**Target Section**: s1-observability-overview.adoc (new section)

## Style and Quality Standards

**Primary Style Reference**: 
Read this file to understand the required style, depth, and structure:
`/Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

**Style Guide**:
Follow the patterns documented in:
`/Users/kaknox/Documents/GitHub/maas-gpu-enablement/STYLE-GUIDE.md`

**Terminology Reference**:
Check canonical definitions in:
`/Users/kaknox/Documents/GitHub/maas-gpu-enablement/TERMINOLOGY.md`

**Key Style Requirements**:
- Depth: Conceptual (WHY) + Architectural (WHAT) + Tactical (HOW)
- Tone: Technical depth with business context
- Audience: Platform Engineers working on production enterprise AI platforms
- Examples: Concrete scenarios with specific timing/metrics (not "quickly" - use "45 seconds")
- Callouts: Production guidance (TIP), warnings (WARNING), critical info (IMPORTANT)
- Integration: Reference Chapter 1 and Chapter 2 concepts, prepare for observability lab

## Integration Requirements

**This content builds on**:
- Chapter 1 (GPU Operator): Deployed GPU infrastructure with ClusterPolicy, operator reconciliation
- Chapter 2 (Configuration): Configured and deployed GPU resources in operation

**This content prepares for**:
- Chapter 3, Section 2 (Lab): Implementing monitoring stack hands-on
- Production operations: Observing and troubleshooting GPU infrastructure

**Cross-references needed**:
- Link to GPU Operator from Chapter 1
- Reference deployed infrastructure from Chapter 2

## Content Request

**GOAL**: Create a single comprehensive page on monitoring and observability for GPU infrastructure

**TARGET AUDIENCE**:
- Role: Platform Engineer
- Expertise Level: Intermediate (completed Chapter 1 on operators and Chapter 2 on configuration)
- Use Case Context: Production enterprise AI platform requiring visibility into GPU utilization, performance, and health

**SCOPE**:

Must Cover:
- Why observability matters for GPU infrastructure (business driver: uptime, utilization, cost optimization)
- The problem observability solves (blind spots, reactive troubleshooting, resource waste)
- Key metrics for GPU monitoring (utilization, memory usage, temperature, power consumption, error rates)
- Monitoring stack architecture (DCGM exporter, Prometheus, Grafana)
- GPU metrics collection via NVIDIA DCGM (Data Center GPU Manager)
- Integration with existing monitoring infrastructure
- Critical dashboards and alerts for production operations
- Trade-offs: Built-in monitoring vs. third-party solutions (decision matrix)
- Production considerations (metric retention, alert thresholds, performance overhead)

Must Exclude:
- Deep dive into Prometheus/Grafana setup (assume familiarity or provide basic setup only)
- Advanced custom metric development beyond standard DCGM metrics
- Application-level AI/ML performance monitoring (focus on infrastructure)
- Cost analysis and chargeback implementation (out of scope)

Placement:
- Course: maas-gpu-enablement
- Chapter: ch3-observability
- Position: First section after chapter index (s1-observability-overview.adoc)

**REFERENCE MATERIALS**:

Style Reference:
- Primary: `/Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`
- Pattern to match: Section 5 "Three-Layer MaaS Operator Stack" shows good depth for technical architecture

Content Reference:
- Check if `operators-reference/` directory exists with vendor documentation
- NVIDIA DCGM Documentation: https://docs.nvidia.com/datacenter/dcgm/latest/
- GPU Operator Monitoring: https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-operator-metrics.html
- DCGM Exporter: https://github.com/NVIDIA/dcgm-exporter

**DEPTH AND STYLE**:

Reading Time: 20 minutes

Content Balance:
- Conceptual (WHY): 30% - Business case for monitoring (uptime, cost optimization, capacity planning)
- Architectural (WHAT): 40% - Monitoring stack components, metrics architecture, data flow
- Practical (HOW): 30% - Deployment examples, query commands, dashboard configuration

Tone:
- [X] Technical depth with business context
- [X] Production-ready guidance (production monitoring strategies)
- [X] Self-contained (assumes Chapter 1 and 2 knowledge of deployed GPU infrastructure)

Required Elements:
- [ ] Concrete example: Production AI platform monitoring 20 GPU nodes with alert thresholds
- [ ] Before/After comparison: Troubleshooting blind vs. with comprehensive monitoring
- [ ] ASCII diagram: Monitoring stack architecture (DCGM → Prometheus → Grafana)
- [ ] Decision matrix: When to use DCGM vs. third-party monitoring solutions (production decision point)
- [ ] Callouts: TIP for production alert thresholds, WARNING about metric collection overhead
- [ ] Annotated YAML for DCGM exporter deployment
- [ ] Specific metrics: "GPU utilization 85%", "memory usage 32GB/40GB", "temperature 78°C" (not vague)
- [ ] Integration: Reference GPU Operator from Chapter 1, deployed infrastructure from Chapter 2

**SUCCESS CRITERIA**:

Learning Objectives - Students should be able to:
- Explain why monitoring is critical for GPU infrastructure and articulate business value (uptime, optimization, cost control)
- Identify key GPU metrics to monitor (utilization, memory, temperature, power, errors)
- Understand the monitoring stack architecture (DCGM, Prometheus, Grafana)
- Deploy DCGM exporter to collect GPU metrics from infrastructure
- Configure meaningful alerts and dashboards for production operations
- Make informed decisions about monitoring strategies and tools

Verification:
- Students can list critical GPU metrics and explain their significance
- Students can describe the data flow from GPU to monitoring dashboard
- Students can deploy DCGM exporter and verify metric collection

Integration Points:
- Builds on: Chapter 1 GPU Operator deployment, Chapter 2 configured infrastructure in operation
- Prepares for: Chapter 3 monitoring lab, production operations and troubleshooting
- Cross-references: GPU Operator (ch1-gpu-operator), deployed infrastructure (Chapter 2)

## Reference Materials

If `operators-reference/` directory exists in the repository, please read all files there to understand monitoring concepts and configuration examples.

If not, use the online NVIDIA DCGM and GPU Operator documentation URLs provided above as reference for technical accuracy.

## Instructions

1. **Read the style reference** (`s2-operators-overview.adoc`) first to understand depth and structure expectations
2. **Read the style guide** (`STYLE-GUIDE.md`) to understand writing patterns and quality standards
3. **Check terminology** (`TERMINOLOGY.md`) for canonical definitions of terms from prior chapters
4. **Read reference materials** (observability-reference/ or online docs) to gather accurate monitoring technical details
5. **Use Plan Mode** to design the page outline before writing any content
6. **Present the plan** for my review and approval before implementing
7. **After approval**, create the content following the approved plan
8. **Verify integration** by checking that:
   - GPU Operator is referenced with link to Chapter 1
   - Monitoring builds on deployed infrastructure from Chapters 1 and 2
   - Transitions to next section are smooth
9. **Update files**:
   - Create `modules/ch3-observability/pages/s1-observability-overview.adoc`
   - Update `modules/ch3-observability/nav.adoc` to include new section
   - Update chapter index if needed
10. **Build and verify** with `npm run build` to ensure no errors

---

## END OF PROMPT TO PASTE

---

# How to Use This Example

1. **Copy everything between the "COPY EVERYTHING BELOW" markers above**
2. **Customize for your actual topic**:
   - Change chapter/section names
   - Update "Must Cover" topics
   - Adjust reference materials
   - Modify success criteria
3. **Paste into new Claude conversation**
4. **Wait for Claude to read and create plan**
5. **Review plan and approve**
6. **Claude implements**

## Customization Points

When adapting this for your next topic, change:

- **Course Information** section: Chapter name, section name
- **Integration Requirements**: What it builds on, what it prepares for
- **SCOPE - Must Cover**: Your specific topics
- **SCOPE - Must Exclude**: What to defer
- **Reading Time**: Estimate based on content volume
- **Required Elements**: Examples specific to your topic
- **Learning Objectives**: What students should be able to do

## What NOT to Change

Keep these sections as-is:
- Style Reference paths (always point to s2-operators-overview.adoc)
- Style Guide reference
- Terminology reference
- Key Style Requirements (depth approach, tone)
- Instructions section (the workflow)
