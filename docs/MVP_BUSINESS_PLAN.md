# MVP Business Plan — innerG·X·change
**Version:** 1.0
**Date:** April 24, 2026
**Status:** MVP Definition

---

## The Problem

Every exchange platform ever built has the same flaw: you can join without giving anything.

You create a profile. You browse. You message. You ghost. You're rated. You feel watched. The community is visible before you've earned the right to be in it. So it becomes a marketplace. A directory. A dead social feed.

What's missing isn't a better algorithm. What's missing is initiation.

Real communities — the ones people are loyal to for decades — require something of you before they let you in. Proof that you're real. Proof that you'll show up. Proof that you give as much as you take.

innerG·X·change is built on that premise: **you earn the community by completing one genuine exchange with another human being, first.**

---

## The Solution

A platform where:

- **Entry is earned.** You see nothing until you've completed your first real-world exchange, confirmed by both parties.
- **Matching is one at a time.** The system gives you one person. You have 72 hours to connect. No lists. No browsing. No rejection theatre.
- **No money moves.** Ever. Only energy — skills, time, shelter, food, labour, care.
- **No ratings.** Just confirmation. It happened. Or it didn't.
- **Your place in the community grows** as you exchange more. First exchange: you arrive. Tenth exchange: you're a node in the constellation.
- **Every member has a card.** A physical/virtual artifact that proves belonging. Shareable. Verifiable. Beautiful.

---

## Vision Statement

A world where human gifts flow freely — not because the economy forces it, but because a community holds it.

---

## Mission Statement

To build the infrastructure for earned belonging: a global network of people who have proven they show up, give genuinely, and receive gracefully.

---

## Open Questions — Assumptions Made for MVP

The following decisions were required to scope the MVP. Each includes a recommendation and rationale.

### 1. Matching: Manual or Algorithmic?
**Recommendation: Algorithmic for MVP, with admin override capability.**

Rationale: Manual curation doesn't scale past 100 members and creates an admin bottleneck during the critical growth phase. A lightweight algorithm — matching on World overlap, complementary offer/need pairs, and location preference — is achievable in Rails without ML. Admin override allows The Voice and The Builder to curate founding-cohort matches manually during launch, then hand off to the algorithm.

The matching algorithm at MVP is: same World > complementary offer/need > geographic proximity (optional filter) > FIFO queue position. No recommendations engine. No ML. Pure Ruby.

### 2. Physical Card: PDF Only or Print-on-Demand?
**Recommendation: Print-ready PDF download only for MVP.**

Rationale: Print-on-demand integration (Printful, Gelato) requires SKU setup, webhook handling, and international shipping logic that adds 3–4 weeks of scope. For MVP, a print-ready PDF at credit-card dimensions (3.5" × 2" at 300dpi) is immediately valuable and proves demand before committing to the fulfilment integration. Defer print-on-demand to MVP+.

### 3. Are the 4 Worlds Fixed Categories for MVP?
**Recommendation: Yes — the 4 Worlds are fixed for MVP.**

The four Worlds — Wellness, Entrepreneurship, Conscious Living, Creative Life — are fixed categories for MVP. Members choose a primary World and optionally a secondary World. Sub-categories within each World (e.g., "Movement" within Wellness) are surface-level tags at MVP and can evolve into a richer taxonomy in V2. Fixed categories reduce matching complexity and create a comprehensible identity system.

### 4. Admin / Moderation Layer for MVP?
**Recommendation: Yes — lightweight admin layer is required for MVP.**

A platform built on trust must have humans behind it at launch. MVP includes:
- Admin dashboard (Rails admin via Administrate or custom) to view members, exchanges, matches
- Ability to manually trigger or reassign a match
- Ability to flag and suspend a member
- Ability to confirm/reverse a disputed exchange
- The two founding nodes (The Voice, The Builder) have admin access from day one

No community moderation by members at MVP. No reporting flows. Admin is the sole moderation layer.

### 5. Card Sigil: Pre-generated or Algorithmic?
**Recommendation: Algorithmically generated SVG per member, seeded by member ID.**

