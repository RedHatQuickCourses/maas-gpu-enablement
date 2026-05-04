# GPU Enablement Course Archive

**Archived**: 2026-05-04  
**Reason**: Repository migrated to Models-as-a-Service (MaaS) course content  
**Original Course**: Nvidia Accelerator Configuration for Scale (Version 2)

## Content Summary

This archive contains the complete GPU enablement course that was replaced with MaaS content. The course covered:

- **Chapter 1**: GPU Operator Deployment
- **Chapter 2**: Multi-Instance GPU (MIG) Configuration
- **Chapter 3**: Observability and Monitoring
- **Chapter 5**: Model Selection Strategies

## Archive Contents

- `modules/` - Complete Antora modules directory (6 modules, 46 AsciiDoc files)
- `antora.yml` - Course metadata and navigation configuration

## Restoration

To review this content, examine the modules in this directory or check out the git branch: `backup-gpu-content-2026-05-04`

## Related Resources

- **Style Guide**: See repository root `STYLE-GUIDE.md` (preserved in main repository)
- **Terminology**: See repository root `TERMINOLOGY.md` (preserved in main repository)
- **Course Creation Guide**: See repository root `COURSE-CREATION-GUIDE.md` (preserved)
- **Course Roadmap**: See repository root `COURSE-ROADMAP.md` (preserved)

## Original Course Structure

From `antora.yml`:
```yaml
name: maas-gpu-enablement
title: Nvidia Accelerator Configuration for Scale
version: 2
nav:
- modules/ROOT/nav.adoc
- modules/LABENV/nav.adoc
- modules/ch1-gpu-operator/nav.adoc
- modules/ch2-mig/nav.adoc
- modules/ch3-observability/nav.adoc
- modules/ch5-model-selection/nav.adoc
```
