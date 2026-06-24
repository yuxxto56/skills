---
name: web-design
description: Use when Codex designs, implements, refines, or reviews premium minimalist visual interfaces for websites, WeChat mini programs, mobile apps, product pages, dashboards, portfolios, brand pages, navigation, visual hierarchy, responsive layouts, and Apple/Google-inspired UI direction.
---

# Web Design

Use this skill as a cross-platform design reference for interfaces that should feel simple, premium, restrained, clear, and product-grade. Blend Apple-like restraint, visual focus, and spatial confidence with Google-like clarity, friendly information grouping, and practical usability.

## Core Direction

- Design the actual usable experience first, not a marketing explanation of features.
- Make the interface calm: fewer elements, stronger hierarchy, clearer affordances, and more deliberate whitespace.
- Use Apple-like qualities for first impressions: confident hero visuals, precise typography, quiet copy, strong product or brand presence, and polished motion.
- Use Google-like qualities for usability: readable structure, simple surfaces, approachable controls, obvious state changes, and efficient task paths.
- Favor content and product evidence over decoration. Prefer real product screenshots, photos, data, or concrete UI states when visuals are needed.
- Keep the result flexible for the platform and audience. This is a reference guide, not a fixed template.

## Visual Rules

- Use restrained palettes: white, black, warm white, soft gray, deep gray, silver, and one purposeful accent color when needed.
- Avoid one-note palettes dominated by a single hue family, especially excessive purple-blue gradients, beige/tan, dark slate, or brown/orange.
- Use large type only for true hero or launch moments. Use smaller, tighter headings inside cards, forms, dashboards, tabs, and mobile panels.
- Keep Chinese letter spacing at `0`. Use weight, scale, line height, contrast, and spacing instead of decorative tracking.
- Use 8px or smaller card radius unless the product system already defines another value. Reserve pill shapes for buttons, chips, segmented controls, and navigation capsules.
- Use subtle borders and tonal surfaces before heavy shadows. Shadows should clarify depth, not decorate the page.
- Give fixed-format UI elements stable dimensions with `aspect-ratio`, min/max sizes, grid tracks, or platform-native layout constraints.
- Never allow Chinese text, labels, prices, badges, tabs, or button text to overflow or stack awkwardly. Shorten copy, widen the container, or reduce type size.

## Platform Guidance

- **Websites**: Lead with a strong first-viewport signal: brand, product, offer, or use case plus real visual content. Keep navigation full-width, sticky when useful, lightly translucent or bordered, and stable across scroll.
- **WeChat mini programs**: Keep flows lightweight and task-first. Prioritize fast scanning, compact sections, native-feeling controls, clear empty states, safe tap targets, and minimal page depth.
- **Mobile apps**: Respect platform conventions for navigation, sheets, tabs, permissions, gestures, and system typography. Use motion and haptics conceptually as feedback, not spectacle.
- **Product tools and dashboards**: Prefer dense but organized layouts, restrained surfaces, readable tables, clear filters, and obvious primary actions. Avoid marketing-style hero sections inside operational tools.
- **Brand pages and portfolios**: Let high-quality visuals carry the experience. Use concise copy, generous spacing, quiet captions, and editorial rhythm without turning the page into a generic template.

## Layout And Components

- Treat navigation as a designed control surface, not a row of plain links. Use clear active states, stable widths, and short labels.
- Keep cards for repeated items, modals, previews, and framed tools. Do not put cards inside cards or turn every section into a floating card.
- Prefer familiar controls: icons for tool buttons, segmented controls for modes, toggles for binary settings, sliders or steppers for numeric values, tabs for view switching, and menus for option sets.
- Use real button hierarchy: one primary action per area, quiet secondary actions, and destructive actions separated visually and behaviorally.
- Keep forms calm and scannable with direct labels, clear error states, and enough spacing for touch.
- For lists and feeds, show the information needed for the decision in the list; reserve long text and heavy media for detail views.
- For search, filters, pagination, and load-more controls, make status visible and controlled, for example "已显示 9 / 16".

## Motion And Interaction

- Use motion to explain cause and effect: open, close, select, filter, refresh, confirm, or transition between related states.
- Keep animation slow enough to feel polished and short enough to stay efficient. Avoid bouncy, flashy, or attention-seeking motion unless the product explicitly needs playfulness.
- Provide visible hover, focus, pressed, selected, disabled, loading, empty, and error states.
- Respect reduced-motion preferences on the web and avoid mandatory decorative animation.
- Ensure tap targets on mobile and mini programs are comfortable, separated, and not dependent on tiny text links.

## Avoid

- Overdecorated gradients, gradient blobs, floating orbs, bokeh backgrounds, ornamental SVGs, and purely atmospheric hero images.
- Heavy shadows, glass effects without purpose, excessive blur, nested cards, noisy borders, and repeated CTA buttons.
- Generic stock-like imagery when the user needs to inspect the actual product, place, service, or UI state.
- Large hero typography inside compact panels, dashboards, drawers, mobile cards, or mini program cells.
- Buttons with crowded Chinese labels, vertical text caused by narrow widths, or icon-only controls without tooltip or accessible label.
- Dark, cropped, or blurred images that hide the subject.
- Decorative complexity that makes the interface feel less clear, less premium, or slower to use.

## Quality Checklist

- The first screen immediately communicates what this is and why it matters.
- The design feels simple, premium, restrained, clear, and usable on its target platform.
- Apple influence appears in hierarchy, restraint, polish, and visual confidence; Google influence appears in clarity, grouping, friendliness, and task efficiency.
- The primary user task is reachable without decorative or marketing friction.
- Navigation, controls, cards, forms, and text keep stable dimensions across desktop, tablet, mobile, and mini program widths.
- Chinese text wraps naturally and never overflows its container.
- Color, radius, shadow, image choice, and motion all serve hierarchy or usability.
- Run available tests, static checks, or visual verification before claiming the design is finished.