Rationale: A pre-generated set of, say, 100 sigils would be reused across members, destroying the sense of uniqueness. The sigil must feel personal. A deterministic algorithm seeded by the member's UUID generates a constellation pattern — a fixed set of points and connecting lines derived from the numeric hash of the ID. This is pure SVG math, no external service required. The same seed always produces the same sigil, making regeneration reliable. The algorithm lives in a Ruby concern.

---

## Target Users

### Primary: The Practitioner
**Who they are:** 28–45, globally mobile or urban, values-led. Coaches, therapists, designers, builders, farmers, teachers, bodyworkers, cooks, artists. People who have skills that the economy undervalues — and who are tired of either giving them away for free or charging for them in ways that feel hollow.

**Pain points:** Can't afford to outsource things they need. Don't want to charge friends. Frustrated by gig platforms that commoditise their gifts. Want community but not another group chat.

**Jobs to be done:** Exchange what I'm good at for something I need, with someone I can trust, in a way that feels meaningful rather than transactional.

### Secondary: The Seeker
**Who they are:** Someone in The Voice's existing audience. Conscious-living adjacent. May not have a clear "offer" yet — needs the declaration process to clarify their own gifts.

**Pain points:** Feels like a consumer of other people's expertise. Wants to contribute but doesn't know how. Existing platforms are either too transactional or too passive (consume content, don't exchange).

**Jobs to be done:** Discover what I have to offer. Find one person to exchange with. Arrive.

### Edge User: The Node
**Who they are:** Members with 10+ completed exchanges. They have become connectors — people others want to exchange with.

**Jobs to be done:** Expand my constellation. Find members in new Worlds. Build a reputation that lives in my exchange count, not a star rating.

---

## The 4 Worlds

Each World is both a category and an identity. Members belong to one world primarily and connect across worlds.

| World | What lives here |
|---|---|
| **Wellness** | Movement, bodywork, mental health, nutrition, healing modalities, breathwork, sleep |
| **Entrepreneurship** | Strategy, tech, design, marketing, finance, legal, operations, growth |
| **Conscious Living** | Permaculture, sustainability, food growing, natural building, intentional community, spirituality |
| **Creative Life** | Music, writing, visual art, performance, craft, film, photography, storytelling |

---

## User Flows

### Flow 1: First Exchange (Onboarding)

```
Landing Page
    ↓
"Declare Your Energy" — form: name/alias, offer (free text + World), need (free text + World), location (optional), bio
    ↓
Profile created → State: WAITING_FOR_MATCH
    ↓
System runs matching (daily batch at MVP — can move to real-time in V2)
    ↓
Match found → Email + in-app notification: "Someone is ready to exchange with you."
72-hour window begins
    ↓
Member A initiates contact (in-app message or preferred contact method shared)
    ↓
Exchange happens in the real world (or video call)
    ↓
Both members independently confirm: "This exchange happened." (binary)
    ↓
Both confirmed → Exchange record sealed → Both members' states: COMMUNITY_MEMBER
    ↓
"You've arrived." — Arrival screen → redirect to Constellation
```

### Flow 2: Community Browse (Post-first-exchange)

```
Constellation view — grid of member cards
    ↓
Filter by World / location
    ↓
Click member card → See: offer, World, exchange count, member since
    ↓
"Request exchange" → enters queue for next match cycle
    ↓
System assigns match when both parties are in queue and compatible
```

### Flow 3: Match Expiry

```
Match assigned → 72-hour window
    ↓
No action from either party by hour 72
    ↓
Match released → Both parties return to WAITING_FOR_MATCH
    ↓
Email notification: "Your match has released. You'll be matched again soon."
```

### Flow 4: Membership Card Access

```
First exchange confirmed
    ↓
Card generated automatically (sigil seeded by member ID, data populated)
    ↓
Card visible on profile page
    ↓
Member can: view card, share image (PNG download), download print-ready PDF
    ↓
QR code on card → public verification URL → /verify/:token
    ↓
Verification page shows: member status, World, exchange count, member since
```

---

## Feature List

### MVP Features (Ship This)

**Onboarding & Matching**
- Declaration form (offer, need, World, location, bio)
- Profile creation with pending state
- Daily matching batch (algorithm: World overlap, offer/need complement, location)
- Admin match override
- 72-hour match window with automated expiry
- In-app messaging between matched pair only (no open DMs)
- Exchange confirmation (binary, both parties required)
- Arrival screen with community unlock

**Community**
- Constellation view (grid of confirmed members)
- World filter + location filter
- Member profile page (public-facing after first exchange)
- Exchange count visible on profiles
- Post-arrival exchange requests (queue-based)

**Membership Card**
- Auto-generated card on first confirmed exchange
- Sigil: deterministic SVG constellation per member
- QR code per member (rqrcode gem)
- Virtual card display on profile
- PNG download
- Print-ready PDF download (credit-card dimensions, 300dpi)
- Public verification page (/verify/:token, no login required)

**Admin**
- Member list with states
- Match dashboard (view current matches, override, reassign)
- Exchange log
- Member suspension / flag
- Founding nodes configuration

**Auth & Account**
- Rails 8 built-in authentication
- Email/password
- Email verification
- Password reset
- Account deletion (GDPR-compliant, anonymises exchange records)

### MVP+ Features (Next Phase)

- Print-on-demand physical card (Printful / Gelato integration)
- Real-time matching (replace daily batch with event-driven queue)
- Sub-category tags within each World
- Member-to-member community reporting
- Animated virtual card (Lottie / CSS shimmer)
- Public profile pages indexable by search engines
- Mobile apps (React Native or PWA)
- Multi-language support (Spanish first, given LATAM wellness community overlap)
- Constellation visualisation (D3.js node graph, not just grid)
- Exchange circles (3+ members, value flows in a loop)

### Intentionally Excluded (Never)
- Money, credits, or any currency
- Star ratings or reviews
- Browsing before first exchange
- Paid tiers or paywalls on community access
- Advertising

---

## Founding Exchange

The founding exchange between The Voice and The Builder is displayed as a pinned record in the constellation — the first node. It demonstrates:

1. The platform works
2. The founding relationship is transparent
3. The exchange was real and confirmed by both

Display on: constellation (pinned first), about page, landing page.

---

## Success Metrics

### North Star Metric
**Confirmed exchange rate** — percentage of matched pairs who complete and confirm an exchange.
Target: 60%+ at steady state.

### Launch Metrics (First 90 Days)
| Metric | Target |
|---|---|
| Declarations submitted | 500 |
| Matches made | 200 |
| Confirmed exchanges | 120 |
| Community members (arrived) | 120 |
| Cards downloaded (PNG or PDF) | 80 |
| Card QR scans (verification page) | 200 |

### Health Metrics (Ongoing)
| Metric | Target |
|---|---|
| Match expiry rate (neither party acts) | < 30% |
| Time from declaration to first match | < 14 days |
| Repeat exchange rate (2+ confirmed) | > 40% at 6 months |
| Admin interventions per week | < 5% of active matches |

---

## Monetisation Notes

innerG·X·change has no revenue model inside the platform. That is intentional and non-negotiable.

**Sustainable paths that respect the philosophy:**

1. **Optional donation on arrival** — "If this exchange meant something to you, contribute to keeping this infrastructure alive." One-time, optional, no value attached to community access.

2. **Physical card revenue** — When print-on-demand is added (MVP+), card printing can be offered at cost plus a small margin. Members pay for the physical artefact, not access.

3. **Community events** — Live gatherings, workshops, retreats facilitated by The Voice and community nodes. Paid events separate from the platform. Revenue stays with event organisers.

4. **Founding supporter NFT / token** — Out of scope for MVP but worth noting: a founding cohort of patrons who fund infrastructure costs in exchange for a recognised founding status in the constellation. Not a product feature — a community fundraising mechanism.

5. **B2B / institutional** — Organisations (companies, schools, intentional communities) could eventually host private constellations on the platform. Enterprise tier. Not MVP.

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Insufficient density for matching | High at launch | High | Launch with The Voice's audience (pre-warmed) as founding cohort |
| Match expiry creates frustration | Medium | Medium | Clear communication at each stage; fast re-match on expiry |
| Bad actors (false confirmations) | Low-Medium | High | Admin can investigate and reverse; both parties must confirm independently |
| Members declare but never follow through | Medium | Medium | 72-hour window creates urgency; notification sequence |
| Platform feels too esoteric for mass adoption | Low | Low | Not targeting mass adoption at MVP; targeting The Voice's specific audience |
| Physical card demand exceeds PDF capacity | Low | Low | PDF is static file generation; scales trivially |
