# Implementation Plan: tszuk Landing Page

## Overview

Build the tszuk branding studio landing page incrementally using Astro, vanilla CSS, and minimal vanilla JavaScript. Each task produces a working, demoable increment — starting with project scaffolding and progressing section-by-section until the full page is deployed on Cloudflare Pages. Assets (artist.png, company.png, tshepo.png, Zukisa.png) exist in the project root and will be moved into the Astro project structure.

## Tasks

- [x] 1. Scaffold Astro project and global styles
  - [x] 1.1 Initialize Astro project with TypeScript and Cloudflare adapter
    - **Depends on:** — (start)
    - Run `npm create astro@latest` with empty template in the project root
    - Install `@astrojs/cloudflare` adapter and configure `astro.config.mjs` for Cloudflare Pages output
    - Move existing assets (`artist.png`, `company.png`, `tshepo.png`, `Zukisa.png`) into `src/assets/`
    - Create `.env.example` with `RESEND_API_KEY=` placeholder
    - Add `.env` to `.gitignore`
    - _Requirements: 11.1, 11.5_

  - [x] 1.2 Create Layout.astro and global.css with design system tokens
    - **Depends on:** 1.1
    - Create `src/layouts/Layout.astro` with full HTML shell, Inter font preconnect, viewport meta, Open Graph tags, and `<slot />`
    - Create `src/styles/global.css` with all CSS custom properties from the design (colors, typography, spacing, motion, sizes)
    - Include `prefers-reduced-motion` media query that zeroes all durations
    - Add `.no-js` class handling for graceful degradation
    - Set up mobile-first base styles (box-sizing, font reset, body defaults)
    - _Requirements: 9.1, 9.2, 9.3, 9.4, 10.4, 11.2_

  - [x] 1.3 Create minimal index.astro page using Layout
    - **Depends on:** 1.2
    - Create `src/pages/index.astro` importing Layout with title "tszuk — a brand that builds"
    - Add a placeholder `<h1>tszuk</h1>` to verify the layout works
    - Verify `npm run dev` serves the page and Inter font loads correctly
    - _Requirements: 9.4, 11.1_

