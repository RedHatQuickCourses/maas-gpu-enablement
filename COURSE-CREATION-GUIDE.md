# Course Creation Guide: Using Claude Code Skills

This guide explains the optimal workflow for creating a Red Hat enablement course using the Claude Code skills in this repository.

## Overview: The 5-Phase Workflow

```
Phase 1: Design → Phase 2: Initialize → Phase 3: Generate → Phase 4: Develop → Phase 5: Publish
```

---

## Phase 1: Course Design (Manual Planning)

**Goal:** Create a structured course design document that will drive automated generation.

### What to Create

Create a file: `prompts/course-design.md` with the following structure:

```markdown
![Course Banner Image](../images/banner.png)

# Course Title

One-sentence tagline or description.

# COURSE GOAL

Single paragraph describing what learners will accomplish by completing this course.
Focus on business value and practical outcomes.

# TARGET AUDIENCE

Who should take this course:
- Job roles (e.g., "OpenShift administrators")
- Experience level (e.g., "Intermediate to advanced")
- Responsibilities (e.g., "Managing AI/ML workloads")

# PREREQUISITES

This course assumes learners have:

* Familiarity with [specific technology/concept]
* Experience with [specific task/tool]
* Basic understanding of [foundational knowledge]

# COURSE DESIGN

| Learning Objective / Section | Session Type |
|------------------------------|--------------|
| **LEARNING OBJECTIVE #1: Brief objective description** | |
| Section 1 description - what learners will do/learn | Presentation |
| Section 2 description - hands-on activity | Lab |
| Section 3 description - knowledge check | Quiz |
| **LEARNING OBJECTIVE #2: Another objective** | |
| Section description for first topic | Lecture |
| Hands-on practice for the topic | Lab |
| **LEARNING OBJECTIVE #3: Final objective** | |
| ... | ... |
```

### Design Best Practices

**Learning Objectives (Chapters):**
- 3-6 learning objectives per course (optimal: 4-5)
- Each represents a major skill or competency
- Should build progressively (basic → intermediate → advanced)
- Format: "LEARNING OBJECTIVE #N: Action verb + specific skill/knowledge"

**Sections (Pages within chapters):**
- 2-5 sections per learning objective
- Follow pedagogical flow: 
  1. **Presentation/Lecture** - Introduce concepts
  2. **Lab** - Hands-on practice
  3. **Quiz** - Knowledge validation
- Each section should take 5-15 minutes
- Section descriptions should be 1-3 sentences

**Session Types:**
- `Presentation` - Slideshow-style content with diagrams/screenshots
- `Lecture` - Text-heavy explanatory content
- `Lab` - Step-by-step hands-on activities
- `Quiz` - Knowledge checks (interactive or list-based)

### Example: GPU Enablement Course Design

For this repository (`maas-gpu-enablement`), a good structure might be:

```markdown
| Learning Objective / Section | Session Type |
|------------------------------|--------------|
| **LEARNING OBJECTIVE #1: Configure GPU nodes for RHOAI** | |
| Understand GPU requirements for AI workloads and MaaS architecture | Presentation |
| Install and configure NVIDIA GPU operator on OpenShift | Lab |
| Verify GPU availability and node labeling | Lab |
| **LEARNING OBJECTIVE #2: Deploy GPU-accelerated inference services** | |
| Configure hardware profiles for GPU-enabled workloads | Presentation |
| Deploy vLLM inference service with GPU acceleration | Lab |
| Test and validate model serving performance | Lab |
| **LEARNING OBJECTIVE #3: Optimize GPU utilization for MaaS** | |
| Understand GPU sharing and time-slicing strategies | Presentation |
| Configure multi-instance GPU (MIG) partitioning | Lab |
| Monitor GPU utilization and troubleshoot common issues | Lab |
```

---

## Phase 2: Initialize Course Project

**Goal:** Configure the repository for your specific course type and lab environment.

### Use Skill: `/initialize-course-project`

This skill will:
1. Ask you to choose course type (`bfx` or `hol`)
2. Ask you to choose lab environment (`demo`, `role`, or `other`)
3. Ask you for the course title
4. Configure `antora.yml` and other files
5. Clean up template files
6. Install npm dependencies
7. Verify the build works
8. Optionally start watch mode

