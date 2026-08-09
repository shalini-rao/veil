# Bachelorette Planner — Product Spec

*Working draft. Built section by section with Shalini.*

---

## 1. Overview

**What it is:** A mobile app for planning a bachelorette trip, where one shared plan is seen differently by three roles so the bride can be involved without spoiling the surprises.

**Grounding case:** Nidhi's bachelorette, Scottsdale, December.

**Reusable by design:** one planner can use the app to plan multiple trips for different brides over time. "A trip" is a reusable object, not a one-off.

**Bride as planning partner:** the bride isn't just a restricted viewer — she's a co-planner who shares the itinerary benefits, communicates with everyone, and contributes ideas. Only a deliberate few things are kept private from her. Her level of planning involvement is configurable (a bride like Nidhi wants to do almost as much as the planner).

**Goals for the project:**
- Strong portfolio case study
- Learn mobile design deeply
- Something actually usable for a real trip

*(vision statement — to refine)*

---

## 2. Roles & Permission Model

*The core system. Every surface refers back to this.*

**Roles**
- **Planner** — full control. Creates and edits everything, holds the visibility toggle.
- **Bride** — a **planning partner**, not just a viewer. Shares itinerary benefits, communicates with everyone, and co-creates via a shared idea board. Sees everything except the deliberate few things the planner hides. Her planning involvement is **configurable** by the planner (from light input up to near-planner access).
- **Guest** — read-mostly. Sees polls to vote on, expense overview + what they owe, itinerary, outfit details. In on the surprises.

**Visibility states (per item)**
- **Everyone** — visible to all roles.
- **Teased** — bride sees "something's planned" with no details; planner + guests see the real thing.
- **Hidden from bride** — bride doesn't see it exists at all; planner + guests see it.

**Cross-surface rules**
| Surface | How it honors visibility |
|---|---|
| Itinerary | Hidden items omitted from bride view (no suspicious gap); teased items show as mystery cards |
| Polls | Some polls exclude the bride entirely; blind votes; bride's vote weighted heavier where included |
| Expenses | Secret/gift expenses hidden from bride; bride's totals must stay believable (see open Q) |
| Outfits / logistics | TBD |
| Messaging | Separate channels: everyone+bride, everyone−bride |

**Open questions**
- Hidden-cost problem: if a surprise costs money, whose split, and how does the bride's total stay believable?
- Real-time multi-user vs. single shared state you role-switch through?
- **Configurable bride involvement:** what exactly does the planner get to dial up/down? (idea-board access, expense visibility, poll creation, etc.) — needs a defined set of toggles.

---

## 3. Surface: Itinerary

*Status: prototyped.*

**Purpose:** A shared timeline of the trip's plans.

**Per-role behavior**
- Planner: add / edit / delete items; set visibility per item; sees planner notes.
- Bride: read-only; hidden items omitted, teased items shown as mystery cards; never sees planner notes.
- Guest: read-only; sees everything with cost.

**Core object — Itinerary item**
- time, title, location, cost per person, planner note (never shown to bride), visibility state
- **Rich planner detail (new):** links, vendor options, vendor/price comparison against the budget tracker, per-event color scheme selector

**Key interactions**
- Tap "+ Add to the day" → bottom sheet with fields + visibility control
- Tap a card (planner) → edit / delete
- Items auto-sort by time
- Save disabled until time + title filled
- **Vendor comparison (new):** planner can attach multiple vendor/price options to an event and see how each plays against the budget

**Edge states**
- Empty day → invitation to add the first plan *(to design)*
- Multi-day / weekend view *(not yet built)*

---

## 4. Surface: Polls / Decisions

*Status: captured, not designed.*

**Purpose:** Structured group decisions so key details get covered and the group chat doesn't spiral.

**Preset poll templates** — make sure the important questions get asked:
- Budget each person wants to spend
- Room / bed sharing preference
- Who they'd or wouldn't be comfortable rooming with
- Activity preferences
- Location preference
- (extensible — more templates over time)

**Poll mechanics**
- **Blind votes:** results hidden until close, so people aren't swayed.
- **Weighted votes:** bride's opinion counts more where she's included.
- **Bride inclusion flag:** some polls exclude the bride entirely (per role model).
- **Results are advisory, not binding:** the app emphasizes "this is what the poll showed." The planner *can* override, but overriding is a conscious, visible choice rather than a silent one.
- Budget poll feeds the expenses pool (see §5).
- Rooming polls feed room assignments (see §6).

