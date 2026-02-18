# Theme Design Workflow

## When to Use This Workflow

Activate when user:
- Implements dark mode
- Creates theme systems
- Designs visual styles
- Plans color schemes
- Implements glassmorphism
- Creates brand themes

---

## Production-Grade Theme Design

### Phase 1: Color System Design

**Semantic Color Palette:**

```typescript
// Base color scales (50-950)
const colorScales = {
  blue: {
    50: '#EFF6FF',
    100: '#DBEAFE',
    500: '#3B82F6', // Base
    900: '#1E3A8A',
    950: '#172554',
  },
  // ... other colors
};

// Semantic mapping
const semanticColors = {
  light: {
    primary: colorScales.blue[600],
    secondary: colorScales.purple[600],
    success: colorScales.green[600],
    error: colorScales.red[600],
    warning: colorScales.amber[600],
    info: colorScales.cyan[600],
    
    background: {
      primary: '#FFFFFF',
      secondary: '#F9FAFB',
      tertiary: '#F3F4F6',
    },
    
    text: {
      primary: '#111827',
      secondary: '#6B7280',
      tertiary: '#9CA3AF',
      inverse: '#FFFFFF',
    },
    
    border: {
      primary: '#E5E7EB',
      secondary: '#D1D5DB',
      focus: colorScales.blue[500],
    },
  },
  
  dark: {
    primary: colorScales.blue[500],
    secondary: colorScales.purple[500],
    success: colorScales.green[500],
    error: colorScales.red[500],
    warning: colorScales.amber[500],
    info: colorScales.cyan[500],
    
    background: {
      primary: '#0F172A',
      secondary: '#1E293B',
      tertiary: '#334155',
    },
    
    text: {
      primary: '#F1F5F9',
      secondary: '#CBD5E1',
      tertiary: '#94A3B8',
      inverse: '#0F172A',
    },
    
    border: {
      primary: '#334155',
      secondary: '#475569',
      focus: colorScales.blue[400],
    },
  },
};
```

---

### Phase 2: Dark Mode Implementation

**Automatic Dark Mode Generation:**

```typescript
function generateDarkMode(lightColors: ColorPalette): ColorPalette {
  return {
    // Invert neutral scale
    neutral: invertScale(lightColors.neutral),
    
    // Lighten semantic colors for dark backgrounds
    success: lighten(lightColors.success, 0.2),
    error: lighten(lightColors.error, 0.2),
    warning: lighten(lightColors.warning, 0.2),
    
    // Adjust shadows (lighter in dark mode)
    shadows: {
      sm: '0 1px 2px 0 rgb(255 255 255 / 0.05)',
      md: '0 4px 6px -1px rgb(255 255 255 / 0.1)',
      // ...
    },
  };
}

// Dark mode toggle
function useDarkMode() {
  const [isDark, setIsDark] = useState(false);

  useEffect(() => {
    // Check system preference
    const mediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
    setIsDark(mediaQuery.matches);

    // Listen for changes
    const handler = (e: MediaQueryListEvent) => setIsDark(e.matches);
    mediaQuery.addEventListener('change', handler);
    return () => mediaQuery.removeEventListener('change', handler);
  }, []);

  useEffect(() => {
    // Apply theme
    document.documentElement.classList.toggle('dark', isDark);
  }, [isDark]);

  return [isDark, setIsDark] as const;
}
```

---

### Phase 3: Visual Style Systems

**Glassmorphism (Controlled):**

```css
/* Safe glassmorphism usage */
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
}

/* Dark mode variant */
.dark .glass-card {
  background: rgba(15, 23, 42, 0.7);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

/* ⚠️ WARNING: Only use for:
   - Modal overlays
   - Floating elements
   - Decorative accents
   
   ❌ NEVER use for:
   - Text-heavy content
   - Form fields
   - Data tables
*/
```

**Neumorphism (Subtle):**