### Decision Points

**Course Type:**
- **`bfx`** (Business Features/Quick Courses) - For most enablement content
  - Modular structure with chapters
  - Best for: Product features, administration, operations
- **`hol`** (Hands-On Labs) - For lab-focused content
  - Simplified structure, lab-centric
  - Best for: Pure hands-on workshops, guided exercises

**Lab Environment:**
- **`demo`** - Self-contained demos, no external lab required
- **`role`** - Uses Red Hat Online Learning (ROLE) classroom labs
- **`other`** - Custom lab environments (self-provisioned, cloud, etc.)

### Example Workflow

```
User: /initialize-course-project

Claude: What course type? (bfx/hol)
User: bfx

Claude: What lab environment? (demo/role/other)  
User: other

Claude: What is the course title?
User: GPU Enablement for Models as a Service

Claude: [runs course-init.sh, updates files, builds, starts watch mode]
```

**IMPORTANT:** This must be done **before** Phase 3. The skill will delete `course-init.sh` after running.

---

## Phase 3: Generate Course Structure

**Goal:** Auto-generate the complete course skeleton from your design document.

### Prerequisites

- ✅ Phase 2 completed (course initialized)
- ✅ `prompts/course-design.md` exists with proper format
- ⚠️ Stop watch mode if running (skill will ask)

### Use Skill: `/generate-course-structure`

This skill will:
1. Parse `prompts/course-design.md`
2. Extract learning objectives and sections from the table
3. Create chapter directories (`modules/ch1-keyword/`, `modules/ch2-keyword/`, etc.)
4. Generate all section files with appropriate templates
5. Create navigation files (`nav.adoc` per chapter)
6. Update `antora.yml` with chapter references
7. Generate "What's Next" transitions between sections
8. Clean up example chapters (chapter1, chapter2, chapter3)
9. Optionally restart watch mode

### What Gets Generated

For each **Learning Objective**:
```
modules/ch{N}-{keyword}/
├── nav.adoc                          # Chapter navigation
├── pages/
│   ├── index.adoc                    # Chapter landing page
│   ├── s1-{keyword}.adoc             # Section 1 (Presentation/Lecture)
│   ├── s2-{keyword}-lab.adoc         # Section 2 (Lab)
│   ├── s3-{keyword}-quiz.adoc        # Section 3 (Quiz)
│   └── ...
└── images/                           # Placeholder for chapter images
```

For the **ROOT** module:
```
modules/ROOT/pages/index.adoc         # Course overview page (from template)
```

### Naming Conventions

The skill uses intelligent keyword extraction:

- **Chapters:** `ch1-gpu-nodes`, `ch2-vllm-deploy`, `ch3-optimization`
  - Number from learning objective number
  - Keyword from main concept in objective
  - Zero-padded if 10+ chapters (ch01, ch02, ...)

- **Sections:** `s1-nvidia-operator-lab.adoc`, `s2-verify-gpu.adoc`
  - Sequential numbering within chapter
  - Keyword from section description
  - Suffix based on session type:
    - Lab → `-lab.adoc`
    - Quiz → `-quiz.adoc`
    - Presentation/Lecture → `.adoc`

### Review Output

After generation, the skill provides a summary:
```
✅ Created 3 chapters
✅ Created 9 sections
   - 3 Presentations
   - 5 Labs  
   - 1 Quiz
✅ Updated navigation in antora.yml
✅ Removed example chapters (chapter1, chapter2, chapter3)
```

### Validation Checklist

- [ ] All chapters appear in `antora.yml` navigation
- [ ] Each chapter has `nav.adoc` with all sections listed
- [ ] Each section file has template structure (title, objective, content placeholders)
- [ ] "What's Next" transitions are generated
- [ ] Build succeeds: `npm run build` (or watch mode rebuilds)

---

## Phase 4: Develop Content (Manual + Claude Assistance)

**Goal:** Fill in the generated skeleton with actual course content.

### Recommended Workflow

**4.1 Start Watch Mode** (if not already running)

```bash
# Terminal 1
npm run watch:adoc

# Terminal 2  
npm run serve
```

Open browser to `http://localhost:8080` to preview course in real-time.

