---
name: workbench-wf
description: Generate high-fidelity wireframes as HTML. Use when the user wants to design, prototype, or visualize UI/UX concepts. Triggers on requests like "wireframe", "mockup", "design a page", "sketch out", or UI design discussions.
---

# Wireframing

## Overview

This skill generates production-ready wireframes as self-contained HTML files. It follows a structured conversation flow: understand the idea → clarify requirements → generate wireframes. Output uses a consistent visual language optimized for developer handoff.

## Conversation Flow

### Phase 1: Understand

When the user describes what they want to build, gather context:

1. **What is it?** - App type, purpose, target users
2. **What pages/screens?** - List the key views needed
3. **What's the platform?** - Web, mobile app, or both
4. **Any references?** - Existing products, styles, or inspirations

Ask clarifying questions if the request is vague. Don't assume - confirm.

### Phase 2: Structure

Before generating, confirm the plan:

```
Here's what I'll wireframe:

**Product:** [Name/description]
**Platform:** [Web / Mobile / Both]

**Pages:**
1. [Page name] - [brief purpose]
2. [Page name] - [brief purpose]
3. ...

Does this look right, or should I adjust anything?
```

Wait for confirmation before proceeding.

### Phase 3: Generate

Create wireframes as HTML files. Each file should be self-contained with embedded Tailwind CSS.

**File naming:** Use kebab-case descriptive names
- `home.html`, `dashboard.html`, `user-profile.html`
- For mobile: `mobile-home.html`, `mobile-checkout.html`

**Output location:** Create a `wireframes/` directory in the user's project, or ask where they'd like files saved.

## Visual Language

All wireframes must follow these constraints exactly:

### Core Rules

| Element | Specification |
|---------|--------------|
| Borders | 1.5px solid black (use `.border-wire` class) |
| Corners | `rounded-md` for all elements (except avatars: `rounded-full`) |
| Colors | Black, white, and grays only. No brand colors. |
| Typography | System fonts only. No custom fonts. |
| Shadows | Simple offset only: `box-shadow: 3px 3px 0 black` (no blur) |
| Grid | 8px base unit, 16px for larger spacing |
| Text hierarchy | Use `font-light` / `font-medium` / `font-bold` - not gray colors |

### Required CSS

Every wireframe file must include this style block:

```html
<style>
  /* 1.5px border utilities */
  .border-wire { border: 1.5px solid black; }
  .border-b-wire { border-bottom: 1.5px solid black; }
  .border-t-wire { border-top: 1.5px solid black; }
  .border-r-wire { border-right: 1.5px solid black; }
  .border-l-wire { border-left: 1.5px solid black; }
  .divide-y-wire > * + * { border-top: 1.5px solid black; }

  /* Simple drop shadow (no blur) */
  .shadow-wire { box-shadow: 3px 3px 0 black; }
</style>
```

### Component Naming

Use shadcn/Radix naming conventions for easy developer handoff:

- `Button` (primary, secondary, link variants)
- `Input`, `Textarea`, `Select`
- `Checkbox`, `Radio`, `Switch`
- `Dialog`, `Sheet`, `Alert`
- `Card`, `Avatar`, `Badge`
- `Tabs`, `Accordion`
- `Table`, `Pagination`
- `DropdownMenu`, `Command`
- `Toast`, `Tooltip`

### Mobile Components

For mobile wireframes, also use:

- `StatusBar` (iOS/Android)
- `NavigationBar` (header)
- `BottomTabBar`
- `ActionSheet`, `BottomSheet`
- `FloatingActionButton`
- `DeviceFrame` (iPhone, Android, iPad)

## HTML Template

Use this base structure for all wireframes:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Page Name] | Wireframe</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['system-ui', '-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'sans-serif'],
          },
        },
      },
    }
  </script>
  <style>
    .border-wire { border: 1.5px solid black; }
    .border-b-wire { border-bottom: 1.5px solid black; }
    .border-t-wire { border-top: 1.5px solid black; }
    .border-r-wire { border-right: 1.5px solid black; }
    .border-l-wire { border-left: 1.5px solid black; }
    .divide-y-wire > * + * { border-top: 1.5px solid black; }
    .shadow-wire { box-shadow: 3px 3px 0 black; }
  </style>
