# Bachelorette Planner — Product Spec (MVP scope)

*Working draft with Shalini. This spec is our starting point. Scoped to a buildable MVP; the fuller vision is preserved in the Future section and in `bach-planner-spec-full.md`.*

---

## 1. Overview

**What it is:** A mobile app for planning a bachelorette trip, where one shared plan is seen differently by role so the bride can be a real planning partner without spoiling the surprises.

**Grounding case:** Nidhi's bachelorette, Scottsdale, December.

**Reusable by design:** one planner can run multiple trips for different brides over time.

**MVP is four tabs:**
1. **Home** — hype + countdown, with the itinerary as the main page
2. **Messaging** — group boards + announcements
3. **Expenses** — event costs + standalone expenses, settle-up
4. **Account / Settings**

The single idea tying it together: **bride visibility** (in or out, per item) works the same way across every surface.

---

## 2. Roles, Permissions & Visibility

*The core system. Two independent axes: a **capability level** (what you can read/write) and the **hidden-from-bride filter** (which always applies to the bride, on top of her capability level).*

**Capability levels**
- **Planner** — the MOH/creator plus anyone granted planner access. Full read + write over everything. No restrictions.
- **Guest** — read-only for the most part, with two write exceptions: submit **pending** expenses (need planner confirmation) and send messages into groups they're already in. Guests **cannot** create new message groups.

**The bride** — capability level is independent of the hidden filter:
- **Bride WITH planner access** — full read + write like any planner, *except* never sees or touches anything hidden-from-bride.
- **Bride WITHOUT planner access** — same as a guest, *except* never sees anything hidden-from-bride.
- **Invariant:** hidden-from-bride *always* filters the bride, regardless of planner access. Planner access changes what she can **write**, never whether she can see secrets.

**Visibility states (per event / message / expense)**
- **Everyone** — visible to all.
- **Teased** *(itinerary only)* — bride sees "something's planned," no details; others see the real thing.
- **Hidden / secret from bride** — bride never sees it exists (any capability level); others do. Covers hidden events, secret expenses, and messages/announcements in groups the bride isn't in.

**Group creation:** any planner can create new message groups, including smaller subsets of the guest list (committees, sub-teams). Guests cannot.

**The through-line — every surface honors the hidden filter:**
- Itinerary → hidden events omitted from bride view (no gap); teased shown as mystery cards.
- Expenses → secret expenses excluded from the bride's total *before* settle-up math runs, so her number never leaks a surprise.
- Messaging → the bride only sees announcements from boards she's in; announcements from bride-excluded boards carry a **secret tag** ("don't blab").

---

## 3. Onboarding & Account

**Account creation (shared by all entry points)**
1. Phone number *(required)*
2. Display name *(required)*
3. Photo *(optional)*
4. Venmo or Zelle handle *(optional, displayed — powers manual settle-up)*

*(Future: link Venmo/payment directly rather than just displaying a handle.)*

**Two entry points, forking after account creation:**
- **Via a group join link** → after account setup: "You're invited to join [XYZ]" → confirm join. Role is set by which link they used.
- **From scratch** (e.g. the MOH) → after account setup: "Create a new group."

---

## 4. Group Creation & Invites

**Create a new group flow**
1. Name of event
2. Dates
3. **Theme picker** (Desert Warmth or Playful Pop — set once, see §7)
4. **Role setup:**
   - Are you the only planner, or grant planning access to someone else?
   - Are you the bride?
     - If **no** → offer to give the bride planning access.
     - If **yes** (bride is creating) → ask whether "hidden from bride" controls still apply to her (self-imposed surprise-blindness).
5. Land on the chosen days → add any events already known.

**Invite links (MVP)**
- On creation, the planner gets three shareable links by permission level: **planning-access**, **bride**, and **everyone-else**.
- Permission is carried by *which link* someone joins with.

