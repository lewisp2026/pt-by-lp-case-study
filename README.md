# PT by LP — product case study

PT by LP is a coaching platform I designed, built and run myself: a web app that
lets a personal trainer onboard clients, collect weekly check-ins and track
nutrition and progress in one place, instead of across spreadsheets, messages
and notes.

It is live with paying clients. It is deliberately small — I built it alongside a
full-time commercial role — and it exists as much to keep my own product
judgement honest as to make money. This repository is a write-up, not the source
code: the product is commercial and the code stays private.

## The problem

A coach with a handful of online clients spends a surprising amount of time on
admin: chasing check-ins, working out whether a client is on track, and turning
scattered numbers into advice. The job worth doing is the coaching conversation.
Everything else should be fast, structured and reliable.

## What I built

- Client onboarding, with invite-based account provisioning
- Coach dashboards showing each client's progress at a glance
- Weekly check-in workflows, with reminders
- Food tracking, including barcode lookup through a third-party food database API
- Push notifications
- Role-based access control, so coaches and clients see only what they should
- Mobile-first design, because clients log from their phones

## The AI feature

Coaches get a short briefing before each weekly check-in, generated from the
client's own data through the Anthropic API. The design choices mattered more
than the model:

- Deterministic first. All the numbers — averages, changes, targets — are
  calculated in code. The model never does the maths.
- Generative only where it adds value. The model turns those figures into a
  readable summary and flags what deserves the coach's attention.
- Human in the loop. Nothing the model writes reaches a client. The coach reads
  the briefing and decides what to say.
- Cost is capped. Generation is triggered by the coach, each briefing costs around a
  penny, and total spend is capped.

## How it's built

- Next.js and TypeScript
- Supabase for authentication and the Postgres database, with row-level security
  so each client's data is isolated at the database level
- Vercel for hosting and continuous deployment

## How I ran it

- Scoped against a lean budget: every feature had to earn its build time, and
  technical debt was a deliberate trade-off rather than an accident.
- Shipped in small increments: at the time of writing, around 290 commits and
  around 290 production deployments.
- Revisited earlier decisions when they stopped holding up — for example,
  rewriting database access policies and adding indexes once a performance review showed
  where it mattered.

## What I'd do next

If I resume active development, the natural next step would be licensing the
platform to other coaches, which would turn a single tool into a B2B product:
multi-coach onboarding, billing and support would become the work.

---

Lewis Patuzzo · [LinkedIn](https://www.linkedin.com/in/lewis-patuzzo) · A live walkthrough is available on request.