**4.2 Work Chapter-by-Chapter**

For each chapter:

1. **Update chapter index** (`modules/ch1-keyword/pages/index.adoc`)
   - Refine the chapter goal
   - Add chapter summary/introduction
   - Remove `WARNING: Not started yet` when complete

2. **Fill section content** (work section-by-section)
   - Start with section 1, work sequentially
   - Follow template structure
   - Add actual content between placeholders

3. **Add images** 
   - Place images in `modules/ch1-keyword/images/`
   - Reference: `image::screenshot.png[]`

4. **Test labs manually**
   - Verify all commands work
   - Document actual outputs
   - Add troubleshooting notes

**4.3 Content Development Tips**

**For Presentations/Lectures:**
```adoc
:time_estimate: 7

= Understanding GPU Requirements for AI Workloads

_Estimated reading time: *{time_estimate} minutes*._

Objective::
Explain the hardware and software requirements for GPU-accelerated 
AI inference workloads in Red Hat OpenShift AI.

== GPU Architecture for AI

Modern AI workloads require specialized hardware...

[NOTE]
====
NVIDIA A100 and H100 GPUs are optimized for transformer-based models.
====

image::gpu-architecture.png[GPU Architecture]

== NVIDIA GPU Operator

The NVIDIA GPU Operator automates...

== What's Next

Now that you understand GPU requirements, the next section walks you 
through installing and configuring the NVIDIA GPU operator.
```

**For Labs:**
```adoc
:time_estimate: 15

= Lab: Install NVIDIA GPU Operator

_Estimated reading time: *{time_estimate} minutes*._

Objective::
Install and configure the NVIDIA GPU operator on OpenShift to enable 
GPU workloads.

== Before you begin

* Access to OpenShift cluster with GPU nodes
* Cluster administrator privileges
* oc CLI installed and configured

== Instructions

1. Verify GPU nodes are available

.. List nodes with GPU hardware
+
[source,console,subs="verbatim,quotes"]
----
$ *oc get nodes -l node-role.kubernetes.io/gpu=*
NAME                       STATUS   ROLES    AGE   VERSION
worker-gpu-1.example.com   Ready    worker   5d    v1.28.0
worker-gpu-2.example.com   Ready    worker   5d    v1.28.0
----

.. Check GPU PCI devices
+
[source,console,subs="verbatim,quotes"]
----
$ *oc debug node/worker-gpu-1.example.com*
Starting pod/worker-gpu-1examplecom-debug ...
sh-4.4# *lspci | grep -i nvidia*
3b:00.0 3D controller: NVIDIA Corporation GA100 [A100 PCIe 40GB]
----

2. Install the NVIDIA GPU Operator

.. Create the namespace
+
[source,console,subs="verbatim,quotes"]
----
$ *oc create namespace nvidia-gpu-operator*
namespace/nvidia-gpu-operator created
----

[continues with detailed steps...]

You have successfully installed the NVIDIA GPU operator and verified 
GPU availability in your OpenShift cluster.

== What's next

In the next section, you'll configure hardware profiles to assign 
GPU resources to AI workload deployments.
```

**For Quizzes:**
```adoc
:time_estimate: 5

= Quiz: GPU Configuration Knowledge Check

_Estimated reading time: *{time_estimate} minutes*._

Objective::
Validate understanding of GPU configuration and the NVIDIA operator.

== Questions

1. What is the primary purpose of the NVIDIA GPU Operator?
   a. To provision GPU nodes in the cluster
   b. To automate GPU driver installation and management
   c. To monitor GPU utilization metrics
   d. To schedule AI workloads on GPU nodes
   
   **Answer: b** - The operator automates driver installation, device 
   plugin deployment, and GPU feature management.

2. Which command verifies GPU devices are detected by the operator?
   a. `oc get gpus`
   b. `oc get nodes -l nvidia.com/gpu.present=true`
   c. `nvidia-smi`
   d. `lspci | grep -i nvidia`
   
   **Answer: b** - The operator labels nodes where GPUs are detected.

[Add 3-5 questions per quiz]

== What's next

Next, you'll learn how to deploy GPU-accelerated inference services 
using vLLM and the LLMInferenceService API.
```

