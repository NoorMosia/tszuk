# Requirements Document

## Introduction

This document specifies the requirements for the tszuk branding studio landing page — a single-page website built with Astro, vanilla CSS, and minimal vanilla JavaScript. The site conveys a luxury-minimalist aesthetic across six distinct sections: Cover, Hero/Manifesto, Our Work, Capabilities, The Minds, and Footer/Contact. It must load fast, respect accessibility preferences, and work seamlessly on mobile.

## Glossary

- **Landing_Page**: The single-page website serving as the public-facing presence for tszuk branding studio
- **Cover_Section**: The full-viewport sage-green introductory section with the tszuk logotype and flip animation
- **Hero_Section**: The manifesto text section with scroll-reveal and highlight animations
- **Work_Section**: The case studies and logo marquee section showcasing portfolio work
- **Capabilities_Section**: The two-column grid listing brand engineering and creative management services
- **Minds_Section**: The two-column founder portraits section with blob shape animations
- **Footer_Section**: The dark-slate contact form and studio information section
- **Flip_Animation**: A 3D rotateX CSS transform triggered by scroll that reveals the Hero section beneath the Cover
- **Scroll_Reveal**: A fade-plus-slide-up animation triggered as elements enter the viewport
- **Highlight_Effect**: Text transitioning from muted grey (#777777) to dark (#181818) as it scrolls into view
- **Marquee**: An infinitely scrolling horizontal strip of logo placeholders using CSS keyframes
- **Blob_Shape**: An organic morphing shape behind founder portraits using CSS border-radius keyframe animation
- **Contact_API**: The serverless POST endpoint at /api/contact that validates form data and sends email via Resend
- **Resend**: The third-party email delivery service used to send contact form submissions

## Requirements

### Requirement 1: Cover Section with Flip Animation

**User Story:** As a visitor, I want to see a clean branded cover that flips away on scroll, so that I experience an engaging entrance to the site.

#### Acceptance Criteria

1. THE Cover_Section SHALL occupy the full viewport height and width with background color #E6F2DD
2. THE Cover_Section SHALL display the text "tszuk" centered horizontally and at eye level using Inter Bold at a large size
3. THE Cover_Section SHALL display the tagline "a brand that builds" below the logotype with letter-spacing 0.15em and lighter weight
4. WHEN the visitor scrolls down for the first time, THE Cover_Section SHALL perform a 3D rotateX flip upward from the bottom edge using CSS perspective
5. WHEN the visitor scrolls back up after the flip, THE Cover_Section SHALL reverse the flip animation and return to its original position
6. THE Flip_Animation SHALL use the easing cubic-bezier(0.25, 1, 0.5, 1)
7. WHILE the user has prefers-reduced-motion enabled, THE Cover_Section SHALL skip the flip animation and reveal content immediately

### Requirement 2: Hero / Manifesto Section

**User Story:** As a visitor, I want to read a clear brand manifesto with subtle animated text highlights, so that I understand what tszuk does and feel the quality of their craft.

#### Acceptance Criteria

1. THE Hero_Section SHALL display a centered text block with max-width 650px on a white background
2. THE Hero_Section SHALL contain the manifesto text: "Branding isn't about complexity, it's about removing distraction. tszuk collaborates with luxury brands and artists to build identities that resonate."
3. WHEN the Hero_Section enters the viewport, THE Landing_Page SHALL animate the text with a fade-plus-slide-up Scroll_Reveal effect
4. WHEN key phrases scroll into the center of the viewport, THE Highlight_Effect SHALL transition those phrases from color #777777 to #181818
5. WHILE the user has prefers-reduced-motion enabled, THE Hero_Section SHALL display all text at full opacity without animation

### Requirement 3: Our Work Section — Case Study Cards

**User Story:** As a visitor, I want to see portfolio case studies presented as minimal cards, so that I can evaluate tszuk's work quality.

#### Acceptance Criteria

1. THE Work_Section SHALL display two case study cards stacked vertically
2. THE Work_Section SHALL display Card 01 with client name "Boss Reminisce", descriptor "singer/songwriter", scope items "Web presence · Strategic partnership · Brand management", and a "Visit" link with an external arrow icon
3. THE Work_Section SHALL display Card 02 with client name "Sunset Retreat", descriptor "hospitality", scope items "Logo · Brand identity · Website", and a "Visit" link with an external arrow icon
4. WHEN a card image scrolls through the viewport, THE Landing_Page SHALL apply a subtle parallax translateY offset to the image
5. WHEN a visitor hovers over a card, THE Landing_Page SHALL scale the card image from 1.0 to 1.03
6. WHEN cards enter the viewport, THE Landing_Page SHALL apply a staggered Scroll_Reveal animation to each card
7. WHILE the user has prefers-reduced-motion enabled, THE Work_Section SHALL display cards without parallax or hover scale animations

### Requirement 4: Our Work Section — Logo Marquee

**User Story:** As a visitor, I want to see a scrolling logo strip beneath the case studies, so that I perceive tszuk works with multiple clients.

#### Acceptance Criteria

1. THE Marquee SHALL display five SVG placeholder icons as geometric shapes in an infinitely scrolling horizontal strip
2. THE Marquee SHALL use pure CSS @keyframes for continuous right-to-left movement
3. WHEN the visitor hovers over the Marquee, THE Marquee SHALL pause the scrolling animation
4. THE Marquee SHALL apply linear gradient masks on left and right edges to fade logos in and out
5. WHILE the user has prefers-reduced-motion enabled, THE Marquee SHALL display logos statically without scrolling

### Requirement 5: Capabilities & Services Section

**User Story:** As a visitor, I want to see tszuk's service offerings organized clearly, so that I can identify whether they can help with my project.

#### Acceptance Criteria

1. THE Capabilities_Section SHALL display a two-column CSS Grid layout that stacks into a single column on mobile viewports
2. THE Capabilities_Section SHALL display Column 1 with heading "Brand Engineering & Strategy" and items: "Visual Identity", "Brand Guidelines", "Digital & Web Presence"
3. THE Capabilities_Section SHALL display Column 2 with heading "Creative Management & Roster" and items: "360° Brand Direction", "Campaign & Release Execution", "Partnerships & Growth"
4. THE Capabilities_Section SHALL display a 1px solid #EAEAEA divider between the two columns
5. WHEN a visitor hovers over a column, THE Capabilities_Section SHALL transition the column background to #F4F9F1
6. WHEN the Capabilities_Section enters the viewport, THE Landing_Page SHALL apply a Scroll_Reveal animation
7. WHILE the user has prefers-reduced-motion enabled, THE Capabilities_Section SHALL display content without scroll-reveal animation

### Requirement 6: The Minds Section

**User Story:** As a visitor, I want to see the founders and their backgrounds, so that I feel confident in the team behind tszuk.

#### Acceptance Criteria

1. THE Minds_Section SHALL display a two-column grid with founder portraits
2. THE Minds_Section SHALL display Zukisa with title "Co-Founder & Creative Director" and qualification "Bachelor in Design & Creative Direction"
3. THE Minds_Section SHALL display Tshepo with title "Co-Founder & Systems Director" and qualification "BSc Computer Science & Mathematics"
4. THE Minds_Section SHALL display an organic Blob_Shape in color #88BDA4 behind each portrait
5. THE Blob_Shape SHALL continuously morph its border-radius using CSS @keyframes over a 15-second loop
6. WHEN a visitor hovers over a portrait, THE Minds_Section SHALL display an overlay tag showing the founder's focus area
7. WHEN the Minds_Section enters the viewport, THE Landing_Page SHALL apply a Scroll_Reveal animation
8. WHILE the user has prefers-reduced-motion enabled, THE Minds_Section SHALL display portraits without blob morphing or scroll-reveal animation

### Requirement 7: Footer and Contact Form

**User Story:** As a visitor, I want to submit an inquiry through a contact form, so that I can start a conversation with tszuk about my project.

#### Acceptance Criteria

1. THE Footer_Section SHALL display a dark slate (#1A231E) background with the headline "Ready to strip away the noise?"
2. THE Footer_Section SHALL display a form with fields: Name (text), Email (text), Project Type (radio: "Brand Identity/Web", "Artist Management", "Other"), Message (textarea), and a Submit button
3. WHEN a form input receives focus, THE Footer_Section SHALL animate the input's bottom border color to #88BDA4
4. WHEN the visitor submits the form with valid data, THE Landing_Page SHALL send a POST request to /api/contact without page reload
5. WHEN the form submission is in progress, THE Footer_Section SHALL display an inline loading indicator
6. WHEN the form submission succeeds, THE Footer_Section SHALL display the message "Inquiry received. We will be in touch shortly."
7. IF the form submission fails, THEN THE Footer_Section SHALL display an error message to the visitor
8. THE Footer_Section SHALL display studio information: email "hello@tszuk.com", location "Port Elizabeth, South Africa", and social links for Instagram and LinkedIn

### Requirement 8: Contact API Endpoint

**User Story:** As a site operator, I want form submissions sent to my email via a serverless endpoint, so that I receive visitor inquiries without managing server infrastructure.

#### Acceptance Criteria

1. THE Contact_API SHALL accept POST requests at the path /api/contact with a JSON body containing name, email, and message fields
2. WHEN name, email, or message is missing from the request, THE Contact_API SHALL return a 400 status with an error message
3. WHEN all required fields are present and valid, THE Contact_API SHALL send an email to hello@tszuk.com using the Resend SDK
4. WHEN the email is sent successfully, THE Contact_API SHALL return a JSON response with { success: true }
5. IF the Resend SDK returns an error, THEN THE Contact_API SHALL return a 500 status with { error: "message" }

### Requirement 9: Global Layout, Typography, and Responsive Design

**User Story:** As a visitor, I want a consistent, fast-loading, mobile-friendly experience, so that the site feels polished on any device.

#### Acceptance Criteria

1. THE Landing_Page SHALL use the Inter font family with weights 300, 400, and 700
2. THE Landing_Page SHALL use Inter Bold for headings, Inter with letter-spacing 0.15em for subtitles, and Inter Regular with line-height 1.6 for body text
3. THE Landing_Page SHALL define CSS custom properties for all colors in the design system
4. THE Landing_Page SHALL render as a single-page layout with sections in order: Cover, Hero, Work, Capabilities, Minds, Footer
5. THE Landing_Page SHALL be fully responsive, stacking multi-column layouts into single columns on mobile viewports
6. THE Landing_Page SHALL use the Astro Image component for image optimization with no cumulative layout shift
7. THE Landing_Page SHALL lazy-load images below the fold

### Requirement 10: Accessibility

**User Story:** As a visitor using assistive technology, I want the site to be navigable and readable, so that I have equal access to tszuk's content.

#### Acceptance Criteria

1. THE Landing_Page SHALL use a proper heading hierarchy (h1, h2, h3) across all sections
2. THE Landing_Page SHALL provide visible labels or accessible names for all form inputs in the Footer_Section
3. THE Landing_Page SHALL provide visible focus indicators using :focus-visible on all interactive elements
4. WHILE the user has prefers-reduced-motion enabled, THE Landing_Page SHALL disable all CSS animations and transitions

### Requirement 11: Project Architecture

**User Story:** As a developer, I want a component-per-section architecture with scoped CSS, so that the codebase is easy to maintain and edit.

#### Acceptance Criteria

1. THE Landing_Page SHALL be built using the Astro framework with component-per-section architecture
2. THE Landing_Page SHALL use vanilla CSS with custom properties for all styling, with no CSS frameworks or UI component libraries
3. THE Landing_Page SHALL scope CSS to each component to prevent style leakage
4. THE Landing_Page SHALL use approximately 20 lines of vanilla JavaScript for the flip mechanic, with no external animation libraries
5. THE Landing_Page SHALL store the RESEND_API_KEY in a .env file that is excluded from version control
