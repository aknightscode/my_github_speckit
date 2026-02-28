# Project Brainstorm: Debatable

**Date**: February 21, 2026
**Status**: Complete

## Project Vision

Debatable is a social debate platform where users participate in structured, turn-based video debates and are rated on the quality of their discourse — not the popularity of their opinions. It bridges the gap between superficial social media exchanges and the need for meaningful, respectful dialogue.

### Problem Statement

In today's fast-paced digital world, individuals often feel their voices are drowned out, their perspectives overlooked, and opportunities for meaningful, respectful dialogue are limited. There's widespread discontentment with the superficiality of social media exchanges and the lack of platforms dedicated to structured, constructive conversation. Moreover, those interested in developing their argumentation and public speaking skills often find few accessible and engaging avenues to do so. This gap between the need for quality discourse and the available platforms poses a significant pain point for our target audience.

### Target Users

- **Influencers & Podcasters** — Spark intellectual discussions and expand reach
- **College Students** — Sharpen debate skills and engage in meaningful discussions
- **Social Justice Advocates** — Promote awareness and debate on societal issues
- **Debate Enthusiasts** — Partake in and learn from structured discussions
- **Politicians & Political Activists** — Foster transparent, informed discourse
- **Debate Coaches & Educators** — Provide students a platform to practice
- **Lawyers** — Debate law propositions and improve argumentation skills
- **Working Professionals** — Enhance persuasion and communication skills
- **Public Speakers** — Polish speaking and argumentation skills
- **Thought Leaders & Experts** — Share knowledge through debate
- **Curious Learners** — Explore different perspectives through debate
- **Sports Enthusiasts & Sportscasters** — Engage in rigorous sports debates

### MVP Definition (Prototype)

An investor demo that proves the core debate loop: browse topics → watch video debates → join by recording a response → rate debaters on multiple quality dimensions. Must look polished and be architecturally ready for growth to beta/launch without rewrites.

### Out of Scope (Prototype)

- Live streaming debates
- AI debate coach
- Badges & gamification system
- Premium membership tiers & payments
- In-app store (emojis, backgrounds, vote types)
- Admin panel UI (use Supabase dashboard + seed scripts)
- Working notifications system (icon present, non-functional)
- Working social graph / follow system (buttons present, non-functional)
- Sharing to social media (icon present, non-functional)
- Time-stamped emoji reactions on video playback
- Competitive/judged debate format
- Calendar integration
- Leaderboard
- Resources section
- Content moderation tools
- Education segment (restricted access)
- Facebook & LinkedIn OAuth
- Matchmaking based on ratings

## Tech Stack

| Layer           | Choice                         | Rationale                                                              |
| --------------- | ------------------------------ | ---------------------------------------------------------------------- |
| Frontend        | Next.js + Tailwind CSS         | SSR for SEO, React ecosystem, future React Native path                 |
| Backend API     | Next.js Route Handlers         | Business logic layer, shared API for future React Native app           |
| Database        | Supabase (Postgres)            | Relational data, migrations, RLS for direct client reads               |
| Auth            | Google OAuth via Supabase Auth | Simplest, highest adoption                                             |
| Storage         | Supabase Storage               | Video uploads, profile images                                          |
| Video Recording | In-browser (MediaRecorder API) | With timer; upload-from-file as fallback. Mux/Cloudflare Stream later. |
| Hosting         | Vercel                         | One-click Next.js deploy, preview deployments                          |
| CI/CD           | GitHub + Vercel auto-deploy    | Push to main = production, branches = previews                         |
| Repo            | Monorepo                       | Single Next.js app + Supabase                                          |

### Architecture Flow

```
Browser → Next.js API Routes (business logic) → Supabase (data/storage)
```

- Business logic (debate rules, rating calculations, video processing) goes through API routes
- Simple reads (debate listings, profiles) can query Supabase directly with RLS
- API routes become the shared backend for future React Native app

## Business Context

- **Revenue Model**: Freemium with 4 tiers (Decaf free, Caffeinated $1.99/mo, Espresso $4.99/mo, Redeye $10.99/mo) + in-app store — post-prototype
- **Compliance**: GDPR/CCPA-aware schema design (user data deletion capability, ownership metadata). No active compliance infrastructure for prototype.
- **Scale Expectations**: Investor demo — dozens of users, not thousands
- **Data Sensitivity**: User PII + video content. Stored with user ownership metadata.
- **Timeline**: Fast as possible — investor demo
- **Future Segments**: Education/schools (restricted access, COPPA/FERPA considerations later)

## Development Practices

