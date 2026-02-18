# Design System Workflow

## When to Use This Workflow

Activate when user:
- Creates design systems
- Defines design tokens
- Builds component libraries
- Plans design documentation
- Implements theming systems
- Scales design across teams

---

## Production-Grade Design System

### Phase 1: Design Tokens Foundation

**Token Structure:**

```typescript
// tokens/colors.ts
export const colors = {
  // Brand Colors
  brand: {
    primary: {
      50: '#EFF6FF',
      100: '#DBEAFE',
      200: '#BFDBFE',
      300: '#93C5FD',
      400: '#60A5FA',
      500: '#3B82F6', // Base
      600: '#2563EB',
      700: '#1D4ED8',
      800: '#1E40AF',
      900: '#1E3A8A',
      950: '#172554',
    },
    secondary: {
      // Similar structure
    },
  },

  // Neutral Colors
  neutral: {
    50: '#F9FAFB',
    100: '#F3F4F6',
    200: '#E5E7EB',
    300: '#D1D5DB',
    400: '#9CA3AF',
    500: '#6B7280',
    600: '#4B5563',
    700: '#374151',
    800: '#1F2937',
    900: '#111827',
    950: '#030712',
  },

  // Semantic Colors
  semantic: {
    success: {
      light: '#D1FAE5',
      base: '#10B981',
      dark: '#065F46',
    },
    error: {
      light: '#FEE2E2',
      base: '#EF4444',
      dark: '#991B1B',
    },
    warning: {
      light: '#FEF3C7',
      base: '#F59E0B',
      dark: '#92400E',
    },
    info: {
      light: '#DBEAFE',
      base: '#3B82F6',
      dark: '#1E40AF',
    },
  },
};

// tokens/typography.ts
export const typography = {
  fontFamily: {
    sans: ['Inter', 'system-ui', 'sans-serif'],
    mono: ['Fira Code', 'monospace'],
    display: ['Cal Sans', 'sans-serif'],
  },

  fontSize: {
    xs: '0.75rem',    // 12px
    sm: '0.875rem',   // 14px
    base: '1rem',     // 16px
    lg: '1.125rem',   // 18px
    xl: '1.25rem',    // 20px
    '2xl': '1.5rem',  // 24px
    '3xl': '1.875rem',// 30px
    '4xl': '2.25rem', // 36px
    '5xl': '3rem',    // 48px
    '6xl': '3.75rem', // 60px
  },

  fontWeight: {
    normal: 400,
    medium: 500,
    semibold: 600,
    bold: 700,
  },

  lineHeight: {
    none: 1,
    tight: 1.25,
    snug: 1.375,
    normal: 1.5,
    relaxed: 1.625,
    loose: 2,
  },
};

// tokens/spacing.ts
export const spacing = {
  0: '0',
  1: '0.25rem',  // 4px
  2: '0.5rem',   // 8px
  3: '0.75rem',  // 12px
  4: '1rem',     // 16px
  5: '1.25rem',  // 20px
  6: '1.5rem',   // 24px
  8: '2rem',     // 32px
  10: '2.5rem',  // 40px
  12: '3rem',    // 48px
  16: '4rem',    // 64px
  20: '5rem',    // 80px
  24: '6rem',    // 96px
};

// tokens/radius.ts
export const radius = {
  none: '0',
  sm: '0.125rem',   // 2px
  base: '0.25rem',  // 4px
  md: '0.375rem',   // 6px
  lg: '0.5rem',     // 8px
  xl: '0.75rem',    // 12px
  '2xl': '1rem',    // 16px
  '3xl': '1.5rem',  // 24px
  full: '9999px',
};

// tokens/shadows.ts
export const shadows = {
  sm: '0 1px 2px 0 rgb(0 0 0 / 0.05)',
  base: '0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1)',
  md: '0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1)',
  lg: '0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1)',
  xl: '0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1)',
  '2xl': '0 25px 50px -12px rgb(0 0 0 / 0.25)',
  inner: 'inset 0 2px 4px 0 rgb(0 0 0 / 0.05)',
  none: 'none',
};
```

---

### Phase 2: Component Library Structure

**Atomic Design Hierarchy:**

```
components/
├── atoms/              # Basic building blocks
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.stories.tsx
│   │   ├── Button.test.tsx
│   │   └── Button.module.css
│   ├── Input/
│   ├── Badge/
│   ├── Avatar/
│   └── Icon/
├── molecules/          # Simple combinations
│   ├── FormField/
│   ├── SearchBar/
│   ├── Card/
│   └── Dropdown/
├── organisms/          # Complex components
│   ├── Navigation/
│   ├── DataTable/
│   ├── Modal/
│   └── Form/
├── templates/          # Page layouts
│   ├── DashboardLayout/
│   ├── AuthLayout/
│   └── MarketingLayout/
└── pages/              # Complete pages
    ├── Dashboard/
    ├── Login/
    └── Landing/
```

