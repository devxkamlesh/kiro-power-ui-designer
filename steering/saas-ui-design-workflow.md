# SaaS UI Design Workflow

## When to Use This Workflow

Activate when user:
- Designs SaaS application interfaces
- Creates subscription product UIs
- Plans user onboarding flows
- Designs settings and account pages
- Implements billing/pricing UIs
- Creates admin dashboards

---

## Production-Grade SaaS UI Design

### Phase 1: Layout Architecture

**Standard SaaS Layout Pattern:**

```
┌─────────────────────────────────────────────────────────┐
│ Topbar (64px height)                                    │
│ [Logo] [Search] [Notifications] [Profile]              │
├──────────┬──────────────────────────────────────────────┤
│          │                                              │
│ Sidebar  │ Main Content Area                            │
│ (240px)  │ ┌────────────────────────────────────────┐  │
│          │ │ Page Header                            │  │
│ [Home]   │ │ Title + Actions                        │  │
│ [Proj]   │ └────────────────────────────────────────┘  │
│ [Team]   │                                              │
│ [Set]    │ ┌────────────────────────────────────────┐  │
│          │ │ Content Cards                          │  │
│ ───────  │ │                                        │  │
│          │ └────────────────────────────────────────┘  │
│ [Help]   │                                              │
│ [Upgrade]│                                              │
└──────────┴──────────────────────────────────────────────┘
```

**Layout Specifications:**

```typescript
// Layout measurements
const LAYOUT = {
  topbar: {
    height: '64px',
    padding: '0 24px',
    zIndex: 50,
  },
  sidebar: {
    width: '240px',
    collapsedWidth: '64px',
    padding: '16px',
    zIndex: 40,
  },
  content: {
    padding: '24px',
    maxWidth: '1440px',
    margin: '0 auto',
  },
};
```

---

### Phase 2: Navigation Design

**Sidebar Navigation Pattern:**

```tsx
// Sidebar structure
<Sidebar>
  {/* Logo */}
  <SidebarHeader>
    <Logo />
    <CollapseButton />
  </SidebarHeader>

  {/* Main Navigation */}
  <SidebarNav>
    <NavItem icon={Home} label="Dashboard" href="/dashboard" />
    <NavItem icon={FolderKanban} label="Projects" href="/projects" />
    <NavItem icon={Users} label="Team" href="/team" />
    <NavItem icon={BarChart} label="Analytics" href="/analytics" />
    
    {/* Nested Navigation */}
    <NavGroup label="Settings">
      <NavItem icon={User} label="Profile" href="/settings/profile" />
      <NavItem icon={CreditCard} label="Billing" href="/settings/billing" />
      <NavItem icon={Bell} label="Notifications" href="/settings/notifications" />
    </NavGroup>
  </SidebarNav>

  {/* Bottom Actions */}
  <SidebarFooter>
    <NavItem icon={HelpCircle} label="Help & Support" />
    <UpgradeButton />
  </SidebarFooter>
</Sidebar>
```

**Navigation States:**

```css
/* Active state */
.nav-item-active {
  background: var(--primary-50);
  color: var(--primary-600);
  font-weight: 600;
}

/* Hover state */
.nav-item:hover {
  background: var(--neutral-100);
}

/* Focus state */
.nav-item:focus {
  outline: 2px solid var(--primary-500);
  outline-offset: 2px;
}
```

---

### Phase 3: Topbar Design

**Topbar Components:**

