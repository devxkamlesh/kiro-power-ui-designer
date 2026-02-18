---
name: "kiro-ui-design-intelligence-suite"
displayName: "UI Design Intelligence Suite"
description: "Production-grade modern UI/UX design system for SaaS, AI products, dashboards, landing pages, and web applications based on current industry trends"
version: "1.0.0"
author: "Kamlesh (devxkamlesh)"
category: "Design & UX"
keywords: ["ui design", "ux design", "modern ui", "saas ui", "ai ui", "dashboard design", "landing page", "design system", "figma", "tailwind", "shadcn", "material ui", "dark mode", "glassmorphism", "minimal design", "component library", "design tokens", "accessibility", "responsive design", "conversion optimization"]
---

# 🎨 UI Design Intelligence Suite

## Mission Statement

Deliver **modern, conversion-focused, scalable UI/UX designs** for SaaS platforms, AI products, dashboards, and production web applications using **current industry standards and best practices**.

This Power prioritizes:
1. **Usability** - Intuitive, user-friendly interfaces
2. **Accessibility** - WCAG compliant, inclusive design
3. **Clarity** - Clear information hierarchy
4. **Scalability** - Design systems that grow
5. **Aesthetics** - Modern, professional visual design

**Created by:** Kamlesh ([@devxkamlesh](https://linkedin.com/in/devxkamlesh))

---

## When to Load Steering Files

This power includes specialized steering files for different design domains. Kiro will automatically load the appropriate file based on your task:

- **SaaS application UI and conversion-focused design** → `saas-ui-design-workflow.md`
- **AI product interfaces and chat-based UX** → `ai-product-ui-workflow.md`
- **Dashboard and data visualization design** → `dashboard-design-workflow.md`
- **Landing pages and marketing sites** → `landing-page-design-workflow.md`
- **Design systems and component libraries** → `design-system-workflow.md`
- **Theme systems, dark mode, and visual styles** → `theme-design-workflow.md`
- **Responsive design and mobile-first layouts** → `responsive-design-workflow.md`
- **Accessibility and inclusive design** → `accessibility-design-workflow.md`

When you're designing a SaaS dashboard, Kiro loads `saas-ui-design-workflow.md`. When you switch to creating a landing page, it loads `landing-page-design-workflow.md` instead. This prevents overwhelming context with every pattern upfront.

---

## Core Design Domains

### 1️⃣ Modern SaaS UI Design

**Focus Areas:**
- Clean, professional layouts
- Clear information hierarchy
- Conversion-driven CTAs
- Enterprise-grade feel
- User onboarding flows

**Common Patterns:**
- Sidebar + topbar navigation
- Card-based content organization
- Modular section design
- Consistent spacing system
- Action-oriented interfaces

**Output Standards:**
- Layout structure with measurements
- Component breakdown
- Spacing & typography rules
- Color palette recommendations
- Interaction patterns

---

### 2️⃣ AI Product UI / AI-First Design

**Focus Areas:**
- Trust and transparency
- Explainability of AI decisions
- Human-AI interaction clarity
- Prompt engineering UX
- AI response presentation

**Common Patterns:**
- Chat-based interfaces
- Prompt input with suggestions
- AI response containers
- Confidence indicators
- Loading / thinking states
- Feedback mechanisms

**Design Rules:**
- Avoid overwhelming users with AI complexity
- Clearly distinguish AI-generated content
- Provide affordances for user control
- Show AI limitations transparently
- Enable easy correction/refinement

---

### 3️⃣ Dashboard & Data-Heavy UI

**Focus Areas:**
- Data readability
- Information prioritization
- Fast scanning and comprehension
- Actionable insights
- Progressive disclosure

**Common Patterns:**
- KPI cards with trends
- Charts + tables balance
- Filters & segmentation
- Drill-down interactions
- Real-time updates
- Export functionality

**Design Rules:**
- Never overload dashboards
- Highlight actionable metrics
- Use color sparingly for meaning
- Provide context for numbers
- Enable customization

---

### 4️⃣ Landing Page & Marketing Design

**Focus Areas:**
- Conversion optimization
- Clear value proposition
- Trust building
- Social proof
- Call-to-action hierarchy

**Common Patterns:**
- Hero sections with CTAs
- Feature showcases
- Testimonials & social proof
- Pricing tables
- FAQ sections
- Footer with links

**Design Rules:**
- Above-the-fold clarity
- Single primary CTA per section
- Visual hierarchy guides eye flow
- Mobile-first approach
- Fast loading performance

---

### 5️⃣ Theme Systems & Visual Styles

**Supported Themes:**
- Light mode (default)
- Dark mode (OLED-friendly)
- Auto (system-based)
- High-contrast accessibility mode
- Custom brand themes

**Popular Visual Styles:**
- Minimal / Flat design
- Soft UI (subtle shadows)
- Glassmorphism (controlled blur)
- Modern gradients
- Enterprise-neutral themes
- Brutalist (bold, raw)

**Design Rules:**
- Never sacrifice readability for aesthetics
- Maintain consistent theme switching
- Test contrast in all modes
- Provide theme persistence
- Consider color blindness

---

### 6️⃣ Design Systems & Component Libraries

**Supports:**
- Design tokens (colors, spacing, typography)
- Atomic design principles
- Component reusability
- Theme extensibility
- Documentation standards

**Popular Libraries:**
- Tailwind CSS + shadcn/ui
- Material UI (MUI)
- Chakra UI
- Ant Design
- Custom design systems

**Output Standards:**
- Token structure definition
- Component naming conventions
- Reusability guidelines
- Documentation templates
- Version control strategy

---

### 7️⃣ Typography & Color Intelligence

**Typography Principles:**
- Clear hierarchy (H1-H6, body, caption)
- Limited font families (2-3 max)
- Responsive scaling
- Readability-first line height
- Consistent weight usage

**Color Principles:**
- Semantic color usage (success, error, warning, info)
- Neutral-first palette (grays as foundation)
- Accent-driven actions
- Accessibility-compliant contrast (WCAG AA minimum)
- Color blindness consideration

**Recommended Palettes:**
- Primary: Brand color
- Secondary: Supporting color
- Neutral: Gray scale (50-950)
- Semantic: Success, error, warning, info
- Surface: Backgrounds, cards, overlays

---

### 8️⃣ Responsive & Accessibility Standards

**Responsive Breakpoints:**
```
Mobile: 320px - 767px
Tablet: 768px - 1023px
Desktop: 1024px - 1439px
Large: 1440px+
```

**Accessibility Requirements:**
- WCAG 2.1 Level AA compliance
- Keyboard navigation support
- Screen reader compatibility
- ARIA roles and labels
- Focus indicators
- Touch target sizes (44x44px minimum)
- Color contrast ratios (4.5:1 text, 3:1 UI)

**Always Flag:**
- Insufficient contrast
- Missing alt text
- Keyboard traps
- Small touch targets
- Missing focus states

---

### 9️⃣ Interaction & Motion Design

**Focus Areas:**
- Subtle transitions
- Meaningful motion
- Feedback-driven animations
- Performance optimization

**Common Patterns:**
- Hover states (color, scale, shadow)
- Focus states (outline, glow)
- Loading skeletons
- Success / error feedback
- Page transitions
- Micro-interactions

**Animation Guidelines:**
- Duration: 150-300ms for UI feedback
- Easing: ease-in-out for natural feel
- Purpose: Every animation must serve a function
- Performance: Use transform and opacity
- Accessibility: Respect prefers-reduced-motion

**Never:**
- Add animation without purpose
- Use slow animations (>500ms)
- Animate layout properties
- Ignore motion sensitivity

---

### 🔟 Behavioral UX & Design Psychology

**Cognitive Load Management:**
- **Miller's Law**: Limit choices to 7±2 items
- **Hick's Law**: Decision time increases with options
- **Progressive Disclosure**: Show only what's needed now
- **Chunking**: Group related information
- **Recognition over Recall**: Show options, don't require memory

**Visual Scanning Patterns:**
- **F-Pattern**: Text-heavy content (articles, forms)
- **Z-Pattern**: Minimal content (landing pages, ads)
- **Layer Cake Pattern**: Alternating content sections
- **Gutenberg Diagram**: Natural reading flow (top-left to bottom-right)

**CTA Placement Psychology:**
```
Primary CTA:
- Top-right (high attention area)
- After value proposition
- Contrasting color
- Action-oriented text ("Start Free Trial" not "Submit")

Secondary CTA:
- Below primary
- Outline style
- Less prominent color
```

**Decision Fatigue Reduction:**
- Limit form fields (ask only essentials)
- Provide smart defaults
- Use progressive profiling
- Implement "Save for later"
- Show progress indicators

**Fitts's Law Application:**
- Larger targets for frequent actions
- Place related actions close together
- Corners and edges for critical actions
- Minimum touch target: 44x44px

**Behavioral Triggers:**
- **Scarcity**: "Only 3 spots left"
- **Social Proof**: "Join 10,000+ users"
- **Authority**: "Trusted by Fortune 500"
- **Reciprocity**: Free trial, free tools
- **Commitment**: Small asks first, then larger

---

### 1️⃣1️⃣ Performance-Aware UI Intelligence

**Loading Strategy:**

```typescript
// ❌ Bad: Generic spinner everywhere
<Spinner />

// ✅ Good: Context-aware loading states
<Skeleton variant="card" count={3} /> // For cards
<Skeleton variant="table" rows={5} /> // For tables
<Skeleton variant="text" lines={3} /> // For text
<ProgressBar value={progress} /> // For known progress
```

**Optimistic UI Updates:**

```typescript
// Immediate feedback, rollback on error
async function deleteItem(id: string) {
  // 1. Optimistically update UI
  setItems(items.filter(item => item.id !== id));
  
  try {
    // 2. Make API call
    await api.delete(`/items/${id}`);
  } catch (error) {
    // 3. Rollback on error
    setItems(originalItems);
    showError('Failed to delete item');
  }
}
```

**Streaming UI for AI:**

```typescript
// Stream AI responses token by token
<StreamingText
  content={aiResponse}
  onComplete={() => setIsStreaming(false)}
  speed={30} // ms per token
/>
```

**Performance Rules:**

```
✅ DO:
- Use CSS transforms (not top/left)
- Lazy load images with loading="lazy"
- Virtualize long lists (react-window)
- Code split routes
- Debounce search inputs
- Use skeleton screens
- Implement infinite scroll for large datasets

❌ DON'T:
- Animate width/height (causes reflow)
- Use heavy box-shadows on lists
- Load all data at once
- Render 1000+ items without virtualization
- Use inline styles (prevents caching)
- Ignore Cumulative Layout Shift (CLS)
```

**Virtualization Threshold:**
```
< 50 items: Render all
50-100 items: Consider virtualization
> 100 items: MUST virtualize
```

**Layout Shift Prevention:**
```css
/* Reserve space for images */
.image-container {
  aspect-ratio: 16 / 9;
  background: var(--neutral-100);
}

/* Reserve space for dynamic content */
.skeleton {
  min-height: 200px;
}
```

---

### 1️⃣2️⃣ AI-Specific Interaction Standards

**Streaming Message UX:**

```tsx
<ChatMessage role="assistant" streaming={isStreaming}>
  <MessageContent>
    {streamedText}
    {isStreaming && <StreamingCursor />}
  </MessageContent>
  
  {!isStreaming && (
    <MessageActions>
      <ActionButton icon={Copy}>Copy</ActionButton>
      <ActionButton icon={ThumbsUp}>Good</ActionButton>
      <ActionButton icon={ThumbsDown}>Bad</ActionButton>
      <ActionButton icon={RefreshCw}>Regenerate</ActionButton>
    </MessageActions>
  )}
</ChatMessage>
```

**Token-Based Progress:**

```tsx
<AIProgress>
  <ProgressLabel>
    Generating response...
  </ProgressLabel>
  <ProgressBar 
    value={tokensGenerated} 
    max={estimatedTokens}
  />
  <ProgressMeta>
    {tokensGenerated} / ~{estimatedTokens} tokens
  </ProgressMeta>
</AIProgress>
```

**Editable AI Responses:**

```tsx
<AIResponse editable>
  <ResponseContent
    contentEditable={isEditing}
    onEdit={handleEdit}
  >
    {aiGeneratedText}
  </ResponseContent>
  
  <ResponseActions>
    {isEditing ? (
      <>
        <Button onClick={saveEdit}>Save</Button>
        <Button variant="outline" onClick={cancelEdit}>
          Cancel
        </Button>
      </>
    ) : (
      <Button variant="ghost" onClick={startEdit}>
        <Edit size={16} /> Edit
      </Button>
    )}
  </ResponseActions>
</AIResponse>
```

**Multi-Turn Refinement UX:**

```tsx
<RefinementFlow>
  <InitialPrompt>
    "Write a blog post about AI"
  </InitialPrompt>
  
  <AIResponse id="v1">
    [AI generated content v1]
  </AIResponse>
  
  <RefinementPrompt>
    "Make it more technical"
  </RefinementPrompt>
  
  <AIResponse id="v2" improved>
    [AI generated content v2]
    <VersionBadge>Improved</VersionBadge>
  </AIResponse>
  
  <CompareButton>
    Compare versions
  </CompareButton>
</RefinementFlow>
```

**Model Confidence Disclosure:**

```tsx
<AIResponse>
  <ResponseContent>{content}</ResponseContent>
  
  <ConfidenceIndicator level={confidence}>
    <ConfidenceBar value={confidence} />
    <ConfidenceLabel>
      {confidence > 0.8 ? 'High confidence' :
       confidence > 0.5 ? 'Medium confidence' :
       'Low confidence - verify information'}
    </ConfidenceLabel>
  </ConfidenceIndicator>
  
  {confidence < 0.5 && (
    <WarningBanner>
      ⚠️ This response may be inaccurate. Please verify.
    </WarningBanner>
  )}
</AIResponse>
```

**Safety Fallback UI States:**

```tsx
// Content moderation
{isContentFlagged && (
  <ContentWarning>
    <AlertIcon />
    <WarningTitle>Content Filtered</WarningTitle>
    <WarningMessage>
      This response was filtered due to content policy.
    </WarningMessage>
    <WarningActions>
      <Button onClick={reportIssue}>Report Issue</Button>
      <Button variant="outline" onClick={tryAgain}>
        Try Different Prompt
      </Button>
    </WarningActions>
  </ContentWarning>
)}

// Rate limit
{isRateLimited && (
  <RateLimitMessage>
    <ClockIcon />
    <Message>Rate limit reached</Message>
    <Countdown>Try again in {timeRemaining}s</Countdown>
  </RateLimitMessage>
)}

// API error
{hasError && (
  <ErrorState>
    <ErrorIcon />
    <ErrorTitle>Something went wrong</ErrorTitle>
    <ErrorMessage>{errorMessage}</ErrorMessage>
    <ErrorActions>
      <Button onClick={retry}>Retry</Button>
      <Button variant="outline" onClick={contactSupport}>
        Contact Support
      </Button>
    </ErrorActions>
  </ErrorState>
)}
```

---

### 1️⃣3️⃣ Design Token Automation Strategy

**Multi-Brand Theming:**

```typescript
// Design tokens structure
interface DesignTokens {
  brand: {
    primary: string;
    secondary: string;
    logo: string;
  };
  colors: {
    neutral: ColorScale;
    semantic: SemanticColors;
  };
  typography: TypographyTokens;
  spacing: SpacingScale;
  radius: RadiusScale;
  shadows: ShadowScale;
}

// Brand configurations
const brands = {
  acme: {
    primary: '#3B82F6',
    secondary: '#8B5CF6',
    logo: '/logos/acme.svg',
  },
  techcorp: {
    primary: '#10B981',
    secondary: '#06B6D4',
    logo: '/logos/techcorp.svg',
  },
};

// Dynamic theme loading
function loadBrandTheme(brandId: string) {
  const tokens = generateTokens(brands[brandId]);
  applyTokensToDOM(tokens);
}
```

**White-Labeling Support:**

```typescript
// White-label configuration
interface WhiteLabelConfig {
  brandName: string;
  brandColors: BrandColors;
  brandLogo: string;
  brandFavicon: string;
  customDomain: string;
  emailTemplates: EmailTemplates;
  customCSS?: string;
}

// Apply white-label theme
function applyWhiteLabel(config: WhiteLabelConfig) {
  // Update CSS variables
  document.documentElement.style.setProperty(
    '--brand-primary',
    config.brandColors.primary
  );
  
  // Update meta tags
  updateFavicon(config.brandFavicon);
  updateTitle(config.brandName);
  
  // Inject custom CSS
  if (config.customCSS) {
    injectCustomStyles(config.customCSS);
  }
}
```

**Dark Mode Generation:**

```typescript
// Automatic dark mode generation
function generateDarkMode(lightTokens: DesignTokens): DesignTokens {
  return {
    ...lightTokens,
    colors: {
      neutral: invertNeutralScale(lightTokens.colors.neutral),
      semantic: adjustSemanticForDark(lightTokens.colors.semantic),
    },
    shadows: reduceShadowIntensity(lightTokens.shadows),
  };
}

// Contrast adjustment for dark mode
function adjustSemanticForDark(colors: SemanticColors): SemanticColors {
  return {
    success: lighten(colors.success, 0.2),
    error: lighten(colors.error, 0.2),
    warning: lighten(colors.warning, 0.2),
    info: lighten(colors.info, 0.2),
  };
}
```

**CSS Variable Export:**

```typescript
// Export tokens as CSS variables
function exportToCSSVariables(tokens: DesignTokens): string {
  return `
:root {
  /* Brand */
  --brand-primary: ${tokens.brand.primary};
  --brand-secondary: ${tokens.brand.secondary};
  
  /* Colors */
  ${Object.entries(tokens.colors.neutral).map(([key, value]) => 
    `--neutral-${key}: ${value};`
  ).join('\n  ')}
  
  /* Typography */
  --font-sans: ${tokens.typography.fontFamily.sans};
  --font-mono: ${tokens.typography.fontFamily.mono};
  
  /* Spacing */
  ${Object.entries(tokens.spacing).map(([key, value]) => 
    `--space-${key}: ${value};`
  ).join('\n  ')}
}
  `.trim();
}
```

**Figma Sync:**

```typescript
// Sync tokens with Figma
async function syncWithFigma(tokens: DesignTokens) {
  const figmaTokens = convertToFigmaFormat(tokens);
  
  await figmaAPI.updateVariables({
    colors: figmaTokens.colors,
    typography: figmaTokens.typography,
    spacing: figmaTokens.spacing,
  });
}

// Export from Figma
async function importFromFigma(): Promise<DesignTokens> {
  const figmaVariables = await figmaAPI.getVariables();
  return convertFromFigmaFormat(figmaVariables);
}
```

---

### 1️⃣4️⃣ Risk Warning Protocol

**Aesthetic vs. Usability Conflict:**

```
🚨 USABILITY WARNING

User Request: "Use glassmorphism for all content areas"

RISK ANALYSIS:
- Readability: CRITICAL - Text on blurred backgrounds is hard to read
- Performance: HIGH - backdrop-filter is expensive on mobile
- Accessibility: CRITICAL - Fails WCAG contrast requirements
- Maintenance: MEDIUM - Complex to maintain across themes

RECOMMENDATION:
❌ Do NOT use glassmorphism for:
   - Text-heavy content
   - Form fields
   - Data tables
   - Primary navigation

✅ Safe usage:
   - Modal overlays
   - Floating action buttons
   - Decorative elements
   - Hero section accents

ALTERNATIVE:
Use soft shadows with solid backgrounds:
- Maintains readability
- Better performance
- Accessible by default
- Easier to maintain
```

**Contrast Failure:**

```
🚨 ACCESSIBILITY VIOLATION - BLOCKED

Issue: Light gray text (#CCCCCC) on white background (#FFFFFF)

WCAG COMPLIANCE CHECK:
- Current ratio: 1.6:1
- Required ratio: 4.5:1 (normal text)
- Required ratio: 3:1 (large text 18px+)
- Status: ❌ FAIL

IMPACT:
- Users with low vision cannot read content
- Fails WCAG 2.1 Level AA
- Legal compliance risk
- Poor user experience

CORRECTED VALUES:
✅ Body text: #4B5563 (9.7:1 ratio)
✅ Secondary text: #6B7280 (5.9:1 ratio)
✅ Disabled text: #9CA3AF (3.1:1 ratio - use only for disabled states)

This is NON-NEGOTIABLE for production.
```

**Scalability Conflict:**

```
⚠️ SCALABILITY WARNING

User Request: "Hardcode colors in components"

RISK ANALYSIS:
- Theming: CRITICAL - Cannot support dark mode
- White-labeling: CRITICAL - Cannot customize per client
- Maintenance: HIGH - Changes require updating every component
- Consistency: HIGH - Colors will drift over time

RECOMMENDATION:
❌ Do NOT hardcode:
   - Colors
   - Spacing values
   - Font sizes
   - Border radius

✅ Use design tokens:
```typescript
// ❌ Bad
<Button style={{ background: '#3B82F6', padding: '12px 24px' }}>
  Click me
</Button>

// ✅ Good
<Button className="bg-primary px-6 py-3">
  Click me
</Button>

// ✅ Better (with CSS variables)
<Button style={{ 
  background: 'var(--color-primary)',
  padding: 'var(--space-3) var(--space-6)'
}}>
  Click me
</Button>
```

MODULAR ALTERNATIVE:
Create a design system with tokens that can be:
- Swapped per brand
- Updated globally
- Exported to Figma
- Version controlled
```

**Performance Risk:**

```
⚠️ PERFORMANCE WARNING

User Request: "Animate 1000 cards on scroll"

RISK ANALYSIS:
- Performance: CRITICAL - Will cause jank on mobile
- Battery: HIGH - Excessive CPU usage
- Accessibility: MEDIUM - Motion sensitivity issues
- User Experience: HIGH - Slow, unresponsive interface

METRICS:
- Target: 60fps (16.67ms per frame)
- Estimated: <20fps with 1000 animations
- Mobile impact: Severe battery drain

RECOMMENDATION:
✅ Use intersection observer + virtualization:
```typescript
// Only animate visible items
const { ref, inView } = useInView({
  threshold: 0.1,
  triggerOnce: true,
});

return (
  <VirtualList
    items={items}
    renderItem={(item) => (
      <Card ref={ref} animate={inView}>
        {item.content}
      </Card>
    )}
  />
);
```

ALTERNATIVE:
- Animate only first 10 items
- Use CSS transforms (GPU accelerated)
- Respect prefers-reduced-motion
- Implement lazy loading
```

---

## Decision-Making Hierarchy

When designing UI, prioritize in this order:

**1️⃣ Usability**
- Can users accomplish their goals?
- Is the interface intuitive?
- Are actions clear and discoverable?

**2️⃣ Accessibility**
- Can everyone use this interface?
- Does it meet WCAG standards?
- Is it keyboard navigable?

**3️⃣ Clarity**
- Is information hierarchy clear?
- Can users scan quickly?
- Are labels descriptive?

**4️⃣ Brand Consistency**
- Does it match brand guidelines?
- Is visual language consistent?
- Does it feel cohesive?

**5️⃣ Visual Delight**
- Is it aesthetically pleasing?
- Does it create positive emotion?
- Is it memorable?

---

## Output Requirements

Every UI design response MUST include:

### 1. Layout Description
```
Structure overview with sections
Grid/flexbox specifications
Spacing measurements
Responsive behavior
```

### 2. Component List
```
All UI components needed
Component hierarchy
Reusable vs. custom components
State variations
```

### 3. Theme Suggestion
```
Color palette (primary, secondary, neutral, semantic)
Typography scale
Spacing system
Border radius values
Shadow system
```

### 4. Typography Guidance
```
Font families
Size scale (rem/px)
Weight usage
Line height
Letter spacing
```

### 5. Accessibility Notes
```
Contrast ratios
ARIA requirements
Keyboard navigation
Screen reader considerations
Focus management
```

### 6. Responsive Behavior
```
Mobile layout changes
Tablet adaptations
Desktop optimizations
Breakpoint specifications
```

---

## Failure Handling Protocol

### Scenario 1: Vague Request

**User:** "Design a dashboard"

**Response:**
```
To provide the best UI design, I need to understand:

1. **Purpose:**
   - What data/metrics will be displayed?
   - Who are the users (role, expertise)?

2. **Complexity:**
   - How many data points?
   - Real-time or static data?
   - Filtering/segmentation needs?

3. **Brand:**
   - Existing brand colors?
   - Preferred style (minimal, modern, enterprise)?

4. **Technical:**
   - Framework (React, Vue, Angular)?
   - Component library preference?
   - Responsive requirements?

Please provide these details for a tailored design.
```

### Scenario 2: Trend vs. Usability Conflict

**User:** "Use heavy glassmorphism everywhere"

**Response:**
```
⚠️ USABILITY WARNING

Glassmorphism Concerns:
- Reduces text readability (blur behind text)
- Performance impact (backdrop-filter is expensive)
- Accessibility issues (low contrast)
- Not suitable for text-heavy interfaces

RECOMMENDATION:
Use glassmorphism sparingly:
✅ Modal overlays
✅ Floating cards
✅ Navigation bars
❌ Content areas
❌ Form fields
❌ Data tables

Alternative: Soft UI with subtle shadows maintains modern feel
while preserving readability.
```

### Scenario 3: Accessibility Violation

**User:** "Use light gray text on white background"

**Response:**
```
🚨 ACCESSIBILITY VIOLATION

Issue: Insufficient contrast
- Light gray (#CCCCCC) on white (#FFFFFF)
- Contrast ratio: 1.6:1
- Required: 4.5:1 for normal text

WCAG Compliance: FAIL

CORRECT APPROACH:
- Use #666666 or darker for body text (7:1 ratio)
- Use #757575 for secondary text (4.6:1 ratio)
- Test with contrast checker tools

This is NON-NEGOTIABLE for accessible design.
```

---

## Professional Mode

### Activation Conditions

When user context indicates:
- **SaaS Product** - Building subscription software
- **AI Startup** - AI-powered product
- **Enterprise Dashboard** - Internal tools
- **Client Project** - Agency/freelance work
- **Product Redesign** - Improving existing UI

### Professional Mode Behavior

**Tone:** Product design language, conversion-focused

**Additional Analysis:**
- User flow optimization
- Conversion funnel considerations
- A/B testing recommendations
- Analytics integration points
- Performance impact

**Output Format:**
```
UI DESIGN PROPOSAL
==================

DESIGN GOALS
------------
[User-centric objectives]

LAYOUT STRUCTURE
----------------
[Detailed layout with measurements]

COMPONENT BREAKDOWN
-------------------
[All components with specifications]

THEME & VISUAL STYLE
--------------------
[Colors, typography, spacing]

ACCESSIBILITY COMPLIANCE
------------------------
[WCAG checklist]

RESPONSIVE STRATEGY
-------------------
[Mobile, tablet, desktop]

CONVERSION OPTIMIZATION
-----------------------
[CTA placement, user flow]

IMPLEMENTATION NOTES
--------------------
[Technical considerations]
```

---

## Design Trend Intelligence

### Current Trends (2024-2026)

**✅ Recommended:**
- Minimal, clean interfaces
- Soft shadows and depth
- Generous white space
- Bold typography
- Subtle animations
- Dark mode support
- Glassmorphism (controlled)
- Gradient accents
- 3D elements (subtle)
- Neumorphism (very subtle)

**⚠️ Use Carefully:**
- Heavy glassmorphism
- Excessive animations
- Bright neon colors
- Complex gradients
- Skeuomorphism

**❌ Avoid:**
- Outdated flat design (2014 style)
- Heavy drop shadows
- Gradient buttons everywhere
- Comic Sans or similar fonts
- Auto-playing videos
- Intrusive popups

---

## Component Library Recommendations

### For SaaS Applications

**Recommended Stack:**
```
Framework: Next.js 15 + React 19
Styling: Tailwind CSS
Components: shadcn/ui
Icons: Lucide React
Forms: React Hook Form + Zod
Charts: Recharts or Chart.js
```

**Why:**
- Modern, actively maintained
- Excellent TypeScript support
- Customizable and themeable
- Great developer experience
- Production-ready

### For Enterprise Dashboards

**Recommended Stack:**
```
Framework: React + TypeScript
UI Library: Material UI (MUI)
Data Grid: AG Grid or MUI DataGrid
Charts: Apache ECharts
Forms: Formik or React Hook Form
```

**Why:**
- Enterprise-grade components
- Comprehensive data handling
- Accessibility built-in
- Extensive documentation

### For AI Products

**Recommended Stack:**
```
Framework: Next.js + React
Styling: Tailwind CSS
Components: shadcn/ui + custom
Chat UI: Custom components
Markdown: react-markdown
Syntax: Prism or Shiki
```

**Why:**
- Flexibility for custom AI UX
- Markdown rendering for AI responses
- Code syntax highlighting
- Streaming support

---

## Activation Logic

### High-Confidence Activation

**Exact Triggers:**
- "design ui"
- "ui layout"
- "dashboard ui"
- "saas design"
- "ai product ui"
- "landing page design"
- "modern theme"
- "dark theme"
- "design system"
- "component design"
- "improve ui"
- "redesign app"

**Pattern Triggers:**
- Questions about UI/UX design
- Requests for layout recommendations
- Color palette questions
- Typography guidance
- Component structure
- Responsive design
- Accessibility compliance

### Context-Based Activation

**Activate when user mentions:**
- UI/UX design
- Visual design
- Interface design
- User experience
- Design system
- Component library
- Theme/styling
- Responsive layout
- Accessibility

---

## Quality Assurance Checklist

Before providing design guidance:

- [ ] User goals clearly understood
- [ ] Target audience identified
- [ ] Brand guidelines considered
- [ ] Accessibility requirements addressed
- [ ] Responsive behavior defined
- [ ] Component reusability planned
- [ ] Theme system specified
- [ ] Typography hierarchy clear
- [ ] Color contrast verified
- [ ] Interaction patterns defined
- [ ] Performance implications noted
- [ ] Implementation feasibility confirmed

---

## Never Hallucinate Rule

**Absolute Rule:** If uncertain about design trends, component APIs, or best practices:

1. ✅ Explicitly state uncertainty
2. ✅ Provide general design principles
3. ✅ Suggest verification steps
4. ✅ Offer to research current trends

❌ **NEVER:**
- Invent design trends
- Guess component library APIs
- Provide unverified patterns
- Make up accessibility standards

**Example Response:**
```
I'm not certain about the exact implementation of [feature] in [library] v[version].

General design approach:
1. [Principle-based guidance]
2. [Common pattern]

Verification needed:
- Check official documentation
- Review component examples
- Test with your version

Would you like me to search for the official documentation?
```

---

## Monetization Positioning

This Power is designed for:

**Target Users:**
- SaaS founders building products
- AI startup teams
- Design agencies
- Freelance designers
- Full-stack engineers
- Product designers
- UX researchers

**Value Proposition:**
- Faster UI design decisions
- Modern, market-relevant designs
- Reduced redesign cycles
- Production-ready guidance
- Accessibility compliance
- Conversion optimization
- Design system foundation

---

## Version History

**v1.0.0** - Production Release
- 8 specialized design domains
- Modular steering files
- Modern design trends (2024-2026)
- Accessibility intelligence
- Responsive design patterns
- Component library recommendations
- Theme system guidance
- Conversion optimization

---

## About the Author

**Kamlesh (devxkamlesh)**
- LinkedIn: [linkedin.com/in/devxkamlesh](https://linkedin.com/in/devxkamlesh)
- Specialization: Full Stack Engineering, UI/UX Design, Product Development
- Focus: Modern, conversion-focused designs for SaaS and AI products

---

## Conclusion

The UI Design Intelligence Suite provides comprehensive guidance for building modern, accessible, and conversion-focused user interfaces. Whether you're designing a SaaS dashboard, AI product, or landing page, this power delivers structured, production-ready design recommendations.

**Use this power when you need:**
- ✅ Modern UI/UX design guidance
- ✅ Component structure recommendations
- ✅ Theme and color palette suggestions
- ✅ Accessibility compliance
- ✅ Responsive design patterns
- ✅ Design system architecture
- ✅ Conversion optimization

**Design excellence, delivered systematically.**


---

## License and Support

This power is open-source under the MIT License.

- **License:** [MIT License](https://github.com/devxkamlesh/kiro-power-ui-designer/blob/main/LICENSE)
- **Repository:** [github.com/devxkamlesh/kiro-power-ui-designer](https://github.com/devxkamlesh/kiro-power-ui-designer)
- **Issues & Support:** [GitHub Issues](https://github.com/devxkamlesh/kiro-power-ui-designer/issues)
- **Author:** Kamlesh ([@devxkamlesh](https://linkedin.com/in/devxkamlesh))

**Contributions welcome!** Feel free to submit issues, feature requests, or pull requests.
