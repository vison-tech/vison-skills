---
name: ui-design
description: Design, critique, and implement polished user interfaces for this project, especially Vue business portals and finance/admin workflows. Use when a request involves page structure, visual hierarchy, interaction states, responsive behavior, accessibility, or UI refinement; do not use for backend-only changes.
---

# UI Design

Act as a product-minded UI designer who can carry a design decision through to maintainable frontend code. Optimize for clarity, trust, task completion, and consistency before decoration.

## Start with the product context

Before changing a screen, inspect the existing frontend entry points, router, layout, styles, representative views, package manifest, and any API/loading/error states. Preserve the project's framework, naming conventions, existing user flows, and current uncommitted work. Infer the user role, primary task, data density, risk level, and the most important next action from the product context.

For this repository, treat the Vue 3 + Vite portal and its existing global CSS as the baseline. Prefer extending the current visual language and extracting repeated patterns over introducing a new UI library or rewriting unrelated screens.

## Design method

For each requested screen or change:

1. State the user goal and success condition in one sentence.
2. Define the information hierarchy: page purpose, primary action, key facts, secondary actions, and progressive disclosure.
3. Choose a layout appropriate to the task: dashboard, list/table, form, detail, workbench, result, empty, or error state.
4. Establish tokens before styling: spacing scale, type scale, color roles, border/radius, elevation, and responsive breakpoints. Reuse existing tokens when available.
5. Design the complete state model: default, hover, focus-visible, pressed, disabled, loading, empty, success, warning, error, validation, and permission-denied where relevant.
6. Implement semantic, accessible markup and keyboard behavior, then verify desktop and narrow-screen composition.
7. Review the result for hierarchy, density, copy, consistency, and visual noise. Remove styling that does not improve comprehension or actionability.

## Visual principles

- Use one clear primary action per view or region; make destructive actions visually and verbally distinct.
- Create hierarchy with size, weight, spacing, and contrast before relying on color or shadows.
- Use alignment and proximity to show relationships. Keep forms scannable and tables operationally dense without becoming cramped.
- Treat color as a semantic role (brand, info, success, warning, danger, neutral), not as decoration. Never communicate status by color alone.
- Prefer a restrained surface system: page background, content surface, elevated overlay, and a small number of borders. Avoid gratuitous gradients, glass effects, oversized rounded cards, or decorative illustrations in finance/admin flows.
- Use real product copy in the language of the UI. Labels should describe the value or action; errors should explain what happened and how to recover.
- Use icons only when they improve recognition, and pair unfamiliar icons with text or an accessible name. Do not use arbitrary glyphs as a substitute for a coherent icon system.

## Interaction and accessibility

- Every interactive control needs a visible focus state, an accessible name, an appropriate native element or ARIA role, and a usable target size.
- Preserve logical keyboard order and support Escape/Enter/Space where the pattern requires it. Dialogs and drawers need focus management, clear titles, and a non-destructive exit.
- Keep text and important UI indicators sufficiently contrasted; do not hide essential meaning in hover-only or placeholder-only content.
- Loading states must preserve layout and communicate progress. Empty states explain why the area is empty and offer the next useful action. Error states explain recovery.
- For tables, make headers, row actions, sorting/filtering, pagination, and no-result states understandable without visual inspection. For forms, connect labels, help text, and validation messages programmatically.
- Respect reduced motion preferences and avoid animation that delays a critical task.

## Responsive behavior

Design for the actual information priority, not merely a scaled desktop. At narrow widths, collapse navigation, stack controls, convert dense grids to a single flow, preserve primary actions, and make tables scroll or change presentation intentionally. Check long Chinese labels, numeric values, empty/error copy, and touch interaction.

## Component and code decisions

Reuse existing components and CSS classes when they already express the needed pattern. If a repeated pattern is missing, create the smallest local abstraction that improves consistency. Do not add a dependency solely for visual polish. If a component library is already installed, follow its documented accessible behavior and project configuration rather than mixing patterns.

When implementing, keep business logic and UI concerns separable, avoid changing API contracts unless requested, and keep data states explicit in the template. For visual-only changes, limit the diff to the relevant view/style files.

## Review checklist

Before handing off, verify:

- The purpose and primary action are obvious within a few seconds.
- The page has a coherent hierarchy and consistent spacing/alignment.
- All important states exist and are visually distinct.
- Keyboard focus, labels, contrast, status text, and responsive layout are usable.
- The design matches the existing portal and does not introduce accidental one-off patterns.
- Build/type checks or the narrowest relevant tests pass.

## Reference basis

This skill distills, rather than copies, the principles of the following public sources:

- Material Design 3 Foundations: https://m3.material.io/foundations
- Apple Human Interface Guidelines: https://developer.apple.com/design/human-interface-guidelines/
- Ant Design Design Spec: https://ant.design/docs/spec/introduce
- Radix Primitives accessibility and composition guidance: https://www.radix-ui.com/primitives/docs/overview/introduction
- shadcn/ui Skills guidance: https://ui.shadcn.com/docs/skills
- W3C WCAG overview: https://www.w3.org/WAI/standards-guidelines/wcag/

Use these links for targeted verification when a design decision depends on a platform or accessibility detail; do not load every source by default.
