# Hunting Tracker - Session Notes

A log of development sessions and changes made to the hunting tracker project.

---

## Session: February 17, 2026

### What We Did
- Located the existing hunting-tracker full-stack project in iCloud Drive
- Reviewed the current frontend implementation (React/TypeScript/Vite)
- Created a new **simple HTML/CSS prototype** (`hunting-tracker-prototype.html`)
  - Single-file application with embedded CSS and JavaScript
  - No build tools or dependencies required
  - Can be opened directly in any browser

### Features Implemented in Prototype
- **Authentication Pages**
  - Login page with demo credentials
  - Register page

- **Dashboard**
  - Upcoming hunts section with countdown timers
  - Past hunts section
  - Status badges (Planning, Scouting, Active, Completed)
  - Harvested badges for successful hunts
  - Sighting and photo counts

- **Create Hunt Form**
  - Target animal, state selector, date range
  - Weapon type selection
  - Status selection
  - Solo hunt toggle with dynamic companions field
  - Notes section

- **Hunt Details Page**
  - Complete hunt information display
  - Interactive status selector buttons
  - Harvested toggle (Yes/No)
  - Delete hunt functionality
  - Sightings section

- **Animal Sightings**
  - Add sighting form with full fields:
    - Animal type, date, time
    - GPS coordinates (latitude/longitude)
    - Elevation
    - Terrain type and cardinal direction
    - Group size toggle
    - Tactics used and notes
  - Sighting display cards
  - Delete sighting functionality

### Design Details
- **Color Palette** (matching original project):
  - `#2E2D4D` (Space Indigo) - navigation, headers, dark accents
  - `#337357` (Turf Green) - primary buttons and actions
  - `#6D9F71` (Sage Green) - secondary highlights
  - `#E4E3D3` (Eggshell) - background color
- Responsive grid layouts
- Interactive hover states and transitions
- Clean, modern UI matching the original design

### Technical Details
- Single HTML file with embedded CSS and JavaScript
- Uses mock data for demonstration
- Full interactivity with JavaScript
- Data stored in memory (resets on page refresh)
- No backend or database required for prototype

### File Location
`/Users/danielleblakeman/Library/Mobile Documents/com~apple~CloudDocs/hunting-tracker/hunting-tracker-prototype.html`

