# Landing Page Design Workflow

## When to Use This Workflow

Activate when user:
- Designs marketing landing pages
- Creates product launch pages
- Plans conversion-focused pages
- Implements hero sections
- Designs pricing pages
- Creates lead generation pages

---

## Production-Grade Landing Page Design

### Phase 1: Landing Page Architecture

**High-Converting Landing Page Structure:**

```
┌─────────────────────────────────────────────────────────┐
│ Navigation (Sticky)                                     │
│ [Logo] [Features] [Pricing] [About] [CTA Button]       │
├─────────────────────────────────────────────────────────┤
│ Hero Section (Above the Fold)                          │
│ ┌─────────────────────────────────────────────────┐   │
│ │ Headline (Value Proposition)                    │   │
│ │ Subheadline (Supporting Text)                   │   │
│ │ [Primary CTA] [Secondary CTA]                   │   │
│ │ Hero Image/Video                                │   │
│ │ Social Proof (Logos, Stats)                     │   │
│ └─────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────┤
│ Social Proof Section                                    │
│ "Trusted by 10,000+ companies"                         │
│ [Logo] [Logo] [Logo] [Logo] [Logo]                    │
├─────────────────────────────────────────────────────────┤
│ Features Section (3-Column Grid)                       │
│ ┌──────┐ ┌──────┐ ┌──────┐                           │
│ │ Icon │ │ Icon │ │ Icon │                           │
│ │ Title│ │ Title│ │ Title│                           │
│ │ Desc │ │ Desc │ │ Desc │                           │
│ └──────┘ └──────┘ └──────┘                           │
├─────────────────────────────────────────────────────────┤
│ How It Works (Steps)                                    │
│ Step 1 → Step 2 → Step 3                              │
├─────────────────────────────────────────────────────────┤
│ Testimonials (Carousel)                                │
│ [Customer Photo] [Quote] [Name, Company]              │
├─────────────────────────────────────────────────────────┤
│ Pricing Section (3 Tiers)                              │
│ [Free] [Pro - Featured] [Enterprise]                  │
├─────────────────────────────────────────────────────────┤
│ FAQ Section (Accordion)                                │
│ Common questions and answers                           │
├─────────────────────────────────────────────────────────┤
│ Final CTA Section                                      │
│ "Ready to get started?"                                │
│ [Large CTA Button]                                     │
├─────────────────────────────────────────────────────────┤
│ Footer                                                  │
│ [Links] [Social] [Legal] [Newsletter]                 │
└─────────────────────────────────────────────────────────┘
```

---

### Phase 2: Hero Section Design

**High-Converting Hero:**

```tsx
<HeroSection>
  <HeroContainer>
    <HeroContent>
      {/* Eyebrow Text (Optional) */}
      <HeroEyebrow>
        <Badge variant="success">New</Badge>
        Introducing AI-powered analytics
      </HeroEyebrow>

      {/* Main Headline */}
      <HeroHeadline>
        Build Better Products
        <GradientText>10x Faster</GradientText>
      </HeroHeadline>

      {/* Subheadline */}
      <HeroSubheadline>
        The all-in-one platform for product teams to ship faster,
        collaborate better, and build products customers love.
      </HeroSubheadline>

      {/* CTA Buttons */}
      <HeroCTAs>
        <Button variant="primary" size="lg" icon={ArrowRight}>
          Start Free Trial
        </Button>
        <Button variant="outline" size="lg" icon={Play}>
          Watch Demo
        </Button>
      </HeroCTAs>

      {/* Trust Indicators */}
      <HeroTrust>
        <TrustItem>
          <CheckCircle /> No credit card required
        </TrustItem>
        <TrustItem>
          <CheckCircle /> 14-day free trial
        </TrustItem>
        <TrustItem>
          <CheckCircle /> Cancel anytime
        </TrustItem>
      </HeroTrust>

      {/* Social Proof */}
      <HeroSocialProof>
        <SocialProofText>
          Trusted by 10,000+ product teams
        </SocialProofText>
        <CompanyLogos>
          <Logo src="/logos/company1.svg" alt="Company 1" />
          <Logo src="/logos/company2.svg" alt="Company 2" />
          <Logo src="/logos/company3.svg" alt="Company 3" />
          <Logo src="/logos/company4.svg" alt="Company 4" />
          <Logo src="/logos/company5.svg" alt="Company 5" />
        </CompanyLogos>
      </HeroSocialProof>
    </HeroContent>

    <HeroVisual>
      {/* Hero Image/Video */}
      <HeroImage
        src="/hero-dashboard.png"
        alt="Product Dashboard"
        priority
      />
      {/* Or Animated Demo */}
      <AnimatedDemo autoPlay loop muted />
    </HeroVisual>
  </HeroContainer>
</HeroSection>
```

