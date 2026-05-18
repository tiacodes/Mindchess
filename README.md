# MindChess

> Chess as practice for emotional control, not just a rating.

[Live demo](#) · [About the product](#what-this-is) · [How to run](#run-locally) · [Roadmap](#roadmap)

---

## What this is

Chess.com asks: *how good are you?*

**MindChess asks: *how present are you?***

Every chess platform on the market measures the same thing — rating, win rate, accuracy. MindChess is the first chess platform that measures the **emotional shape** of your play. We track:

- **Composure** — how steady is your move timing?
- **Patience** — do you sit with hard positions, or rush them?
- **Resilience** — how do you play the move *after* a blunder?
- **Focus** — how consistent is the quality of your decisions across a game?

  MindChess is chess as practice for emotional control. Every chess platform measures how good you are — MindChess measures who you become when the position turns against you. We track composure, patience, resilience, and focus through a real-time "Pulse" meter, then an AI coach reads the emotional shape of each game. Built for founders, traders, and anyone training high-stakes decision-making — not for grandmasters.

These four numbers tell you something rating never could: who you are when the position turns against you. And they translate. The person who tilts after a blunder on move 24 is often the same person who tilts after a hard email at 4pm.

**MindChess is chess as a mirror for high-stakes thinking.**

---

## The niche we're building for

We are not trying to beat Chess.com at being Chess.com. Their moat is a decade of network effects and 10M+ daily players. We can't outspend that, and shouldn't try.

Instead we're building for the audience chess platforms ignore:

- **Founders** rehearsing composure before a board meeting.
- **Traders** training the muscle of not chasing losses.
- **Engineers** preparing for high-pressure interviews where panic kills 80% of the signal.
- **Therapists, coaches, performers** who already know that what happens *inside* under pressure is the whole game.
- **Anyone in personal-growth space** — the Headspace/Calm audience who'd never download Chess.com, but who'd play a chess app that frames itself as practice.

This audience has higher willingness to pay than casual chess players, and is hungry for tools that work on *self-regulation*. There are no good ones in this space. Chess is a perfect substrate for it — short enough to fit in a day, structured enough to measure, hard enough to provoke real emotional response.

---

## Core features (built in this MVP)

### 1. **Intention setting**
Before every session, choose what you're practicing today: Patience, Resilience, Focus, or Just Play. The whole post-game review is framed around whether you found what you came for.

### 2. **The Pulse** — real-time emotional state estimation
A live meter from "centered" to "tilted." It reads three signals:
- **Move-quality decay** (vs engine evaluation)
- **Time variance after pain** — rushing right after a blunder is a textbook tilt signal
- **Consecutive bad moves** — spirals are detected and weighted

You can watch your own emotional state move in real time as the game pressures you.

### 3. **Mindful Pause** — opt-in intervention
When the Pulse spikes, or right after a blunder, the app may gently offer a 10-second breathing pause with an animated visualization. You can dismiss it; the point isn't to interrupt, it's to give you a deliberate exit ramp from spiral states. **The breathing pause itself slightly lowers your Pulse** — modeling how the act of pausing changes physiology.

### 4. **Post-game Reflection**
Not "your blunders were on moves 11 and 23." Instead, narrative insights like:

> "After your slip on move 14, you replied in under 4 seconds. Speed after pain is the body trying to outrun the feeling. The position deserved longer."

The AI coach reads the *emotional shape* of the game. Insights are categorized: strengths, patterns, observations. Each game generates 1–4 insights tailored to what actually happened.

### 5. **Growth Metrics**
Composure, Patience, Resilience, Focus — tracked over time with EMA smoothing. Plus a rating, because we're not naive.

### 6. **Journal**
Save a written reflection alongside the data. Over time, see the patterns in your own words.

### 7. **City Leaderboard** (Almaty-themed for the incubator)
Ranking that weights composure alongside rating — "the composed play long." This is the first chess leaderboard where being calm under pressure is the actual flex.

### 8. **MindChess Pro** (monetization hook in place)
$8/mo for deeper pattern reports, personalized growth plans, AI coach that remembers your history across sessions. Stripe stub in place.

---

## What makes it a product, not a feature

The defensibility isn't the chess engine — anyone can wrap Stockfish. The defensibility is **the proprietary emotional-state model** trained on game data over time. The longer a user plays, the more accurate their personal Pulse calibration becomes. Switching cost grows with every game logged.

Adjacent products this opens up:
- **MindChess for Teams** — leadership coaching using chess as the assessment instrument
- **MindChess for Trading desks** — pre-market warmup with composure scoring
- **MindChess for Interview Prep** — partnered with FAANG interview coaches, "practice your composure" as a parallel track to LeetCode

---

## Tech

This MVP is built as a **single HTML file** — no build step, no framework lock-in, deploys to any static host in 30 seconds. Deliberate choice: an incubator submission should be diffable in one file, and a stack should be sized to its problem.

Under the hood:
- **Vanilla JavaScript** — no React/Vue. ~1400 lines of clean code.
- **chess.js** — battle-tested move generation + rules validation (full chess, including castling, en passant, promotion, all draw conditions).
- **Custom minimax engine** with alpha-beta pruning and piece-square tables, three difficulty levels.
- **Move classification** — every player move is graded (excellent / good / inaccuracy / mistake / blunder) by comparing the position evaluation before and after the move to the engine's best move at the same depth.
- **Local storage persistence** — all stats, journal entries, and onboarding state.
- **No backend required** to demo — every feature works offline after first load.

For production we'd add:
- Backend (Supabase) for cross-device sync, real leaderboards, social
- Stockfish.js Web Worker for stronger AI without UI lag
- WebSockets for multiplayer
- Stripe for Pro tier

---

## Design

Editorial / contemplative aesthetic. Cream and ink with clay and gold accents. Fraunces (variable serif) for display, Geist for body, JetBrains Mono for data. The board uses warm green/cream squares rather than the standard tournament green-and-buff — small choice, big mood difference.

The Pulse meter is positioned as a co-equal element to the board itself. The board is what you're doing; the Pulse is what's happening to you. Both deserve visual weight.

---

## Run locally

```bash
# Just open the file in any browser. No build step.
open index.html

# Or serve over HTTP (some browsers prefer this for fonts/CDN):
python3 -m http.server 8000
# Then go to http://localhost:8000
```

For production deploy, drop `index.html` onto:
- **Vercel** — `vercel deploy`
- **Netlify** — drag-and-drop the file
- **GitHub Pages** — push to a repo with Pages enabled
- **Cloudflare Pages** — same deal

No environment variables, no secrets, no build pipeline needed for the MVP.

---

## Roadmap

**Now (this submission):** working game, Pulse, Mindful Pause, Reflection, Journal, city leaderboard, Pro upsell hook.

**Next 30 days:**
- Stockfish.js engine for stronger play
- Real auth + cloud sync (Supabase)
- Daily Mindful Puzzle — a tactic framed as an emotional control exercise
- Streak system tied to *intention completion*, not games played

**Next 90 days:**
- AI Coach v2 — uses your last 20 games as context for personalized pattern reports
- Multiplayer with friend-by-link (WebSockets)
- "Composure profiles" you can share publicly — your stats but no rating, more like a meditation-app share screen

**Next 6 months:**
- B2B pilot with one tech company doing interview prep with their candidates
- One trading firm pilot using MindChess as a pre-market warmup
- Mobile app (PWA first, then native)

---

## Why this submission

The brief asked for a chess app that could be a real product. I chose a niche where chess platforms don't compete: emotional intelligence and personal growth. The differentiation isn't a feature — it's the entire framing of what chess is *for*. That's how products defend themselves against deeper-pocketed incumbents.

This isn't a course exercise pretending to be a startup. It's an MVP for a real one I'd like to build.

— Built with care for the n_factorial submission, May 2026.

---

## Credits

- `chess.js` by Jeff Hlywa — MIT licensed move generation & rules.
- Fonts: Fraunces (SIL OFL), Geist (SIL OFL), JetBrains Mono (Apache 2.0).
- Everything else is original.

---


