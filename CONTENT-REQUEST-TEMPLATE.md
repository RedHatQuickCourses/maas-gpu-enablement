# Course Content Request Template

Use this template when requesting new course pages, sections, or labs. This ensures consistent depth, style, and quality across all course materials.

## Template Structure

```markdown
GOAL: Create [single page | section | lab | chapter] on [topic]

TARGET AUDIENCE:
- Role: [Platform Engineer | Developer | SRE | Architect]
- Expertise Level: [Beginner | Intermediate | Advanced]
- Use Case Context: [Development | Testing | Production | Enterprise Scale]

SCOPE:
Must Cover:
- [Topic 1 with specific subtopics]
- [Topic 2 with specific subtopics]
- [Topic 3 with specific subtopics]

Must Exclude:
- [Topics to defer to other sections]
- [Out-of-scope content]

Placement:
- Course: [course name]
- Chapter: [chapter number/name]
- Position: [Before X / After Y / Between X and Y]

REFERENCE MATERIALS:
Style Reference:
- Primary: /Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc
- Secondary: [Any additional style references]

Content Reference:
- [Path to vendor documentation]
- [Path to example materials]
- [Path to PDFs or external docs]

DEPTH AND STYLE:
Reading Time: [X minutes]
Content Balance:
- Conceptual (WHY): [X%]
- Architectural (WHAT): [Y%]
- Practical (HOW): [Z%]

Tone:
- [X] Technical depth with business context
- [X] Production-ready guidance
- [X] Self-contained (assumes prior chapters read)

Required Elements:
- [ ] Concrete examples with real scenarios
- [ ] Before/After comparisons
- [ ] ASCII diagrams where helpful
- [ ] Decision matrices for production choices
- [ ] Callouts (TIP, WARNING, NOTE, IMPORTANT)
- [ ] Annotated YAML/code examples
- [ ] Specific timing/metrics (not "quickly" - use "45 seconds")
- [ ] Integration with course narrative

SUCCESS CRITERIA:
Learning Objectives - Students should be able to:
- [Objective 1 - action verb + specific outcome]
- [Objective 2 - action verb + specific outcome]
- [Objective 3 - action verb + specific outcome]

Verification:
- [How to verify students achieved objectives]

Integration Points:
- Builds on: [Previous section concepts]
- Prepares for: [Next section concepts]
- Cross-references: [Related chapters/sections]
```

---

## Example Request (Using This Template)

```markdown
GOAL: Create single page on GPU Multi-Instance GPU (MIG) configuration

TARGET AUDIENCE:
- Role: Platform Engineer
- Expertise Level: Intermediate (completed Chapter 1 operators)
- Use Case Context: Production enterprise AI platform with multi-tenant workloads

SCOPE:
Must Cover:
- What is MIG and why it exists (business driver: GPU utilization)
- MIG profiles (1g.5gb, 2g.10gb, 3g.20gb, 4g.20gb, 7g.40gb)
- MIG modes: Single vs. Mixed
- Enabling MIG via ClusterPolicy
- Node labeling and scheduling with MIG
- Trade-offs: MIG vs. time-slicing vs. full GPU allocation

Must Exclude:
- MIG performance benchmarking (defer to observability chapter)
- Advanced MIG partitioning strategies (out of scope)

Placement:
- Course: maas-gpu-enablement
- Chapter: ch2-mig
- Position: First section after chapter index

REFERENCE MATERIALS:
Style Reference:
- Primary: /Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc
- Secondary: /Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s1-hardware-stack.adoc

Content Reference:
- /Users/kaknox/Documents/GitHub/maas-gpu-enablement/mig-reference/ (if exists)
- NVIDIA MIG User Guide: https://docs.nvidia.com/datacenter/tesla/mig-user-guide/
- GPU Operator MIG documentation

DEPTH AND STYLE:
Reading Time: 20 minutes
Content Balance:
- Conceptual (WHY): 30% - Business case for MIG
- Architectural (WHAT): 40% - MIG profiles, modes, architecture
- Practical (HOW): 30% - Configuration examples

Tone:
- [X] Technical depth with business context
- [X] Production-ready guidance (production decision matrices)
- [X] Self-contained (assumes Chapter 1 knowledge of operators)

Required Elements:
- [ ] Concrete example: Multi-tenant inference platform sharing A100-40GB
- [ ] Before/After: Cluster utilization with/without MIG
- [ ] ASCII diagram: MIG profile partitioning on single GPU
- [ ] Decision matrix: When to use MIG vs. time-slicing vs. full GPU
- [ ] Callouts: TIP for production MIG mode selection, WARNING about reconfiguration downtime
- [ ] Annotated ClusterPolicy YAML with MIG enabled
- [ ] Specific metrics: "7x higher utilization", "reduces idle time from 60% to 15%"
- [ ] Integration: References ClusterPolicy from Chapter 1

SUCCESS CRITERIA:
Learning Objectives - Students should be able to:
- Explain what MIG is and articulate business value (improved utilization)
- Identify appropriate MIG profiles for workload requirements
- Choose between MIG modes (Single vs. Mixed) for production use cases
- Enable MIG via ClusterPolicy Custom Resource
- Verify MIG configuration via node labels and GPU resource counts

Verification:
- Students can determine correct MIG profile for given workload specs
- Students can explain trade-offs between MIG and alternatives

Integration Points:
- Builds on: Chapter 1 ClusterPolicy configuration, operator reconciliation
- Prepares for: MIG deployment lab, observability chapter (monitoring MIG instances)
- Cross-references: Chapter 3 for monitoring MIG utilization
```

---

## Instructions for Claude

When receiving this template:

1. **Use Plan Mode**: Always use plan mode to design before writing
2. **Read References**: Read all reference materials FIRST
3. **Extract Patterns**: Analyze style reference for:
   - Section structure patterns
   - Heading hierarchy
   - Callout usage patterns
   - Code example formatting
   - Transition text between sections
4. **Create Outline**: Design detailed outline matching reference style
5. **Get Approval**: Present plan before writing content
6. **Write Content**: Follow approved plan with reference style
7. **Verify Integration**: Ensure cross-references and transitions work

---

## Quality Checklist

Before marking content complete, verify:

### Content Depth
- [ ] Explains WHY (business value, problem it solves)
- [ ] Explains WHAT (concepts, components, architecture)
- [ ] Explains HOW (configuration, commands, workflow)
- [ ] Includes concrete examples (not generic/abstract)
- [ ] Uses specific metrics/timing (not vague terms)

### Technical Accuracy
- [ ] YAML examples are valid and tested
- [ ] Commands include expected output
- [ ] Version-specific details are correct
- [ ] Terminology matches official documentation

### Course Integration
- [ ] Builds on previous sections (references prior concepts)
- [ ] Prepares for next sections (previews upcoming content)
- [ ] Cross-references work (xref links are valid)
- [ ] Transitions are smooth (What's Next sections)

### Production Guidance
- [ ] Decision matrices for production choices
- [ ] Best practices callouts (TIP)
- [ ] Anti-patterns warnings (WARNING)
- [ ] Support and SLA considerations

### Readability
- [ ] Reading time estimate accurate
- [ ] Headings follow hierarchy (=, ==, ===, ====)
- [ ] Code examples are annotated (<1> callouts)
- [ ] ASCII diagrams are formatted correctly
- [ ] Callouts enhance (not distract from) content

### AsciiDoc Quality
- [ ] Builds without errors (`npm run build`)
- [ ] Navigation links work
- [ ] Images render correctly
- [ ] Tables display properly
- [ ] Code syntax highlighting works
