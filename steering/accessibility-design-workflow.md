# Accessibility Design Workflow

## When to Use This Workflow

Activate when user:
- Implements WCAG compliance
- Designs accessible interfaces
- Plans keyboard navigation
- Creates screen reader support
- Implements ARIA patterns
- Audits accessibility

---

## Production-Grade Accessibility Design

### Phase 1: WCAG 2.1 Compliance

**Level AA Requirements (Minimum):**

```
✅ Perceivable:
- Text alternatives for images
- Captions for videos
- Color contrast 4.5:1 (text), 3:1 (UI)
- Resizable text up to 200%

✅ Operable:
- Keyboard accessible
- No keyboard traps
- Skip navigation links
- Focus visible
- Touch targets 44x44px

✅ Understandable:
- Readable text
- Predictable navigation
- Input assistance
- Error identification

✅ Robust:
- Valid HTML
- ARIA used correctly
- Compatible with assistive tech
```

---

### Phase 2: Color Contrast

**Contrast Requirements:**

```typescript
// Contrast checker
function checkContrast(fg: string, bg: string): {
  ratio: number;
  passes: {
    normalAA: boolean;   // 4.5:1
    normalAAA: boolean;  // 7:1
    largeAA: boolean;    // 3:1
    largeAAA: boolean;   // 4.5:1
    uiAA: boolean;       // 3:1
  };
} {
  const ratio = calculateContrastRatio(fg, bg);
  
  return {
    ratio,
    passes: {
      normalAA: ratio >= 4.5,
      normalAAA: ratio >= 7,
      largeAA: ratio >= 3,
      largeAAA: ratio >= 4.5,
      uiAA: ratio >= 3,
    },
  };
}

// Example usage
const result = checkContrast('#6B7280', '#FFFFFF');
// { ratio: 5.9, passes: { normalAA: true, ... } }
```

**Safe Color Combinations:**

```css
/* ✅ WCAG AA Compliant */
.text-primary {
  color: #111827; /* 16.1:1 on white */
}

.text-secondary {
  color: #4B5563; /* 9.7:1 on white */
}

.text-tertiary {
  color: #6B7280; /* 5.9:1 on white */
}

/* ❌ FAILS WCAG AA */
.text-light-gray {
  color: #D1D5DB; /* 1.8:1 on white - TOO LOW */
}

/* ⚠️ WARNING: Auto-block insufficient contrast */
```

---

### Phase 3: Keyboard Navigation

**Focus Management:**

```tsx
// Visible focus indicators
<Button className="focus:ring-2 focus:ring-primary-500 focus:ring-offset-2">
  Click me
</Button>

// CSS
.button:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}

// Skip to main content
<SkipLink href="#main-content">
  Skip to main content
</SkipLink>

<main id="main-content">
  {/* Main content */}
</main>

// Focus trap in modals
function Modal({ isOpen, onClose, children }) {
  const modalRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (!isOpen) return;

    const modal = modalRef.current;
    if (!modal) return;

    // Get focusable elements
    const focusableElements = modal.querySelectorAll(
      'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );

    const firstElement = focusableElements[0] as HTMLElement;
    const lastElement = focusableElements[focusableElements.length - 1] as HTMLElement;

    // Focus first element
    firstElement?.focus();

    // Trap focus
    const handleTab = (e: KeyboardEvent) => {
      if (e.key !== 'Tab') return;

      if (e.shiftKey) {
        if (document.activeElement === firstElement) {
          e.preventDefault();
          lastElement?.focus();
        }
      } else {
        if (document.activeElement === lastElement) {
          e.preventDefault();
          firstElement?.focus();
        }
      }
    };

    modal.addEventListener('keydown', handleTab);
    return () => modal.removeEventListener('keydown', handleTab);
  }, [isOpen]);

  return (
    <div ref={modalRef} role="dialog" aria-modal="true">
      {children}
    </div>
  );
}
```

**Keyboard Shortcuts:**

