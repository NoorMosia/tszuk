---
inclusion: fileMatch
fileMatchPattern: '**/*.astro'
---

# Animation Patterns

Reusable patterns for all interactive behaviors in the tszuk landing page. Every animation must use only `transform` and `opacity` — never animate layout properties (width, height, top, left, margin, padding).

## Scroll-Reveal (fade + slide up)

Used on: Hero, CaseStudyCard, Capabilities, Minds.

**CSS (in scoped `<style>`):**
```css
.section {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity var(--duration-reveal) var(--easing),
              transform var(--duration-reveal) var(--easing);
}

.section.visible {
  opacity: 1;
  transform: translateY(0);
}
```

**JS (in inline `<script>`):**
```js
const section = document.querySelector('.section');
const observer = new IntersectionObserver(
  ([entry]) => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target); // one-shot
    }
  },
  { threshold: 0.15 }
);
observer.observe(section);
```

**Rules:**
- One-shot: unobserve after adding `.visible`.
- Threshold: 0.15 (element 15% visible).
- For staggered cards: add `transition-delay` per index.

## Highlight Effect (text color transition)

Used on: Hero key phrases.

**CSS:**
```css
.highlight {
  color: var(--color-muted);
  transition: color var(--duration-highlight) var(--easing);
}

.highlight--active {
  color: var(--color-text);
}
```

**JS:**
- Observe each `<span class="highlight">` independently.
- Threshold: 0.5 (center of viewport).
- Toggle `.highlight--active` on intersect/unintersect (not one-shot).

## Parallax (subtle vertical offset)

Used on: CaseStudyCard images.

**JS pattern:**
```js
let ticking = false;
function onScroll() {
  if (!ticking) {
    requestAnimationFrame(() => {
      const offset = window.scrollY * parseFloat(getComputedStyle(document.documentElement).getPropertyValue('--parallax-factor'));
      element.style.transform = `translateY(${offset}px)`;
      ticking = false;
    });
    ticking = true;
  }
}
window.addEventListener('scroll', onScroll, { passive: true });
```

**Rules:**
- Batch with `requestAnimationFrame` — never apply transforms directly in the scroll handler.
- Use `{ passive: true }` on the scroll listener.
- Add `will-change: transform` on the parallax element.

## Cover Flip (scroll-mapped 3D rotation)

**JS pattern:**
```js
const rotation = Math.max(-180, Math.min(0, (window.scrollY / 300) * -180));
cover.style.transform = `rotateX(${rotation}deg)`;
```

**Rules:**
- Clamp rotation between 0 and -180 degrees.
- Apply `perspective` on the parent container.
- Add `will-change: transform` on the cover element.
- Batch with `requestAnimationFrame`.

## Reduced Motion Contract

- If `prefers-reduced-motion: reduce` is active:
  - Do NOT register Intersection Observers for scroll-reveal (display all content visible).
  - Do NOT register scroll listeners for parallax.
  - Cover: hide immediately when `scrollY > 0` (no rotation).
  - Marquee: display statically (CSS handles this via `0ms` duration).
  - Blob morph: stops (CSS handles this via `0ms` duration).

**Detection pattern:**
```js
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
if (prefersReducedMotion) return; // skip all JS animations
```