```tsx
<Topbar>
  {/* Left Section */}
  <TopbarLeft>
    <MobileMenuButton /> {/* Mobile only */}
    <Breadcrumbs>
      <BreadcrumbItem href="/dashboard">Dashboard</BreadcrumbItem>
      <BreadcrumbItem href="/projects">Projects</BreadcrumbItem>
      <BreadcrumbItem current>Project Alpha</BreadcrumbItem>
    </Breadcrumbs>
  </TopbarLeft>

  {/* Center Section */}
  <TopbarCenter>
    <SearchBar
      placeholder="Search projects, tasks, people..."
      shortcut="⌘K"
    />
  </TopbarCenter>

  {/* Right Section */}
  <TopbarRight>
    <NotificationButton badge={3} />
    <HelpButton />
    <UserMenu>
      <UserAvatar />
      <UserDropdown>
        <DropdownItem icon={User}>Profile</DropdownItem>
        <DropdownItem icon={Settings}>Settings</DropdownItem>
        <DropdownItem icon={CreditCard}>Billing</DropdownItem>
        <DropdownDivider />
        <DropdownItem icon={LogOut}>Sign out</DropdownItem>
      </UserDropdown>
    </UserMenu>
  </TopbarRight>
</Topbar>
```

---

### Phase 4: Content Area Design

**Page Header Pattern:**

```tsx
<PageHeader>
  <PageHeaderContent>
    <PageTitle>Projects</PageTitle>
    <PageDescription>
      Manage and track all your projects in one place
    </PageDescription>
  </PageHeaderContent>
  
  <PageHeaderActions>
    <Button variant="outline" icon={Filter}>
      Filter
    </Button>
    <Button variant="outline" icon={Download}>
      Export
    </Button>
    <Button variant="primary" icon={Plus}>
      New Project
    </Button>
  </PageHeaderActions>
</PageHeader>
```

**Content Cards:**

```tsx
<ContentGrid>
  {/* Stats Cards */}
  <StatsCard
    title="Total Projects"
    value="24"
    change="+12%"
    trend="up"
    icon={FolderKanban}
  />
  <StatsCard
    title="Active Tasks"
    value="156"
    change="+8%"
    trend="up"
    icon={CheckSquare}
  />
  <StatsCard
    title="Team Members"
    value="12"
    change="+2"
    trend="up"
    icon={Users}
  />
  <StatsCard
    title="Completion Rate"
    value="87%"
    change="+5%"
    trend="up"
    icon={TrendingUp}
  />

  {/* Main Content Card */}
  <Card>
    <CardHeader>
      <CardTitle>Recent Projects</CardTitle>
      <CardActions>
        <Button variant="ghost" size="sm">View All</Button>
      </CardActions>
    </CardHeader>
    <CardContent>
      <ProjectList />
    </CardContent>
  </Card>
</ContentGrid>
```

---

### Phase 5: Data Display Patterns

**Table Design:**

```tsx
<DataTable>
  <TableHeader>
    <TableRow>
      <TableHead sortable>Project Name</TableHead>
      <TableHead sortable>Status</TableHead>
      <TableHead sortable>Team</TableHead>
      <TableHead sortable>Progress</TableHead>
      <TableHead sortable>Due Date</TableHead>
      <TableHead>Actions</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    <TableRow>
      <TableCell>
        <div className="flex items-center gap-3">
          <ProjectIcon />
          <div>
            <div className="font-medium">Project Alpha</div>
            <div className="text-sm text-neutral-500">
              Website redesign
            </div>
          </div>
        </div>
      </TableCell>
      <TableCell>
        <Badge variant="success">Active</Badge>
      </TableCell>
      <TableCell>
        <AvatarGroup max={3}>
          <Avatar src="/user1.jpg" />
          <Avatar src="/user2.jpg" />
          <Avatar src="/user3.jpg" />
        </AvatarGroup>
      </TableCell>
      <TableCell>
        <ProgressBar value={75} />
      </TableCell>
      <TableCell>
        <time>Dec 31, 2024</time>
      </TableCell>
      <TableCell>
        <DropdownMenu>
          <DropdownItem icon={Eye}>View</DropdownItem>
          <DropdownItem icon={Edit}>Edit</DropdownItem>
          <DropdownItem icon={Trash} variant="danger">
            Delete
          </DropdownItem>
        </DropdownMenu>
      </TableCell>
    </TableRow>
  </TableBody>
</DataTable>
```

