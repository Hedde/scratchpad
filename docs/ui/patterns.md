# UI Patterns

> **Status:** [NOT YET CONFIGURED] — Update this file when the UI framework and component approach is established.

## UI Framework

[Specify: TailwindCSS, Bootstrap, Material UI, DaisyUI, custom, etc.]

## Component Architecture

[Describe the component system: atomic design, hierarchical, flat, etc.]

```
# Component directory structure
```

### Layer Hierarchy

```
# Example:
# Atoms (primitives) → Molecules (groups) → Organisms (sections) → Pages
# Or: Base → Composite → Feature-specific
```

### Import / Usage Mechanism

[How components are imported and used in templates/views]

## Styling Conventions

### Preferred Approach

[Semantic classes vs utility-first vs CSS modules — what's the standard?]

```
<!-- Preferred -->
[example]

<!-- Avoid -->
[example]
```

### Theme

[Dark/light mode, color system, design tokens]

## Component Extraction Rules

Extract a component when:
- The same markup appears in **3+ places**
- The pattern has **clear variants** (size, color, state)
- It encapsulates **behavior** (not just styling)

Don't extract when:
- Used only once or twice (inline is fine)
- The "component" would just be a CSS class wrapper
- Extraction would make the code harder to understand

## Common Patterns

### Variant Helpers

[How to handle component variants: size, color, state]

```
# Example
```

### Form Components

[Form input patterns, validation display, error states]

```
# Example
```

### Slot-Based / Children Composition

[How to compose complex components from simple ones]

```
# Example
```

### Loading States

[How to show loading, error, and empty states]

```
# Example
```

### Responsive Patterns

[Mobile-first, breakpoint strategy, responsive utilities]

```
# Example
```

## Component Inventory

> Update this list as components are built. Remove this note when the design system is established.

| Component | Module/File | Purpose |
|-----------|-------------|---------|
| [name] | [path] | [what it does] |
