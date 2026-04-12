# Step-by-Step: Starting a New Chat for Course Content

This is your exact checklist for starting a fresh conversation with Claude to create new course content.

---

## 📋 Pre-Chat Checklist (5-10 minutes)

### ☐ Step 1: Know What You Want

Write down in one sentence:
```
"I need a [X-minute] page about [TOPIC] in [CHAPTER]"
```

Example:
```
"I need a 20-minute page about MIG configuration in Chapter 2"
```

---

### ☐ Step 2: Open the Example Template

```bash
cd /Users/kaknox/Documents/GitHub/maas-gpu-enablement
open EXAMPLE-FRESH-PROMPT.md
```

This file has a complete, ready-to-use prompt template.

---

### ☐ Step 3: Customize the Template (5 minutes)

Open `EXAMPLE-FRESH-PROMPT.md` and edit these sections:

**Change These**:
```markdown
**Current Chapter**: Chapter 2 - Multi-Instance GPU (MIG)  ← YOUR CHAPTER
**Target Section**: s1-mig-overview.adoc                   ← YOUR SECTION

Must Cover:
- What is MIG...                                           ← YOUR TOPICS
- MIG profiles...
- [etc.]

Must Exclude:
- Performance benchmarking...                              ← WHAT TO SKIP

Learning Objectives:
- Explain what MIG is...                                   ← YOUR OBJECTIVES
- [etc.]
```

