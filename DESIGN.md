# DESIGN.md — astrocurse-devtalles

## Architecture Decisions

This document records key design decisions for the astrocurse-devtalles project.

## Content Architecture

### Decision: Content-First Approach

**Context**: Building an Astro course/blog for DevTalles Spanish programming education.

**Decision**: Store content in `assets/` directory before building the Astro site.

**Rationale**:
- Content creation can happen independently of site development
- Posts and images are ready for any static site generator
- Allows content review before technical implementation

### Decision: Spanish-First Content

**Context**: DevTalles is a Spanish programming education platform.

**Decision**: All content is written in Spanish with no i18n infrastructure initially.

**Rationale**:
- Primary audience is Spanish-speaking developers
- Simplifies content creation workflow
- i18n can be added later if needed

## File Organization

### Decision: Numbered Post Convention

**Context**: Need consistent naming for posts and images.

**Decision**: Use `post-XX` pattern for both posts and images.

**Rationale**:
- Clear relationship between post and its image
- Easy to reference and sort
- Simple automation possible

### Decision: Image Optimization

**Context**: Large images impact site performance.

**Decision**: Store optimized AVIF versions in `assets/images/optimized/`.

**Rationale**:
- AVIF provides better compression than PNG/JPEG
- Optimized folder separate from source images
- Build process can reference optimized versions

## Future Astro Implementation

### Expected Content Collections

```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const postsCollection = defineCollection({
  schema: z.object({
    title: z.string(),
    date: z.date(),
    description: z.string(),
    author: z.string(),
    image: z.string(),
    tags: z.array(z.string()),
  }),
});

export const collections = {
  posts: postsCollection,
};
```

### Image Handling Strategy

- Source images: `assets/images/`
- Build output: `public/images/`
- Use Astro's built-in image optimization
- Reference images with absolute paths in frontmatter

## Tooling Decisions

### Decision: AI-Assisted Content Workflow

**Context**: Content creation for educational platform.

**Decision**: Configure gentle-ai and mimo-ai for content workflows.

**Rationale**:
- Accelerates content generation
- Maintains consistent style
- Supports Spanish language content

## Open Questions

- [ ] Should we add English translations?
- [ ] What Astro integrations are needed (MDX, tailwind, etc.)?
- [ ] Should images be in `public/` or processed through Astro?
