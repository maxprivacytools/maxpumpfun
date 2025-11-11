# Max's Privacy Toolkit

## Overview

Max's Privacy Toolkit is a privacy-focused dashboard for Solana/pump.fun traders. Built with the pump.fun color scheme (dark navy blue #1a2332 with teal/mint green #4ade80 accents), it provides privacy tools to help traders avoid being copy-traded and maintain anonymity on-chain. Currently features an Anonymous Token Launch tool with plans for SOL Mixer, Stealth Swap, and Burner Wallets.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18+ with Vite for development and build tooling

**Routing**: Wouter (lightweight client-side routing)

**UI Component Library**: Radix UI primitives with custom shadcn/ui components styled using Tailwind CSS

**Design System**: 
- Pump.fun-inspired color scheme: dark navy blue (#1a2332) background with teal/mint green (#4ade80) accents
- CSS variables for theming with HSL color system
- Tailwind CSS for utility-first styling with custom configuration
- Clean, dashboard-style interface with tool cards and minimal decoration

**State Management**: 
- TanStack Query (React Query) for server state and API caching
- React hooks for local component state
- Custom wallet connection state via usePhantomWallet hook

**Key UI Patterns**:
- Card-based layouts with elevated backgrounds and subtle borders
- Gradient overlays and blur effects for depth
- Responsive design with mobile-first considerations
- Toast notifications for user feedback

### Backend Architecture

**Server**: Express.js with TypeScript

**Development Environment**: 
- Vite middleware integration for HMR during development
- Custom logging middleware for API request tracking
- Static file serving for production builds

**Data Layer**:
- In-memory storage implementation (MemStorage) for development
- Interface-based storage design (IStorage) allowing easy swap to persistent storage
- Drizzle ORM configured for PostgreSQL migrations (database not yet provisioned)

**Storage Schema**:
- **Commitments**: Stores commit-reveal hashes with reveal status tracking
- **Sealed Orders**: Batch auction orders with settlement tracking
- **Audit Events**: Immutable log of all launch events (commits, reveals, settlements, escrow releases)
- **Escrows**: Vesting schedule and release tracking for developer funds

**API Design**: RESTful endpoints under `/api` prefix (routes to be implemented)

### Blockchain Integration

**Solana Integration**:
- @solana/web3.js for blockchain interactions
- Connection to Devnet for development, Mainnet for production
- Phantom wallet adapter for user authentication and transaction signing

**Wallet Management**:
- Phantom provider detection and connection handling
- Keypair generation for launch wallets (client-side)
- Private key import/export support (base64 and JSON array formats)
- Balance checking and transaction submission

**Privacy Features**:
- SOL mixing through temporary wallet (currently uses placeholder wallet address)
- Transaction history tracking for mixing operations
- Launch wallet generation separate from user wallet for anonymity

**Token Creation Integration**:
- Direct pump.fun token creation via PumpPortal Local Transaction API
- Complete client-side transaction signing (no private keys sent to APIs)
- IPFS metadata upload for token image and details
- VersionedTransaction signing with both launch wallet and mint keypairs
- Automatic confirmation tracking on Solana network
- Success state with pump.fun and Solscan links

**Anti-Sniping Mechanisms** (UI components built, on-chain contracts are placeholders):
- Commit-reveal flow to prevent parameter front-running
- Sealed order batch auctions for fair price discovery
- Time-locked commitment windows before reveal

### Build & Deployment

**Build Process**:
- Frontend: Vite builds React app to `dist/public`
- Backend: esbuild bundles Express server to `dist/index.js`
- Single production command runs compiled Express server serving static frontend

**Development Workflow**:
- `npm run dev`: Runs Express with Vite middleware for HMR
- `npm run build`: Production build of both frontend and backend
- `npm start`: Runs production server
- `npm run db:push`: Drizzle schema push (requires DATABASE_URL)

**Type Safety**: 
- Shared types between client and server via `@shared` path alias
- TypeScript strict mode enabled
- Zod schemas for runtime validation

## External Dependencies

### Core Framework Dependencies

- **React Ecosystem**: react, react-dom, react-router (via wouter)
- **Build Tools**: Vite, esbuild, TypeScript
- **Backend**: Express.js with TypeScript support (tsx runtime)

### Blockchain & Wallet

- **@solana/web3.js**: Solana blockchain interaction library
- **Phantom Wallet**: Browser extension wallet integration (client-side detection)
- **Buffer polyfill**: Required for Solana web3.js in browser environment

### UI Component Libraries

- **Radix UI**: Headless component primitives (@radix-ui/react-*)
  - Includes: dialog, dropdown, popover, tabs, toast, accordion, checkbox, select, and 20+ other primitives
- **shadcn/ui**: Pre-built components using Radix UI + Tailwind
- **Tailwind CSS**: Utility-first CSS framework with custom KURAI theme
- **class-variance-authority**: Type-safe component variant management
- **Lucide React**: Icon library
- **react-icons**: Additional icon set (includes FaXTwitter)

### State & Data Management

- **TanStack Query**: Server state management and caching
- **React Hook Form**: Form state and validation
- **Zod**: Schema validation and type inference
- **@hookform/resolvers**: Zod integration for React Hook Form

### Database & ORM

- **Drizzle ORM**: TypeScript ORM for PostgreSQL
- **@neondatabase/serverless**: PostgreSQL driver for Neon database
- **drizzle-kit**: Migration and schema management CLI
- **Note**: Database URL must be configured via `DATABASE_URL` environment variable

### Development Tools

- **@replit/vite-plugin-***: Replit-specific development plugins
  - runtime-error-modal: Error overlay
  - cartographer: File navigation
  - dev-banner: Development mode indicator
- **PostCSS & Autoprefixer**: CSS processing

### Session & Storage

- **connect-pg-simple**: PostgreSQL session store for Express (configured but not actively used)

### Utility Libraries

- **date-fns**: Date manipulation and formatting
- **clsx & tailwind-merge**: Class name utilities
- **cmdk**: Command palette component
- **nanoid**: Unique ID generation

## Recent Changes (November 2025)

### Complete Redesign to Max's Privacy Toolkit (November 11, 2025)
- **Rebranded**: From "KURAI Launchpad" to "Max's Privacy Toolkit"
- **New Color Scheme**: Pump.fun colors - dark navy blue (#1a2332) + teal/mint green (#4ade80)
- **New Homepage**: Dashboard with 4 privacy tool cards:
  1. **SOL Mixer** (Coming Soon) - Break on-chain links to prevent copy trading
  2. **Anonymous Launch** (Active) - Launch pump.fun tokens privately
  3. **Stealth Swap** (Coming Soon) - Swap tokens with randomized timing
  4. **Burner Wallets** (Coming Soon) - Generate disposable trading wallets
- **Navigation**: Twitter link to x.com/maxprivacytools in header
- **Files Modified**:
  - `client/src/index.css`: Updated all color variables to pump.fun scheme
  - `client/src/pages/HomePage.tsx`: New dashboard with 4 tool cards
  - `client/src/pages/LaunchPage.tsx`: Renamed from CreateLaunchPage, added header
  - `client/src/App.tsx`: Simplified routing, removed old Header component
  - `client/index.html`: Updated title to "Max's Privacy Toolkit"
  - `design_guidelines.md`: New design system based on pump.fun aesthetics

### Pump.fun Token Creation Integration (Functional)
- **Status**: Fully implemented and functional in Anonymous Launch tool
- **Implementation**: PumpPortal Local Transaction API integration
- **Security**: All private keys remain client-side; transaction signing happens in browser

### Missing/Placeholder Integrations

- **On-chain Smart Contracts**: CommitmentRegistry, BatchAuction, EscrowVesting, LBPController contracts are not implemented (require Anchor/Solidity development)
- **Privacy Mixing Protocol**: Currently uses hardcoded temporary wallet instead of actual mixing protocol
- **PostgreSQL Database**: Configured but not provisioned (using in-memory storage)
- **API Routes**: Backend routes are registered but not implemented (placeholder only)