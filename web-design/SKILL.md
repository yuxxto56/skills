---
name: web-design
description: High-end website and landing-page design guidance for Apple/Google-inspired visual systems. Use when Codex is designing, implementing, or refining websites, portfolios, product pages, marketing pages, navigation bars, hero sections, visual hierarchy, card layouts, responsive polish, or premium minimalist interfaces, especially when the user asks for advanced, artistic, clean, gallery-like, Apple-like, or Google-like web design.
---

# Web Design

Use this skill to make websites feel premium, restrained, and product-grade rather than like generic templates.

## Core Direction

- Build the actual usable page first, not a marketing explanation of features.
- Use Apple-like large visual storytelling: strong first screen, minimal copy, clear hierarchy, generous whitespace, and decisive calls to action.
- Use Google-like clarity for content sections: simple cards, soft surfaces, readable spacing, and friendly information grouping.
- Keep the page calm. Avoid decorative clutter, busy gradients, excessive shadows, nested cards, and ornamental UI.
- Prefer real photographic or product assets. Do not rely on empty placeholders, fake image boxes, CSS art, or decorative blobs.

## Visual Rules

- Use a restrained palette: black, white, light gray, deep gray, warm white, and subtle silver accents.
- Keep typography clean and modern. Use large type only for true hero moments; reduce heading size in explanatory sections, cards, sidebars, and nav.
- Use 8px or smaller card radius unless the existing design system says otherwise. Use full-pill shapes only for controls like buttons, chips, and nav capsules.
- Use stable dimensions for image slots, cards, nav, and buttons so text, hover states, and images do not shift the layout.
- Never let Chinese text overflow its container. Check long headings at tablet and mobile widths.
- For Chinese premium sites, keep letter spacing at 0 and use weight, scale, spacing, and contrast instead of decorative tracking.
- Treat real browser wrapping as the source of truth. If an important Chinese headline wraps awkwardly, reduce size slightly, widen its content box, or adjust max-width before adding line breaks.

## Brand And Logo

- A logo must be legible at the actual nav size first, usually 32-44px. Test it on white, warm-white, and glass backgrounds.
- For complex camera, aperture, or geometric marks, prefer a real raster asset or carefully drawn solid vector over a tiny transparent SVG with fragile strokes.
- On light navigation bars, default logo marks should be pure black or high-contrast dark gray. Avoid pale gray details that disappear on translucent white.
- Keep the brand area compact and stable. Do not let text labels, icons, or hover states change nav height or shift adjacent links.
- If the mark itself carries the brand, the nav can use logo-only branding; avoid forcing extra text when it makes the header noisy.

## Navigation Pattern

- Treat the header as a designed control surface, not a row of plain links.
- For Apple/Google-like official-site navigation, prefer a full-width sticky top bar: top at 0, no floating gap, translucent background, subtle border, blur, and low shadow.
- Use capsule navigation only when the brief explicitly wants a floating gallery or editorial surface. Otherwise avoid a small isolated pill that feels detached from the page.
- Keep the outer header flat and wide. Put hierarchy into spacing, active states, and fine borders instead of large rounded containers.
- Keep nav labels short and evenly spaced. Use refined hover indicators such as a faint underline or subtle highlight.
- Active nav states should be clear but lightweight: underline, soft surface, or slight weight change. Avoid heavy black pill buttons unless the whole design language depends on them.
- Nav links must have stable min-widths and `white-space: nowrap`; Chinese labels like “新闻资讯” and “关于我们” should never stack vertically.
- Do not duplicate a strong page CTA in the top nav when the hero already contains it, unless conversion pressure is explicitly more important than restraint.
- On mobile, convert nav into a compact floating panel or clean menu. Avoid a full-width generic white dropdown when a polished compact surface fits.

## Page Composition

- Start with one strong first-viewport signal: brand/product/site purpose plus real visual content.
- For hero sections, use a large photograph or product visual with concise text and 1-2 clear actions.
- Hero images should feel immersive without swallowing the page. Use responsive height clamps and aspect-ratio so the next section remains reachable and the image does not become a wall.
- Overlay hero text must stay inside the photo composition. Avoid text so large that it collides with the header, important subjects, or viewport edges.
- For galleries or portfolios, let images carry the page. Captions should be quiet, short, and optional.
- For lists such as services, products, or series, use clean cards with one image, one title, one short description, and one action.
- For editorial/news sections, use magazine-like image/text rhythm without turning the page into a news portal.
- For about sections, use one memorable belief statement plus compact proof/process blocks.
- Search bars, filters, and load-more controls should be calm and functional. Buttons need enough width for Chinese labels, and count hints such as “已显示 9 / 16” help pagination feel controlled.

## Interaction And Polish

- Add subtle scroll reveal or hover movement only when it supports perceived quality. Keep motion slow, small, and optional for reduced-motion users.
- Buttons should feel tactile but understated. Prefer simple dark/light contrast over bright accent colors.
- Make focus and hover states visible and tasteful.
- Confirm responsive behavior at desktop, tablet, and mobile breakpoints when possible.

## Implementation Checklist

- Ensure the first screen immediately communicates the site category and quality level.
- Ensure navigation feels intentionally designed, not ordinary text links or an accidental capsule widget.
- Ensure logo assets are readable at final rendered size and have enough contrast on the real header background.
- Ensure primary CTAs are present but not repeated in a way that makes the design feel commercial or noisy.
- Ensure content density stays low enough for premium feel but high enough to understand the offering.
- Check real browser screenshots for hero height, nav stickiness, Chinese wrapping, and vertical button text before calling the design finished.
- Run available tests or static checks before claiming completion.
