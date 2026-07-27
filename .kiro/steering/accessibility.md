# Accessibility

These rules apply to every component and page in the project.

## Heading Hierarchy

- Single `<h1>` on the page (the "tszuk" logotype or site title).
- Each section uses `<h2>` for its heading.
- Sub-items within sections use `<h3>`.
- Never skip heading levels.

## Focus Indicators

- All interactive elements (links, buttons, form inputs) must have a visible `:focus-visible` style.
- Default pattern: `outline: 2px solid var(--color-accent); outline-offset: 2px;`
- Never use `outline: none` without a replacement indicator.

## Form Inputs

- Every input must have a visible `<label>` element with a `for` attribute matching the input's `id`.
- Do not rely on `placeholder` as the accessible name.
- Use `required` attribute for mandatory fields (enables native browser validation).
- Form success/error messages must be in an `aria-live="polite"` region so screen readers announce state changes.

## Images

- All `<Image>` components must have a meaningful `alt` attribute describing the content.
- Decorative images (blob shapes, marquee icons) use `alt=""` and `aria-hidden="true"`.

## Reduced Motion

- All animations and transitions must respect `prefers-reduced-motion: reduce`.
- CSS durations are zeroed globally via custom properties — components inherit this automatically.
- JS animations must check `window.matchMedia('(prefers-reduced-motion: reduce)').matches` and skip if true.

## Semantic HTML

- Use `<section>` with an `aria-label` or visible heading for each page section.
- Use `<nav>` for navigation, `<footer>` for the footer.
- Use `<a>` for navigation links, `<button>` for actions.
- External links should include `rel="noopener noreferrer"` and visually indicate they open externally.

## No-JS Fallback

- Add a `.no-js` class on `<html>` that is removed by a script in `<head>`.
- In CSS, `.no-js` targets display all content at full opacity (scroll-reveal elements visible by default).
- The page must be fully readable without JavaScript.
