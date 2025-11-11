# Max's Privacy Toolkit Design Guidelines

## Design Approach
**Reference-Based**: Phantom wallet dashboard + DEX interfaces (Uniswap, Jupiter) + privacy-first tooling aesthetics. Clean, utility-focused design prioritizing quick access to tools and clear data presentation.

## Color System
```css
Primary Palette:
- Navy Background: #1a2332
- Card Background: #1f2937 (slightly lighter navy)
- Teal/Mint Accent: #4ade80
- Accent Hover: #22c55e
- Text Primary: #f9fafb
- Text Secondary: #9ca3af
- Border Subtle: rgba(74, 222, 128, 0.1)
- Success: #4ade80
- Warning: #fbbf24
- Error: #ef4444

Gradients:
- Body: linear-gradient(180deg, #1a2332, #0f1419)
- Cards: subtle gradient overlay for depth
- Buttons: linear-gradient(90deg, #4ade80, #22c55e)
```

## Typography
- **Font Family**: Inter via Google Fonts
- **Headings**: SemiBold (600), sizes 24px-32px for dashboard title, 18px-20px for card headers
- **Body**: Regular (400), 14px-16px, #f9fafb
- **Monospace**: For addresses/keys - 'Fira Code' or 'Monaco', 13px

## Layout System
**Spacing**: Tailwind units of 2, 4, 6, 8, 12, 16
- Container: max-w-7xl, px-6
- Dashboard grid: 2x2 cards on desktop (md:grid-cols-2), stack on mobile
- Card padding: p-6
- Section spacing: py-12

## Component Library

### Header/Navigation
- Sticky header with navy background (#1a2332)
- Logo: "Max's Privacy Toolkit" with small shield icon
- Navigation: Dashboard, Tools, Settings (right-aligned)
- Wallet connection button (teal accent when connected)
- Bottom border: 1px solid rgba(74, 222, 128, 0.1)

### Dashboard Tool Cards (4 cards)
Each card displays a specific privacy tool:

**Card 1 - Wallet Mixer**
- Icon: Shuffle/mixing icon
- Title: "Wallet Mixer"
- Description: "Break on-chain links between addresses"
- CTA: "Mix Tokens" button
- Status indicator: Available/Processing

**Card 2 - Clean Address Generator**
- Icon: Sparkles/new icon
- Title: "Fresh Wallet Generator"
- Description: "Create clean wallets with no history"
- CTA: "Generate Wallet" button
- Quick stats: "X wallets created"

**Card 3 - Transaction Obscurer**
- Icon: Eye-off icon
- Title: "Transaction Privacy"
- Description: "Add noise to trading patterns"
- CTA: "Configure" button
- Toggle: Enable/Disable

**Card 4 - Holdings Splitter**
- Icon: Split/divide icon
- Title: "Holdings Splitter"
- Description: "Distribute tokens across multiple wallets"
- CTA: "Split Now" button
- Input field: Number of wallets

**Card Styling**:
- Background: #1f2937
- Border: 1px solid rgba(74, 222, 128, 0.1)
- Border-radius: 12px
- Padding: p-6
- Hover: Slight teal glow (box-shadow)
- Icon size: 40px, teal color

### Buttons
**Primary (.btn-primary)**:
- Gradient: linear-gradient(90deg, #4ade80, #22c55e)
- Text: #1a2332 (dark navy for contrast)
- Padding: px-6 py-3
- Border-radius: 8px
- Font-weight: 600
- Hover: Brightness increase, no other effects

**Secondary (.btn-secondary)**:
- Background: transparent
- Border: 1px solid #4ade80
- Text: #4ade80
- Same padding/radius

### Input Fields
- Background: rgba(31, 41, 55, 0.8)
- Border: 1px solid rgba(74, 222, 128, 0.2)
- Focus border: #4ade80
- Text: #f9fafb
- Padding: px-4 py-2.5
- Border-radius: 8px
- Placeholder: #9ca3af

### Status Indicators
- Small badges with colored backgrounds
- Active: Teal background with dark text
- Pending: Yellow/warning
- Error: Red with white text
- Positioned top-right of cards

### Data Display
- Monospace font for wallet addresses
- Truncate long addresses with ellipsis (show first 4 and last 4 chars)
- Copy-to-clipboard icon on hover
- Transaction hashes as clickable links (styled in teal)

## Images
**Hero Section**: No large hero image. Instead, use a compact header with small decorative privacy-themed icon/graphic (lock with circuit pattern) positioned next to the main title "Max's Privacy Toolkit". Keep focus on the dashboard grid.

**Tool Icons**: Use Heroicons via CDN for all tool card icons (shield, sparkles, eye-off, arrows-right-left). Size: 40px, color: #4ade80.

## Animations
Minimal utility-focused animations:
- Card hover: Subtle teal glow effect (box-shadow transition)
- Button hover: Brightness filter
- Loading states: Simple spinner for wallet operations
- Success feedback: Brief green checkmark animation

## Layout Structure
**Homepage Dashboard**:
1. Compact header (h-20) - no hero
2. Main title section (py-8): "Privacy Tools Dashboard" + subtitle
3. 4-card grid (gap-6, md:grid-cols-2)
4. Footer: Links to docs, GitHub, wallet disconnect

**Tool Detail Pages** (when card is clicked):
- Breadcrumb navigation
- Tool-specific form/interface
- Results panel
- Action history log (table format)

## Key Design Principles
- Dashboard-first: Immediate access to all 4 tools
- Data clarity: High contrast, clear typography for addresses/hashes
- Quick actions: Primary CTAs prominently displayed on each card
- Status visibility: Always show operation states
- Privacy-themed: Subtle use of shield/lock iconography
- Performance: Instant feedback for all interactions