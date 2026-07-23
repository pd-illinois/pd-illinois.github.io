# PD Illinois Site Principles and Growth Approach

## Purpose
This document defines how the main site is built, how to preserve its design system, and how content should be extended over time.

The main goal is simple:
- Keep one strong template and interaction model.
- Add content without breaking structure.
- Support fast updates when asked to add a blog or add a repo.

## Core Product Decisions

### 1) Single page architecture
- The full experience is powered from one main file: index.html.
- UI, layout, interaction logic, topology map, and rendering runtime are coordinated in that file.
- Content is data-driven, not hardcoded per page section.

### 2) Console topology visual language
- The site uses a console-inspired card system with map-style navigation.
- Parent pages (Blogs, Repos, Author) act as top-level nodes.
- Child pages flow from their parent node.
- Numbering is hierarchical and stable (example style: 01, 01.01, 01.02).

### 3) Content model for blogs
- Blog entries are stored in blogs/blogCatalog.json.
- Each entry carries metadata used for cards, filters, sorting, and child pages.
- Supported blog sources:
  - Local markdown
  - LinkedIn
  - Other external sites
- Local content supports markdown rendering with fallback behavior.

### 4) Theme and readability
- Theme is token-driven using semantic variables.
- Dark and light themes share the same semantic system.
- New UI parts must consume semantic tokens to remain readable in both themes.

### 5) Map behavior and legend
- Map view is a topology overview mode.
- Legend appears in sidebar only when map view is active.
- Legend is category-focused and aligned with filtering behavior.

## Technical Structure Summary

### UI layers
- Sidebar: route map, controls, and map-only legend section.
- Topbar: navigation state, journey band, theme toggle.
- Canvas: topology cards and link paths.
- Stage overlay: navigation and zoom controls.

### Data sources
- blogs/blogCatalog.json: primary blog catalog.
- blogs/*.md: local markdown posts.
- Fallback data exists for resilience during local preview edge cases.

### Rendering responsibilities
- Build slides from catalog and static root sections.
- Render cards and child pages from metadata.
- Render connections in map mode.
- Keep content filters and sort state consistent across blog views.

## Growth Model

### Going forward for blogs
When asked to add a blog, preserve template and only extend catalog and content assets.

Expected blog addition flow:
1. Collect minimum metadata:
   - Title
   - Topic
   - Category
   - Summary
   - Source type (local or external)
   - URL or markdown path
   - Date
2. Add or update blogs/blogCatalog.json.
3. If local blog, add markdown file under blogs.
4. Ensure filters, sort, related links, and child navigation remain intact.
5. Validate light and dark readability and map topology consistency.

### Going forward for repos
When asked to add a repo, preserve template and extend repo content cards in the Repos section.

Expected repo addition flow:
1. Collect minimum metadata:
   - Repo name
   - Public link
   - Topic
   - Category
   - Optional short summary
2. Add repo item to Repos section data/content block while preserving style.
3. Keep hierarchy and map linkage unchanged.

## Operating Protocol for Future Requests

User intent pattern supported:
- Add this blog
- Add this repo

Assistant behavior:
1. Preserve existing template, tokens, and topology model.
2. Ask only targeted categorization questions when needed.
3. Apply minimal edits to keep architecture stable.
4. Validate no structural regressions.

## Required Guardrails
- Do not redesign layout unless explicitly asked.
- Do not break numbering hierarchy.
- Do not hardcode visual values that bypass theme tokens.
- Do not remove map linkage behavior.
- Keep content extension data-driven.

## Suggested Category Clarification Questions
Use only when category is missing or ambiguous:
- Which category should this blog belong to?
- Should this repo use an existing category or a new one?
- Is this source local markdown or external link?

## Definition of Done for Content Updates
A blog or repo addition is complete when:
- Content appears in the right section.
- Styling matches current template.
- Theme readability is preserved in both modes.
- Filters and sorting still work.
- Topology and navigation remain coherent.

## Maintenance Notes
- Keep this document updated whenever core decisions change.
- If content volume grows significantly, consider moving slide generation into modular data files while preserving the same UI contract.