**4.4 Update Time Estimates**

Use the included script to calculate reading times:

```bash
bash reading-time.sh modules/ch1-gpu-nodes/pages/s1-requirements.adoc
# Counted 1247 words and 3 images, for a reading time of 7 minutes
# Updates :time_estimate: attribute automatically
```

**4.5 Iterative Preview**

- Save files → watch mode rebuilds → refresh browser
- Review navigation flow
- Check that "What's Next" transitions make sense
- Verify images render correctly
- Test all xref links work

---

## Phase 5: Publish and Export

**Goal:** Generate final outputs and deploy the course.

### 5.1 Generate PDF Export

Use Skill: `/generate-pdf`

This will:
1. Install `asciidoctor-pdf` gem (if needed)
2. Install `@antora/pdf-extension` (if needed)
3. Build course with PDF extension
4. Locate generated PDF
5. Open PDF for preview

Output location: `build/assembler-pdf/{component}/{version}/_exports/index.pdf`

**Use Cases:**
- Offline distribution
- Print materials
- Archival copies
- LMS uploads

### 5.2 Deploy to GitHub Pages

**Automatic Deployment** (if configured):
- Push to `main` branch
- GitHub Actions workflow (`.github/workflows/main.yml`) runs
- Builds site with `npm run build`
- Publishes to GitHub Pages

**Manual Deployment:**
```bash
npm run build
# Manually upload build/site/ to web server
```

### 5.3 Final Quality Checks

- [ ] All sections complete (no "WARNING: Not started" blocks)
- [ ] All images display correctly
- [ ] All navigation links work
- [ ] Labs tested and verified
- [ ] Reading time estimates updated
- [ ] PDF exports successfully
- [ ] GitHub Pages deployment succeeds

---

## Advanced Workflows

### Scenario 1: Iterative Design Updates

**Problem:** You need to add a new chapter or reorganize sections.

**Solution:**
1. Update `prompts/course-design.md` with new structure
2. Run `/generate-course-structure` again
3. Skill will ask: "Keep existing modules or start fresh?"
4. Choose "keep existing" to preserve completed content
5. New chapters/sections will be added
6. Manually reconcile any conflicts

### Scenario 2: Templating Custom Section Types

**Problem:** You have a custom section type (e.g., "Demo Video", "Case Study").

**Solution:**
1. Create new template in `templates/demo.adoc`
2. Update skill prompt or manually create sections
3. Use session type "Demo" in course design table
4. Skill will attempt to use `templates/demo.adoc`

### Scenario 3: Collaborative Development

**Problem:** Multiple authors working on different chapters.

**Solution:**
1. One person runs Phase 1-3 (design & generate)
2. Commit skeleton to git
3. Authors work on separate chapters (branch per chapter)
4. Merge completed chapters to main
5. Generate PDF from main branch

### Scenario 4: Course Updates and Revisions

**Problem:** Course needs updates for new product version.

**Solution:**
1. Create new version branch (e.g., `v2.0`)
2. Update `antora.yml` version number
3. Modify affected sections
4. Keep old version branch for reference
5. Antora can build multi-version documentation

---

## Troubleshooting

### Build Fails After Generation

**Symptom:** `npm run build` produces errors

**Solutions:**
- Check `antora.yml` for syntax errors (YAML indentation)
- Verify all xref targets exist (typo in filename?)
- Look for malformed AsciiDoc (unclosed blocks, invalid attributes)
- Run: `npx antora --log-level=debug antora-playbook.yml`

### Navigation Not Showing Sections

**Symptom:** Chapter appears but sections don't show in nav

**Solutions:**
- Check `modules/ch1-keyword/nav.adoc` exists
- Verify xref format: `** xref:s1-section.adoc[]`
- Ensure filenames match exactly (case-sensitive)
- Rebuild: `npm run build`

### Images Not Displaying

**Symptom:** Broken image links in rendered site

**Solutions:**
- Verify image is in `modules/ch1-keyword/images/`
- Use correct syntax: `image::filename.png[]` (not `![](filename.png)`)
- Check filename matches exactly (case-sensitive)
- Rebuild and hard refresh browser (Cmd+Shift+R / Ctrl+Shift+F5)

### Watch Mode Not Rebuilding

