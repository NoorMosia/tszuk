tszuk — Website Specification & Interactive Blueprint
A complete blueprint and copy document for the tszuk landing page. Engineered for a fast, luxury-minimalist aesthetic (ideal for implementation with Astro, GSAP, and CSS).

🎨 Global Design System
Palette:

Base Canvas: #FFFFFF (Pure White)

Hero Canvas: #E6F2DD (Soft Sage)

Frame Accent: #88BDA4 (Organic Blob Green)

Text / Primary: #181818 (Deep Off-Black)

Footer / Accent: #1A231E (Dark Slate)

Typography:

Logotype & Headings: Modern geometric sans-serif (e.g., Neue Haas Grotesk, Inter Bold)

Subtitles & Captions: Monospace or tracked sans-serif (letter-spacing: 0.15em)

Body Text: Clean sans-serif with generous line height (1.6)

Motion Physics:

Easing: cubic-bezier(0.25, 1, 0.5, 1) (Smooth luxury deceleration)

Scrolling: Integrated smooth scroll via Lenis or native CSS (scroll-behavior: smooth)

SECTION 1: HERO SCREEN
Visual Setup
Background: #E6F2DD (Soft Sage)

Layout: Centered full viewport (100vh), generous vertical spacing.

Content
Logotype: tszuk

Tagline: a brand that build

Live Micro-Interactions
Entry Animation: On initial page load, tszuk gently scales up from 98% to 100% while fading in over 1.2s.

Mouse Parallax: Moving the cursor subtly floats the logotype and tagline in opposite directions (3px displacement) for a sense of depth.

Scroll Cue: A minimal indicator at the bottom pulses gently (opacity: 0.4 -> 1.0).

SECTION 2: THE MANIFESTO
Visual Setup
Background: Smooth background color transition from #E6F2DD to #FFFFFF as the user scrolls.

Layout: Centered text block, max-width 650px, generous top and bottom padding (160px).

Content
"tszuk is a branding studio that strips away the noise to reveal the core identity of luxury brands and visionary creators. We listen, refine, and build enduring visual worlds."

Live Micro-Interactions
Scroll Reveal (Stagger): Text splits into lines or words and moves smoothly upward into view as the user scrolls down (GSAP ScrollTrigger).

Highlight Effect: Keywords like "strips away the noise" transition from a light grey (#777777) to a solid off-black (#181818) as they cross the center of the screen.

SECTION 3: OUR WORK (CASE STUDIES & LOGO MARQUEE)
Visual Setup
Background: #FFFFFF

Layout: Single-column stacked cards with large, high-resolution media containers.

Hero Case 01: Artist Spotlight
Category: 01 — CREATIVE IDENTITY & MANAGEMENT

Visual Container: [ Full-Bleed Image / Video Asset ]

Client: [ Artist / Creative Name ]

Scope: Visual Identity, Release Campaign, Strategy & Management

Description: Complete visual architecture and strategic roadmap for an independent release.

Link: [ Explore Case Study → ]

Hero Case 02: Enterprise Spotlight
Category: 02 — BRAND STRATEGY & SYSTEMS

Visual Container: [ Full-Bleed Image / Video Asset ]

Client: [ Business / Enterprise Name ]

Scope: Rebrand, Brand Architecture, Digital Experience

Description: Comprehensive brand identity overhaul and scalable digital platform engineering.

Link: [ Explore Case Study → ]

Interactive Behavior (Hero Cards)
Parallax Scroll: Images move slightly slower inside their containers as the user scrolls past.

Hover State: Cursor morphs into a dark circle displaying VIEW CASE STUDY →, while the image scales gently (1.0 -> 1.03).

The Client Logo Belt (Infinite Marquee)
Layout: Full-width container positioned directly beneath the hero case studies.

Content:

Client Logo 01

Client Logo 02

Client Logo 03

Client Logo 04

Client Logo 05

Live Micro-Interactions
Infinite Scroll: Continuous, seamless right-to-left marquee movement using pure CSS @keyframes.

Hover Pause: Hovering over the ticker smoothly decelerates the marquee to a pause.

Edge Masks: Linear gradient masks on the left and right edges fade logos in and out smoothly.

SECTION 4: CAPABILITIES & SERVICES
Visual Setup
Background: #FFFFFF

Layout: Two-column minimalist grid (stacked on mobile) separated by fine dividers (1px solid #EAEAEA).

Column 01: Brand Engineering & Strategy
For businesses, startups, and product launches.

Visual Identity: Signature mark, custom typography, color systems.

Brand Guidelines: Comprehensive rules for scalable, consistent growth.

Digital & Web Presence: Minimalist digital hubs, web architecture, and UI/UX.

Column 02: Creative Management & Roster
For artists and visionaries seeking long-term backing.

360° Brand Direction: Aligning visual identity with artistic output and cultural positioning.

Campaign & Release Execution: End-to-end planning for drops, launches, and press.

Partnerships & Commercial Growth: Negotiating agency collaborations and brand deals.

Live Micro-Interactions
Hovering over a column subtly changes its background to a very soft sage tint (#F4F9F1).

SECTION 5: THE MINDS
Visual Setup
Background: #FFFFFF

Layout: Two-column grid with portraits framed by organic #88BDA4 blob shapes.

Left Column: Zukisa
Frame Accent: Organic fluid shape in #88BDA4

Name & Role: Zukisa — Co-Founder & Creative Director

Qualifications: Bachelor in Design & Creative Direction

Bio: Leads aesthetic vision, visual harmony, and the core creative direction that gives every brand its distinctive, iconic edge.

Right Column: Tshepo
Frame Accent: Organic fluid shape in #88BDA4

Name & Role: Tshepo — Co-Founder & Systems Director

Qualifications: BSc Computer Science & Mathematics

Bio: Combines structural logic with technical execution, ensuring every brand strategy is backed by scalable systems and digital precision.

Live Micro-Interactions
Blob Morph: The #88BDA4 organic shape slowly morphs its vector path (d coordinates) in a continuous 15-second loop.

Hover State: Hovering over a portrait highlights an overlay tag showing their primary focus area (Creative Direction / Systems Architecture).

SECTION 6: THE INVITATION & FOOTER
Visual Setup
Background: #1A231E (Dark Slate) or #E6F2DD (Sage)

Layout: Minimalist contact form paired with direct studio contact info.

Headline
Ready to strip away the noise?

Inquiry Form
Field 1: Name [ Text Input ]

Field 2: Email [ Text Input ]

Field 3: Project Type [ Radio Toggle: Brand Identity / Web | Artist Management | Other ]

Field 4: Message [ Textarea ]

Action Button: [ Send Inquiry ]

Studio Coordinates
Direct Email: hello@tszuk.com

Location: Port Elizabeth, South Africa

Socials: Instagram | LinkedIn

Live Clock: PORT ELIZABETH, ZA — [HH:MM:SS SAST]

Live Micro-Interactions
Input Focus: Clicking an input field animates its bottom border color to #88BDA4.

Form Submission: Submitting triggers a smooth, inline loading transition (no page reload), replaced by: "Inquiry received. We will be in touch shortly."