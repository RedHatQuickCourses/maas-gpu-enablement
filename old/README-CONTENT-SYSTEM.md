# Course Content Creation System

This repository includes a comprehensive system for creating consistent, high-quality course content across fresh conversation sessions with Claude Code.

---

## Quick Start

### For Your Next Content Request

1. **Read the style reference**:
   ```
   modules/ch1-gpu-operator/pages/s2-operators-overview.adoc
   ```
   This shows the depth, structure, and quality expected for all content.

2. **Fill out the request template**:
   ```
   CONTENT-REQUEST-TEMPLATE.md
   ```
   Provides the structure for your content request.

3. **Start fresh conversation with**:
   ```
   FRESH-PROMPT-WORKFLOW.md → "Template: Quick Start Message for Fresh Prompts"
   ```
   Ensures Claude has the right context from the start.

4. **Claude creates content following**:
   ```
   STYLE-GUIDE.md
   ```
   Extracts all patterns from the reference implementation.

5. **Maintain consistency with**:
   ```
   TERMINOLOGY.md
   ```
   Ensures terms are used consistently across chapters.

---

## System Components

### 📋 CONTENT-REQUEST-TEMPLATE.md
**Purpose**: Structured template for requesting new course content

**Use when**: Starting any new page, section, lab, or chapter

**Key sections**:
- Target Audience
- Scope (must cover / must exclude)
- Reference Materials
- Depth and Style requirements
- Success Criteria

**Example included**: MIG configuration page request

---

### 🎨 STYLE-GUIDE.md
**Purpose**: Comprehensive style patterns extracted from s2-operators-overview.adoc

**Use when**: Writing or reviewing course content

**Covers**:
- Document structure patterns (headings, frontmatter, transitions)
- Writing style (tone, voice, concrete vs. abstract)
- Example patterns (scenarios, before/after, code examples)
- Callout usage (TIP, WARNING, NOTE, IMPORTANT)
- Tables and decision matrices
- Three depth levels (WHY/WHAT/HOW)
- Quality standards and anti-patterns
- Review checklist

**Key sections**:
- Section 2: Writing Style Patterns
- Section 4: Code Example Conventions
- Section 7: Depth Levels by Knowledge Type
- Section 12: Review Checklist

---

### 🔄 FRESH-PROMPT-WORKFLOW.md
**Purpose**: Step-by-step workflow for maintaining consistency across fresh conversation sessions

**Use when**: Starting a new Claude conversation for content creation

**Covers**:
- Pre-request preparation steps
- Fresh prompt structure template
- Conversation workflow phases
- Terminology consistency maintenance
- Cross-chapter consistency checklist
- Common pitfalls and solutions
- Ready-to-use message templates

**Critical sections**:
- "Fresh Prompt Structure" (copy-paste template)
- "Maintaining Terminology Consistency"
- "Template: Quick Start Message for Fresh Prompts"

---

### 📖 TERMINOLOGY.md
**Purpose**: Canonical definitions for all technical terms used across the course

**Use when**: 
- Writing new content (check first)
- Referencing prior concepts
- Adding new terms after content approval

**Covers**:
- Operators and OLM terms (Operator, CR, CRD, Controller, CSV, etc.)
- GPU Components (NFD, GPU Operator, ClusterPolicy, DCGM, etc.)
- MaaS Architecture (Three-layer stack, Layer 1/2/3)
- OpenShift AI Components (DataScienceCluster, KServe, Kueue)
- Acronym reference table
- Deprecated/avoided terms

**Key features**:
- Exact canonical definition with source chapter
- First defined location for cross-referencing
- Usage patterns and examples
- Acronym expansion table

---

### 📚 README-CONTENT-SYSTEM.md (This File)
**Purpose**: Overview and quick reference for the entire system

---

## Workflow Diagrams

### Creating New Content: Full Workflow

