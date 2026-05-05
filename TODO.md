# Hunting Tracker - TODO

## Recently Completed
- [x] OTC / Draw filter on Explorer page
- [x] "I plan to hunt the whole season" auto-populates start/end dates from season data
- [x] Fix state selection so "California" (and all states) show in the stepper detail under "Where"
- [x] Hierarchical animal selection (category > subspecies > sex)
- [x] Wizard-based hunt creation (6 steps)
- [x] Resident / Non-Resident selector
- [x] Season Explorer page with filters (state, residency, weapon, animal)
- [x] **Planning checklist on hunt details** — auto-generated checklist (buy license, draw deadline, enter draw, scout units, gear check, travel, regs, sight-in) with progress bar, custom items, localStorage persistence
- [x] **License preview on hunt details** — shows matching state license card with status badge, or warning + "Add License" button if none found
- [x] **"Plan this Hunt" navigates to hunt details** — creates hunt card on home AND navigates to details page (not dashboard)
- [x] Selection summary feedback in wizard stepper
- [x] Season date auto-population based on animal/state/weapon/residency
- [x] Draft auto-save to localStorage
- [x] "Plan This Hunt" from Explorer pre-fills wizard
- [x] Archery/Bow weapon mapping
- [x] **Planner page** — Season Plan with timeline, priority hunts, draw results, backup hunts, overlap detection
- [x] Nav renamed: Dashboard → "My Hunts", Season Plan → "Planner"
- [x] Import real 2026 Colorado season data from CPW Big Game brochure (Deer, Elk, Pronghorn, Bear, Moose)
- [x] License tracking page — CRUD for hunting licenses with status badges, expiration tracking
- [x] Application deadline alerts on Dashboard and Licenses page (shows upcoming draw deadlines with urgency)
- [x] CA deer zone map — real CDFW zone names (C1-C4, X1-X12, named zones), draw vs OTC separation
- [x] **My Zones of Interest** — save favorite zones, orange highlight on map, localStorage persistence
- [x] Nav reorder: Home, Explorer, States, Deadlines, Licenses, Past Hunts, Danielle dropdown (Settings + Logout)
- [x] Explorer filter persistence (localStorage) + Reset Filters button + universal search bar
- [x] "Plan a Hunt" button on home → directs to Explorer
- [x] Wizard text changed to past tense (Log Hunt, "Where did you hunt?", etc.)
- [x] Deadlines sorted by soonest first
- [x] **State pictures on hunt cards** — Unsplash landscape thumbnails for 20+ states
- [x] **Drag & drop hunts on home page** — reorder upcoming hunts, order persists in localStorage
- [x] **Past hunts details overhaul** — status hidden for past hunts, added journal (day-by-day entries), photo uploads, learnings & takeaways sections
- [x] **Editable hunt name** — click title on hunt details to rename, saves to localStorage
- [x] **Hunter Education certificates** — upload certificate, track cert number, state, course type, provider on Licenses page
- [x] **Draw Applications on Home** — track applications with state, species, year, app number, multi-choice draw entries (code, manner of take, unit, dates), status, preference points, unsuccessful option
- [x] **States page** — state profiles for CO, CA, MT, WY, ID, UT, OR, NM, AZ, TX with highlights, species, draw dates, official resource links (agency, licenses, draw info, regulations, hunting atlas)
- [x] **"Plan This Hunt" on each season card** — individual button per season in Explorer (not just one per group)
- [x] **Draw application history** — multi-choice support, preference points, status tracking (entered/drawn/not drawn/pending)
- [x] State regulation / license purchase links (via States page)
- [x] Application deadline warnings — draw deadlines shown inline on Explorer season cards
- [x] Animal sightings white background
- [x] Nav dropdown z-index fix
- [x] Remove "Good morning" greeting, remove "+Add to Plan" button
- [x] Remove "Open Now & Opening Soon" section from Explorer
- [x] All hunt data persists in localStorage (auto-save on first load)
- [x] **Add California season data** — sourced from official 2026 CDFW Big Game Digest (Deer zones A/B/C/D/X with exact dates, Elk by zone, Pronghorn, Bighorn Sheep, Bear, Wild Pig, Turkey, Quail, Waterfowl). Application opens Apr 15, deadline Jun 2.
- [x] **Announcement banners on home page** — date-triggered, dismissible banners for CA draw app opening (Apr 15), CO draw deadline, CA draw results (~Jun 15). CSS-styled with action buttons, localStorage dismiss persistence.
- [x] **Hunt status badges on home page** — colored status badges (Planning, Waiting for Draw, Scouting, etc.) now visible on both draw and OTC hunt cards on the home page
- [x] **Nevada added to Explorer** — 35 season entries (deer, elk, pronghorn, bighorn sheep, bear, mountain lion, turkey, chukar/quail, rabbit). NV state profile on States page with NDOW links. Wizard season data for deer/elk.
- [x] **Plan This Hunt flow tested & hardened** — duplicate hunts now open the existing hunt (was: native alert + dashboard bounce); `currentMapHuntId` persisted via `openHuntMap()` (was: direct assignment, refresh lost state); `tagType` included in duplicate checks so OTC vs Draw are distinct; `residency` and `zone` captured as structured fields on both `mockHunts` and `seasonPlanHunts` entries (was: lost after plan).