**Keep These** (Don't Change):
```markdown
**Primary Style Reference**: 
`/Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

**Style Guide**:
`/Users/kaknox/Documents/GitHub/maas-gpu-enablement/STYLE-GUIDE.md`

[All the paths and instructions - keep as-is]
```

---

### ☐ Step 4: Gather Reference Materials (Optional but Recommended)

If you have PDFs or documentation:

```bash
# Create reference directory
mkdir /Users/kaknox/Documents/GitHub/maas-gpu-enablement/mig-reference

# Add your PDFs/docs there
cp ~/Downloads/nvidia-mig-guide.pdf mig-reference/
```

Update the prompt:
```markdown
**Reference Materials**:
Located in: `mig-reference/`
- nvidia-mig-guide.pdf: NVIDIA MIG user guide
- [other files]
```

**If you don't have reference materials**: That's OK! Just note the URLs in the template:
```markdown
**Reference Materials**:
- NVIDIA MIG User Guide: https://docs.nvidia.com/...
```

---

## 💬 Starting the New Chat

### ☐ Step 5: Open New Claude Conversation

- Go to claude.ai/code
- OR open Claude desktop app
- OR use VS Code extension and start new conversation

**Important**: This must be a **NEW** conversation (fresh prompt)

---

### ☐ Step 6: Paste Your Customized Prompt

1. Copy **everything** from your customized template (from EXAMPLE-FRESH-PROMPT.md)
2. Paste it into the new conversation
3. Send

**What you're pasting** (from the example):
```markdown
I'm creating content for the **maas-gpu-enablement** course...

[... entire template ...]

Instructions:
1. Read the style reference...
2. Read the style guide...
[etc.]
```

---

## 🤖 What Happens Next (Claude's Turn)

### ☐ Step 7: Wait for Claude to Load Context (2-3 minutes)

Claude will:
1. Read `s2-operators-overview.adoc` (style reference)
2. Read `STYLE-GUIDE.md`
3. Read `TERMINOLOGY.md`
4. Read any reference materials you provided
5. Possibly launch Explore/Plan agents

**You'll see messages like**:
```
"I'll explore the course structure and reference materials..."
"Reading the style reference to understand depth expectations..."
```

---

### ☐ Step 8: Claude Presents a Plan

Claude will present a detailed plan showing:
- Page title and objective
- Section outline (with subsections)
- Estimated reading time breakdown
- Key examples to include
- Integration points
- Code snippets planned

**Example of what you'll see**:
```markdown
## Implementation Plan: MIG Overview Page

**Title**: Understanding Multi-Instance GPU (MIG)

**Objective**: [detailed objective]

**Section 1: The GPU Sharing Challenge (5 min)**
- Why full GPU allocation wastes resources
- Underutilization problem (40% idle time)
- Multi-tenant requirements

**Section 2: What is MIG (7 min)**
- MIG definition and architecture
- How partitioning works
- Memory and compute isolation
[etc.]
```

---

### ☐ Step 9: Review the Plan (You Do This)

Check the plan for:

✅ **Depth matches reference**:
- Does it have WHY (business value)?
- Does it have WHAT (architecture)?
- Does it have HOW (configuration)?

✅ **Examples are concrete**:
- Not "MIG improves utilization"
- But "MIG increases utilization from 40% to 95%"

✅ **Integration is clear**:
- References Chapter 1 ClusterPolicy?
- Builds on prior knowledge?

✅ **Structure matches style guide**:
- Similar section flow to s2-operators-overview.adoc?
- Has decision matrices, callouts planned?

**If the plan looks good**: Say "Approved, proceed with implementation"

**If something's off**: Say "The [SECTION] needs more depth. See STYLE-GUIDE.md Section 7 for the three-layer approach. Reference how s2-operators-overview.adoc Section 5 covers the three-layer MaaS stack with specific examples."

---

### ☐ Step 10: Claude Implements (5-10 minutes)

After your approval, Claude will:
1. Create the new `.adoc` file
2. Update navigation (`nav.adoc`)
3. Update transitions in adjacent sections
4. Build the course (`npm run build`)
5. Verify no errors

**You'll see**:
```
✅ Created s1-mig-overview.adoc
✅ Updated nav.adoc
✅ Updated chapter index
✅ Build successful - no errors
```

---

### ☐ Step 11: Review the Content (You Do This)

Claude will show you what was created. Check:

✅ **Reading time is accurate**: Count sections and estimate
✅ **Examples are specific**: "45 seconds" not "quickly"
✅ **Callouts are present**: TIP, WARNING where appropriate
✅ **Code is annotated**: YAML has `<1>` callout numbers
✅ **Integration works**: References to Chapter 1 are correct

**If satisfied**: Move to Step 12

**If needs tweaks**: Ask Claude to adjust specific sections:
```
"Section 3 needs a concrete example. Add a scenario showing 
a 3-team platform sharing one A100 with MIG profiles."
```

---

## 📝 Post-Chat Checklist (5 minutes)

### ☐ Step 12: Update TERMINOLOGY.md

If new technical terms were introduced:

```bash
# Open terminology file
vim /Users/kaknox/Documents/GitHub/maas-gpu-enablement/TERMINOLOGY.md

# Add new terms (example):
### Multi-Instance GPU (MIG)
**Canonical Definition** (from ch2-mig/s1-mig-overview.adoc):
> Multi-Instance GPU (MIG) is NVIDIA technology that partitions 
> a single physical GPU into up to seven independent instances...

**First Defined**: Chapter 2, Section 1

### MIG Profile
**Canonical Definition** (from ch2-mig/s1-mig-overview.adoc):
> A MIG profile defines a specific GPU partition configuration 
> specifying compute resources and memory allocation...

**First Defined**: Chapter 2, Section 1
```

---

### ☐ Step 13: Verify Build Locally

```bash
cd /Users/kaknox/Documents/GitHub/maas-gpu-enablement

# Build the course
npm run build

# Check for errors
# Should see: "BUILD SUCCEEDED"

# Optional: Preview locally
npm run serve
# Open http://localhost:8080 and navigate to your new section
```

---

### ☐ Step 14: Commit Everything Together

```bash
# Stage all changes
git add modules/ch2-mig/
git add TERMINOLOGY.md

# Commit with descriptive message
git commit -m "Add Chapter 2 Section 1: MIG Overview

- Created s1-mig-overview.adoc (20 min read)
- Updated navigation and transitions
- Added MIG-related terms to TERMINOLOGY.md
- Integration with: Chapter 1 ClusterPolicy
- Prepares for: Chapter 2 MIG deployment lab"

# Push to remote
git push origin main
```

---

## 🎯 Success Criteria

You've successfully used the system if:

✅ Claude read the style reference before creating content
✅ Content matches s2-operators-overview.adoc depth (WHY/WHAT/HOW)
✅ Examples are concrete with specific metrics
✅ Integration with prior chapters works
✅ Build succeeds with no errors
✅ New terms are in TERMINOLOGY.md
✅ Everything is committed together

---

## 🚨 Troubleshooting

### Problem: Claude's plan doesn't match style depth

**Solution**: Point to specific sections
```
"This plan is too shallow. Compare with s2-operators-overview.adoc 
Section 1 which includes:
- Concrete example (GPU driver version management)
- Before/after comparison (imperative vs declarative)
- Self-healing scenario with specific timing (45 seconds)

Add similar depth to each section of your plan."
```

---

### Problem: Claude didn't read the style reference

**Solution**: Be explicit
```
"Before continuing, please:
1. Read modules/ch1-gpu-operator/pages/s2-operators-overview.adoc completely
2. Note the structure of Section 5 (Three-Layer MaaS Operator Stack)
3. Tell me what patterns you observed

Then revise your plan to match that depth."
```

---

### Problem: Terminology is inconsistent with Chapter 1

**Solution**: Reference TERMINOLOGY.md
```
"Check TERMINOLOGY.md for the canonical definition of 'ClusterPolicy'. 
Use that exact definition when referencing it in this section."
```

---

### Problem: Examples are too generic

**Solution**: Give specific guidance
```
"Replace the generic example with a concrete scenario:

Before: 'MIG improves GPU utilization'
After: 'MIG increases GPU utilization from 40% to 95% by enabling 
7 teams to share a single A100-40GB instead of requiring dedicated 
GPUs. This reduces idle time from 18 hours/day to 1.2 hours/day 
per GPU, improving ROI by $42K per GPU annually.'

Make all examples this specific."
```

---

## 📞 Quick Reference Commands

### Check if files exist before starting
```bash
ls -l /Users/kaknox/Documents/GitHub/maas-gpu-enablement/STYLE-GUIDE.md
ls -l /Users/kaknox/Documents/GitHub/maas-gpu-enablement/EXAMPLE-FRESH-PROMPT.md
ls -l /Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc
```

### View the style reference quickly
```bash
less /Users/kaknox/Documents/GitHub/maas-gpu-enablement/modules/ch1-gpu-operator/pages/s2-operators-overview.adoc
```

### Check existing terminology
```bash
grep -i "ClusterPolicy" /Users/kaknox/Documents/GitHub/maas-gpu-enablement/TERMINOLOGY.md
```

### Build and verify
```bash
cd /Users/kaknox/Documents/GitHub/maas-gpu-enablement && npm run build
```

---

## ⏱️ Time Budget

**Total time for one new section: ~30-45 minutes**

- Pre-chat preparation: 5-10 min
- Chat conversation (context loading + planning): 5-10 min  
- Review and approve plan: 5 min
- Implementation: 5-10 min
- Post-chat (terminology update + commit): 5-10 min

**The plan-first approach saves time** because you catch issues early instead of doing full rewrites.

---

## 🎓 Your First Time: Extra Guidance

### If this is your FIRST fresh prompt using this system:

1. **Read s2-operators-overview.adoc yourself first** (10 min)
   - Understand the depth you're asking for
   - Note the section structure
   - See the before/after examples
   - Observe the callout usage

2. **Read STYLE-GUIDE.md Section 7** (5 min)
   - Understand the three-layer depth approach
   - See the WHY/WHAT/HOW pattern
   - Note the concrete vs. abstract examples

3. **Use the EXAMPLE-FRESH-PROMPT.md exactly as-is** for MIG
   - Don't customize for your first try
   - Just use the MIG example to see how it works
   - You can do your actual topic next

4. **After the first success**, you'll understand the pattern and can use it for any topic

---

## ✅ Final Checklist

Before starting your new chat, verify:

- [ ] I know what topic I want (wrote it in one sentence)
- [ ] I opened EXAMPLE-FRESH-PROMPT.md
- [ ] I customized it for my topic (or using as-is for first try)
- [ ] I have reference materials ready (or noted URLs)
- [ ] I'm ready to open a NEW conversation (not continuing existing one)
- [ ] I understand I'll paste the whole template at once
- [ ] I know to wait for Claude to present a PLAN before implementation
- [ ] I'm ready to review the plan against STYLE-GUIDE.md standards
- [ ] I have TERMINOLOGY.md ready to update afterward

**If all checkboxes are checked: You're ready! Open a new chat and paste your prompt.**

---

## 📎 Files You'll Reference

Keep these open in tabs/windows:

1. `EXAMPLE-FRESH-PROMPT.md` - Your template to customize
2. `STYLE-GUIDE.md` - For reviewing Claude's plan
3. `TERMINOLOGY.md` - For checking existing terms
4. `s2-operators-overview.adoc` - The gold standard reference

**Pro tip**: Keep these 4 files open while you work through the chat conversation.
