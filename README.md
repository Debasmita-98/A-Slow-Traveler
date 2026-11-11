# Wanderlog

A premium, editorial personal travel journal — built with Next.js 15, TypeScript, Tailwind CSS, and MDX. This is not a travel-agency template: it's a slow-travel, storytelling-first journal for someone who travels rarely but writes about it deeply.

**Live design language:** calm, minimal, magazine-inspired (Kinfolk / Cereal / Medium), cream background, serif display type, warm clay accent.

---

## Tech stack

- **Next.js 15** (App Router, TypeScript, static generation)
- **Tailwind CSS v4** (CSS-first `@theme` design tokens)
- **Framer Motion** for restrained entrance animations
- **MDX** (`next-mdx-remote`) for blog content, with frontmatter via `gray-matter`
- **next-themes** for dark mode
- **Lucide** icons
- Self-hosted fonts via `@fontsource` (Cormorant Garamond, Inter, JetBrains Mono) — no runtime dependency on Google Fonts

## Folder structure

```
app/                  Routes (App Router) — home, about, journal, destinations, gallery, contact, 404
  journal/[slug]/      Individual blog post pages
  destinations/[country]/  Country detail pages
  sitemap.ts, robots.ts, rss.xml/route.ts   SEO endpoints
components/
  ui/                  Button, Tag, Quote, SectionTitle, EmptyState, LoadingSkeleton
  layout/              Navbar, Footer, ThemeToggle, ScrollToTop, ReadingProgressBar, Breadcrumb
  home/                 Hero, AboutPreview, LatestStories, FeaturedDestination, QuoteSection, GalleryPreview, Newsletter
  journal/              StoryCard, SearchBar, Pagination, JournalExplorer, MDXContent, TableOfContents, ShareButtons
  destinations/         DestinationCard
  gallery/              MasonryGallery (with lightbox)
content/
  nepal/ india/ bangladesh/    Sample MDX posts, organized by country
lib/                   posts.ts (MDX loading), utils.ts
types/                 Shared TypeScript types
constants/             site.ts (nav, socials), gallery.ts
public/images/placeholders/   Procedurally generated placeholder artwork (swap for real photos)
```

## Getting started

```bash
npm install
npm run dev
```

Visit `http://localhost:3000`.

```bash
npm run build   # production build
npm run start   # serve the production build
npm run lint     # ESLint
```

## Adding a new journal entry

1. Create a new `.mdx` file inside `content/<country>/` (country must be one of `nepal`, `india`, `bangladesh` — or add a new one in `constants/site.ts` under `COUNTRIES`).
2. Add frontmatter:

```mdx
---
title: "Your Title"
excerpt: "One or two sentences."
date: "2026-01-01"
country: "nepal"
location: "Somewhere, Nepal"
category: "Reflection"
tags: ["mountains", "solo travel"]
coverImage: "/images/placeholders/post-nepal-1.svg"
coverAlt: "Description for accessibility"
---
```

3. Write the body in Markdown/MDX below the frontmatter — headings, blockquotes, tables, `<figure>` images, and fenced code blocks are all styled.

The Journal, Destinations, sitemap, and RSS feed all pick this post up automatically.

## Replacing placeholder images

`public/images/placeholders/*.svg` were generated procedurally to match the site's palette (see `scripts/gen-placeholders.mjs`) since no real photography was supplied. Swap any `coverImage` / gallery path for a real photo of the same aspect ratio — `next/image` handles the rest.

## Deployment

Deploy on [Vercel](https://vercel.com):

```bash
npm i -g vercel
vercel
```

Update `constants/site.ts` (`SITE.url`) to your production domain before deploying — it feeds `metadataBase`, the sitemap, and the RSS feed.

## Design tokens

| Token | Value |
|---|---|
| Background | `#F8F6F2` |
| Foreground | `#2E2E2E` |
| Secondary | `#6E6A63` |
| Accent | `#B68C63` |
| Border | `#DDD6CE` |
| Heading font | Cormorant Garamond |
| Body font | Inter |
| Mono font | JetBrains Mono |

Dark mode uses a warm near-black (`#171614`) rather than pure black, to keep the premium, non-clinical feel.

## License

MIT — do whatever you like with it.