**Empty States:**

```tsx
<EmptyState
  icon={FolderKanban}
  title="No projects yet"
  description="Get started by creating your first project"
  action={
    <Button variant="primary" icon={Plus}>
      Create Project
    </Button>
  }
/>
```

---

### Phase 6: Forms & Input Design

**Form Layout:**

```tsx
<Form onSubmit={handleSubmit}>
  <FormSection>
    <FormSectionTitle>Project Details</FormSectionTitle>
    
    <FormField>
      <Label htmlFor="name" required>
        Project Name
      </Label>
      <Input
        id="name"
        placeholder="Enter project name"
        error={errors.name}
      />
      {errors.name && (
        <FormError>{errors.name.message}</FormError>
      )}
    </FormField>

    <FormField>
      <Label htmlFor="description">
        Description
      </Label>
      <Textarea
        id="description"
        placeholder="Describe your project"
        rows={4}
      />
      <FormHint>
        Provide a brief overview of the project goals
      </FormHint>
    </FormField>

    <FormRow>
      <FormField>
        <Label htmlFor="status">Status</Label>
        <Select id="status">
          <SelectOption value="planning">Planning</SelectOption>
          <SelectOption value="active">Active</SelectOption>
          <SelectOption value="completed">Completed</SelectOption>
        </Select>
      </FormField>

      <FormField>
        <Label htmlFor="dueDate">Due Date</Label>
        <DatePicker id="dueDate" />
      </FormField>
    </FormRow>
  </FormSection>

  <FormSection>
    <FormSectionTitle>Team Members</FormSectionTitle>
    
    <FormField>
      <Label htmlFor="members">Assign Members</Label>
      <MultiSelect
        id="members"
        options={teamMembers}
        placeholder="Select team members"
      />
    </FormField>
  </FormSection>

  <FormActions>
    <Button variant="outline" type="button">
      Cancel
    </Button>
    <Button variant="primary" type="submit">
      Create Project
    </Button>
  </FormActions>
</Form>
```

---

### Phase 7: Settings Pages

**Settings Layout:**

```tsx
<SettingsLayout>
  {/* Settings Sidebar */}
  <SettingsSidebar>
    <SettingsNav>
      <SettingsNavItem active icon={User}>
        Profile
      </SettingsNavItem>
      <SettingsNavItem icon={Lock}>
        Security
      </SettingsNavItem>
      <SettingsNavItem icon={Bell}>
        Notifications
      </SettingsNavItem>
      <SettingsNavItem icon={CreditCard}>
        Billing
      </SettingsNavItem>
      <SettingsNavItem icon={Users}>
        Team
      </SettingsNavItem>
      <SettingsNavItem icon={Sliders}>
        Preferences
      </SettingsNavItem>
    </SettingsNav>
  </SettingsSidebar>

  {/* Settings Content */}
  <SettingsContent>
    <SettingsHeader>
      <SettingsTitle>Profile Settings</SettingsTitle>
      <SettingsDescription>
        Manage your personal information and preferences
      </SettingsDescription>
    </SettingsHeader>

    <SettingsSection>
      <SettingsSectionTitle>Personal Information</SettingsSectionTitle>
      
      <SettingsItem>
        <SettingsItemLabel>
          <Label>Profile Photo</Label>
          <SettingsItemDescription>
            Update your profile photo
          </SettingsItemDescription>
        </SettingsItemLabel>
        <SettingsItemControl>
          <AvatarUpload />
        </SettingsItemControl>
      </SettingsItem>

      <SettingsItem>
        <SettingsItemLabel>
          <Label>Full Name</Label>
        </SettingsItemLabel>
        <SettingsItemControl>
          <Input defaultValue="John Doe" />
        </SettingsItemControl>
      </SettingsItem>

      <SettingsItem>
        <SettingsItemLabel>
          <Label>Email Address</Label>
          <SettingsItemDescription>
            Your email for notifications and login
          </SettingsItemDescription>
        </SettingsItemLabel>
        <SettingsItemControl>
          <Input type="email" defaultValue="john@example.com" />
        </SettingsItemControl>
      </SettingsItem>
    </SettingsSection>

    <SettingsActions>
      <Button variant="outline">Cancel</Button>
      <Button variant="primary">Save Changes</Button>
    </SettingsActions>
  </SettingsContent>
</SettingsLayout>
```

