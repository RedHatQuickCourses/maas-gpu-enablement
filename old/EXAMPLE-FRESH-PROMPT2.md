# Example Fresh Prompt for New Content

This is a complete, ready-to-paste example for your next fresh conversation with Claude.

---

## COPY EVERYTHING BELOW THIS LINE AND PASTE INTO NEW CHAT

---

I'm creating content for the **maas-gpu-enablement** course. This is part of an ongoing content development effort, and I need to maintain consistency with existing materials.

## Course Information

**Course**: Nvidia Accelerator Configuration for Scale (maas-gpu-enablement)
**Working Directory**: `/Users/kaknox/Documents/GitHub/maas-gpu-enablement/`
**Current Chapter**: Chapter 1 - Operator Foundations and GPU Stack Deployment
**Target Section**: s3-deploy-operators-lab.adoc (update section)

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
- Integration: Reference Chapter 1 concepts, prepare for Chapter 2 lab

## Integration Requirements

**This content builds on**:
- Chapter 1, Section 2 (Understanding Operators and Platform Automation): ClusterPolicy Custom Resource, operator reconciliation
- Chapter 1, Section 3 (Lab): Deployed GPU Operator with ClusterPolicy

**This content prepares for**:
- Chapter 2, Section 2 (Lab): Deploying MIG configurations hands-on
- Chapter 3 (Observability): Monitoring MIG instances

**Cross-references needed**:
- Link to ClusterPolicy definition from Chapter 1
- Reference GPU Operator from Chapter 1

## Content Request

**GOAL**: Create a single comprehensive page on Nvidia GPU OPerator and the features that can be enabled, how they work and build from fundamentals.

**TARGET AUDIENCE**:
- Role: Platform Engineer
- Expertise Level: Intermediate (completed Chapter 1 on operators section)
- Use Case Context: Production enterprise AI platform with multi-tenant workloads needing efficient GPU sharing, maximize GPU ROI for Enterprise.

**SCOPE**:

Must Cover:
- Nvidia GPU Operation (driver: dcgm, dcgm exporter, container toolkit, dfg, MIG Manager, Sharing)
- The problem Operator solves (underutilized GPUs, inability to share across teams)
- Node labeling and scheduling with MIG instances
- Trade-offs: Utilizing the various features and resource consumption
- Production considerations (reconfiguration downtime, workload placement)
-Export GPU metrics to OpenShift Dashboard
- Export GPU and cluster and node metrics to Grafana Operator Dashboard using template dashboard. 


Placement:
- Course: maas-gpu-enablement
- Chapter: ch1-lab
- Position: Next page after chapter index (s2-operators-overview.adoc)

**REFERENCE MATERIALS**:

Style Reference:
- Primary: `/Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`
- Pattern to match: Section 5 "Three-Layer MaaS Operator Stack" shows good depth for technical architecture

Content Reference:
look in teh operator-reference directory for additional context documents. 

**DEPTH AND STYLE**:

Reading Time: 20 minutes

Content Balance:
- Conceptual (WHY): 30% - Business case  (utilization metrics, cost savings)
- Architectural (WHAT): 40% -Enable Operator features - how  works
- Practical (HOW): 30% - Configuration examples, verification commands

Tone:
- [X] Technical depth with business context
- [X] Production-ready guidance (production decision matrices)
- [X] Self-contained (assumes Chapter 1 knowledge of operators and ClusterPolicy)


**SUCCESS CRITERIA**:

Learning Objectives - Students should be able to:
- Explain what Nvidia GPU Operator does and articulate business value (improved GPU utilization, multi-tenant isolation)
- Identify appropriate Operator settings  given workload requirements (memory, compute)
- Explain trade-offs between MIG, time-slicing, and full GPU allocation
- Make informed production decisions about configuration

Verification:
- Students can determine correct policies for workload with specific GPU needs
- Students can explain how metrics collection works and view gpu information and stats
- Students can configure Nvidia GPU Operator Policies YAML

Integration Points:
- Prepares for: Chapter 2 MIG deployment lab, Chapter 3 monitoring MIG instances
- Cross-references: ClusterPolicy (ch1-gpu-operator/s2-operators-overview.adoc)

## Reference Materials

If `operatopr-reference/` directory exists in the repository, please read all files there to understand concepts and configuration examples.

If not, use the online NVIDIA documentation URLs provided above as reference for technical accuracy.

## Instructions

1. **Read the style reference** (`s2-operators-overview.adoc`) first to understand depth and structure expectations
2. **Read the style guide** (`STYLE-GUIDE.md`) to understand writing patterns and quality standards
3. **Check terminology** (`TERMINOLOGY.md`) for canonical definitions of terms from Chapter 1 (ClusterPolicy, Operator, Custom Resource, etc.)
4. **Read reference materials** (mig-reference/ or online docs) to gather accurate MIG technical details
5. **Use Plan Mode** to design the page outline before writing any content
6. **Present the plan** for my review and approval before implementing
7. **After approval**, create the content following the approved plan
8. **Verify integration** by checking that:
   - ClusterPolicy is referenced with link to Chapter 1 definition
   - MIG configuration builds on Chapter 1 operator knowledge
   - Transitions to next section are smooth
9. **Update files**:
   - Update `modules/ch1-gpu-operator/pages/s3-deploy-operators.adoc` to include new section
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
