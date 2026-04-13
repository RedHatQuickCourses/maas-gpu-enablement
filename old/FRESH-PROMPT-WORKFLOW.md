# Fresh Prompt Workflow for Course Consistency

When starting a new conversation session (fresh prompt) to create additional course content, follow this workflow to maintain consistency with existing materials.

---

## Overview

**Problem**: Each new Claude conversation starts fresh without context from previous sessions.

**Solution**: Provide structured context upfront to ensure:
- Consistent style and depth
- Terminology alignment
- Narrative continuity
- Technical accuracy

---

## Pre-Request Preparation (YOU DO)

### Step 1: Identify Reference Materials

Gather these materials before starting the conversation:

**Required:**
- [ ] Course structure file: `antora.yml`
- [ ] Style reference: `modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`
- [ ] Style guide: `STYLE-GUIDE.md`
- [ ] Request template: `CONTENT-REQUEST-TEMPLATE.md`

**For the specific topic:**
- [ ] Any vendor documentation (PDFs, links)
- [ ] Existing related pages in the course
- [ ] Reference implementations from other sources

### Step 2: Map Integration Points

Before requesting new content, identify:

**Prior concepts it builds on:**
- Chapter/section references: [list]
- Key terms already defined: [list]
- Prerequisites students must know: [list]

**Future concepts it prepares:**
- Next section preview: [description]
- Concepts introduced here: [list]

**Cross-references needed:**
- Related chapters: [list]
- Labs that use this content: [list]

### Step 3: Fill Out Request Template

Complete the `CONTENT-REQUEST-TEMPLATE.md` with:
- Specific topic details
- Required vs. excluded content
- Integration points identified in Step 2
- Reference materials from Step 1

---

## Fresh Prompt Structure

Use this exact structure when starting a new conversation:

```markdown
# CONTEXT: Course Content Creation Request

I'm creating content for the **[Course Name]** course. This is part of an ongoing content development effort, and I need to maintain consistency with existing materials.

## Course Information

**Course**: [Course name from antora.yml]
**Working Directory**: /Users/kaknox/Documents/GitHub/[course-repo]/
**Current Chapter**: [chapter number/name]
**Target Section**: [new section name/number]

## Style and Quality Standards

**Primary Style Reference**: 
Read this file to understand the required style, depth, and structure:
`/Users/kaknox/Documents/GitHub/[course-repo]/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

**Style Guide**:
Follow the patterns documented in:
`/Users/kaknox/Documents/GitHub/[course-repo]/STYLE-GUIDE.md`

**Key Style Requirements**:
- Depth: Conceptual (WHY) + Architectural (WHAT) + Tactical (HOW)
- Tone: Technical depth with business context
- Audience: Platform Engineers working on production enterprise AI platforms
- Examples: Concrete scenarios with specific timing/metrics
- Callouts: Production guidance (TIP), warnings (WARNING), critical info (IMPORTANT)

## Integration Requirements

**This content builds on**:
- [Chapter/Section]: [Key concepts students already learned]
- [Chapter/Section]: [Prior knowledge to reference]

**This content prepares for**:
- [Next Section/Lab]: [How this section sets up future content]

**Cross-references needed**:
- Link to: [existing pages to reference]

## Content Request

[PASTE YOUR FILLED-OUT CONTENT-REQUEST-TEMPLATE.md HERE]

## Reference Materials

I'm providing the following reference materials in this directory:
`/Users/kaknox/Documents/GitHub/[course-repo]/[reference-dir]/`

Files include:
- [file1.pdf]: [description]
- [file2.pdf]: [description]

Please read these materials to understand the style and depth I'm looking for.

## Instructions