</head>
<body class="bg-white min-h-screen font-sans">

  <!-- Wireframe content here -->

</body>
</html>
```

## Mobile Device Frames

When creating mobile app wireframes, wrap content in device frames:

### iPhone (393 × 852 at 80% scale = 314 × 682)

```html
<div class="w-[314px] h-[682px] rounded-[44px] border-[3px] border-black bg-white relative overflow-hidden">
  <!-- Status bar -->
  <div class="flex items-center justify-between px-6 pt-3 pb-1">
    <span class="text-sm font-semibold">9:41</span>
    <div class="absolute top-3 left-1/2 -translate-x-1/2 w-[100px] h-[32px] bg-black rounded-full"></div>
    <!-- Battery/signal icons -->
  </div>

  <!-- Content area -->
  <div class="flex-1 overflow-auto">
    <!-- Screen content -->
  </div>

  <!-- Home indicator -->
  <div class="absolute bottom-2 left-1/2 -translate-x-1/2 w-[134px] h-[5px] bg-black rounded-full"></div>
</div>
```

### Android (360 × 800 at 80% scale = 288 × 640)

```html
<div class="w-[288px] h-[640px] rounded-[24px] border-[3px] border-black bg-white relative overflow-hidden">
  <!-- Status bar -->
  <div class="flex items-center justify-between px-4 pt-2 pb-1">
    <span class="text-sm">6:19</span>
    <div class="flex items-center gap-1.5">
      <!-- Signal, 5G, battery -->
    </div>
  </div>

  <!-- Content area -->
  <div class="flex-1 overflow-auto">
    <!-- Screen content -->
  </div>

  <!-- Android nav buttons -->
  <div class="absolute bottom-3 left-0 right-0 flex items-center justify-center gap-12">
    <div class="w-5 h-5 border-2 border-black rounded-sm"></div>
    <div class="w-5 h-5 border-2 border-black rounded-full"></div>
    <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M15 19l-7-7 7-7"/></svg>
  </div>
</div>
```

## Component Reference

This skill includes a complete component library. Reference these files for exact component markup:

- **Desktop components:** `assets/workbench-template/pages/components.html`
- **Mobile components:** `assets/workbench-template/pages/components-mobile.html`

When building wireframes, copy component patterns directly from these references to ensure consistency.

## Workbench Template

For comprehensive project documentation (multiple pages, flows, versions), use the workbench template:

- **Template:** `assets/workbench-template/index.html`
- **Sample pages:** `assets/workbench-template/pages/`

The workbench follows Swiss/International Typographic Style and includes:
- Project overview and summary
- Feature breakdown
- User flows
- Page galleries with version history
- Theme switcher (light/sepia/dark viewing modes)

## Examples

### Simple Request

**User:** "Wireframe a login page"

**Response flow:**
1. Confirm: "I'll create a login page wireframe. Should this be for web or mobile? Any specific requirements like social login or forgot password?"
2. After confirmation, generate a single `login.html` file

### Complex Request

**User:** "Design an e-commerce checkout flow"

**Response flow:**
1. Clarify: "For the checkout flow, I'm thinking: Cart → Shipping → Payment → Confirmation. Web, mobile, or both?"
2. Confirm the page list
3. Generate multiple files: `checkout-cart.html`, `checkout-shipping.html`, etc.
4. Optionally create a workbench document to tie them together

## Key Principles

1. **Clarity over decoration** - Wireframes communicate structure, not aesthetics
2. **Consistency** - Same components should look identical across all pages
3. **Developer-ready** - Use real component names and patterns that map to implementation
4. **Self-contained** - Each HTML file works independently, no external dependencies except Tailwind CDN
5. **Iterate through conversation** - Users can request changes, additions, or variations

## Resources

### assets/workbench-template/
Complete working templates and component references:
- `index.html` - Workbench documentation template
- `pages/components.html` - Desktop component library
- `pages/components-mobile.html` - Mobile component library
- `pages/home.html` - Sample web page wireframe
- `pages/mobile-app.html` - Sample mobile app wireframe