---

### Phase 3: Component API Design

**Button Component Example:**

```tsx
// components/atoms/Button/Button.tsx
import { forwardRef } from 'react';
import { cva, type VariantProps } from 'class-variance-authority';

const buttonVariants = cva(
  // Base styles
  'inline-flex items-center justify-center rounded-md font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50',
  {
    variants: {
      variant: {
        primary: 'bg-primary-600 text-white hover:bg-primary-700',
        secondary: 'bg-secondary-600 text-white hover:bg-secondary-700',
        outline: 'border border-neutral-300 bg-transparent hover:bg-neutral-100',
        ghost: 'hover:bg-neutral-100',
        danger: 'bg-error-600 text-white hover:bg-error-700',
      },
      size: {
        sm: 'h-8 px-3 text-sm',
        md: 'h-10 px-4 text-base',
        lg: 'h-12 px-6 text-lg',
      },
      fullWidth: {
        true: 'w-full',
      },
    },
    defaultVariants: {
      variant: 'primary',
      size: 'md',
    },
  }
);

export interface ButtonProps
  extends React.ButtonHTMLAttributes<HTMLButtonElement>,
    VariantProps<typeof buttonVariants> {
  icon?: React.ReactNode;
  iconPosition?: 'left' | 'right';
  loading?: boolean;
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  (
    {
      className,
      variant,
      size,
      fullWidth,
      icon,
      iconPosition = 'left',
      loading,
      disabled,
      children,
      ...props
    },
    ref
  ) => {
    return (
      <button
        ref={ref}
        className={buttonVariants({ variant, size, fullWidth, className })}
        disabled={disabled || loading}
        {...props}
      >
        {loading && <Spinner className="mr-2" />}
        {icon && iconPosition === 'left' && (
          <span className="mr-2">{icon}</span>
        )}
        {children}
        {icon && iconPosition === 'right' && (
          <span className="ml-2">{icon}</span>
        )}
      </button>
    );
  }
);

Button.displayName = 'Button';
```

**Component Documentation:**

```tsx
// Button.stories.tsx
import type { Meta, StoryObj } from '@storybook/react';
import { Button } from './Button';
import { Plus, Download } from 'lucide-react';

const meta: Meta<typeof Button> = {
  title: 'Atoms/Button',
  component: Button,
  tags: ['autodocs'],
  argTypes: {
    variant: {
      control: 'select',
      options: ['primary', 'secondary', 'outline', 'ghost', 'danger'],
    },
    size: {
      control: 'select',
      options: ['sm', 'md', 'lg'],
    },
  },
};

export default meta;
type Story = StoryObj<typeof Button>;

export const Primary: Story = {
  args: {
    children: 'Button',
    variant: 'primary',
  },
};

export const WithIcon: Story = {
  args: {
    children: 'Add Item',
    icon: <Plus size={16} />,
    variant: 'primary',
  },
};

export const Loading: Story = {
  args: {
    children: 'Loading',
    loading: true,
  },
};

export const AllVariants: Story = {
  render: () => (
    <div className="flex gap-4">
      <Button variant="primary">Primary</Button>
      <Button variant="secondary">Secondary</Button>
      <Button variant="outline">Outline</Button>
      <Button variant="ghost">Ghost</Button>
      <Button variant="danger">Danger</Button>
    </div>
  ),
};
```

---

### Phase 4: Theme System

**Multi-Theme Support:**

```typescript
// themes/index.ts
export interface Theme {
  name: string;
  colors: typeof colors;
  typography: typeof typography;
  spacing: typeof spacing;
  radius: typeof radius;
  shadows: typeof shadows;
}

// Light Theme (Default)
export const lightTheme: Theme = {
  name: 'light',
  colors: {
    ...colors,
    background: {
      primary: '#FFFFFF',
      secondary: '#F9FAFB',
      tertiary: '#F3F4F6',
    },
    text: {
      primary: '#111827',
      secondary: '#6B7280',
      tertiary: '#9CA3AF',
    },
  },
  // ... other tokens
};

// Dark Theme
export const darkTheme: Theme = {
  name: 'dark',
  colors: {
    ...colors,
    background: {
      primary: '#0F172A',
      secondary: '#1E293B',
      tertiary: '#334155',
    },
    text: {
      primary: '#F1F5F9',
      secondary: '#CBD5E1',
      tertiary: '#94A3B8',
    },
  },
  // ... other tokens
};

// Theme Provider
import { createContext, useContext, useState, useEffect } from 'react';

const ThemeContext = createContext<{
  theme: Theme;
  setTheme: (theme: Theme) => void;
  toggleTheme: () => void;
}>({
  theme: lightTheme,
  setTheme: () => {},
  toggleTheme: () => {},
});

export function ThemeProvider({ children }: { children: React.ReactNode }) {
  const [theme, setTheme] = useState<Theme>(lightTheme);

  useEffect(() => {
    // Apply theme to DOM
    const root = document.documentElement;
    Object.entries(theme.colors).forEach(([key, value]) => {
      if (typeof value === 'object') {
        Object.entries(value).forEach(([subKey, subValue]) => {
          root.style.setProperty(`--color-${key}-${subKey}`, subValue);
        });
      } else {
        root.style.setProperty(`--color-${key}`, value);
      }
    });
  }, [theme]);

  const toggleTheme = () => {
    setTheme(theme.name === 'light' ? darkTheme : lightTheme);
  };

  return (
    <ThemeContext.Provider value={{ theme, setTheme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export const useTheme = () => useContext(ThemeContext);
```