- [x] 2. Implement Cover section with flip animation
  - [x] 2.1 Create Cover.astro component with static content
    - **Depends on:** 1.3
    - Create `src/components/Cover.astro` with full-viewport sage-green section
    - Render "tszuk" logotype centered using Inter Bold at large size
    - Render tagline "a brand that builds" below with letter-spacing 0.15em
    - Apply `position: fixed`, full viewport sizing, and `perspective` CSS
    - Style with scoped CSS (background #E6F2DD, centered flexbox layout)
    - _Requirements: 1.1, 1.2, 1.3, 11.3_

  - [x] 2.2 Implement scroll-driven flip mechanic in JavaScript
    - **Depends on:** 2.1
    - Add inline `<script>` with ~20 lines of vanilla JS
    - Map `scrollY` to rotation: `rotation = clamp(scrollY / 300 * -180, -180, 0)`
    - Apply `transform: rotateX(${rotation}deg)` to the cover element
    - Use `requestAnimationFrame` for batched scroll handling
    - Add `will-change: transform` for GPU compositing
    - Respect `prefers-reduced-motion`: if enabled, hide cover immediately on scroll > 0
    - Add spacer div after cover to allow scroll content beneath
    - _Requirements: 1.4, 1.5, 1.6, 1.7, 11.4_

  - [x] 2.3 Wire Cover into index.astro and verify
    - **Depends on:** 2.2
    - Import and render Cover.astro in index.astro above placeholder content
    - Add enough content below to allow scrolling
    - Verify flip animation plays correctly, reverses on scroll-up, and is disabled with `prefers-reduced-motion`
    - _Requirements: 1.4, 1.5, 1.7_

- [x] 3. Implement Hero / Manifesto section
  - [x] 3.1 Create Hero.astro with manifesto text and highlight spans
    - **Depends on:** 2.3
    - Create `src/components/Hero.astro` with centered text block (max-width 650px, white background)
    - Render manifesto text with key phrases wrapped in `<span class="highlight">` elements
    - Style `.highlight` with initial color #777777 and transition to #181818
    - Add scoped CSS for scroll-reveal: initial `opacity: 0; translateY(20px)`, visible state `opacity: 1; translateY(0)`
    - _Requirements: 2.1, 2.2, 11.3_

  - [x] 3.2 Add Intersection Observer logic for scroll-reveal and highlights
    - **Depends on:** 3.1
    - Register one-shot Intersection Observer (threshold 0.15) to add `.visible` class on the section
    - Register per-span Intersection Observer (threshold 0.5) to toggle `.highlight--active` class
    - Unobserve section after reveal (one-shot), keep observing highlights for toggle behavior
    - Respect `prefers-reduced-motion`: skip observers and display all content at full opacity
    - _Requirements: 2.3, 2.4, 2.5_

  - [x] 3.3 Wire Hero into index.astro below the Cover
    - **Depends on:** 3.2
    - Import and place Hero.astro after the Cover spacer
    - Verify scroll-reveal fires when Hero enters viewport
    - Verify highlights transition as text scrolls through center
    - _Requirements: 2.3, 2.4_

- [x] 4. Implement Our Work section — Case Study Cards
  - [x] 4.1 Create CaseStudyCard.astro component
    - **Depends on:** 3.3
    - Create `src/components/CaseStudyCard.astro` accepting props: number, clientName, descriptor, scope[], image, imageAlt, link
    - Render image in a parallax container, card metadata, scope items joined with " · ", and external "Visit" link
    - Style with scoped CSS: image container with overflow hidden, hover scale 1.03, scroll-reveal initial state
    - _Requirements: 3.1, 3.2, 3.3, 11.3_

  - [x] 4.2 Add scroll-reveal, parallax, and hover interactions to CaseStudyCard
    - **Depends on:** 4.1
    - Register Intersection Observer for staggered reveal (apply `.visible` with delay per card index)
    - Register scroll listener for parallax: `translateY(scrollY * 0.05)` on `.case-study-image`
    - Batch parallax with `requestAnimationFrame`
    - Add hover scale transition: `transform: scale(var(--hover-scale))` on image
    - Respect `prefers-reduced-motion`: disable parallax and hover scale
    - _Requirements: 3.4, 3.5, 3.6, 3.7_

  - [x] 4.3 Wire case study cards into index.astro
    - **Depends on:** 4.2
    - Import CaseStudyCard and Astro `<Image>` for artist.png and company.png
    - Render Card 01 (Boss Reminisce) and Card 02 (Sunset Retreat) in the Work section
    - Verify staggered reveal, parallax, and hover scale work in browser
    - _Requirements: 3.1, 3.2, 3.3, 9.6_

- [x] 5. Implement Logo Marquee section
  - [x] 5.1 Create Marquee.astro component
    - **Depends on:** 4.3
    - Create `src/components/Marquee.astro` with duplicated set of 5 SVG placeholder icons (geometric shapes)
    - Apply CSS `@keyframes` for seamless right-to-left infinite scroll
    - Add `animation-play-state: paused` on `:hover`
    - Apply `linear-gradient` masks on left/right edges
    - Respect `prefers-reduced-motion`: display logos statically
    - _Requirements: 4.1, 4.2, 4.3, 4.4, 4.5, 11.3_

  - [x] 5.2 Wire Marquee into index.astro below case study cards
    - **Depends on:** 5.1
    - Import and place Marquee.astro after the case study cards
    - Verify continuous scrolling, hover pause, and edge fade masks
    - _Requirements: 4.1, 4.2, 4.3_

- [x] 6. Checkpoint — Core visual sections complete
  - **Depends on:** 5.2
  - Ensure `npm run build` succeeds without errors
  - Verify Cover flip, Hero scroll-reveal + highlights, Case Study cards, and Marquee all function correctly
  - Ensure all tests pass, ask the user if questions arise.

- [x] 7. Implement Capabilities section
  - [x] 7.1 Create Capabilities.astro component
    - **Depends on:** 6
    - Create `src/components/Capabilities.astro` with two-column CSS Grid
    - Column 1: heading "Brand Engineering & Strategy" with items "Visual Identity", "Brand Guidelines", "Digital & Web Presence"
    - Column 2: heading "Creative Management & Roster" with items "360° Brand Direction", "Campaign & Release Execution", "Partnerships & Growth"
    - Style with 1px solid #EAEAEA divider between columns
    - Add hover background transition to #F4F9F1 per column
    - Add Intersection Observer for scroll-reveal
    - Responsive: stack to single column below 768px
    - Respect `prefers-reduced-motion`
    - _Requirements: 5.1, 5.2, 5.3, 5.4, 5.5, 5.6, 5.7, 11.3_

  - [x] 7.2 Wire Capabilities into index.astro
    - **Depends on:** 7.1
    - Import and place after Marquee
    - Verify two-column layout, hover effect, scroll-reveal, and responsive stacking
    - _Requirements: 5.1, 9.5_

- [x] 8. Implement The Minds section
  - [x] 8.1 Create Minds.astro component
    - **Depends on:** 6
    - Create `src/components/Minds.astro` with two-column grid
    - Render Zukisa: portrait (Zukisa.png), "Co-Founder & Creative Director", "Bachelor in Design & Creative Direction"
    - Render Tshepo: portrait (tshepo.png), "Co-Founder & Systems Director", "BSc Computer Science & Mathematics"
    - Add blob shape behind each portrait: `border-radius` morph CSS @keyframes over 15s loop, color #88BDA4
    - Add hover overlay showing focus area tag
    - Use Astro `<Image>` for portrait optimization
    - Add Intersection Observer for scroll-reveal
    - Responsive: stack to single column below 768px
    - Respect `prefers-reduced-motion`: disable blob morph and scroll-reveal
    - _Requirements: 6.1, 6.2, 6.3, 6.4, 6.5, 6.6, 6.7, 6.8, 9.6, 11.3_

  - [x] 8.2 Wire Minds into index.astro
    - **Depends on:** 8.1
    - Import and place after Capabilities
    - Verify blob animations, hover overlays, responsive stacking, and image optimization
    - _Requirements: 6.1, 6.7, 9.5_

- [x] 9. Implement Footer and Contact Form UI
  - [x] 9.1 Create ContactForm.astro component
    - **Depends on:** 6
    - Create `src/components/ContactForm.astro` with fields: Name (text, required), Email (text, required), Project Type (radio group: "Brand Identity/Web", "Artist Management", "Other"), Message (textarea, required), Submit button
    - Add visible `<label>` for each input with accessible names
    - Style with scoped CSS: dark background context, focus bottom-border animation to #88BDA4 using `:focus-visible`
    - Add `required` attributes for browser-native validation
    - Add inline `<script>` for fetch-based form submission (to be wired in next task)
    - Manage UI states: idle, loading (spinner/indicator), success message, error message
    - _Requirements: 7.2, 7.3, 7.4, 7.5, 7.6, 7.7, 10.2, 10.3_

  - [x] 9.2 Create Footer.astro component
    - **Depends on:** 9.1
    - Create `src/components/Footer.astro` with dark slate background (#1A231E)
    - Render headline "Ready to strip away the noise?"
    - Render ContactForm component
    - Render studio info: email "hello@tszuk.com", location "Port Elizabeth, South Africa", social links (Instagram, LinkedIn)
    - _Requirements: 7.1, 7.8, 11.3_

  - [x] 9.3 Wire Footer into index.astro
    - **Depends on:** 9.2
    - Import and place as the final section
    - Verify form renders, focus animations work, and studio info displays correctly
    - _Requirements: 7.1, 7.2, 9.4_

- [x] 10. Implement Contact API endpoint
  - [x] 10.1 Create /api/contact.ts serverless endpoint
    - **Depends on:** 9.3
    - Create `src/pages/api/contact.ts` with POST handler
    - Parse JSON body and validate required fields (name, email, message)
    - Validate email with basic format regex
    - Return 400 with appropriate error messages for missing/invalid fields
    - On success: call Resend SDK to send email to hello@tszuk.com
    - Return 200 `{ success: true }` on successful send
    - Return 500 `{ error: "..." }` on Resend failure
    - Use environment variable `RESEND_API_KEY` from runtime env
    - _Requirements: 8.1, 8.2, 8.3, 8.4, 8.5_

  - [x] 10.2 Install Resend SDK and wire form submission
    - **Depends on:** 10.1
    - Install `resend` package
    - Connect ContactForm's fetch POST to `/api/contact`
    - Verify full flow: form submission → API validation → success/error response → UI state update
    - _Requirements: 7.4, 7.5, 7.6, 7.7, 8.3, 8.4_

  - [ ]* 10.3 Write unit tests for Contact API endpoint
    - **Depends on:** 10.2
    - Install Vitest and configure for Astro project
    - Test: missing name returns 400
    - Test: missing email returns 400
    - Test: invalid email format returns 400
    - Test: valid payload calls Resend and returns 200 `{ success: true }`
    - Test: Resend failure returns 500 with error message
    - Mock the Resend SDK in all tests
    - _Requirements: 8.1, 8.2, 8.3, 8.4, 8.5_

- [x] 11. Checkpoint — Full functionality complete
  - **Depends on:** 7.2, 8.2, 10.2
  - Ensure `npm run build` succeeds without errors
  - Verify all sections render in order: Cover → Hero → Work → Marquee → Capabilities → Minds → Footer
  - Verify contact form submits and receives responses
  - Ensure all tests pass, ask the user if questions arise.

- [x] 12. Responsive polish, accessibility audit, and deployment configuration
  - [x] 12.1 Responsive refinements across all breakpoints
    - **Depends on:** 11
    - Verify and fix mobile layout (< 768px): single-column stacking, reduced padding, full-bleed card images
    - Verify tablet (768px+): two-column capabilities and minds, proper spacing
    - Verify desktop (1024px+): full spacing, all interactions
    - Adjust Cover logotype font size for mobile
    - Adjust Marquee speed for mobile readability
    - _Requirements: 9.5, 5.1, 6.1_

  - [x] 12.2 Accessibility audit and fixes
    - **Depends on:** 11
    - Verify heading hierarchy: single h1, logical h2/h3 structure per section
    - Verify all form inputs have visible labels with accessible names
    - Verify all images have meaningful alt text
    - Verify `:focus-visible` indicators on all interactive elements (links, buttons, form inputs)
    - Verify `prefers-reduced-motion` disables ALL animations (flip, scroll-reveal, highlights, marquee, blob, hover transitions)
    - Add `aria-live="polite"` region for form success/error messages
    - Run Lighthouse accessibility check and target 100 score
    - _Requirements: 10.1, 10.2, 10.3, 10.4, 9.6, 9.7_

  - [x] 12.3 Performance optimization and build verification
    - **Depends on:** 12.1, 12.2
    - Verify all images use Astro `<Image>` with explicit width/height (no CLS)
    - Verify images below the fold have `loading="lazy"`
    - Verify only `transform` and `opacity` used for animations (no layout thrash)
    - Run `npm run build` and verify production bundle: JS < 3KB gzipped, no unused CSS
    - Run Lighthouse performance check, target 90+ score
    - _Requirements: 9.6, 9.7, 11.4_

  - [x] 12.4 Configure Cloudflare Pages deployment
    - **Depends on:** 12.3
    - Ensure `astro.config.mjs` has `output: 'server'` with Cloudflare adapter for the API route
    - Add `wrangler.toml` or Cloudflare Pages configuration if needed
    - Document required env var: `RESEND_API_KEY` for production
    - Verify `npm run build` produces correct output for Cloudflare Pages
    - _Requirements: 8.3, 11.1, 11.5_

- [x] 13. Final checkpoint — Production ready
  - **Depends on:** 12.4
  - Ensure all tests pass
  - Verify full site works end-to-end in production build (`npm run preview`)
  - Ensure all tests pass, ask the user if questions arise.

## Task Dependency Graph

```json
{
  "waves": [
    {
      "wave": 1,
      "tasks": ["1.1"],
      "depends_on": []
    },
    {
      "wave": 2,
      "tasks": ["1.2"],
      "depends_on": ["1.1"]
    },
    {
      "wave": 3,
      "tasks": ["1.3"],
      "depends_on": ["1.2"]
    },
    {
      "wave": 4,
      "tasks": ["2.1"],
      "depends_on": ["1.3"]
    },
    {
      "wave": 5,
      "tasks": ["2.2"],
      "depends_on": ["2.1"]
    },
    {
      "wave": 6,
      "tasks": ["2.3"],
      "depends_on": ["2.2"]
    },
    {
      "wave": 7,
      "tasks": ["3.1"],
      "depends_on": ["2.3"]
    },
    {
      "wave": 8,
      "tasks": ["3.2"],
      "depends_on": ["3.1"]
    },
    {
      "wave": 9,
      "tasks": ["3.3"],
      "depends_on": ["3.2"]
    },
    {
      "wave": 10,
      "tasks": ["4.1"],
      "depends_on": ["3.3"]
    },
    {
      "wave": 11,
      "tasks": ["4.2"],
      "depends_on": ["4.1"]
    },
    {
      "wave": 12,
      "tasks": ["4.3"],
      "depends_on": ["4.2"]
    },
    {
      "wave": 13,
      "tasks": ["5.1"],
      "depends_on": ["4.3"]
    },
    {
      "wave": 14,
      "tasks": ["5.2"],
      "depends_on": ["5.1"]
    },
    {
      "wave": 15,
      "tasks": ["6"],
      "depends_on": ["5.2"]
    },
    {
      "wave": 16,
      "tasks": ["7.1", "8.1", "9.1"],
      "depends_on": ["6"]
    },
    {
      "wave": 17,
      "tasks": ["7.2", "8.2", "9.2"],
      "depends_on": ["7.1", "8.1", "9.1"]
    },
    {
      "wave": 18,
      "tasks": ["9.3"],
      "depends_on": ["9.2"]
    },
    {
      "wave": 19,
      "tasks": ["10.1"],
      "depends_on": ["9.3"]
    },
    {
      "wave": 20,
      "tasks": ["10.2"],
      "depends_on": ["10.1"]
    },
    {
      "wave": 21,
      "tasks": ["11"],
      "depends_on": ["7.2", "8.2", "10.2"]
    },
    {
      "wave": 22,
      "tasks": ["12.1", "12.2"],
      "depends_on": ["11"]
    },
    {
      "wave": 23,
      "tasks": ["12.3"],
      "depends_on": ["12.1", "12.2"]
    },
    {
      "wave": 24,
      "tasks": ["12.4"],
      "depends_on": ["12.3"]
    },
    {
      "wave": 25,
      "tasks": ["13"],
      "depends_on": ["12.4"]
    }
  ]
}
```

## Notes

- Tasks marked with `*` are optional and can be skipped for faster MVP
- Each task references specific requirement acceptance criteria for traceability
- Checkpoints ensure incremental validation between major phases
- The Cover flip mechanic (Task 2) is isolated as its own focused task due to interaction complexity
- Assets already exist in the project root — Task 1.1 moves them into Astro's src/assets/ directory
- No property-based tests are included (PBT was assessed as not applicable for this UI-focused project)