**Hero Psychology:**

```
✅ Headline Formula:
[Benefit] + [Speed/Ease] + [Outcome]
"Build Better Products 10x Faster"

✅ Subheadline Formula:
[What it is] + [Who it's for] + [Key benefit]
"The all-in-one platform for product teams to ship faster"

✅ CTA Psychology:
Primary: Action-oriented ("Start Free Trial" not "Sign Up")
Secondary: Low commitment ("Watch Demo" not "Learn More")

✅ Trust Signals:
- No credit card required
- Free trial duration
- Cancel anytime
- Money-back guarantee
```

---

### Phase 3: Social Proof Section

**Effective Social Proof:**

```tsx
<SocialProofSection>
  <SectionContainer>
    <SocialProofHeader>
      <SocialProofTitle>
        Trusted by industry leaders
      </SocialProofTitle>
      <SocialProofStats>
        <StatItem>
          <StatNumber>10,000+</StatNumber>
          <StatLabel>Active Users</StatLabel>
        </StatItem>
        <StatItem>
          <StatNumber>4.9/5</StatNumber>
          <StatLabel>Average Rating</StatLabel>
        </StatItem>
        <StatItem>
          <StatNumber>99.9%</StatNumber>
          <StatLabel>Uptime</StatLabel>
        </StatItem>
      </SocialProofStats>
    </SocialProofHeader>

    {/* Company Logos */}
    <LogoGrid>
      {companies.map((company) => (
        <LogoItem key={company.id}>
          <CompanyLogo
            src={company.logo}
            alt={company.name}
            grayscale
            hoverColor
          />
        </LogoItem>
      ))}
    </LogoGrid>

    {/* Testimonial Highlight */}
    <FeaturedTestimonial>
      <TestimonialQuote>
        "This tool has transformed how our team works. We've
        increased productivity by 300% in just 3 months."
      </TestimonialQuote>
      <TestimonialAuthor>
        <AuthorAvatar src="/avatars/ceo.jpg" />
        <AuthorInfo>
          <AuthorName>Sarah Johnson</AuthorName>
          <AuthorTitle>CEO, TechCorp</AuthorTitle>
        </AuthorInfo>
      </TestimonialAuthor>
    </FeaturedTestimonial>
  </SectionContainer>
</SocialProofSection>
```

**Social Proof Types:**

```
1. Customer Logos: Shows credibility
2. Statistics: Quantifies success
3. Testimonials: Emotional connection
4. Case Studies: Detailed proof
5. Awards/Badges: Third-party validation
6. Media Mentions: Press coverage
7. User Count: Popularity signal
8. Ratings/Reviews: Quality indicator
```

---

### Phase 4: Features Section

**Feature Showcase:**

```tsx
<FeaturesSection>
  <SectionHeader>
    <SectionEyebrow>Features</SectionEyebrow>
    <SectionTitle>
      Everything you need to succeed
    </SectionTitle>
    <SectionDescription>
      Powerful features designed to help you work smarter, not harder
    </SectionDescription>
  </SectionHeader>

  <FeaturesGrid>
    <FeatureCard>
      <FeatureIcon>
        <Zap size={32} />
      </FeatureIcon>
      <FeatureTitle>Lightning Fast</FeatureTitle>
      <FeatureDescription>
        Built for speed with optimized performance that keeps
        your team moving quickly.
      </FeatureDescription>
      <FeatureLink href="/features/performance">
        Learn more →
      </FeatureLink>
    </FeatureCard>

    <FeatureCard featured>
      <FeaturedBadge>Most Popular</FeaturedBadge>
      <FeatureIcon>
        <Users size={32} />
      </FeatureIcon>
      <FeatureTitle>Team Collaboration</FeatureTitle>
      <FeatureDescription>
        Work together seamlessly with real-time collaboration
        and instant updates.
      </FeatureDescription>
      <FeatureLink href="/features/collaboration">
        Learn more →
      </FeatureLink>
    </FeatureCard>

    <FeatureCard>
      <FeatureIcon>
        <Shield size={32} />
      </FeatureIcon>
      <FeatureTitle>Enterprise Security</FeatureTitle>
      <FeatureDescription>
        Bank-level security with SOC 2 compliance and
        end-to-end encryption.
      </FeatureDescription>
      <FeatureLink href="/features/security">
        Learn more →
      </FeatureLink>
    </FeatureCard>
  </FeaturesGrid>
</FeaturesSection>
```

