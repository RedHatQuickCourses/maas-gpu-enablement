# Quick Start Guide: Fresh Chat in 3 Steps

**Goal**: Create new course content in a fresh Claude conversation with consistent quality.

---

## The 3-Step Process

```
┌─────────────────────────────────────────┐
│  STEP 1: PREPARE (5 min)                │
│  - Open EXAMPLE-FRESH-PROMPT.md         │
│  - Customize for your topic             │
│  - Save your version                    │
└─────────────────────────────────────────┘
                  ↓
┌─────────────────────────────────────────┐
│  STEP 2: NEW CHAT (20 min)              │
│  - Open NEW Claude conversation         │
│  - Paste your customized prompt         │
│  - Review Claude's plan                 │
│  - Approve → Claude implements          │
└─────────────────────────────────────────┘
                  ↓
┌─────────────────────────────────────────┐
│  STEP 3: FINALIZE (5 min)               │
│  - Update TERMINOLOGY.md                │
│  - Verify build works                   │
│  - Commit everything                    │
└─────────────────────────────────────────┘
```

---

## STEP 1: PREPARE (5 minutes)

### Open the template

```bash
cd /Users/kaknox/Documents/GitHub/maas-gpu-enablement
open EXAMPLE-FRESH-PROMPT.md
```

### Customize these 4 sections

Find and edit:

**1. Course Information**
```markdown
**Current Chapter**: Chapter 2 - YOUR CHAPTER NAME
**Target Section**: s1-your-section.adoc
```

**2. Integration Requirements**
```markdown
**This content builds on**:
- Chapter X: WHAT CONCEPTS FROM BEFORE

**This content prepares for**:
- Chapter Y: WHAT COMES NEXT
```

**3. Must Cover Topics**
```markdown
Must Cover:
- YOUR TOPIC 1
- YOUR TOPIC 2
- YOUR TOPIC 3
```

**4. Learning Objectives**
```markdown
Learning Objectives - Students should be able to:
- YOUR OBJECTIVE 1
- YOUR OBJECTIVE 2
```

### Everything else stays the same

**DON'T CHANGE**:
- Style Reference path (always s2-operators-overview.adoc)
- Style Guide path
- Instructions section
- The overall structure

### Save your customized version

```bash
# Save as a new file (optional, or just copy to clipboard)
cp EXAMPLE-FRESH-PROMPT.md my-mig-prompt.md
# Edit my-mig-prompt.md
```

---

## STEP 2: NEW CHAT (20 minutes)

### A. Start Fresh Conversation

- **claude.ai/code** → New conversation
- **OR** Claude desktop → New chat
- **OR** VS Code extension → New conversation

**IMPORTANT**: Must be a NEW conversation (not continuing old one)

---

### B. Paste Your Prompt

1. **Copy** your customized prompt (everything from EXAMPLE-FRESH-PROMPT.md)
2. **Paste** into the new conversation
3. **Send**

**What you're pasting looks like**:
```markdown
I'm creating content for the **maas-gpu-enablement** course...

## Course Information
[your chapter/section info]

## Style and Quality Standards
[paths to style guide, reference page]

## Integration Requirements
[what it builds on, prepares for]

## Content Request
[your specific topics, objectives]

## Instructions
1. Read the style reference...
2. Use plan mode...
[etc.]
```

---

### C. Wait for Plan (5 minutes)

**Claude will**:
1. Read s2-operators-overview.adoc
2. Read STYLE-GUIDE.md
3. Read TERMINOLOGY.md
4. Maybe launch Explore/Plan agents
5. Present a detailed plan

**You'll see**:
```
"I'll explore the reference materials..."
"Reading the style reference to understand depth..."
[Plan appears showing sections, examples, time estimates]
```

---

### D. Review Plan (5 minutes)

**Check these**:

✅ **Has all three layers?**
- WHY (business value, problem it solves)
- WHAT (architecture, components)
- HOW (configuration, commands)

✅ **Examples are specific?**
- "95% utilization" NOT "high utilization"
- "45 seconds" NOT "quickly"

✅ **Includes production guidance?**
- Decision matrices?
- TIP/WARNING callouts?

✅ **Integrates with prior chapters?**
- References ClusterPolicy from Chapter 1?
- Builds on established concepts?

**If plan looks good**:
```
"Approved, proceed with implementation"
```

**If needs work**:
```
"Section 2 needs more depth. See STYLE-GUIDE.md Section 7. 
Match the depth of s2-operators-overview.adoc Section 5."
```

---

### E. Claude Implements (10 minutes)

After approval, Claude will:
- Create new .adoc file
- Update navigation
- Update transitions
- Build course
- Verify

**You'll see**:
```
✅ Created s1-your-topic.adoc
✅ Updated nav.adoc  
✅ Build successful
```

---

## STEP 3: FINALIZE (5 minutes)

### A. Update TERMINOLOGY.md

If new terms were introduced:

```bash
vim TERMINOLOGY.md
```

Add entries like:
```markdown
### Your New Term
**Canonical Definition** (from ch2-topic/s1-overview.adoc):
> Your term is...

**First Defined**: Chapter 2, Section 1
```

---

### B. Verify Build

```bash
cd /Users/kaknox/Documents/GitHub/maas-gpu-enablement
npm run build
```

**Should see**: `BUILD SUCCEEDED`

**If errors**: Ask Claude to fix them

---

### C. Commit Everything

```bash
# Stage changes
git add modules/ch2-topic/
git add TERMINOLOGY.md

# Commit
git commit -m "Add Chapter 2 Section 1: Your Topic

- Created s1-overview.adoc (20 min read)
- Updated navigation
- Added terms to TERMINOLOGY.md"

# Push
git push origin main
```

---