```
┌─────────────────────────────────────────────────────┐
│ STEP 1: Preparation (YOU DO)                       │
│ - Read s2-operators-overview.adoc (style ref)      │
│ - Identify integration points with prior chapters  │
│ - Gather reference materials (PDFs, docs)          │
│ - Fill out CONTENT-REQUEST-TEMPLATE.md             │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 2: Fresh Prompt (YOU DO)                      │
│ - Use template from FRESH-PROMPT-WORKFLOW.md       │
│ - Include: context, style refs, filled template    │
│ - Specify integration requirements                 │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 3: Context Loading (CLAUDE DOES)              │
│ - Reads style reference                            │
│ - Reads STYLE-GUIDE.md                             │
│ - Reads reference materials                        │
│ - Reads integration point pages                    │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 4: Planning (CLAUDE DOES)                     │
│ - Uses Explore agents for reference materials      │
│ - Uses Plan agent to design outline                │
│ - Presents plan matching style guide               │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 5: Review (YOU DO)                            │
│ - Review plan for alignment                        │
│ - Clarify requirements                             │
│ - Approve or request changes                       │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 6: Implementation (CLAUDE DOES)               │
│ - Creates content following approved plan          │
│ - Updates navigation and transitions               │
│ - Builds course to verify                          │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 7: Verification (CLAUDE DOES)                 │
│ - Checks against STYLE-GUIDE.md review checklist   │
│ - Verifies terminology against TERMINOLOGY.md      │
│ - Confirms integration points work                 │
└─────────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────────┐
│ STEP 8: Post-Implementation (YOU DO)               │
│ - Review final content                             │
│ - Add new terms to TERMINOLOGY.md                  │
│ - Update CLAUDE.md if needed                       │
│ - Commit all changes together                      │
└─────────────────────────────────────────────────────┘
```

---

## Key Success Factors

### What Made s2-operators-overview.adoc Successful

1. **Reference materials provided**
   - PDFs showing desired style and depth
   - Technical documentation for accuracy
   - Example formats to match

2. **Specific content requirements**
   - Bulleted list of must-cover topics
   - Clear scope boundaries (include/exclude)
   - Target audience and context defined

3. **Plan-first approach**
   - Used specialized agents (Explore, Plan)
   - Designed outline before writing
   - Got approval before implementation

4. **Style consistency**
   - Referenced existing high-quality page
   - Matched depth across all sections
   - Maintained three-layer approach (WHY/WHAT/HOW)

5. **Integration clarity**
   - Clear position in course structure
   - Identified prior/future concepts
   - Smooth transitions

---

## Common Questions

### Q: How do I ensure depth consistency across chapters?

**A**: 
1. Always use `s2-operators-overview.adoc` as style reference
2. Include in fresh prompt: "Match the depth of Section X in s2-operators-overview.adoc"
3. Verify all three layers present (WHY/WHAT/HOW) in STYLE-GUIDE.md Section 7

### Q: How do I reference concepts from prior chapters?

**A**:
1. Check `TERMINOLOGY.md` for canonical definitions
2. Use pattern: `The ClusterPolicy Custom Resource (introduced in Chapter 1, Section 2)...`
3. Include actual prior chapter pages in fresh prompt for Claude to read

### Q: What if I'm not sure about terminology?

**A**:
1. Search `TERMINOLOGY.md` first
2. If not found, search existing course content
3. Define it once, add to `TERMINOLOGY.md` immediately
4. Use that definition consistently everywhere

### Q: How much should I tell Claude about prior content?

**A**:
For fresh prompts:
- **Always**: Include paths to style reference and style guide
- **Always**: List prior chapters this builds on
- **Often**: Include reference to specific prior pages to read
- **Sometimes**: Include prior chapter index pages for context

### Q: Can I skip the plan mode step?

**A**: 
- **For simple updates** (fixing typos, small edits): Yes
- **For new substantial content** (pages, sections, labs): No
- **Why**: Plan mode ensures alignment before writing, saves time on revisions

### Q: What if the content doesn't match the style guide?

**A**:
1. Point Claude to specific STYLE-GUIDE.md sections that were missed
2. Reference specific parts of s2-operators-overview.adoc as examples
3. Ask to revise specific sections rather than full rewrite
4. Update STYLE-GUIDE.md if you discover new patterns

---

## File Organization

### Primary Working Directory
```
/Users/kaknox/Documents/GitHub/maas-gpu-enablement/
```