**Feature Psychology:**

```
✅ Benefit-Focused:
"Lightning Fast" not "Optimized Code"
"Team Collaboration" not "Real-time Sync"

✅ Icon Selection:
- Use recognizable icons
- Consistent style
- Meaningful representation

✅ Description Formula:
[What it does] + [How it helps]
"Real-time collaboration that keeps your team aligned"
```

---

### Phase 5: Pricing Section

**Conversion-Optimized Pricing:**

```tsx
<PricingSection>
  <SectionHeader>
    <SectionTitle>Simple, transparent pricing</SectionTitle>
    <SectionDescription>
      Choose the plan that's right for you
    </SectionDescription>
    
    {/* Billing Toggle */}
    <BillingToggle>
      <ToggleOption active={billing === 'monthly'}>
        Monthly
      </ToggleOption>
      <ToggleOption active={billing === 'annual'}>
        Annual
        <SaveBadge>Save 20%</SaveBadge>
      </ToggleOption>
    </BillingToggle>
  </SectionHeader>

  <PricingGrid>
    {/* Free Tier */}
    <PricingCard>
      <PricingHeader>
        <PricingTier>Free</PricingTier>
        <PricingPrice>
          <PriceAmount>$0</PriceAmount>
          <PricePeriod>/month</PricePeriod>
        </PricingPrice>
        <PricingDescription>
          Perfect for trying out
        </PricingDescription>
      </PricingHeader>

      <PricingFeatures>
        <Feature included>
          <CheckIcon /> Up to 3 projects
        </Feature>
        <Feature included>
          <CheckIcon /> 5 team members
        </Feature>
        <Feature included>
          <CheckIcon /> Basic support
        </Feature>
        <Feature excluded>
          <XIcon /> Advanced analytics
        </Feature>
        <Feature excluded>
          <XIcon /> Priority support
        </Feature>
      </PricingFeatures>

      <PricingCTA>
        <Button variant="outline" fullWidth>
          Get Started
        </Button>
      </PricingCTA>
    </PricingCard>

    {/* Pro Tier (Featured) */}
    <PricingCard featured>
      <PopularBadge>Most Popular</PopularBadge>
      <PricingHeader>
        <PricingTier>Pro</PricingTier>
        <PricingPrice>
          <PriceAmount>$29</PriceAmount>
          <PricePeriod>/month</PricePeriod>
        </PricingPrice>
        <PricingDescription>
          For growing teams
        </PricingDescription>
      </PricingHeader>

      <PricingFeatures>
        <Feature included>
          <CheckIcon /> Unlimited projects
        </Feature>
        <Feature included>
          <CheckIcon /> Unlimited team members
        </Feature>
        <Feature included>
          <CheckIcon /> Priority support
        </Feature>
        <Feature included>
          <CheckIcon /> Advanced analytics
        </Feature>
        <Feature included>
          <CheckIcon /> Custom integrations
        </Feature>
      </PricingFeatures>

      <PricingCTA>
        <Button variant="primary" fullWidth>
          Start Free Trial
        </Button>
        <CTASubtext>No credit card required</CTASubtext>
      </PricingCTA>
    </PricingCard>

    {/* Enterprise Tier */}
    <PricingCard>
      <PricingHeader>
        <PricingTier>Enterprise</PricingTier>
        <PricingPrice>
          <PriceAmount>Custom</PriceAmount>
        </PricingPrice>
        <PricingDescription>
          For large organizations
        </PricingDescription>
      </PricingHeader>

      <PricingFeatures>
        <Feature included>
          <CheckIcon /> Everything in Pro
        </Feature>
        <Feature included>
          <CheckIcon /> Dedicated support
        </Feature>
        <Feature included>
          <CheckIcon /> SLA guarantee
        </Feature>
        <Feature included>
          <CheckIcon /> Custom contracts
        </Feature>
        <Feature included>
          <CheckIcon /> On-premise option
        </Feature>
      </PricingFeatures>

      <PricingCTA>
        <Button variant="outline" fullWidth>
          Contact Sales
        </Button>
      </PricingCTA>
    </PricingCard>
  </PricingGrid>

  {/* Pricing FAQ */}
  <PricingFAQ>
    <FAQTitle>Frequently asked questions</FAQTitle>
    <FAQGrid>
      <FAQItem>
        <FAQQuestion>Can I change plans later?</FAQQuestion>
        <FAQAnswer>
          Yes, you can upgrade or downgrade at any time.
        </FAQAnswer>
      </FAQItem>
      <FAQItem>
        <FAQQuestion>What payment methods do you accept?</FAQQuestion>
        <FAQAnswer>
          We accept all major credit cards and PayPal.
        </FAQAnswer>
      </FAQItem>
    </FAQGrid>
  </PricingFAQ>
</PricingSection>
```