1. **Read the style reference** (s2-operators-overview.adoc) to understand depth and structure
2. **Read the style guide** (STYLE-GUIDE.md) to understand writing patterns
3. **Read reference materials** in [reference-dir]/ to gather technical content
4. **Use Plan Mode** to design the page before writing
5. **Present the plan** for review before implementing
6. **Verify integration** with existing course structure after implementation
```

---

## Conversation Workflow (CLAUDE DOES)

### Phase 1: Context Loading

**Claude should**:
1. Read `antora.yml` to understand course structure
2. Read style reference (`s2-operators-overview.adoc`) to extract patterns
3. Read `STYLE-GUIDE.md` to understand requirements
4. Read any reference materials provided
5. Read integration point pages to understand context

**Expected output**: Confirmation of what was read and key takeaways

### Phase 2: Planning

**Claude should**:
1. Launch Explore agents to read reference materials
2. Launch Plan agent to design page outline
3. Present detailed plan including:
   - Section structure matching style guide
   - Integration points with existing content
   - Code examples planned
   - Estimated reading time
   - How it matches reference style

**Expected output**: Detailed implementation plan

### Phase 3: Review and Refinement

**You do**:
1. Review the plan
2. Identify any gaps or misalignments
3. Clarify requirements
4. Approve or request changes

**Claude does**:
1. Incorporates feedback
2. Updates plan
3. Confirms understanding

### Phase 4: Implementation

**Claude should**:
1. Create new content file(s)
2. Update navigation (`nav.adoc`)
3. Update chapter index if needed
4. Update transition text in adjacent sections
5. Build course to verify (`npm run build`)
6. Check for errors and broken links

**Expected output**: All files created/updated, build successful

### Phase 5: Verification

**Claude should verify**:
- [ ] Content matches style guide patterns
- [ ] All three depth layers present (WHY/WHAT/HOW)
- [ ] Concrete examples included
- [ ] Production guidance present
- [ ] Integration points work
- [ ] Cross-references are valid
- [ ] Build is clean (no errors)
- [ ] Reading time is accurate

**Expected output**: Verification checklist with results

---

## Maintaining Terminology Consistency

### Terminology Reference Document

Create and maintain: `TERMINOLOGY.md`

**Structure**:
```markdown
# Course Terminology

## Operators and OLM
- **Operator**: [Canonical definition from ch1]
- **Custom Resource (CR)**: [Canonical definition]
- **ClusterPolicy**: [Specific to NVIDIA GPU Operator, definition]

## GPU Concepts
- **MIG (Multi-Instance GPU)**: [Definition]
- **MIG Profile**: [Definition]

## OpenShift AI
- **DataScienceCluster**: [Definition]
- **Models-as-a-Service (MaaS)**: [Definition]

[Continue for all key terms...]
```

### Terminology Checklist for New Content

Before finalizing new content:
- [ ] Check all technical terms against `TERMINOLOGY.md`
- [ ] If introducing new terms, define on first use
- [ ] Add new canonical definitions to `TERMINOLOGY.md`
- [ ] Reference prior definitions instead of re-defining

---

## Cross-Chapter Consistency Checklist

### Before Starting New Chapter/Section

**Review**:
- [ ] What terms are already defined in prior chapters?
- [ ] What examples are already used (avoid repetition)?
- [ ] What style patterns exist in the same chapter?
- [ ] What reading time/depth level is consistent with chapter?

### During Content Creation

**Ensure**:
- [ ] References to prior chapters use `xref:` links
- [ ] Terminology matches `TERMINOLOGY.md`
- [ ] Examples are distinct from prior chapters (no copy-paste scenarios)
- [ ] Difficulty progression is appropriate (builds on prior knowledge)

### After Content Creation

**Verify**:
- [ ] New terms added to `TERMINOLOGY.md`
- [ ] Related pages updated with cross-references
- [ ] Chapter index reflects new content
- [ ] Navigation is updated
- [ ] Build is clean

---

## Example: Maintaining Narrative Continuity

### Chapter 1 Creates Foundation

Chapter 1 establishes:
- Operators provide self-healing automation
- ClusterPolicy is the CR for GPU Operator
- OLM manages operator lifecycle
- Three-layer MaaS operator stack

### Chapter 2 Builds On It

When creating Chapter 2 content (MIG), reference Chapter 1:

**✅ GOOD - References Prior Knowledge:**
```asciidoc
In Chapter 1, you configured the GPU Operator via the ClusterPolicy
Custom Resource. To enable MIG, you'll edit the same ClusterPolicy
to add MIG-specific configuration:

[source,yaml]
----
apiVersion: nvidia.com/v1
kind: ClusterPolicy
metadata:
  name: gpu-cluster-policy
spec:
  mig:
    strategy: mixed  # <1>
----
<1> New MIG configuration added to existing ClusterPolicy from Chapter 1
```

**❌ BAD - Doesn't Reference:**
```asciidoc
Edit the ClusterPolicy to enable MIG.
```

### Chapter 3 Continues Narrative

When creating Chapter 3 (Observability), reference both prior chapters:

**✅ GOOD:**
```asciidoc
In Chapter 1, you deployed DCGM for GPU monitoring. In Chapter 2,
you enabled MIG partitioning. This chapter shows how to observe
both full GPU metrics and per-MIG-instance metrics using the DCGM
Exporter you deployed in Chapter 1.
```

---

## Updating CLAUDE.md for Fresh Prompts

After creating new high-quality content, update the project's `CLAUDE.md`:

### Add to CLAUDE.md

```markdown
## Content Style Standards