---

### Phase 8: Billing & Pricing UI

**Pricing Table:**

```tsx
<PricingGrid>
  <PricingCard>
    <PricingCardHeader>
      <PricingTier>Free</PricingTier>
      <PricingPrice>
        <PricingAmount>$0</PricingAmount>
        <PricingPeriod>/month</PricingPeriod>
      </PricingPrice>
      <PricingDescription>
        Perfect for trying out
      </PricingDescription>
    </PricingCardHeader>
    
    <PricingFeatures>
      <PricingFeature icon={Check}>Up to 3 projects</PricingFeature>
      <PricingFeature icon={Check}>5 team members</PricingFeature>
      <PricingFeature icon={Check}>Basic support</PricingFeature>
      <PricingFeature icon={X} disabled>Advanced analytics</PricingFeature>
    </PricingFeatures>
    
    <PricingAction>
      <Button variant="outline" fullWidth>
        Current Plan
      </Button>
    </PricingAction>
  </PricingCard>

  <PricingCard featured>
    <PricingBadge>Most Popular</PricingBadge>
    <PricingCardHeader>
      <PricingTier>Pro</PricingTier>
      <PricingPrice>
        <PricingAmount>$29</PricingAmount>
        <PricingPeriod>/month</PricingPeriod>
      </PricingPrice>
      <PricingDescription>
        For growing teams
      </PricingDescription>
    </PricingCardHeader>
    
    <PricingFeatures>
      <PricingFeature icon={Check}>Unlimited projects</PricingFeature>
      <PricingFeature icon={Check}>Unlimited team members</PricingFeature>
      <PricingFeature icon={Check}>Priority support</PricingFeature>
      <PricingFeature icon={Check}>Advanced analytics</PricingFeature>
      <PricingFeature icon={Check}>Custom integrations</PricingFeature>
    </PricingFeatures>
    
    <PricingAction>
      <Button variant="primary" fullWidth>
        Upgrade to Pro
      </Button>
    </PricingAction>
  </PricingCard>

  <PricingCard>
    <PricingCardHeader>
      <PricingTier>Enterprise</PricingTier>
      <PricingPrice>
        <PricingAmount>Custom</PricingAmount>
      </PricingPrice>
      <PricingDescription>
        For large organizations
      </PricingDescription>
    </PricingCardHeader>
    
    <PricingFeatures>
      <PricingFeature icon={Check}>Everything in Pro</PricingFeature>
      <PricingFeature icon={Check}>Dedicated support</PricingFeature>
      <PricingFeature icon={Check}>SLA guarantee</PricingFeature>
      <PricingFeature icon={Check}>Custom contracts</PricingFeature>
      <PricingFeature icon={Check}>On-premise option</PricingFeature>
    </PricingFeatures>
    
    <PricingAction>
      <Button variant="outline" fullWidth>
        Contact Sales
      </Button>
    </PricingAction>
  </PricingCard>
</PricingGrid>
```

---

### Phase 9: Onboarding Flow

**Onboarding Steps:**