---

## 5. Surface: Expenses

*Status: captured, not designed. Richest section.*

**Two expense modes**
1. **Pooled budget:** each attendee commits a total budget (via poll) → one shared pool the planner works within.
2. **Pay-per-expense:** each expense is paid + split individually (Splitwise/Venmo-style).

*(Open Q: are these two separate modes, or one system where the pool is just planned expenses and pay-per-expense is live tracking? Likely the latter — see gaps.)*

**Bride contribution rules**
- Bride may or may not contribute to the pool (planner sets).
- **Secret/gift expenses:** bridesmaids split these; bride never sees them.
- Bride pays her own share of non-secret expenses.

**Budget tracker (planning phase)**
- As activities/expenses are added, a running tracker shows: total cost, how it fits the agreed budget, and the average per bridesmaid.
- **Overage handling:** if the group goes over the agreed bridesmaid budget, flag it — bride may cover the overage.
- Each expense has a **split selector**: who's in on this split.

**Live weekend tracker (trip phase)**
- Splitwise/Venmo-style: add an expense, pick who paid, pick who split it, optimize the settle-up math.
- Handles on-the-ground spending (ubers, drinks, etc.).

---

## 6. Surface: Outfits, Themes & Logistics

*Status: captured, not designed.*

**Theming system**
- White-forward default (bride aesthetic).
- Color-scheme selectors: presets or color wheels.
- **Pinterest color extraction → future.** Middle-ground for now: prompt the user to run their image through an external color-extractor site and paste the hex values in.
- One overarching bachelorette theme + per-event themes.

**Outfits**
- Outfit color schemes per event, with color sets.
- Pinterest-style mood board / inspo per event.

**Packing list**
- Consolidated packing list for attendees + bride, generated from the event color schemes.

**Room assignments / housing**
- Add housing details.
- Auto-pair people from rooming-preference polls (who wants to share, bed preferences, comfort/compatibility).
- **Privacy:** "who you would/wouldn't be comfortable sharing with" is sensitive. Visible to the **planner only**, and tucked behind a **second tap** (never surfaced at a glance, never shown to the group).

**Planner + Bride idea board (new)**
- A shared collaboration space where planner and bride throw in ideas together: event ideas, color schemes, decor inspo.
- This is the heart of "bride as planning partner" — a co-creation surface, not a permission gate.
- *(Hidden/surprise items live outside this board, in planner-only space.)*

**Inspo / high-level planning**
- Mood boards to help decide location and activities.
- Mood board = image grid the planner (or bride) uploads to, not live Pinterest embeds (for now).

---

## 7. Messaging

*Status: captured, not designed.*

- Multiple channels by audience: everyone **+** bride, everyone **−** bride, etc.
- Ties directly to the role model — the "−bride" channel is where surprises get coordinated.

---

## 8. Onboarding & Invites

*Status: captured, not designed.*

- Planner sends guests a **join link**.
- Each person creates a **basic profile**: name, photo, phone number / email (for confirmation communications).
- Role is assigned as part of joining (planner designates the bride; everyone else is a guest).
- **Trips are reusable:** a planner can run multiple trips over time for different brides.

---

## 9. Design System

*Status: not started.*

- White-forward base (see §6 theming).
- Themeable: overarching + per-event color schemes drive the interface, not just outfits.
- Tokens, type, color, components — TBD.

---

## 10. Open Questions & Parking Lot

**Resolved this round:**
- ~~How guests get invited~~ → join link + basic profile (see §8).
- ~~Rooming privacy~~ → planner-only, behind a second tap (see §6).
- ~~Are poll results binding~~ → advisory, override is a conscious choice (see §4).
- ~~Pinterest scope~~ → future; paste-hex middle ground for now (see §6).
- ~~One trip or many~~ → reusable; planner runs many trips (see §1, §8).

**Still open:**
- **Hidden-cost handling:** whose split, how the bride's total stays believable. *(Leaning: bride gets a separate ledger showing only her-eligible costs, so her math is internally consistent — needs confirming.)*
- **Pool vs. pay-per-expense:** likely one continuum (planning phase → trip phase), not two modes — to confirm.
- **Overage:** real tracked money flow, or just a flag? — to decide.
- **Configurable bride involvement:** define the exact set of planner toggles.
- **Real-time multi-user vs. single-device** role-switching.
- **Notifications.**
- How theming propagates: does an event color scheme drive UI, outfits, and packing at once?