```css
.neomorphic-card {
  background: #E0E5EC;
  box-shadow: 
    9px 9px 16px rgba(163, 177, 198, 0.6),
    -9px -9px 16px rgba(255, 255, 255, 0.5);
  border-radius: 16px;
}

.neomorphic-card:active {
  box-shadow: 
    inset 9px 9px 16px rgba(163, 177, 198, 0.6),
    inset -9px -9px 16px rgba(255, 255, 255, 0.5);
}
```

**Modern Gradients:**

```css
/* Subtle gradient backgrounds */
.gradient-bg {
  background: linear-gradient(
    135deg,
    #667eea 0%,
    #764ba2 100%
  );
}

/* Gradient text */
.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Mesh gradient (modern) */
.mesh-gradient {
  background: 
    radial-gradient(at 40% 20%, hsla(28,100%,74%,1) 0px, transparent 50%),
    radial-gradient(at 80% 0%, hsla(189,100%,56%,1) 0px, transparent 50%),
    radial-gradient(at 0% 50%, hsla(355,100%,93%,1) 0px, transparent 50%);
}
```

---

### Phase 4: Theme Switching

**Smooth Theme Transition:**

```typescript
function ThemeToggle() {
  const { theme, toggleTheme } = useTheme();

  const handleToggle = () => {
    // Add transition class
    document.documentElement.classList.add('theme-transitioning');
    
    // Toggle theme
    toggleTheme();
    
    // Remove transition class after animation
    setTimeout(() => {
      document.documentElement.classList.remove('theme-transitioning');
    }, 300);
  };

  return (
    <button onClick={handleToggle} aria-label="Toggle theme">
      {theme === 'light' ? <Moon /> : <Sun />}
    </button>
  );
}

// CSS for smooth transition
.theme-transitioning,
.theme-transitioning *,
.theme-transitioning *::before,
.theme-transitioning *::after {
  transition: 
    background-color 300ms ease,
    border-color 300ms ease,
    color 300ms ease !important;
}
```

---

### Phase 5: Accessibility in Themes

**Contrast Checking:**

```typescript
function checkContrast(foreground: string, background: string): {
  ratio: number;
  passes: {
    aa: boolean;
    aaa: boolean;
  };
} {
  const ratio = calculateContrastRatio(foreground, background);
  
  return {
    ratio,
    passes: {
      aa: ratio >= 4.5,  // WCAG AA
      aaa: ratio >= 7,   // WCAG AAA
    },
  };
}

// Validate theme colors
function validateTheme(theme: Theme): ValidationResult[] {
  const issues: ValidationResult[] = [];
  
  // Check text on backgrounds
  const textOnPrimary = checkContrast(
    theme.colors.text.primary,
    theme.colors.background.primary
  );
  
  if (!textOnPrimary.passes.aa) {
    issues.push({
      severity: 'error',
      message: 'Text color fails WCAG AA contrast requirements',
      suggestion: 'Use darker text or lighter background',
    });
  }
  
  return issues;
}
```

---

## Risk Warnings

**Glassmorphism Warning:**

```
🚨 USABILITY WARNING

Request: "Use glassmorphism for all content"

RISKS:
- Readability: CRITICAL - Blurred backgrounds reduce text clarity
- Performance: HIGH - backdrop-filter is expensive
- Accessibility: CRITICAL - Fails WCAG contrast
- Browser Support: MEDIUM - Not supported in older browsers

SAFE USAGE:
✅ Modal overlays
✅ Floating action buttons
✅ Decorative elements

❌ NEVER:
- Text-heavy content
- Form fields
- Data tables
- Primary navigation

ALTERNATIVE:
Use solid backgrounds with subtle shadows for better
readability and performance.
```

---

## Production Checklist

- [ ] Light and dark themes implemented
- [ ] Smooth theme transitions
- [ ] System preference detection
- [ ] Theme persistence (localStorage)
- [ ] All colors pass WCAG AA
- [ ] Visual styles used appropriately
- [ ] Performance optimized
- [ ] Browser compatibility tested
- [ ] Accessibility audited
- [ ] Documentation complete

---

This workflow ensures production-grade theme systems with accessibility and performance.
