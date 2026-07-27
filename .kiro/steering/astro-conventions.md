# Astro Conventions

## Project Structure

```
src/
  assets/         # Images (artist.png, company.png, tshepo.png, Zukisa.png)
  components/     # One .astro file per section (PascalCase)
  layouts/        # Layout.astro (HTML shell)
  pages/          # index.astro + api/contact.ts
  styles/         # global.css (design tokens + base styles)
```

## Component Rules

- One `.astro` component per visual section (Cover, Hero, CaseStudyCard, etc.)
- Use **scoped CSS** (`<style>` in component) for all component styles — no global class collisions.
- Use **CSS custom properties** from `global.css` for shared values — never hardcode colors, spacing, or durations.
- Props use a TypeScript `interface` in the component frontmatter.

## Images

- Always use Astro's `<Image>` component — never raw `<img>` tags.
- Import images in frontmatter: `import artist from '../assets/artist.png';`
- Provide explicit `width` and `height` to prevent CLS.
- Add `loading="lazy"` on any image below the fold.

## JavaScript

- Use inline `<script>` tags within components for interaction logic.
- No external JS frameworks, animation libraries, or bundled modules.
- Total JS budget: < 3KB gzipped across the entire site.
- Batch scroll listeners with `requestAnimationFrame`.

## TypeScript

- Strict mode enabled in `tsconfig.json`.
- Type all component props and API payloads.

## Naming

- Components: `PascalCase.astro` (e.g., `CaseStudyCard.astro`)
- CSS classes: kebab-case (e.g., `.case-study-image`)
- CSS custom properties: `--category-name` (e.g., `--color-sage`, `--duration-reveal`)
- Files in `pages/`: lowercase (e.g., `index.astro`, `api/contact.ts`)