---

## Bugs / Fixes
- [ ] Verify season data accuracy — CO is sourced from 2026 CPW brochure; other states are AI-generated placeholder, not sourced from state wildlife agencies
- [ ] Hidden `<select id="state">` options — fixed dynamically but should be pre-populated on init
- [x] Test "Plan This Hunt" flow end-to-end from Explorer > Wizard with all pre-fills

---

## Features - Prototype (hunting-tracker-prototype.html)

### High Priority
- [ ] **Draw Strategy / Dependencies flow** — if/then decision tree for draw applications
  - Apply for first choice (e.g., CA X Zone Mule Deer draw)
  - If not drawn, fallback to second choice (e.g., CA D Zone draw)
  - If none hit, fallback to OTC backup (e.g., CA A Zone archery OTC)
  - Cross-state fallbacks (e.g., if no CA draw, fall back to CO OTC)
  - Track draw results as they come in and surface next steps
- [ ] **Interactive US map state selector** — replace card grid with clickable SVG map
  - Click a state on the map to select it
  - Highlight states with available seasons / color-code by tag type
  - Keep card grid as fallback / secondary option below map
- [x] Add California season data for Deer, Elk, Pronghorn, Bighorn Sheep (sourced from 2026 CDFW Big Game Digest, updated 4/1/2026)
- [ ] Zone/unit selection step in wizard (many states have zone-specific seasons)

### Explorer Page
- [ ] Sort results by season start date (soonest first)
- [ ] Filter by seasons still open vs. closed (based on current date)
- [ ] Map view of seasons by state

### Hunt Wizard
- [ ] Add zone/unit selector after state (for states with zone-based seasons)
- [ ] Multiple weapon selection (some hunts allow archery + muzzleloader)
- [ ] Tag/license cost display based on state + residency + animal
- [ ] "Either sex" option for sex selection
- [ ] Validation — warn if selected dates fall outside official season

### Dashboard
- [ ] **Customizable homepage** — let users choose which widgets/sections appear
- [ ] Calendar view of upcoming hunts
- [ ] Quick-stats: total hunts, success rate, species count
- [ ] Weather forecast integration for upcoming hunts

### Hunt Details
- [ ] **Observation insights** — auto-generated summary from sightings, sign, and trail cam data (patterns, hot spots, peak times, terrain preferences)
- [ ] Map showing sighting GPS locations
- [ ] Gear checklist per hunt
- [ ] Harvest reporting with measurements (antler score, weight, etc.)
- [ ] Trail/track recording
- [ ] **Biologist contact information & notes** — store CDFW regional biologist contacts, phone numbers, notes from conversations per zone/unit
- [ ] **AI journal summarizer** — "Summarize" button on journal section that calls Claude API to generate a summary of all journal entries for a hunt (key moments, patterns, animal behavior, learnings). Requires Anthropic API key stored in settings. ~50 lines JS for API call + prompt engineering for hunting-specific summaries. Could also generate "Learnings & Takeaways" auto-suggestions.
- [ ] **Edit past hunt details** — ability to edit location, dates, weapon, companions, harvest status, and notes on past hunt detail pages