**Symptom:** Changes don't trigger rebuild

**Solutions:**
- Kill and restart `npm run watch:adoc`
- Check that you're editing files in `modules/` directory
- Verify `watch` is monitoring correct directory
- Try manual build: `npm run build`

### PDF Generation Fails

**Symptom:** `/generate-pdf` skill errors

**Solutions:**
- Install Ruby: `brew install ruby` (macOS) or `apt install ruby` (Linux)
- Install gem manually: `gem install asciidoctor-pdf`
- Install PDF extension: `npm install @antora/pdf-extension`
- Check for AsciiDoc syntax errors (PDF renderer is stricter)

---

## Best Practices Summary

### Design Phase
✅ Start with clear learning objectives (4-6 is optimal)  
✅ Balance theory (Presentation) and practice (Lab)  
✅ Include knowledge checks (Quiz) after key concepts  
✅ Keep sections focused and short (5-15 minutes each)  
✅ Design for progressive learning (simple → complex)  

### Development Phase
✅ Work sequentially (complete chapter 1 before chapter 2)  
✅ Test all lab instructions yourself  
✅ Use watch mode for real-time preview  
✅ Update time estimates with `reading-time.sh`  
✅ Add images generously (diagrams, screenshots, flowcharts)  
✅ Write "What's Next" to create flow between sections  

### Technical Quality
✅ Use AsciiDoc syntax correctly (see USAGEGUIDE.adoc)  
✅ Keep code blocks short and focused  
✅ Highlight important output in command examples  
✅ Test all xref links  
✅ Use NOTE, WARNING, TIP callouts appropriately  

### Content Quality  
✅ Write for the target audience level  
✅ Define technical terms on first use  
✅ Provide context (why, not just how)  
✅ Include troubleshooting tips in labs  
✅ Show actual command output (not theoretical)  
✅ Validate prerequisites are accurate  

---

## Quick Reference: Skill Usage

| Skill | When to Use | Prerequisites | Output |
|-------|-------------|---------------|--------|
| `/initialize-course-project` | Once at project start | Clean repository with `course-init.sh` | Configured project, installed deps |
| `/generate-course-structure` | After creating design doc | Course initialized, `prompts/course-design.md` exists | Complete course skeleton |
| `/generate-pdf` | When ready to export | Course content complete | PDF file in `build/` |

---

## Example: Complete Workflow for This Repository

### Day 1: Design
```bash
# Create design document
vi prompts/course-design.md
# [Write complete course design for GPU enablement]
```

### Day 2: Initialize & Generate
```bash
# Run initialization skill
/initialize-course-project
# → Choose: bfx, other, "GPU Enablement for Models as a Service"

# Generate structure from design
/generate-course-structure  
# → Reviews prompts/course-design.md
# → Creates ch1-gpu-nodes, ch2-vllm-deploy, ch3-optimization
# → Generates all section skeletons
```

### Days 3-10: Develop Content
```bash
# Start watch mode (if not running)
npm run watch:adoc    # Terminal 1
npm run serve         # Terminal 2

# Edit files in order:
# - modules/ROOT/pages/index.adoc (course overview)
# - modules/LABENV/pages/index.adoc (lab environment setup)
# - modules/ch1-gpu-nodes/pages/index.adoc (chapter 1 intro)
# - modules/ch1-gpu-nodes/pages/s1-requirements.adoc
# - modules/ch1-gpu-nodes/pages/s2-install-operator-lab.adoc
# [continue through all chapters...]

# Update time estimates as you complete sections
bash reading-time.sh modules/ch1-gpu-nodes/pages/s1-requirements.adoc
```

### Day 11: Publish
```bash
# Generate PDF
/generate-pdf

# Commit and push (triggers GitHub Pages deployment)
git add -A
git commit -m "Complete GPU enablement course"
git push origin main
```

---

## Next Steps

1. **Review** this guide thoroughly
2. **Create** your course design in `prompts/course-design.md`
3. **Run** `/initialize-course-project` skill
4. **Run** `/generate-course-structure` skill
5. **Develop** content chapter by chapter
6. **Export** and publish when complete

For AsciiDoc syntax reference, see: `USAGEGUIDE.adoc`