### Content System Files (Root Level)
```
maas-gpu-enablement/
├── CONTENT-REQUEST-TEMPLATE.md    # Template for content requests
├── STYLE-GUIDE.md                 # Extracted style patterns
├── FRESH-PROMPT-WORKFLOW.md       # Workflow for fresh conversations
├── TERMINOLOGY.md                 # Canonical term definitions
├── README-CONTENT-SYSTEM.md       # This file - system overview
├── CLAUDE.md                      # Project instructions for Claude
└── antora.yml                     # Course structure
```

### Style Reference Implementation
```
modules/ch1-gpu-operator/pages/s2-operators-overview.adoc
```
**This is the gold standard.** All content should match this depth and style.

### Reference Materials Directory
```
operator-reference/                # Reference PDFs for operators
mig-reference/                     # Reference materials for MIG (if exists)
[topic]-reference/                 # Reference materials for other topics
```

---

## Templates and Examples

### Template 1: Quick Fresh Prompt

```markdown
I'm creating content for the **maas-gpu-enablement** course.

**Style Reference**: 
Match depth/style of: `modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`
Follow: `STYLE-GUIDE.md`

**New Content**: [Chapter X, Section Y on TOPIC]

**Integration**:
Builds on: [Chapter/Section]
Prepares for: [Chapter/Section]

**Request**: [Filled-out CONTENT-REQUEST-TEMPLATE.md]

**References**: Located in `[directory]/`

**Instructions**: Read style ref, use plan mode, present plan for approval.
```

### Template 2: Integration Reference

When referencing prior content:

```asciidoc
In Chapter 1, you learned about the ClusterPolicy Custom Resource
and how the GPU Operator uses it to manage the complete GPU stack.
To enable MIG, you'll add new configuration to that same ClusterPolicy:

[source,yaml]
----
apiVersion: nvidia.com/v1
kind: ClusterPolicy
metadata:
  name: gpu-cluster-policy  # <1>
spec:
  mig:
    strategy: mixed          # <2>
----
<1> Same ClusterPolicy from Chapter 1
<2> New MIG configuration added here
```

### Template 3: New Term Introduction

When introducing a new term:

```asciidoc
**Multi-Instance GPU (MIG)** is NVIDIA technology that partitions
a single physical GPU into up to seven independent GPU instances,
each with isolated memory and compute resources. This enables
higher utilization by allowing multiple workloads to share a
single GPU simultaneously.
```

Then add to `TERMINOLOGY.md`:
```markdown
### Multi-Instance GPU (MIG)
**Canonical Definition** (from ch2-mig/s1-mig-overview.adoc):
> Multi-Instance GPU (MIG) is NVIDIA technology that partitions a single physical GPU into up to seven independent GPU instances, each with isolated memory and compute resources.

**First Defined**: Chapter 2, Section 1
```

---

## Maintenance and Updates

### When to Update System Files

**Update STYLE-GUIDE.md when**:
- You discover new successful patterns in content
- Style reference evolves with course improvements
- Anti-patterns are identified that should be documented

**Update TERMINOLOGY.md when**:
- New content introduces new technical terms
- Product names change (e.g., RHODS → OpenShift AI)
- Terms are deprecated or become ambiguous

**Update FRESH-PROMPT-WORKFLOW.md when**:
- You discover better ways to structure fresh prompts
- Common pitfalls are identified
- Workflow steps change

**Update CONTENT-REQUEST-TEMPLATE.md when**:
- New section types are added (e.g., example template for labs)
- Required fields change
- Success criteria patterns evolve

### Version Control Best Practices

**Commit together**:
- New content file(s)
- Updated navigation
- Updated TERMINOLOGY.md (if new terms added)
- Updated index/transition files

**Commit message format**:
```
Add [Chapter X Section Y]: [Topic]

- Created s[N]-[topic-name].adoc (XX min read)
- Updated navigation and transitions
- Added N new terms to TERMINOLOGY.md
- Integration with: [prior chapters]
```

---

## Success Metrics

### Content Quality Checklist

Your content meets the standard when it has:

- [ ] **Three depth layers**: WHY (business value) + WHAT (architecture) + HOW (usage)
- [ ] **Concrete examples**: Specific scenarios with real timing/metrics
- [ ] **Production guidance**: Decision matrices, TIP/WARNING callouts
- [ ] **Integration**: References prior chapters, prepares for future content
- [ ] **Code quality**: Annotated YAML/commands with expected output
- [ ] **Terminology**: Consistent with TERMINOLOGY.md
- [ ] **Build success**: No errors from `npm run build`
- [ ] **Readability**: Estimated reading time accurate, flows well

### System Effectiveness Check

The content system is working when:

- [ ] Fresh prompt conversations consistently produce quality content
- [ ] New content matches s2-operators-overview.adoc depth
- [ ] Terminology is consistent across chapters
- [ ] Integration between chapters flows smoothly
- [ ] Build errors are minimal
- [ ] Revisions are minor (plan-first approach working)

---

## Next Steps

### For Your Next Content Request

1. **Read**: `modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`
2. **Review**: `STYLE-GUIDE.md` Section 7 (Depth Levels)
3. **Fill out**: `CONTENT-REQUEST-TEMPLATE.md`
4. **Use**: Template from `FRESH-PROMPT-WORKFLOW.md` → "Template: Quick Start Message"
5. **Start conversation** with structured prompt

### To Improve This System

As you create more content:
- Document new patterns in STYLE-GUIDE.md
- Add new canonical terms to TERMINOLOGY.md
- Update examples in CONTENT-REQUEST-TEMPLATE.md
- Refine fresh prompt templates based on what works

---

## Support and Questions

### If Content Doesn't Match Style

**First**: Point Claude to specific STYLE-GUIDE.md sections
**Example**: "This needs more depth. See STYLE-GUIDE.md Section 7 for the three-layer approach (WHY/WHAT/HOW). Reference how s2-operators-overview.adoc Section 5 covers the three-layer MaaS stack."

### If Terminology Is Inconsistent

**First**: Reference TERMINOLOGY.md canonical definition
**Example**: "Use the canonical definition from TERMINOLOGY.md: 'ClusterPolicy is the Custom Resource for the NVIDIA GPU Operator...'"

### If Integration Is Unclear

**First**: Ask Claude to read prior chapter pages
**Example**: "Read ch1-gpu-operator/s2-operators-overview.adoc Section 3 to understand how Custom Resources were introduced, then reference that when explaining MIG configuration."

---

## Summary: The System in One Page

```
┌─────────────────────────────────────────────────────────────────┐
│                 Course Content Creation System                  │
└─────────────────────────────────────────────────────────────────┘

BEFORE REQUEST:
1. Read: s2-operators-overview.adoc (style reference)
2. Fill: CONTENT-REQUEST-TEMPLATE.md
3. Check: TERMINOLOGY.md for existing terms
4. Gather: Reference materials (PDFs, docs)

FRESH PROMPT:
Use template from FRESH-PROMPT-WORKFLOW.md including:
- Course context (directory, chapter)
- Style reference paths (s2-operators-overview.adoc, STYLE-GUIDE.md)
- Filled request template
- Integration requirements (builds on / prepares for)
- Reference materials directory

CLAUDE WORKFLOW:
1. Read style reference + style guide
2. Read reference materials
3. Use plan mode to design
4. Present plan for approval
5. Implement after approval
6. Verify against style guide checklist

AFTER CREATION:
1. Review content quality
2. Add new terms to TERMINOLOGY.md
3. Update navigation/transitions
4. Commit changes together

STYLE STANDARDS (from s2-operators-overview.adoc):
- Depth: WHY + WHAT + HOW for all major concepts
- Examples: Concrete scenarios with specific timing
- Production: Decision matrices, TIP/WARNING callouts
- Integration: Reference prior, prepare for next
- Reading time: 15-30 min per substantial section

TERMINOLOGY CONSISTENCY (from TERMINOLOGY.md):
- Check canonical definitions first
- Reference chapter where first defined
- Add new terms immediately after approval
- Use exact definitions across all content
```

---

**Last Updated**: 2026-04-11
**Maintained By**: Course Authors
**Version**: 1.0

For questions or improvements to this system, update the relevant file(s) and commit with a descriptive message.