**Pricing Psychology:**

```
✅ Anchoring Effect:
Show expensive plan first to make others seem reasonable

✅ Decoy Effect:
Middle tier (Pro) looks best compared to Free and Enterprise

✅ Loss Aversion:
"Save 20%" on annual billing

✅ Social Proof:
"Most Popular" badge on recommended tier

✅ Reduce Friction:
"No credit card required" removes barrier
```

---

### Phase 6: Testimonials Section

**Credible Testimonials:**

```tsx
<TestimonialsSection>
  <SectionHeader>
    <SectionTitle>
      Loved by thousands of users
    </SectionTitle>
  </SectionHeader>

  <TestimonialCarousel>
    <TestimonialCard>
      <TestimonialRating>
        <Star filled />
        <Star filled />
        <Star filled />
        <Star filled />
        <Star filled />
      </TestimonialRating>

      <TestimonialQuote>
        "This is hands down the best tool we've used. It's
        intuitive, powerful, and has saved us countless hours.
        Our team productivity has increased by 300%."
      </TestimonialQuote>

      <TestimonialAuthor>
        <AuthorAvatar src="/avatars/sarah.jpg" />
        <AuthorInfo>
          <AuthorName>Sarah Johnson</AuthorName>
          <AuthorTitle>CEO, TechCorp</AuthorTitle>
          <AuthorCompany>
            <CompanyLogo src="/logos/techcorp.svg" />
          </AuthorCompany>
        </AuthorInfo>
      </TestimonialAuthor>

      {/* Verification Badge */}
      <VerifiedBadge>
        <CheckCircle /> Verified Customer
      </VerifiedBadge>
    </TestimonialCard>
  </TestimonialCarousel>

  {/* Video Testimonials */}
  <VideoTestimonials>
    <VideoTestimonial>
      <VideoThumbnail>
        <PlayButton />
        <VideoDuration>2:30</VideoDuration>
      </VideoThumbnail>
      <VideoAuthor>
        <AuthorName>John Smith</AuthorName>
        <AuthorTitle>CTO, StartupCo</AuthorTitle>
      </VideoAuthor>
    </VideoTestimonial>
  </VideoTestimonials>
</TestimonialsSection>
```

**Testimonial Best Practices:**

```
✅ Specific Results:
"Increased productivity by 300%" not "Great tool"

✅ Real People:
Photos, names, titles, companies

✅ Verification:
"Verified Customer" badge

✅ Variety:
Mix of text, video, and case studies

✅ Relevance:
Match testimonials to target audience
```

---

### Phase 7: FAQ Section

**Conversion-Focused FAQ:**