**Style Reference Page**: 
`modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

This page demonstrates the required depth, structure, and quality for all course content.

**Style Guide**: `STYLE-GUIDE.md`
**Request Template**: `CONTENT-REQUEST-TEMPLATE.md`
**Fresh Prompt Workflow**: `FRESH-PROMPT-WORKFLOW.md`

When creating new course content:
1. Read the style reference page to understand depth expectations
2. Follow the style guide patterns
3. Use the request template to structure requirements
4. Follow the fresh prompt workflow for consistency

**Key Quality Standards**:
- All concepts must include: WHY (business value) + WHAT (architecture) + HOW (usage)
- Examples must be concrete with specific timing/metrics
- Production guidance required (decision matrices, best practices)
- Integration with prior/future chapters mandatory
```

---

## Quick Reference: Fresh Prompt Checklist

**Before starting conversation**:
- [ ] Fill out `CONTENT-REQUEST-TEMPLATE.md`
- [ ] Gather reference materials
- [ ] Identify integration points
- [ ] Check terminology in existing chapters

**In fresh prompt, provide**:
- [ ] Course and chapter context
- [ ] Path to style reference (s2-operators-overview.adoc)
- [ ] Path to style guide (STYLE-GUIDE.md)
- [ ] Filled-out request template
- [ ] Reference materials directory
- [ ] Integration requirements

**During conversation, ensure Claude**:
- [ ] Reads style reference first
- [ ] Uses plan mode
- [ ] Presents plan before writing
- [ ] Verifies integration points
- [ ] Builds and tests content

**After content creation**:
- [ ] Update `TERMINOLOGY.md` with new terms
- [ ] Update `CLAUDE.md` if patterns change
- [ ] Document any new style patterns found
- [ ] Commit all changes together

---

## Common Pitfalls and Solutions

### Pitfall 1: Claude doesn't match style depth

**Symptom**: Content is too shallow or too tutorial-like

**Solution**: 
- Explicitly ask Claude to read s2-operators-overview.adoc first
- Point out specific sections as examples: "Match the depth of the 'Three-Layer MaaS Operator Stack' section"
- Request plan mode to design before writing

### Pitfall 2: Terminology inconsistency

**Symptom**: Different terms for same concept across chapters

**Solution**:
- Maintain `TERMINOLOGY.md` and reference it in every fresh prompt
- Ask Claude to verify terminology against prior chapters
- Include prior chapter pages in the fresh prompt references

### Pitfall 3: Missing integration with prior concepts

**Symptom**: Content stands alone, doesn't reference prior chapters

**Solution**:
- Explicitly list "builds on" requirements in request template
- Ask Claude to read prior chapter pages before planning
- Review transitions between sections for continuity

### Pitfall 4: Style drift over time

**Symptom**: Later chapters don't match Chapter 1 quality

**Solution**:
- Always use s2-operators-overview.adoc as style reference
- Periodically review `STYLE-GUIDE.md` and update with new patterns
- Use plan mode for every major content piece

---

## Template: Quick Start Message for Fresh Prompts

Copy this template for quick fresh prompt starts:

```markdown
I'm creating content for the **maas-gpu-enablement** course.

**Context**:
- Working Directory: /Users/kaknox/Documents/GitHub/maas-gpu-enablement
- Chapter: [chapter name]
- New Section: [section name]

**Style Requirements**:
Match the depth and style of:
`modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

Follow patterns in:
`STYLE-GUIDE.md`

**Integration**:
Builds on: [prior chapters/sections]
Prepares for: [next section]

**Request**:
[Paste filled-out CONTENT-REQUEST-TEMPLATE.md]

**Reference Materials**:
Located in: `[reference-dir]/`
- [list files]

**Instructions**:
1. Read style reference (s2-operators-overview.adoc)
2. Read style guide (STYLE-GUIDE.md)
3. Read reference materials
4. Use plan mode to design
5. Present plan for approval
6. Implement after approval
```

---

## Verification: Is Your Fresh Prompt Ready?

**Before starting the conversation, confirm**:

✅ **Context Section**:
- [ ] Course name and working directory specified
- [ ] Chapter and section clearly identified
- [ ] Style reference path provided
- [ ] Style guide path provided

✅ **Integration Section**:
- [ ] Prior chapters/concepts listed
- [ ] Future concepts this prepares listed
- [ ] Cross-reference needs identified

✅ **Request Section**:
- [ ] Request template filled out completely
- [ ] Target audience specified
- [ ] Must-cover topics listed
- [ ] Must-exclude topics listed
- [ ] Reading time estimated

✅ **Reference Materials**:
- [ ] Reference directory specified
- [ ] All reference files listed and described
- [ ] Vendor docs or examples provided

✅ **Instructions**:
- [ ] Explicitly asks to read style reference
- [ ] Explicitly asks to use plan mode
- [ ] Explicitly asks for approval before writing

If all checkboxes are ✅, you're ready to start the fresh prompt conversation with consistent results.