### Updates - Card/Tile Selectors
- **Replaced text input for Target Animal** with visual card selector
  - 13 animal options with emojis: Deer, Elk, Moose, Bear, Mountain Lion, Turkey, Pronghorn, Wild Boar, Duck, Goose, Pheasant, Quail, Rabbit
  - Click-to-select interaction
  - Click again to deselect
  - Selected state: green border (3px) and light green background (#f0f7f2)
  - Hover effect: lifts card with shadow

- **Replaced dropdown for Weapon Type** with visual card selector
  - 6 weapon options with emojis: Rifle, Bow, Crossbow, Shotgun, Muzzleloader, Handgun
  - Same interactive card design
  - Responsive grid layout (auto-fill, min 140px)

- **Visual Design Details**:
  - Large emoji icons (2.5rem) for easy recognition
  - Smooth transitions on hover and selection
  - Cards maintain form validation through hidden inputs
  - Matches app color scheme (green accents on selection)

### Updates - Wizard Interface & Improvements
- **Converted Create Hunt form to 4-step wizard**:
  - **Step 1: What & How** - Select animal and weapon
  - **Step 2: Where** - Select state, view season info
  - **Step 3: When** - Select hunt dates
  - **Step 4: Details** - Solo/companions, status, notes

- **Process Stepper**:
  - Visual progress indicator at top
  - Clickable steps to jump between sections
  - Active step highlighted in green
  - Completed steps marked with green checkmark

- **Auto-save & Draft Functionality**:
  - Progress automatically saved to localStorage
  - "Save as Draft" button to manually save
  - Draft restored when returning to form
  - Auto-save triggers on step navigation and card selections

- **Wizard Navigation**:
  - Next/Previous buttons
  - "Create Hunt" button appears on final step
  - Cancel button with confirmation dialog
  - Smooth fade animations between steps

- **Additional Improvements**:
  - **Full state names** instead of abbreviations in dropdown (all 50 states)
  - **Date validation**: End date must be after start date
  - **Date picker restriction**: End date picker only shows dates after start date
  - Automatic clearing of end date if invalid
  - Season dates shown as informational only (not auto-filled)
  - Persistent login state using localStorage

---

## Session: April 2, 2026

### California Season Data — Official 2026 CDFW Big Game Digest
Sourced all California big game season data from the official 2026 Big Game Hunting Digest (PDF, updated 4/1/2026).

**Deer — corrected/expanded:**
- X Zones: individual entries for X1–X8 (Oct 3–Oct 18), X9A/X9B (Sep 19–Oct 12), X9C (Oct 17–Nov 8), X10 (Sep 26–Oct 11), X12 (Sep 19–Oct 12) with tag quotas and success rates
- C Zones: added — general Sep 19–Oct 25 (8,150 tags), archery A1 tag Aug 15–Sep 6 (1,945 tags)
- D Zones: split into unrestricted OTC (D3–19) and premium draw (D12, D14, D17) with correct dates
- Added premium Muzzleloader hunts (M3–MA3) and General Methods hunts (G1–G40)
- All draw entries include `applicationOpens: '2026-04-15'`

**Elk — major overhaul:**
- Replaced generic entries with specific zones: Cache Creek, La Panza, Grizzly Island, Fort Hunter Liggett, Central Coast, Owens Valley (Tule), Marble Mountains, Northwestern, Siskiyou (Roosevelt), Northeastern (Rocky Mountain), Mendocino
- Correct dates, tag quotas, success rates from brochure

**Pronghorn — corrected:** General methods Aug 22–Aug 30, Archery Aug 8–Aug 16

**Bighorn Sheep — NEW:** Desert Bighorn Dec 5–Feb 7, White Mountains Aug 15–Sep 27

**Bear — enhanced:** Added rifle general season (Sep 7–Dec 27 OTC) to wizard data

### Announcement Banners — NEW FEATURE
Date-triggered, dismissible banners on the home page:
- "CA 2026 Big Game Digest Released!" (Apr 1 – May 15)
- "CA Draw Applications Open April 15!" (Apr 2 – Apr 14)
- "CA Draw Applications NOW OPEN!" (Apr 15 – Jun 2)
- "CA Draw Deadline in Less Than 2 Weeks!" (May 20 – Jun 2)
- "CA Draw Results Available ~June 15!" (Jun 10 – Jul 15)
- "CO Primary Draw Deadline: April 7" (Mar 15 – Apr 7)

**Technical:** `renderAnnouncementBanners()` called from `loadDashboard()`. Banner data array with `showFrom`/`showUntil` dates. Dismiss via localStorage (`dismissedBanners`). CSS with gradient backgrounds per type (info/action/success/urgent).

### Hunt Status Badges on Home Page
Both draw and OTC hunt cards now show the hunt status badge (from `huntStatuses` object) directly on the home page cards. Replaces the generic "Planned Hunt" label on OTC cards. Draw cards show status below title alongside the draw results countdown.

### Nevada Added to Explorer
35 season entries: Mule Deer (archery/muzzleloader/early rifle/late rifle), Elk, Pronghorn, Bighorn Sheep (desert + California), Black Bear, Mountain Lion (OTC year-round), Turkey (spring/fall), Chukar & Quail, Rabbit. NV state profile added to States page with NDOW links. Wizard season data for deer and elk.

### TODO Updates
- Added "Biologist contact information & notes" to Hunt Details feature list
- Marked CA season data as done

---

## Future Sessions
(Notes will be added here as we continue working on the project)

### Updates - Hierarchical Animal Selection (MAJOR FEATURE)

**Implemented 3-level animal selection system:**

#### Level 1: Animal Category
13 main categories with emojis and descriptions:
- Deer 🦌
- Elk 🫎
- Moose 🫎
- Bear 🐻
- Mountain Lion 🦁
- Turkey 🦃
- Pronghorn 🦌
- Waterfowl 🦆
- Wild Boar 🐗
- Javelina 🐗
- Pheasant 🦃
- Quail 🐦
- Rabbit 🐰

#### Level 2: Subspecies (Dynamic)
Appears only for animals with subspecies:
- **Deer**: Mule, Whitetail, Coues, Blacktail, Axis
- **Elk**: Rocky Mountain, Roosevelt, Manitoban, Tule
- **Bear**: Black, Grizzly
- **Waterfowl**: Duck, Goose

Animals without subspecies (Moose, Mountain Lion, Turkey, etc.) skip directly to sex selection.

#### Level 3: Sex Selection
Species-specific terminology:
- Deer: Buck/Doe
- Elk: Bull/Cow
- Bear: Boar/Sow
- Turkey: Tom/Hen
- Waterfowl: Drake/Hen
- Pronghorn: Buck/Doe
- Wild Boar: Boar/Sow
- Javelina: Boar/Sow
- Mountain Lion: Tom/Female
- Pheasant: Rooster/Hen
- Quail: Male/Female
- Rabbit: Buck/Doe

**Wizard Restructure:**
- Expanded from 5 steps to dynamic 6-7 steps:
  1. Animal Category
  2. Subspecies (shown/hidden dynamically)
  3. Sex
  4. Weapon
  5. Where (State)
  6. When (Dates)
  7. Details (Status, companions, notes)

**Technical Implementation:**
- Created `animalHierarchy` data structure with all relationships
- Tracking variables: `selectedAnimalCategory`, `selectedSubspecies`, `selectedSex`
- Dynamic subspecies step visibility based on category selection
- Smart wizard navigation that skips hidden steps
- Dynamic max step calculation (6 or 7)
- Photo preview for categories and subspecies
- Auto-population of sex labels based on species
- Final animal string combines subspecies + sex (e.g., "Mule Deer Buck", "Rocky Mountain Elk Bull")

**JavaScript Functions Added:**
- `selectAnimalCategory()` - Handle Level 1 selection, show/hide subspecies step
- `populateSubspeciesSelector()` - Dynamically create subspecies cards
- `selectSubspecies()` - Handle Level 2 selection with photo preview
- `selectSex()` - Handle Level 3 selection, build final animal string
- `getMaxStep()` - Calculate wizard max step based on subspecies visibility
- `getNextVisibleStep()` - Navigate forward, skipping hidden steps
- `getPreviousVisibleStep()` - Navigate backward, skipping hidden steps
- Updated `goToWizardStep()` - Handle dynamic step navigation
- Updated `autoSaveWizardData()` - Include hierarchical selections
- Updated `loadWizardDraft()` - Restore all three selection levels
- Updated `resetWizardForm()` - Clear all hierarchical selections

**Apple-Style Split View:**
- When animal/subspecies selected, large photo appears on right
- Card selector collapses to single column on left
- Smooth transitions with opacity fade-in
- Description text below photo
- Preview hides when deselected

### Updates - Selection Summary Feature

**Implemented selection summary card to provide visual feedback of previous selections:**

**Features:**
- Summary card appears below wizard stepper showing user's previous selections
- Hidden on Step 1 (Animal selection)
- Visible on Steps 2-6 when there are selections to show
- Displays up to 4 items: Animal (with emoji), Weapon (with emoji), State, and Dates
- Glassmorphism styling with burnt orange accent border (#EA580C)
- Horizontal flex layout with proper spacing

**Technical Implementation:**
- Added HTML structure for `.selection-summary` with individual `.selection-item` divs
- Created `updateSelectionSummary()` function that:
  - Checks current wizard step and hides summary on step 1
  - Populates animal with category emoji and full name (e.g., "🦌 Mule Deer Buck")
  - Populates weapon with emoji (🔫, 🏹) and weapon name
  - Shows state name
  - Shows formatted date range
  - Conditionally shows/hides each item based on whether it's been selected
  - Adds `.visible` class to summary when appropriate

**JavaScript Integration:**
- Called `updateSelectionSummary()` in:
  - `goToWizardStep()` - updates when navigating between steps
  - `selectSex()` - updates when sex is selected/deselected
  - `selectWeapon()` - updates when weapon is selected/deselected
  - `state` dropdown onchange handler
  - `startDate` and `endDate` input onchange handlers
  - `loadWizardDraft()` - restores summary when loading saved draft
  - `resetWizardForm()` - hides summary when form is reset

**CSS Styling:**
- `.selection-summary`: Frosted glass background with burnt orange border
- `.selection-label`: Small uppercase burnt orange labels
- `.selection-value`: Dark indigo values with emoji support
- `.selection-emoji`: Larger emoji icons (1.2rem)
- Responsive flex-wrap layout

**User Experience:**
- Users can always see what they've selected in previous steps
- Provides context while making selections in later steps
- No need to navigate back to verify previous choices
- Summary updates in real-time as selections are made

### Updates - Moved Selection Feedback to Stepper

**Relocated selection feedback directly into wizard stepper for better visibility:**

**Implementation:**
- Removed separate summary card
- Added `.wizard-step-detail` div under each step's label
- Shows selection directly below step number and title
- Cleaner, more integrated design

**What Each Step Shows:**
- **Step 1 (Animal)**: Shows "Mule Deer" or "Elk" (category or subspecies)
- **Step 2 (Sex)**: Shows "Buck", "Bull", "Hen", etc.
- **Step 3 (Weapon)**: Shows "Bow", "Rifle", etc.
- **Step 4 (Where)**: Shows state name
- **Step 5 (When)**: Shows abbreviated date range (e.g., "Oct 25 - Nov 5")
- **Step 6 (Details)**: Shows hunt status (Planning, Scouting, Active, Completed)

**CSS Styling:**
- `.wizard-step-detail`: Small text (0.7rem), centered, gray color
- Active step detail: Burnt orange (#EA580C), bold
- Completed step detail: Sage green (#6D9F71)
- Minimum height to prevent layout shift

**Technical Changes:**
- Completely rewrote `updateSelectionSummary()` function
- Populates step details instead of summary card
- Added `onchange="updateSelectionSummary()"` to status dropdown
- Simplified logic - directly sets textContent for each step
- Date formatting uses abbreviated month names (Jan, Feb, etc.)

### Updates - Season Selector in When Section

**Moved season information from "Where" step to "When" step for better context:**

**Implementation:**
- Removed season info from Step 4 (Where - state selection)
- Added season info display to Step 5 (When - date selection)
- Shows official hunting season dates at top of step
- User's hunt dates shown separately below with "Your Hunt Dates" heading

**Display Structure:**
1. **Official Season Card** (green gradient, prominent display)
   - Season name (e.g., "General Rifle Season")
   - Official season dates (e.g., "Oct 25, 2026 - Nov 5, 2026")
2. **Your Hunt Dates Section**
   - Heading: "Your Hunt Dates"
   - Start date picker
   - End date picker

**Benefits:**
- User sees official season dates when selecting their specific hunt dates
- Prevents selecting dates outside the legal hunting season
- Clear distinction between official season and personal hunt dates
- Better workflow - state selection → weapon selection → dates with season context

**Technical Updates:**
- Updated `updateSeasonDates()` to use new element IDs: `seasonInfoWhen`, `seasonNameWhen`, `seasonDatesWhen`
- Added call to `updateSeasonDates()` in `goToWizardStep()` when navigating to step 5
- Season info automatically displays when animal + state + weapon are all selected
- Label changed from "Season Dates:" to "Official Season:" for clarity

---

## Session: February 18, 2026

### Updates - Resident/Non-Resident Selector

**Added residency status selector to Step 4 (Where):**

**Implementation:**
- Appears conditionally after a state is selected
- Two card-style buttons using existing `.animal-card` styling:
  - 🏠 **Resident**
  - ✈️ **Non-Resident**
- Same visual interaction pattern as animal/weapon selectors
- Click to select, click again to deselect
- Selection persisted in draft auto-save system

**Technical Details:**
- Added `selectedResidency` tracking variable (line 2235)
- Created `showResidencySelector()` function to conditionally display selector
- Created `selectResidency(residency)` function to handle selection with visual feedback
- Updated `autoSaveWizardData()` to include `selectedResidency` in draft data
- Updated `loadWizardDraft()` to restore residency selection and show selector if state exists
- Updated `resetWizardForm()` to clear residency selection and hide selector
- Added `showResidencySelector()` call to state dropdown's `onchange` handler

**HTML Structure (lines 1553-1566):**
```html
<div id="residencySelector" style="display: none; margin-top: 2rem;">
    <h4>Residency Status</h4>
    <div style="display: flex; gap: 1rem; max-width: 500px;">
        <div class="animal-card" onclick="selectResidency('resident')">
            <div class="animal-emoji">🏠</div>
            <div class="animal-name">Resident</div>
        </div>
        <div class="animal-card" onclick="selectResidency('non-resident')">
            <div class="animal-emoji">✈️</div>
            <div class="animal-name">Non-Resident</div>
        </div>
    </div>
</div>
```

**Rationale:**
- Hunting season dates and regulations often differ between residents and non-residents
- Provides foundation for future season data that varies by residency status
- Maintains consistent UI/UX with other card-based selectors

---

### PENDING TASK: Season Data Population

**Goal:** Pre-populate official hunting season dates based on:
- Animal type
- State
- Residency status (resident vs non-resident)
- Weapon type

**Current Status:**
- Basic `huntingSeasons` object exists with limited data (lines 1791-1909)
- Currently supports: Animal → State → Weapon → {start, end, name}
- Needs expansion to include residency variations

**Recommended Data Structure:**
```javascript
const huntingSeasons = {
    "AnimalName": {
        "StateName": {
            "resident": {
                "WeaponType": {
                    start: "YYYY-MM-DD",
                    end: "YYYY-MM-DD",
                    name: "Season Name"
                }
            },
            "non-resident": {
                "WeaponType": {
                    start: "YYYY-MM-DD",
                    end: "YYYY-MM-DD",
                    name: "Season Name"
                }
            }
        }
    }
};
```

**Accepted Data Formats:**
1. **Structured Text** (easiest):
   ```
   Montana Deer - Resident
   - Rifle: Oct 25 to Nov 5, 2026 (General Rifle Season)
   - Bow: Sep 5 to Oct 15, 2026 (Archery Season)

   Montana Deer - Non-Resident
   - Same as resident
   ```

2. **CSV/Spreadsheet**:
   ```csv
   Animal,State,Residency,Weapon,Start Date,End Date,Season Name
   Deer,Montana,resident,Rifle,2026-10-25,2026-11-05,General Rifle Season
   ```

3. **Direct JSON** (for complete data sets)

**Implementation Plan (when data is provided):**
1. Update/expand `huntingSeasons` object with new data structure
2. Modify `updateSeasonDates()` function to:
   - Check `selectedResidency` variable
   - Look up season using: animal → state → residency → weapon
   - Display appropriate season dates in Step 5 (When)
3. Handle subspecies by mapping to base animal categories
4. Gracefully handle missing data (hide season card if no data available)

**Notes:**
- Data can be added incrementally (start with most-hunted states/animals)
- If resident and non-resident seasons are identical, can note that for efficiency
- Season names provide helpful context (e.g., "Early Archery", "General Rifle", "Youth Season")
- Dates should be for 2026 to match prototype's timeframe

**Next Steps:**
- User will compile comprehensive season date information
- Format can be flexible (any of the three options above)
- Focus on accuracy for primary hunting states first

---

## Session: May 7, 2026

### What We Did
End-to-end test and hardening of the **Plan This Hunt flow** (Explorer season card → home page + season plan + huntMap view).

### Bugs Found & Fixed (commit 2ac665a)

1. **Duplicate hunt UX** (`planHuntFromExplorer` line ~13694)
   - Was: native `alert('This hunt is already on your home page.')` + `showPage('dashboard')`
   - Now: opens the existing hunt (huntMap if in `seasonPlanHunts`, huntDetails fallback). Also now checks both `mockHunts` **and** `seasonPlanHunts` before returning — prevents the asymmetric-dup-check case where a seasonPlan existed without a matching mockHunt.

2. **`currentMapHuntId` not persisted** (line ~13752 and line ~13864 manual hunt entry)
   - Was: `currentMapHuntId = planHunt.id; showPage('huntMap');` — only the in-memory var was set, relied on `beforeunload` to save.
   - Now: uses `openHuntMap(planHunt.id)` which writes to `localStorage.currentMapHuntId` immediately. Applied to both `planHuntFromExplorer` and the manual hunt entry flow for consistency.

3. **`tagType` missing from duplicate match** (three `.find()` calls)
   - Was: state + animal + weapon only — "CA Deer Archery OTC" and "CA Deer Archery Draw" treated as duplicates.
   - Now: a `matchesTag` helper compares `(t || 'otc') === (tagType || 'otc')` in all three lookups. OTC and Draw variants are distinct hunts.

4. **Residency lost on plan** (signature + button + both hunt objects)
   - Was: Explorer season data has `s.residency` (resident/non-resident), but button didn't pass it and `planHuntFromExplorer` didn't capture it.
   - Now: button passes `s.residency`, `planHuntFromExplorer` accepts it as 9th param, stored as `residency` field on both `mockHunts` and `seasonPlanHunts` entries.

5. **Zone lost on plan** (signature + button + both hunt objects)
   - Was: `s.zone` was concatenated into `seasonName` for display and buried in `notes`. No structured field — couldn't tie into "My Zones of Interest" or map.
   - Now: button passes `s.zone`, `planHuntFromExplorer` accepts as 10th param, stored as `zone` field on both hunt objects. Also updated `planZoneHunt` (CA deer zone map) to pass zone structurally.

### Files Changed
- `hunting-tracker-prototype.html` — `planHuntFromExplorer` function (+ button + `planZoneHunt` wrapper)
- `TODO.md` — checked off "Test Plan This Hunt flow end-to-end", added completed entry

### Deployed
- Backup: `backups/prototype-2026-05-05-1426.html`
- Commit `2ac665a` pushed to `origin/main`
- Live at https://dannyeliza.github.io/hunting-tracker/hunting-tracker-prototype.html

### Known Remaining (not addressed this session)
- Legacy `startHuntFromExplorer` (line ~13875) still passes only 8 args — safe because residency/zone default to `''`, but nothing actually calls it from what I saw.
- Other callers of `openHuntMap` are fine; the helper is now the canonical nav-to-hunt path.
- No UI yet reads the new `residency` / `zone` fields — they're stored but not displayed. Surfacing them on hunt cards / detail header is a follow-up.

### Candidate Next Features (from TODO)
1. Draw Strategy / Dependencies flow (if/then draw decision tree) — highest product value
2. Interactive US map state selector (SVG replacing Explorer card grid)
3. Observation insights (auto-summary of sightings/sign/trail cam)
4. Edit past hunt details
5. Zone/unit selector in wizard
6. Dark mode