- **Testing**: Pragmatic integration-first. TypeScript strict mode as first line of defense. TDD reserved for complex business logic (rating system). Override Speckit's default strict-TDD for this project.
- **Code Style**: TypeScript strict, ESLint, Prettier
- **Team Size**: Solo developer + AI assistance
- **Project Type**: Greenfield — but structured for production from day one
- **Documentation**: First-class citizen. Everything documented for future team onboarding.
- **Architecture Principles**: Feature-based folder structure, proper DB migrations, environment-based config (dev/staging/prod), component library matching Figma design system, multi-tenancy awareness in data model

## Core Features (Prototype)

1. **Landing Page** — Value proposition, featured debates, sign-up CTA
2. **Google OAuth Sign-Up/In** — Via Supabase Auth
3. **User Onboarding** — Name, profile photo, tag name (handle), select interests from predefined categories
4. **Browse Debates** — By interest category (politics, sports, tech, etc.), showing topic, format, participant count
5. **View Debate Thread** — Watch participants' video responses in round order, see debate topic/rules/format
6. **Join Debate** — In-browser video recording with countdown timer (upload fallback), max 4 debaters per room, first joiner gets last word (speaks last in final round)
7. **Configurable Debate Formats** — Admin-seeded formats with configurable rounds, time limits per participant, and rules. Seeded defaults (e.g., "Quick Take" 1 round/2min, "Point-Counterpoint" 3 rounds/3min, "Open Forum" 2 rounds/5min)
8. **Rate Debaters** — 4 dimensions on 1-5 star scale: Debate Skill, Respectfulness, Relevance, Persuasiveness
9. **User Profile** — Bio, debate history, aggregate ratings
10. **Scaffolded UI (Non-Functional)** — Follow buttons, notification bell, share icons, data models created but logic deferred to MVP

## User Journeys

### Primary Journey (Prototype)

1. User lands on the homepage → sees value prop and featured debates
2. Clicks "Sign Up" → authenticates with Google
3. Completes onboarding → name, photo, handle, interests
4. Browses debates by interest category
5. Clicks into a debate thread → watches existing video responses
6. Joins the debate → records a video response with timer
7. Rates other debaters on 4 dimensions after watching their videos
8. Views their own profile with aggregate ratings

### Admin Journey (Prototype)

1. Log into Supabase dashboard
2. Create debate formats (rounds, time limits, rules)
3. Seed debate topics with categories, descriptions, thumbnail images, and assigned formats
4. Monitor participation via Supabase table views

## Future Features (Post-Prototype)

### MVP / Beta

- Time-stamped emoji reactions on video playback (float up right side synced to video time)
- Working notification system
- Working social graph (follow/unfollow)
- Sharing debates to social media
- Facebook & LinkedIn OAuth providers
- Admin panel UI
- Basic content moderation

### v2+

- Live streaming debates (real-time video with audience)
- AI debate coach (performance feedback, speech analysis, edit suggestions)
- Badges & gamification (10 badge types: Rookie Debater, Persuasive Speaker, Fact Finder, Fair Play, Master of Style, Community Builder, Frequent Debater, Topic Expert, Marathon Debater, Debate Mentor)
- Premium membership tiers (Decaf → Redeye)
- In-app store (emojis, backgrounds, vote types)
- Competitive/judged debate format (with judges rating teams)
- Calendar integration for scheduling
- Leaderboard by interest category
- Resources/education section
- Matchmaking based on ratings (pair debaters of similar skill)
- Education segment (schools, restricted access, COPPA/FERPA)
- Video transcoding/optimization (Mux or Cloudflare Stream)
- React Native mobile app

## Integrations

- **Supabase** — Database, auth, storage, realtime
- **Google OAuth** — Authentication provider
- **Vercel** — Hosting and deployment (MCP available for workflow integration)
- **Figma** — Design source (IA & Feature List + DebateCafeDesigns files)

## Design Assets

- **Figma IA & Feature List**: https://www.figma.com/board/Z8C5bU7wMppsfAZOphDxJG/IA---Feature-List
- **Figma Mockups (DebateCafeDesigns)**: https://www.figma.com/design/yy8B3RePLkPquNtD31cxpO/DebateCafeDesigns
- **Pitch Deck**: documents/DebatablePitchOnly.pptx

## Key Design Decisions

1. **Multi-dimensional ratings are the core differentiator** — Not agree/disagree popularity voting. Rating on skill, respect, relevance, and persuasiveness enables future matchmaking and sets the platform's cultural tone.
2. **Configurable debate formats from day one** — Not hardcoded. The format engine (rounds, time limits, rules) is built as a flexible system that admins can extend.
3. **In-browser recording with timer** — Sets up the future AI coaching pipeline. Timer enforces structure.
4. **First joiner gets last word** — Incentivizes early participation; first debater to join speaks last in the final round.
5. **Production architecture for a prototype** — Feature-based folders, proper migrations, env config, clean API layer separation. No rewrites when scaling to beta.
6. **Scaffold future features in UI** — Follow buttons, notification bell, share icons present but non-functional. Database tables created. Zero migration pain when activating.