```tsx
<FAQSection>
  <SectionHeader>
    <SectionTitle>
      Frequently asked questions
    </SectionTitle>
    <SectionDescription>
      Everything you need to know about our product
    </SectionDescription>
  </SectionHeader>

  <FAQAccordion>
    <FAQItem>
      <FAQQuestion onClick={() => toggle(1)}>
        How does the free trial work?
        <ChevronDown />
      </FAQQuestion>
      <FAQAnswer expanded={expanded === 1}>
        You get full access to all Pro features for 14 days.
        No credit card required. Cancel anytime.
      </FAQAnswer>
    </FAQItem>

    <FAQItem>
      <FAQQuestion onClick={() => toggle(2)}>
        Can I cancel my subscription?
        <ChevronDown />
      </FAQQuestion>
      <FAQAnswer expanded={expanded === 2}>
        Yes, you can cancel anytime from your account settings.
        No questions asked, no cancellation fees.
      </FAQAnswer>
    </FAQItem>

    <FAQItem>
      <FAQQuestion onClick={() => toggle(3)}>
        What payment methods do you accept?
        <ChevronDown />
      </FAQQuestion>
      <FAQAnswer expanded={expanded === 3}>
        We accept all major credit cards (Visa, Mastercard, Amex),
        PayPal, and bank transfers for annual plans.
      </FAQAnswer>
    </FAQItem>

    <FAQItem>
      <FAQQuestion onClick={() => toggle(4)}>
        Is my data secure?
        <ChevronDown />
      </FAQQuestion>
      <FAQAnswer expanded={expanded === 4}>
        Absolutely. We use bank-level encryption, are SOC 2
        compliant, and never share your data with third parties.
      </FAQAnswer>
    </FAQItem>
  </FAQAccordion>

  <FAQFooter>
    <FAQFooterText>
      Still have questions?
    </FAQFooterText>
    <Button variant="outline" icon={MessageCircle}>
      Contact Support
    </Button>
  </FAQFooter>
</FAQSection>
```

---

### Phase 8: Final CTA Section

**High-Converting Final CTA:**

```tsx
<FinalCTASection>
  <CTAContainer>
    <CTAContent>
      <CTAEyebrow>Ready to get started?</CTAEyebrow>
      <CTAHeadline>
        Start your free trial today
      </CTAHeadline>
      <CTADescription>
        Join 10,000+ teams already using our platform to
        build better products faster.
      </CTADescription>
      <CTAButtons>
        <Button variant="primary" size="lg" icon={ArrowRight}>
          Start Free Trial
        </Button>
        <Button variant="outline" size="lg" icon={Calendar}>
          Schedule Demo
        </Button>
      </CTAButtons>
      <CTATrust>
        <TrustItem>
          <CheckCircle /> No credit card required
        </TrustItem>
        <TrustItem>
          <CheckCircle /> 14-day free trial
        </TrustItem>
        <TrustItem>
          <CheckCircle /> Cancel anytime
        </TrustItem>
      </CTATrust>
    </CTAContent>
  </CTAContainer>
</FinalCTASection>
```

---

## Conversion Optimization Psychology

### Above the Fold:
- **5-Second Rule**: Visitor should understand value in 5 seconds
- **Clear CTA**: Primary action obvious and prominent
- **Trust Signals**: Remove friction immediately

### Scarcity & Urgency:
- "Limited time offer"
- "Only 3 spots left"
- Countdown timers (use ethically)

### Social Proof Hierarchy:
1. Customer logos (credibility)
2. Statistics (quantified success)
3. Testimonials (emotional connection)
4. Case studies (detailed proof)

### CTA Optimization:
- **Color**: High contrast with background
- **Size**: Large enough to notice
- **Copy**: Action-oriented ("Start Free Trial" not "Submit")
- **Position**: Multiple CTAs throughout page

---

## Performance Optimization

```typescript
// Lazy load below-the-fold content
const TestimonialsSection = lazy(() => import('./Testimonials'));
const PricingSection = lazy(() => import('./Pricing'));

// Optimize images
<Image
  src="/hero.jpg"
  alt="Hero"
  priority // Above the fold
  quality={90}
  sizes="(max-width: 768px) 100vw, 50vw"
/>

// Preload critical resources
<link rel="preload" href="/fonts/inter.woff2" as="font" />
```

---

## Production Checklist

- [ ] Hero section above the fold
- [ ] Clear value proposition
- [ ] Strong primary CTA
- [ ] Social proof visible
- [ ] Features benefit-focused
- [ ] Pricing transparent
- [ ] Testimonials credible
- [ ] FAQ addresses objections
- [ ] Final CTA compelling
- [ ] Mobile responsive
- [ ] Fast loading (<3s)
- [ ] Accessibility compliant
- [ ] SEO optimized
- [ ] Analytics tracking
- [ ] A/B testing ready

---

This workflow ensures production-grade landing pages with maximum conversion potential.