*(Future: direct per-person invites via phone number — pre-populate the group list, pre-set each person's permission, generate a unique per-person link. Also resolves the shared-link trust quirk where a link could be forwarded to the wrong person.)*

---

## 5. Surface: Itinerary (Home)

**Purpose:** the shared timeline and the app's main page.

**Home framing**
- Before the party: "Get pumped for [party name]" + a **countdown in days** (no hours/minutes).
- Once it starts: "Welcome to [party name]."
- Either way, the main page is the itinerary.
- During the party: itinerary defaults to the **current day, scrolled to the current hour**, with a **"Coming up — [next event] in [X hrs Y min]"** cue (precise, unlike the coarse pre-party countdown).

**Creating an event** (anyone with planning access)
- Date
- Time (start + duration)
- Location
- Dress code *(future: color swatches, Pinterest links, richer display)*
- Images (mood board or cover)
- **Bride visibility toggle** (everyone / teased / hidden)
- Cost: amount, whether it includes the bride, optional exact split (per-person amounts; some excluded)
- Notes

**Timeline view**
- Day-by-day; chiclets at top to switch days, plus scroll.
- Full hours shown, events as blocks on their hours so **breaks are visible**.
- Each day **auto-crops** to the first event's start and last event's end (no dead midnight–6am, no empty arrival morning).

*(Edit/delete of events by planners — assumed; to spec.)*

---

## 6. Surface: Expenses

**Purpose:** track trip costs and settle up, driven by event costs + standalone expenses.

**Sources of expenses**
- **Event costs** flow in automatically.
- **Standalone expenses** can be added (below).

**An expense has:**
- Date, amount, who paid
- Split: who owes what (custom amounts) or equal split among selected members
- Secret-from-bride flag
- Receipt photo(s)
- Description + notes

**Who can add / confirm**
- Planners add expenses directly (confirmed).
- Non-planners can submit expenses → **pending**, must be verified/confirmed by a planner. Planners can edit details.
- **Pending visibility:** everyone sees only confirmed expenses; planners have a **pending tab**; the submitter sees their own pending expense in their main view with a **pending visual treatment**. Totals reflect confirmed only.

**What a user sees**
- **"What you owe"** at top — a single net number, no recipient.
- Math uses **debt simplification** (Splitwise/Venmo-style): prioritizes paying each payer back with the fewest transactions, not each person paying their share to each payer.
- **Settle up** resolves the net number into concrete instructions: send $X to person Y (uses their displayed Venmo/Zelle handle).
- **Expense list:** snapshot rows (total cost · date · what it is · what you owe); tap to open full detail (all fields, complete split, what everyone owes).

**Closing out**
- Planners can **"Close out tab"** → signals all expenses are in; everyone settles up for real.
- Ledger has an open vs. closed state.
- If a **non-planner** tries to settle before close-out: soft warning — "the expenses aren't locked in, your number may change." (Warned, not blocked.)

**Bride rule:** secret expenses are excluded from her ledger *before* the simplification runs, so her settle-up never reveals a surprise via a weird number.

---

## 7. Surface: Messaging

**Boards**
- Anyone with planning access can create a board.
- **Default boards:** everyone **+** bride, everyone **−** bride, and a planning-access-only board (in both **+** and **−** bride flavors).
- Operates like a normal messaging platform.

**Announcements**
- Planning-access people can mark any message as a **broadcast/announcement**.
- Announcements are visually differentiated and **pinned** in their board; planners can unpin.
- Every announcement also mirrors to a single dedicated **Announcements board** (one consolidated feed of everything important, fully in-app — no SMS).
- **Bride rule:** she only sees announcements from boards she's in. Announcements originating from a bride-excluded board carry a **secret tag** so no one blabs.

---

## 8. Design System & Theming

*Status: token plan defined.*

**Two themes, chosen once at setup** by the group creator. A property of the weekend, inherited by everyone. No per-user theming, no mid-trip switching.
- **Desert Warmth** — Scottsdale-inspired. Terracotta / sand / sage. Cormorant Garamond + DM Sans. Earthy, calm, refined.
- **Playful Pop** — celebratory. Coral / lilac. Fredoka + Poppins. High-energy.

**One system, swappable tokens** (structure fixed, only tokens change):
- **Primitive tokens** — raw values (hex, fonts, radii); differ per theme.
- **Semantic tokens** — named roles the UI references; names identical across themes, values resolve per theme.

**Semantic roles**
- Color: `surface-page`, `surface-card`, `ink-primary`, `ink-secondary`, `accent`, `accent-quiet`, `visibility-everyone`, `visibility-teased`, `visibility-hidden`
- Type: `font-display`, `font-body`, shared type scale (family swaps; sizes/line-heights don't, so layouts never reflow)
- Shape/depth: `radius-card`, `radius-chip`, `radius-sheet`, `shadow-card`, `border-card`
- Spacing: single shared scale, never themed.

**Key constraint:** the visibility states stay semantically legible in both themes (hidden = slightly alert, teased = warm/anticipatory, everyone = calm). Meaning survives the theme swap.

---

## 9. Navigation

Bottom tab bar, four tabs: **Home (itinerary)** · **Messaging** · **Expenses** · **Account/Settings**.

---

## 10. Future / Cut (preserved, not building now)

Full detail in `bach-planner-spec-full.md`.

- **Polls / decisions:** preset templates (budget, rooming, activities), blind votes, weighted bride vote, advisory-not-binding.
- **Rich expenses:** pooled budget mode, overage-to-bride, bride contribution rules.
- **Shared tab organizer:** in-the-moment single-bill splitter (tableside "who had what") that feeds one expense into the main tracker.
- **Outfits, themes & logistics:** richer dress-code display, preset/wheel color schemes, Pinterest color extraction (paste-hex middle ground), per-event mood boards, packing lists, room assignments from rooming polls (planner-only, behind a second tap).
- **Planner + bride idea board:** shared co-creation space; ideas graduate into itinerary events.
- **Configurable bride involvement:** a defined set of planner toggles.
- **Direct invites:** per-person links via phone number with pre-set permissions.
- **Payment linking:** real Venmo/Zelle integration beyond a displayed handle.
- **Notifications.**
- **Deeper theme flexibility:** more than two themes; independent font/color breakout at setup.

---

## 11. Open Questions & Resolutions

**Resolved via sketch review (both batches):**
- Event edit (planner) = the Add Activity form reused.
- Event detail view drawn in all three visibility states: full ("Yoga class"), secret (red "This is a secret from THE BRIDE" banner), and teased ("There's something being planned for you… don't sweat the details, just show up!" — shows only the time slot).
- Teased vs hidden do different jobs on the bride's timeline: teased holds the time slot visibly (mystery block), hidden vanishes entirely (no gap). Confirmed consistent in Home-bride sketch.
- Guest messaging = planner view minus announcement-compose.
- Settled state = "You're settled up!" replaces the owe number.
- Tab-closed state: shows "Tab is closed out. You owe $X", Settle Up present, **Add Expense removed**.
- Close-out confirmation screen drawn ("All expenses will be locked in and no others can be added. Back / Confirm").
- Bride's settle-up view = guest settled view minus her hidden expenses.
- Bride creating her own party = planner flow.
- Setup role questions revised & drawn: "Are you the only planner?" → "Are you the bride?" → (if yes) "Do you want surprises to be hidden from you?"
- Bride invite screen has its own warmer copy ("Hey BRIDE!").

**Still open:**
- **"Bride is paying for herself" checkbox** (from batch 1): how does it interact with the three visibility states? A hidden event can't also have the bride self-paying — needs a rule. (Only dangling logic item.)
- **Close-out for planners:** once closed, can a planner reopen/add, or is it locked for everyone?
- **Overlapping events on the timeline** — nest/overlap visually, or enforce no-overlap? (Home sketches show stacked blocks.)
- **Compose-time secret warning** when posting an announcement to a no-bride board? (Output/secret-tag is drawn; compose moment isn't.)
- **Empty states:** first-run Expenses, empty board, event-less day.
- ~~Real multi-user vs. single-device demo~~ → **RESOLVED: portfolio demo first** (front-end only, seeded data, role-switch to "view as planner/bride/guest"). The role toggle actively dramatizes the visibility system for reviewers. Real multi-user backend is a possible phase two, not now.