### Licenses
- [ ] **Stamps tracking** — Upland Game Stamp, Federal Duck Stamp, Habitat Stamp, etc. (separate from licenses)
- [ ] **Auto-populate license types & prices by state** — show that state's available licenses with real costs
- [ ] Draw application history enhancements:
  - Year-over-year view (e.g., 2025 Applications, 2024 Applications)
  - Preference/bonus point accumulation tracking across years
  - Import from state websites or manual entry
  - Insight: "Applied 4 years for CA Bighorn Sheep, 4 pts accumulated, avg wait 15 yrs"

### Data & Content
- [ ] Source real 2026 season data from state wildlife agencies (priority states: ~~CO~~, CA, MT, WY, ID, OR, NM, AZ, TX, WI)
- [ ] Add more animals to Explorer data (Waterfowl, Pheasant, Quail, Rabbit, Wild Boar, Javelina)
- [ ] Non-resident tag quotas and draw odds where available
- [ ] **Real hunting unit boundary GeoJSON** — download official GIS data from state wildlife agencies
  - Priority: CO GMU 61, UT EB3022 (Wasatch), UT EB3006 (Manti)
  - Colorado CPW, Utah DWR, MT FWP, WY G&F, CA DFW, ID F&G
- [ ] **Huntinfool.com draw deadlines** — manually copy draw deadline data and update prototype
- [ ] Add more states to States page profiles (WI, MI, PA, MN, AK, NV, WA, KS, NE, SD)

---

## Features - Full-Stack App (React + Node)

### Backend
- [ ] Sync prototype features to React frontend
- [ ] Season data API endpoint (serve from database vs. hardcoded)
- [ ] Draw deadline notification system
- [ ] Photo storage (S3 or local uploads)

### Frontend (React)
- [ ] Port wizard flow from prototype to React components
- [ ] Port Explorer page to React
- [ ] Leaflet map integration for hunt locations
- [ ] Zustand store for wizard state

### Infrastructure
- [ ] Database migration for season data tables
- [ ] Seed script for hunting seasons
- [ ] User preferences (home state, residency, preferred weapons)

---

## Ideas / Someday
- [ ] **Announcement banners** — timely alerts for state-specific events (e.g., "CA 2026 Hunting Guide released!", "CO draw applications now open"). Dismissable banners on home or relevant state pages. Could pull from a curated list of key dates per state
- [ ] **Scouting log** — pre-season scouting trips with trail cam photos, GPS waypoints, water sources, glassing spots. Link scouting data to a future hunt
- [ ] **Tag inventory dashboard** — one-glance view of all tags across states, what's filled, what's open, what expires when
- [ ] **Offline mode indicator** — make it obvious everything works offline (localStorage). Visual badge or banner when no connection
- [ ] **Quick-log sighting** — one-tap "I just saw something" that grabs GPS + timestamp automatically, fill in details later at camp
- [ ] **Season overlap detector** — "Your CO elk archery and CA deer X3a overlap by 5 days" with suggestion to resolve + ability to add to plan
- [ ] **Dark mode** — for 4am alarm checking hunt details
- [ ] **Regulation quick-reference cards** — per hunt: legal shooting hours, tag attachment rules, check-in requirements. The stuff you need in the field
- [ ] OnX Hunt integration (when API available)
- [ ] Social features — share hunts with friends
- [ ] Public land overlay on maps
- [ ] Pack-out weight calculator
- [ ] Sunrise/sunset times for hunt dates
- [ ] Moon phase display
- [ ] Export hunt log to PDF
- [ ] Import hunts from spreadsheet/CSV
