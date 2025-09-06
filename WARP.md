# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Commands

### Development
- `npm run dev` - Start development server with TinaCMS at localhost:4321
- `npm run start` - Alias for `npm run dev`
- `npm run build` - Build production site to ./dist/
- `npm run preview` - Preview production build locally
- `npm run sync` - Generate TypeScript types for Astro modules

### Code Quality
- `npm run format` - Format code with Prettier (includes Astro files)
- `npm run format:check` - Check code formatting without changes
- `npm run lint` - Lint code with ESLint

### Content Management
- Visit `/admin` after running `npm run dev` to access TinaCMS admin interface
- Blog posts are stored as Markdown files in `src/content/blog/`

### Docker (Alternative)
- `docker build -t astropaper .` - Build Docker image
- `docker run -p 4321:80 astropaper` - Run in container
- `docker compose up -d` - Run with docker-compose

## Architecture

### Core Framework
- **Astro 5.13+** - Static site generator with islands architecture
- **TinaCMS** - Git-based headless CMS for content editing
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling with custom theme system
- **React** - Used for interactive components (Search, Card, etc.)

### Content System
- **Astro Content Collections** - Type-safe content management in `src/content/`
- **Blog Schema** - Defined in `src/content/config.ts` with Zod validation
- **TinaCMS Integration** - Live editing via `tina/config.ts` configuration
- **Markdown Processing** - remark-toc and remark-collapse plugins for enhanced content

### Theme Architecture
- **CSS Custom Properties** - Theme colors defined as CSS variables
- **Tailwind Skin System** - Custom utility classes using `withOpacity()` function
- **Dark/Light Mode** - Controlled via `[data-theme]` attribute
- **Responsive Design** - Mobile-first approach with `sm:` breakpoint at 640px

### Key Directories
- `src/config.ts` - Site configuration, social links, and settings
- `src/components/` - Reusable Astro and React components
- `src/layouts/` - Page templates (Layout, PostDetails, Posts, etc.)
- `src/pages/` - File-based routing with dynamic post/tag pages
- `src/utils/` - Utility functions for post filtering, sorting, and tags
- `src/styles/` - Global styles and CSS custom properties
- `public/` - Static assets (images, favicon, etc.)

### Content Management Workflow
- Edit content via TinaCMS admin at `/admin` or directly edit Markdown files
- Blog posts support frontmatter: title, author, tags, dates, featured status, OG images
- Dynamic OG image generation for posts using Satori
- RSS feed and sitemap automatically generated
- Tag-based organization with archive pages

### Build System
- **Astro Config** - `astro.config.ts` with integrations for Tailwind, React, Sitemap
- **Vite Optimization** - Excludes @resvg/resvg-js from optimization
- **TypeScript** - Strict configuration in `tsconfig.json`
- **Content Layer** - Now stable in Astro 5 (no longer experimental)

### Styling System
- **Custom Theme Variables** - Colors defined in CSS custom properties
- **Tailwind Extensions** - Custom color palette using skin namespace
- **Typography Plugin** - @tailwindcss/typography for rich content styling
- **Font Configuration** - IBM Plex Mono for monospace text

### Search & Navigation
- **Fuse.js** - Fuzzy search implementation for blog posts
- **Breadcrumbs** - Navigation component for post hierarchies
- **Pagination** - Built-in pagination for post lists
- **Tag System** - Automatic tag collection and filtering

## Environment Variables

### TinaCMS (Required for Admin)
- `NEXT_PUBLIC_TINA_CLIENT_ID` - Tina client ID
- `TINA_TOKEN` - Tina authentication token  
- `TINA_INDEXER_TOKEN` - For search functionality

### Optional
- `PUBLIC_GOOGLE_SITE_VERIFICATION` - Google site verification meta tag

## Development Notes

### Astro 5 Upgrade
- Upgraded from Astro 4.16.18 to Astro 5.13.5
- Removed experimental `contentLayer` config (now stable)
- Updated React types to v19 for compatibility
- All build and development commands remain the same
- TinaCMS integration continues to work seamlessly

### Content Editing
- New posts can be created via TinaCMS admin or by adding Markdown files to `src/content/blog/`
- Post filenames are auto-generated based on topic and title
- Images should be optimized and placed in `public/` directory
- OG images must be at least 1200x630 pixels

### Customization Points
- Site configuration in `src/config.ts`
- Theme colors in Tailwind config and CSS custom properties  
- Social media links and contact information
- Logo and branding assets in `public/`
- Typography and spacing via Tailwind utilities

### Performance Considerations
- Static site generation for optimal loading speed
- Image optimization with @resvg/resvg-js
- Minimal JavaScript - only for interactive components
- Critical CSS inlined, non-critical CSS loaded asynchronously

### Deployment
- Static files output to `./dist/` directory
- Compatible with Cloudflare Pages, Netlify, Vercel
- Requires Node.js 18+ for TinaCMS integration
- Environment variables needed for TinaCMS admin functionality