```tsx
// Global keyboard shortcuts
useEffect(() => {
  const handleKeyboard = (e: KeyboardEvent) => {
    // Cmd/Ctrl + K: Open search
    if ((e.metaKey || e.ctrlKey) && e.key === 'k') {
      e.preventDefault();
      openSearch();
    }

    // Escape: Close modal
    if (e.key === 'Escape') {
      closeModal();
    }

    // Arrow keys: Navigate
    if (e.key === 'ArrowDown') {
      navigateDown();
    }
  };

  window.addEventListener('keydown', handleKeyboard);
  return () => window.removeEventListener('keydown', handleKeyboard);
}, []);
```

---

### Phase 4: ARIA Patterns

**Common ARIA Patterns:**

```tsx
// Button
<button
  type="button"
  aria-label="Close dialog"
  aria-pressed={isPressed}
>
  <X />
</button>

// Toggle
<button
  role="switch"
  aria-checked={isEnabled}
  onClick={toggle}
>
  {isEnabled ? 'Enabled' : 'Disabled'}
</button>

// Accordion
<div>
  <button
    aria-expanded={isExpanded}
    aria-controls="panel-1"
    onClick={toggle}
  >
    Section Title
  </button>
  <div
    id="panel-1"
    role="region"
    aria-labelledby="button-1"
    hidden={!isExpanded}
  >
    Panel content
  </div>
</div>

// Tabs
<div role="tablist">
  <button
    role="tab"
    aria-selected={activeTab === 'tab1'}
    aria-controls="panel-1"
    id="tab-1"
  >
    Tab 1
  </button>
</div>
<div
  role="tabpanel"
  id="panel-1"
  aria-labelledby="tab-1"
  hidden={activeTab !== 'tab1'}
>
  Panel content
</div>

// Live Region (for dynamic updates)
<div
  role="status"
  aria-live="polite"
  aria-atomic="true"
>
  {statusMessage}
</div>

// Alert
<div
  role="alert"
  aria-live="assertive"
>
  {errorMessage}
</div>
```

---

### Phase 5: Screen Reader Support

**Semantic HTML:**

```tsx
// ✅ Good: Semantic HTML
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>

<main>
  <article>
    <h1>Article Title</h1>
    <p>Content...</p>
  </article>
</main>

<aside>
  <h2>Related Links</h2>
</aside>

// ❌ Bad: Div soup
<div className="nav">
  <div className="nav-item">Home</div>
  <div className="nav-item">About</div>
</div>
```

**Alt Text Best Practices:**

```tsx
// ✅ Descriptive alt text
<img
  src="/chart.png"
  alt="Bar chart showing 50% increase in revenue from Q1 to Q2"
/>

// ✅ Decorative images
<img
  src="/decoration.png"
  alt=""
  role="presentation"
/>

// ❌ Bad alt text
<img src="/chart.png" alt="chart" />
<img src="/photo.jpg" alt="image" />
```

**Screen Reader Only Text:**

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}

/* Usage */
<button>
  <X />
  <span className="sr-only">Close dialog</span>
</button>
```

---

### Phase 6: Form Accessibility

**Accessible Forms:**

```tsx
<form>
  {/* Label association */}
  <div>
    <label htmlFor="email">
      Email Address
      <span aria-label="required">*</span>
    </label>
    <input
      id="email"
      type="email"
      required
      aria-required="true"
      aria-invalid={hasError}
      aria-describedby={hasError ? 'email-error' : undefined}
    />
    {hasError && (
      <div id="email-error" role="alert">
        Please enter a valid email address
      </div>
    )}
  </div>

  {/* Fieldset for grouped inputs */}
  <fieldset>
    <legend>Shipping Address</legend>
    <label htmlFor="street">Street</label>
    <input id="street" type="text" />
    
    <label htmlFor="city">City</label>
    <input id="city" type="text" />
  </fieldset>

  {/* Error summary */}
  {errors.length > 0 && (
    <div role="alert" aria-labelledby="error-summary">
      <h2 id="error-summary">Please fix the following errors:</h2>
      <ul>
        {errors.map((error) => (
          <li key={error.field}>
            <a href={`#${error.field}`}>{error.message}</a>
          </li>
        ))}
      </ul>
    </div>
  )}
