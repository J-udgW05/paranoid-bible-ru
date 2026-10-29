# UI/UX Pro Max Design Intelligence Rule

When working on user interfaces, web layouts, visual design, components, or styling in this project:

1. **Consult UI/UX Intelligence First**:
   - Before inventing arbitrary color palettes, typography, or UI layouts, run the local search tool via `run_command`:
     ```powershell
     python .agents/skills/ui-ux-pro-max/scripts/search.py "<product_type> <keywords>" --design-system
     ```
   - For specific domain lookups:
     - Styles & AI prompts: `--domain style`
     - Typography pairings: `--domain typography`
     - Color palettes: `--domain color`
     - UX guidelines & WCAG: `--domain ux`
     - Icons (Phosphor/Lucide): `--domain icons`
     - Framework/Stack tips: `--stack html-tailwind` (or `react`, `vue`, etc.)

2. **Strict UI/UX Pre-Delivery Checklist**:
   - [ ] No emojis as interface icons (use SVG or semantic icon sets).
   - [ ] `cursor: pointer` on all interactive/clickable elements.
   - [ ] Contrast ratio: minimum 4.5:1 for body text (WCAG 2.1 AA).
   - [ ] Visible `:focus-visible` outlines for keyboard accessibility.
   - [ ] Respect `prefers-reduced-motion` for transitions and animations.
   - [ ] Avoid Layout Thrashing / CLS (< 0.1).
   - [ ] Responsive design across standard viewports (375px mobile, 768px tablet, 1024px+ desktop).

3. **Active Skills**:
   - `ui-ux-pro-max`: Core design intelligence database and search tool.
   - `ui-styling`: Tailwind CSS & accessible component patterns.
   - `design-system`: Token architecture and component specifications.