## ✅ Done!

You've successfully created consistent, high-quality content using the fresh prompt system.

**For your next topic**: Repeat these 3 steps with a new topic.

---

## 🎯 First Time? Use This Exact Workflow

If this is your **first time** using this system:

### Option 1: Try the Example As-Is

1. Open `EXAMPLE-FRESH-PROMPT.md`
2. **Don't customize anything** - use the MIG example exactly as written
3. Paste into new chat
4. See how it works
5. Review the result
6. Then customize for your real topic

### Option 2: Follow the Detailed Guide

Read `STEP-BY-STEP-NEW-CHAT.md` for:
- Detailed explanations of each step
- Troubleshooting common issues
- Time budgets
- Success criteria

---

## 📋 One-Page Cheat Sheet

```
┌──────────────────────────────────────────────────────┐
│  BEFORE NEW CHAT                                     │
├──────────────────────────────────────────────────────┤
│  [ ] Open EXAMPLE-FRESH-PROMPT.md                    │
│  [ ] Change: Chapter, Section, Topics, Objectives    │
│  [ ] Keep: All paths, Instructions, Structure        │
│  [ ] Copy customized prompt                          │
└──────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────┐
│  IN NEW CHAT                                         │
├──────────────────────────────────────────────────────┤
│  1. Paste prompt → Send                              │
│  2. Wait for Claude to load context & create plan    │
│  3. Review plan against STYLE-GUIDE.md               │
│  4. Say "Approved" or request changes                │
│  5. Claude implements                                │
│  6. Review final content                             │
└──────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────┐
│  AFTER CHAT                                          │
├──────────────────────────────────────────────────────┤
│  [ ] Update TERMINOLOGY.md (new terms)               │
│  [ ] Run npm run build (verify)                      │
│  [ ] git add + commit + push (all together)          │
└──────────────────────────────────────────────────────┘
```

---

## 🚨 Common Mistakes to Avoid

### ❌ DON'T: Continue an existing conversation
**✅ DO**: Always start a NEW conversation

### ❌ DON'T: Skip the style reference paths
**✅ DO**: Always include paths to s2-operators-overview.adoc and STYLE-GUIDE.md

### ❌ DON'T: Approve plan without reviewing depth
**✅ DO**: Check plan has WHY/WHAT/HOW for each major concept

### ❌ DON'T: Forget to update TERMINOLOGY.md
**✅ DO**: Add new terms immediately after content is done

### ❌ DON'T: Commit only the new content file
**✅ DO**: Commit new file + nav updates + TERMINOLOGY.md together

---

## 💡 Pro Tips

### Tip 1: Keep Files Open
While working in the chat, keep these open in other tabs:
- STYLE-GUIDE.md (for reviewing plan)
- TERMINOLOGY.md (for checking terms)
- s2-operators-overview.adoc (for reference)

### Tip 2: Be Specific When Giving Feedback
Instead of:
```
"Make it more detailed"
```

Say:
```
"Section 2 needs concrete examples. See s2-operators-overview.adoc 
Section 1 for the pattern: scenario + specific timing + result.
Add a similar example showing MIG partition allocation with 
specific memory numbers (7g.40gb) and timing (30 seconds)."
```

### Tip 3: Verify Locally Before Committing
```bash
npm run build
npm run serve
# Open http://localhost:8080
# Navigate to your new section
# Verify it looks good
```

### Tip 4: Use Git Branches for Big Changes
```bash
git checkout -b chapter-2-mig
# Do all your work
# Test everything
git checkout main
git merge chapter-2-mig
```

---

## 📞 Need Help?

### If stuck on customizing the template
→ Read: `STEP-BY-STEP-NEW-CHAT.md` (detailed guide)

### If Claude's plan doesn't match style
→ Read: `STYLE-GUIDE.md` Section 7 (depth levels)
→ Point Claude to specific sections of s2-operators-overview.adoc

### If terminology is inconsistent  
→ Check: `TERMINOLOGY.md` for canonical definitions
→ Tell Claude to use exact definition from there

### If build fails
→ Ask Claude to fix the errors
→ Check AsciiDoc syntax in USAGEGUIDE.adoc

---

## 🎓 Learning Path

**Your first time through**:
1. Read this Quick Start Guide (you are here!)
2. Read s2-operators-overview.adoc to see the quality standard
3. Try the EXAMPLE-FRESH-PROMPT.md exactly as-is (MIG topic)
4. See how it works
5. Customize for your real topic

**Second time**:
1. Use EXAMPLE-FRESH-PROMPT.md with your topic
2. Reference STYLE-GUIDE.md when reviewing plan
3. Update TERMINOLOGY.md with new terms

**Third time and beyond**:
1. You've got the pattern down
2. Each fresh prompt takes ~5 min to prepare
3. Quality is consistent across all content

---

## ⏱️ Time Investment

**First time using system**: 45-60 min
- 15 min: Read style reference + style guide
- 10 min: Customize prompt template
- 25 min: Chat conversation
- 10 min: Finalize and commit

**Subsequent times**: 25-35 min
- 5 min: Customize prompt template  
- 20 min: Chat conversation
- 5 min: Finalize and commit

**ROI**: Consistent quality, no major rewrites, maintainable content

---

## ✨ Success Looks Like

After using this system, you'll have:

✅ New content matching s2-operators-overview.adoc depth
✅ All three layers present (WHY/WHAT/HOW)
✅ Concrete examples with specific metrics
✅ Integration with prior chapters
✅ Updated terminology reference
✅ Clean build with no errors
✅ Commits with clear history

**And for future fresh prompts**: The same quality every time!

---

**Ready to start? → Open `EXAMPLE-FRESH-PROMPT.md` and begin Step 1!**