</form>
```

---

### Phase 7: Motion & Animation

**Respect User Preferences:**

```css
/* Reduce motion for users who prefer it */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* Alternative: Provide toggle */
.no-motion * {
  animation: none !important;
  transition: none !important;
}
```

```tsx
// React implementation
function useReducedMotion() {
  const [prefersReducedMotion, setPrefersReducedMotion] = useState(false);

  useEffect(() => {
    const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    setPrefersReducedMotion(mediaQuery.matches);

    const handler = (e: MediaQueryListEvent) => {
      setPrefersReducedMotion(e.matches);
    };

    mediaQuery.addEventListener('change', handler);
    return () => mediaQuery.removeEventListener('change', handler);
  }, []);

  return prefersReducedMotion;
}
```

---

### Phase 8: Testing & Auditing

**Automated Testing:**

```typescript
// Jest + Testing Library
import { render, screen } from '@testing-library/react';
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

test('Button is accessible', async () => {
  const { container } = render(<Button>Click me</Button>);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});

// Check for alt text
test('Image has alt text', () => {
  render(<img src="/test.jpg" alt="Test image" />);
  expect(screen.getByAltText('Test image')).toBeInTheDocument();
});

// Check for labels
test('Input has label', () => {
  render(
    <>
      <label htmlFor="email">Email</label>
      <input id="email" />
    </>
  );
  expect(screen.getByLabelText('Email')).toBeInTheDocument();
});
```

**Manual Testing Checklist:**

```
✅ Keyboard Navigation:
- [ ] Tab through all interactive elements
- [ ] Shift+Tab works in reverse
- [ ] Enter/Space activates buttons
- [ ] Escape closes modals
- [ ] Arrow keys navigate menus

✅ Screen Reader:
- [ ] Test with NVDA (Windows)
- [ ] Test with JAWS (Windows)
- [ ] Test with VoiceOver (Mac/iOS)
- [ ] Test with TalkBack (Android)

✅ Visual:
- [ ] Zoom to 200%
- [ ] Test with high contrast mode
- [ ] Test with color blindness simulator
- [ ] Check focus indicators

✅ Tools:
- [ ] Lighthouse accessibility audit
- [ ] axe DevTools
- [ ] WAVE browser extension
- [ ] Color contrast checker
```

---

## Accessibility Risk Warnings

**Contrast Violation:**

```
🚨 ACCESSIBILITY VIOLATION - BLOCKED

Issue: Insufficient color contrast
- Foreground: #CCCCCC
- Background: #FFFFFF
- Ratio: 1.6:1
- Required: 4.5:1

IMPACT:
- Users with low vision cannot read text
- Fails WCAG 2.1 Level AA
- Legal compliance risk

CORRECTED:
✅ Use #4B5563 (9.7:1 ratio)
✅ Use #6B7280 (5.9:1 ratio)

This is NON-NEGOTIABLE.
```

**Missing Alt Text:**

```
⚠️ ACCESSIBILITY WARNING

Issue: Image missing alt text
<img src="/chart.png" />

IMPACT:
- Screen reader users miss content
- Fails WCAG 2.1 Level A

CORRECTED:
<img 
  src="/chart.png" 
  alt="Bar chart showing 50% revenue increase"
/>

Or for decorative images:
<img src="/decoration.png" alt="" role="presentation" />
```

---

## Production Checklist

- [ ] WCAG 2.1 Level AA compliant
- [ ] Color contrast verified (4.5:1 text, 3:1 UI)
- [ ] Keyboard navigation works
- [ ] Focus indicators visible
- [ ] ARIA attributes correct
- [ ] Alt text on all images
- [ ] Form labels associated
- [ ] Error messages clear
- [ ] Skip navigation link
- [ ] Semantic HTML used
- [ ] Screen reader tested
- [ ] Motion preferences respected
- [ ] Touch targets 44x44px
- [ ] Automated tests passing
- [ ] Manual audit complete

---

This workflow ensures production-grade accessibility compliance and inclusive design.
