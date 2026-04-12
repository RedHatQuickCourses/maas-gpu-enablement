# Project Context

Red Hat Product Enablement course for IT professionals (developers/sysadmins).

## Critical Constraints

**MUST initialize course project before adding any content**
- If there is a `course-init.sh` file, offer to initialize the project using the skill.

**NEVER modify**:
- `antora-playbook.yml`
- `*.sh` scripts, `devfile.yaml`, `package.json`
- `ui-assets/`, `ui-bundle/`, `supplemental-ui/`, `templates/`

**Watch mode**:
- Run both `npm run watch:adoc` AND `npm run serve` as background tasks.
- Restart both background tasks if `antora.yaml` changes.
- After stopping the `npm run serve` task must also stop the `npm exec http-server build/site -c-1` backgroud process.

**Autostat watch mode**: Offer to start watch mode before making any changes to course content, if not active already.

## Content Structure
This is an Antora documentation project:
- `antora.yml`: course book structure (chapters) and main navigation, chapter ordering
- `modules/`: course content, each subdirectory is a chapter
   - `nav.adoc`: chapter navigation, section or page ordering
   - `pages/`: sections or pages of a chapter, one asciidoc file (`*.adoc`) per section
   - `images/`: optional sudirectory for images of a chapter
   - `attachments/` optional subdirectory for downloadable content of a chapter

## Hints
- Read the AsciiDoc reference: [USAGEGUIDE.adoc](USAGEGUIDE.adoc) when needed

## Content Creation System

This project uses a comprehensive content creation system to ensure consistency, depth, and quality across all course materials.

### Style Reference

**Primary Style Reference**: `modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`

This page demonstrates the required depth, structure, and quality for all course content. It includes:
- Three-layer depth approach: WHY (business value) + WHAT (architecture) + HOW (usage)
- Concrete examples with specific timing and metrics
- Production guidance (decision matrices, TIP/WARNING callouts)
- Integration with prior and future concepts
- Annotated code examples with callouts

### System Files

**For creating new content**:
- `CONTENT-REQUEST-TEMPLATE.md` - Template for structuring content requests
- `STYLE-GUIDE.md` - Comprehensive style patterns extracted from reference implementation
- `FRESH-PROMPT-WORKFLOW.md` - Workflow for maintaining consistency across fresh conversation sessions
- `TERMINOLOGY.md` - Canonical definitions for all technical terms
- `README-CONTENT-SYSTEM.md` - System overview and quick reference

### When Creating New Course Content

1. **Read the style reference first**: Always read `s2-operators-overview.adoc` to understand depth expectations
2. **Follow the style guide**: Use patterns documented in `STYLE-GUIDE.md`
3. **Use plan mode**: For any substantial new content (pages, sections, labs)
4. **Verify terminology**: Check `TERMINOLOGY.md` for canonical definitions
5. **Maintain integration**: Reference prior concepts, prepare for future concepts

### Key Quality Standards

All course content must include:
- **Conceptual depth (WHY)**: Business value, problem it solves, concrete ROI/metrics
- **Architectural depth (WHAT)**: Components, relationships, how parts work together
- **Tactical depth (HOW)**: Configuration, commands, workflows, verification steps
- **Concrete examples**: Real scenarios with specific timing (not "quickly" - use "45 seconds")
- **Production guidance**: Decision matrices for production choices, TIP/WARNING callouts
- **Integration**: References to prior chapters, preparation for future concepts

### Fresh Conversation Sessions

When starting a new conversation session to create content:
1. Reference the style guide: `STYLE-GUIDE.md`
2. Reference the style implementation: `modules/ch1-gpu-operator/pages/s2-operators-overview.adoc`
3. Use the fresh prompt template from: `FRESH-PROMPT-WORKFLOW.md`
4. Check terminology consistency with: `TERMINOLOGY.md`

See `README-CONTENT-SYSTEM.md` for complete workflow and examples.
