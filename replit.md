# Trend Al-Madinah - ترند المدينة

## Overview

Trend Al-Madinah is a Twitter-like social platform focused on Al-Madinah city in Saudi Arabia. The application allows users to share tweets, ask questions, discover local places (restaurants, cafes, hotels), and track trending hashtags specific to different neighborhoods in Al-Madinah. The platform is designed with RTL (right-to-left) support for Arabic content and features a modern, responsive UI built with React and shadcn/ui components.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Build Tool**
- Uses **Vite** as the build tool and development server for fast hot module replacement (HMR)
- Built with **React** (not Next.js - this is a SPA, not SSR)
- Written in **TypeScript** with strict type checking enabled
- Uses **Wouter** for client-side routing instead of React Router

**UI Component Library**
- **shadcn/ui** components built on top of Radix UI primitives
- Uses the "new-york" style variant
- **Tailwind CSS** v4 for styling with custom CSS variables for theming
- **Lucide React** for icons
- RTL support configured globally with `dir="rtl"` and Arabic font (Tajawal from Google Fonts)

**State Management**
- **TanStack Query (React Query)** for server state management and data fetching
- Context API for global state (LocationContext for neighborhood selection)
- No Redux or other state management libraries

**Key Design Patterns**
- Component composition with shadcn/ui base components
- Custom hooks for reusable logic (useIsMobile, useToast)
- Portal pattern for rendering components in specific DOM nodes (TrendList uses createPortal)
- React Hook Form with Zod validation for form handling

**Project Structure**
- `/client/src` - All frontend code
  - `/components` - Reusable UI components (feed, layout, location, map, trends, ui)
  - `/pages` - Route components (home, explore, restaurants, questions, profile)
  - `/lib` - Utilities, API clients, types, and context providers
  - `/hooks` - Custom React hooks

### Backend Architecture

**Server Framework**
- **Express.js** server for REST API
- **HTTP server** created with Node's `http` module (supports future WebSocket upgrades)
- Development uses **tsx** for TypeScript execution
- Production build uses **esbuild** to bundle server code

**API Design**
- RESTful API structure with `/api/*` routes
- Routes defined in `server/routes.ts` using Express router
- Request/response logging middleware for debugging
- JSON body parsing with raw body capture for webhook support

**Key Endpoints**
- `GET /api/tweets` - Fetch tweets (optionally filtered by locationId)
- `GET /api/tweets/:id` - Get single tweet
- `POST /api/tweets` - Create new tweet
- Similar patterns for questions, answers, places, neighborhoods, trends

**Data Validation**
- **Zod schemas** defined in `shared/schema.ts` for runtime validation
- **Drizzle-Zod** integration to generate Zod schemas from database schemas
- Request validation in route handlers

**Error Handling**
- Try-catch blocks in route handlers
- Zod validation errors return 400 with error details
- Generic 500 errors for unexpected failures
- Custom logging function for request/response tracking

### Data Storage

**Database**
- **PostgreSQL** as the primary database
- Connection managed through **node-postgres (pg)** connection pool
- Database URL provided via `DATABASE_URL` environment variable

**ORM**
- **Drizzle ORM** for type-safe database queries
- Schema definitions in `shared/schema.ts` (shared between client and server)
- Drizzle Kit for migrations (configuration in `drizzle.config.ts`)
- Migration files stored in `/migrations` directory

**Database Schema**
- **users** - User profiles with handles, avatars, bio, verification status
- **neighborhoods** - Al-Madinah neighborhoods/districts with IDs and names
- **tweets** - User posts with content, images, engagement metrics, location tags
- **questions** - Community Q&A posts with location context
- **answers** - Responses to questions
- **places** - Local businesses (restaurants, cafes, hotels) with ratings and categories
- **trends** - Trending hashtags with post counts and rankings

**Storage Interface**
- Abstracted through `IStorage` interface in `server/storage.ts`
- Methods for CRUD operations on all entities
- Supports filtering (e.g., tweets by location)
- Returns joined data (e.g., tweets with user information)
- Dynamic trends system extracts hashtags from user tweets automatically

## Recent Changes (December 2025)

### Dynamic Trending System
- Implemented internal trending system that extracts hashtags from user tweets
- Hashtags are counted and ranked by popularity
- Trends are filtered by neighborhood when a specific location is selected
- Falls back to static trends if no dynamic trends are available

### Updated Neighborhoods
- Updated to 51 official Al-Madinah neighborhoods
- Neighborhoods include: العزيزية، الملك فهد، الربوة، سيد الشهداء، قباء، العنابس، السحمان، المستراح، البحر، الجبور، النصر، العنبرية، العوالي، العيون، المناخة، الأغوات، الساحة، زقاق الطيار، الحرة الشرقية، التاجوري، باب المجيدي، باب الشامي، الحرة الغربية، الجرف، الدويمة، القبلتين، أبيار علي، الخالدية، الإسكان، المطار، البيداء، تلعة الهبوب، المبعوث، العاقول، الخضراء، وعيرة، الفيصل، الحرة الشمالية الشرقية، قربان، المنشية، السيح، الوبرة، عروة، الدخل المحدود، العصبة، شوران، الراية، الفتح، الحمراء، أبو مرخه، المصانع

### Places Enhancement
- Hotels and cafes with location "المدينة المنورة" (all) appear for all neighborhoods
- Fixed filtering to include general places when specific neighborhood is selected
- Current counts: 5 cafes, 5 hotels, 7 restaurants

### External Dependencies

**Third-Party Services**
- **Replit** - Deployment platform (evidenced by Replit-specific Vite plugins)
- **Google Fonts** - Tajawal Arabic font family
- **Unsplash** - Placeholder images for avatars and covers (in dummy data)

**Development Tools**
- **@replit/vite-plugin-runtime-error-modal** - Development error overlay
- **@replit/vite-plugin-cartographer** - Development navigation aid
- **@replit/vite-plugin-dev-banner** - Development environment banner
- Custom **metaImagesPlugin** for OpenGraph image meta tag updates

**Build & Deployment**
- Production build creates optimized bundles in `/dist`
- Client bundle in `/dist/public`
- Server bundle in `/dist/index.cjs` (CommonJS for Node execution)
- Static file serving in production from bundled client
- Server bundling with allowlist for specific dependencies (reduces cold start times)

**UI Libraries**
- Multiple **@radix-ui** components for accessible primitives
- **class-variance-authority** for component variant management
- **cmdk** for command palette functionality
- **embla-carousel-react** for carousel components
- **date-fns** for date formatting

**Form Handling**
- **react-hook-form** for form state management
- **@hookform/resolvers** for validation integration

**Utilities**
- **clsx** and **tailwind-merge** for className management
- **nanoid** for unique ID generation
- **zod-validation-error** for user-friendly validation messages