```tsx
<OnboardingWizard>
  <OnboardingProgress>
    <ProgressStep completed>Welcome</ProgressStep>
    <ProgressStep active>Profile Setup</ProgressStep>
    <ProgressStep>Team Invite</ProgressStep>
    <ProgressStep>First Project</ProgressStep>
  </OnboardingProgress>

  <OnboardingContent>
    <OnboardingStep>
      <OnboardingIcon>
        <User size={48} />
      </OnboardingIcon>
      
      <OnboardingTitle>
        Set up your profile
      </OnboardingTitle>
      
      <OnboardingDescription>
        Tell us a bit about yourself to personalize your experience
      </OnboardingDescription>

      <OnboardingForm>
        <FormField>
          <Label>Full Name</Label>
          <Input placeholder="Enter your name" />
        </FormField>
        
        <FormField>
          <Label>Role</Label>
          <Select>
            <SelectOption>Product Manager</SelectOption>
            <SelectOption>Developer</SelectOption>
            <SelectOption>Designer</SelectOption>
            <SelectOption>Other</SelectOption>
          </Select>
        </FormField>

        <FormField>
          <Label>Company Size</Label>
          <RadioGroup>
            <Radio value="1-10">1-10 employees</Radio>
            <Radio value="11-50">11-50 employees</Radio>
            <Radio value="51-200">51-200 employees</Radio>
            <Radio value="200+">200+ employees</Radio>
          </RadioGroup>
        </FormField>
      </OnboardingForm>
    </OnboardingStep>
  </OnboardingContent>

  <OnboardingActions>
    <Button variant="outline">
      Skip for now
    </Button>
    <Button variant="primary">
      Continue
    </Button>
  </OnboardingActions>
</OnboardingWizard>
```

---

## Color Palette (SaaS Professional)

```css
:root {
  /* Primary */
  --primary-50: #EFF6FF;
  --primary-100: #DBEAFE;
  --primary-500: #3B82F6;
  --primary-600: #2563EB;
  --primary-700: #1D4ED8;

  /* Neutral */
  --neutral-50: #F9FAFB;
  --neutral-100: #F3F4F6;
  --neutral-200: #E5E7EB;
  --neutral-500: #6B7280;
  --neutral-700: #374151;
  --neutral-900: #111827;

  /* Semantic */
  --success: #10B981;
  --error: #EF4444;
  --warning: #F59E0B;
  --info: #06B6D4;
}
```

---

## Typography Scale

```css
:root {
  /* Font Families */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'Fira Code', monospace;

  /* Font Sizes */
  --text-xs: 0.75rem;    /* 12px */
  --text-sm: 0.875rem;   /* 14px */
  --text-base: 1rem;     /* 16px */
  --text-lg: 1.125rem;   /* 18px */
  --text-xl: 1.25rem;    /* 20px */
  --text-2xl: 1.5rem;    /* 24px */
  --text-3xl: 1.875rem;  /* 30px */
  --text-4xl: 2.25rem;   /* 36px */

  /* Font Weights */
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;
}
```

---

## Spacing System

```css
:root {
  --space-1: 0.25rem;  /* 4px */
  --space-2: 0.5rem;   /* 8px */
  --space-3: 0.75rem;  /* 12px */
  --space-4: 1rem;     /* 16px */
  --space-5: 1.25rem;  /* 20px */
  --space-6: 1.5rem;   /* 24px */
  --space-8: 2rem;     /* 32px */
  --space-10: 2.5rem;  /* 40px */
  --space-12: 3rem;    /* 48px */
  --space-16: 4rem;    /* 64px */
}
```

---

## Production Checklist

Before launching SaaS UI:

- [ ] Navigation is intuitive and consistent
- [ ] All interactive elements have hover/focus states
- [ ] Empty states designed for all data views
- [ ] Loading states for async operations
- [ ] Error states with clear messaging
- [ ] Success feedback for user actions
- [ ] Responsive design tested (mobile, tablet, desktop)
- [ ] Accessibility compliance (WCAG AA)
- [ ] Keyboard navigation works throughout
- [ ] Forms have proper validation
- [ ] Settings pages are organized logically
- [ ] Onboarding flow is smooth
- [ ] Billing/pricing UI is clear
- [ ] Help/support easily accessible
- [ ] Performance optimized (fast loading)

---

This workflow ensures production-grade SaaS UI with professional design and excellent UX.
