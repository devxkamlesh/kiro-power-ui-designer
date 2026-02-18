# Responsive Design Workflow

## When to Use This Workflow

Activate when user:
- Implements responsive layouts
- Designs mobile-first interfaces
- Plans breakpoint strategies
- Creates adaptive components
- Optimizes for different devices
- Implements fluid typography

---

## Production-Grade Responsive Design

### Phase 1: Breakpoint Strategy

**Standard Breakpoints:**

```typescript
const breakpoints = {
  xs: '320px',   // Small phones
  sm: '640px',   // Large phones
  md: '768px',   // Tablets
  lg: '1024px',  // Laptops
  xl: '1280px',  // Desktops
  '2xl': '1536px', // Large desktops
};

// Tailwind config
module.exports = {
  theme: {
    screens: {
      'xs': '320px',
      'sm': '640px',
      'md': '768px',
      'lg': '1024px',
      'xl': '1280px',
      '2xl': '1536px',
    },
  },
};
```

**Mobile-First Approach:**

```css
/* Base styles (mobile) */
.container {
  padding: 1rem;
  font-size: 0.875rem;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    padding: 1.5rem;
    font-size: 1rem;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    padding: 2rem;
    max-width: 1280px;
    margin: 0 auto;
  }
}
```

---

### Phase 2: Responsive Layout Patterns

**Flexible Grid:**

```tsx
<Grid
  cols={{ xs: 1, sm: 2, md: 3, lg: 4 }}
  gap={{ xs: 4, md: 6 }}
>
  <GridItem>Content 1</GridItem>
  <GridItem>Content 2</GridItem>
  <GridItem>Content 3</GridItem>
  <GridItem>Content 4</GridItem>
</Grid>

// CSS Grid implementation
.grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: 1fr;
}

@media (min-width: 640px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
  }
}

@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

**Responsive Navigation:**

```tsx
// Mobile: Hamburger menu
// Desktop: Horizontal nav

<Navigation>
  {/* Mobile Menu Button */}
  <MobileMenuButton className="lg:hidden">
    <Menu />
  </MobileMenuButton>

  {/* Desktop Navigation */}
  <DesktopNav className="hidden lg:flex">
    <NavItem href="/">Home</NavItem>
    <NavItem href="/features">Features</NavItem>
    <NavItem href="/pricing">Pricing</NavItem>
  </DesktopNav>

  {/* Mobile Drawer */}
  <MobileDrawer open={mobileMenuOpen} className="lg:hidden">
    <NavItem href="/">Home</NavItem>
    <NavItem href="/features">Features</NavItem>
    <NavItem href="/pricing">Pricing</NavItem>
  </MobileDrawer>
</Navigation>
```

---

### Phase 3: Fluid Typography

**Responsive Font Sizes:**

```css
/* Fluid typography using clamp() */
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
  /* Min: 32px, Preferred: 5vw, Max: 64px */
}

h2 {
  font-size: clamp(1.5rem, 3vw, 3rem);
}

body {
  font-size: clamp(1rem, 2vw, 1.125rem);
}

/* Alternative: Responsive scale */
:root {
  --font-size-base: 16px;
}

@media (min-width: 768px) {
  :root {
    --font-size-base: 18px;
  }
}

@media (min-width: 1024px) {
  :root {
    --font-size-base: 20px;
  }
}
```

---

### Phase 4: Touch-Friendly Design

**Touch Target Sizes:**

```css
/* Minimum 44x44px for touch targets */
.button {
  min-height: 44px;
  min-width: 44px;
  padding: 12px 24px;
}

/* Increase spacing on mobile */
@media (max-width: 767px) {
  .nav-item {
    padding: 16px;
    margin: 8px 0;
  }
}

/* Larger tap areas */
.icon-button {
  padding: 12px;
  /* Creates 48x48px tap area */
}
```

---

### Phase 5: Responsive Images

**Optimized Image Loading:**

```tsx
<Image
  src="/hero.jpg"
  alt="Hero"
  sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
  width={1200}
  height={800}
  priority
/>

// Art direction with picture element
<picture>
  <source
    media="(max-width: 767px)"
    srcSet="/hero-mobile.jpg"
  />
  <source
    media="(min-width: 768px)"
    srcSet="/hero-desktop.jpg"
  />
  <img src="/hero-desktop.jpg" alt="Hero" />
</picture>
```

---

### Phase 6: Container Queries

**Component-Level Responsiveness:**

```css
/* Container queries (modern approach) */
.card-container {
  container-type: inline-size;
}

.card {
  display: flex;
  flex-direction: column;
}

/* When container is > 400px */
@container (min-width: 400px) {
  .card {
    flex-direction: row;
  }
}

/* When container is > 600px */
@container (min-width: 600px) {
  .card {
    gap: 2rem;
  }
}
```

---

## Behavioral Psychology for Mobile

### Thumb Zone Optimization:
```
┌─────────────┐
│   Hard      │ Top corners (hard to reach)
│             │
│   Easy      │ Middle (easy to reach)
│             │
│   Natural   │ Bottom (thumb rests here)
└─────────────┘

Place primary actions in bottom 1/3 of screen
```

### Progressive Disclosure:
- Show essential info first
- Hide advanced options behind "More"
- Use accordions for long content
- Implement "Show more" patterns

---

## Production Checklist

- [ ] Mobile-first approach
- [ ] All breakpoints tested
- [ ] Touch targets 44x44px minimum
- [ ] Fluid typography implemented
- [ ] Images optimized for all sizes
- [ ] Navigation works on mobile
- [ ] Forms usable on mobile
- [ ] Tables responsive (scroll or stack)
- [ ] Performance optimized
- [ ] Tested on real devices
- [ ] Landscape orientation handled
- [ ] Tablet-specific layouts
- [ ] Print styles (if needed)

---

This workflow ensures production-grade responsive design across all devices.