---

### Phase 5: Documentation System

**Component Documentation Template:**

```markdown
# Button

A versatile button component with multiple variants and sizes.

## Usage

```tsx
import { Button } from '@/components/atoms/Button';

function Example() {
  return (
    <Button variant="primary" size="md">
      Click me
    </Button>
  );
}
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| variant | 'primary' \| 'secondary' \| 'outline' \| 'ghost' \| 'danger' | 'primary' | Button style variant |
| size | 'sm' \| 'md' \| 'lg' | 'md' | Button size |
| fullWidth | boolean | false | Make button full width |
| icon | ReactNode | - | Icon to display |
| iconPosition | 'left' \| 'right' | 'left' | Icon position |
| loading | boolean | false | Show loading state |
| disabled | boolean | false | Disable button |

## Examples

### Basic Usage
```tsx
<Button>Default Button</Button>
```

### With Icon
```tsx
<Button icon={<Plus />}>Add Item</Button>
```

### Loading State
```tsx
<Button loading>Loading...</Button>
```

### Variants
```tsx
<Button variant="primary">Primary</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="danger">Danger</Button>
```

## Accessibility

- Keyboard accessible (Tab, Enter, Space)
- ARIA attributes included
- Focus visible indicator
- Disabled state properly handled

## Best Practices

✅ DO:
- Use primary variant for main actions
- Use outline for secondary actions
- Provide clear, action-oriented labels
- Include loading states for async actions

❌ DON'T:
- Use multiple primary buttons in same context
- Make buttons too small (min 44x44px)
- Use vague labels like "Click here"
```

---

### Phase 6: Design System Governance

**Contribution Guidelines:**

```markdown
# Contributing to the Design System

## Adding New Components

1. **Proposal**: Create RFC (Request for Comments)
2. **Design**: Create Figma designs
3. **Review**: Get design team approval
4. **Implementation**: Build component
5. **Documentation**: Write docs and stories
6. **Testing**: Add unit and visual tests
7. **Review**: Code review
8. **Merge**: Merge to main

## Component Checklist

- [ ] Follows atomic design principles
- [ ] Uses design tokens
- [ ] Fully typed with TypeScript
- [ ] Accessible (WCAG AA)
- [ ] Responsive
- [ ] Documented with examples
- [ ] Storybook stories added
- [ ] Unit tests written
- [ ] Visual regression tests added
- [ ] Peer reviewed

## Naming Conventions

- Components: PascalCase (Button, FormField)
- Props: camelCase (variant, isDisabled)
- CSS classes: kebab-case (button-primary)
- Files: PascalCase (Button.tsx)

## Version Control

- Major: Breaking changes
- Minor: New features
- Patch: Bug fixes

## Release Process

1. Update CHANGELOG.md
2. Bump version in package.json
3. Create git tag
4. Publish to npm
5. Update documentation site
```

---

## Design System Maturity Model

### Level 1: Ad-hoc
- No design system
- Inconsistent components
- No documentation

### Level 2: Documented
- Basic component library
- Some documentation
- Inconsistent usage

### Level 3: Systematic
- Complete component library
- Full documentation
- Design tokens
- Consistent usage

### Level 4: Optimized
- Automated testing
- Version control
- Contribution guidelines
- Governance process

### Level 5: Innovative
- AI-powered tools
- Automated accessibility
- Performance monitoring
- Continuous improvement

---

## Production Checklist

- [ ] Design tokens defined
- [ ] Component library built
- [ ] Theme system implemented
- [ ] Documentation complete
- [ ] Storybook configured
- [ ] Testing setup
- [ ] Accessibility audited
- [ ] Performance optimized
- [ ] Version control
- [ ] Contribution guidelines
- [ ] Governance process
- [ ] Release process
- [ ] Migration guide
- [ ] Training materials
- [ ] Support channels

---

This workflow ensures production-grade design systems that scale across teams and products.
