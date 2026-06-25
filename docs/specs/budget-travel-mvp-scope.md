# Product Scope: Budget-First Travel Discovery

## Working Name

Leeway

This is an internal working name, not a cleared public brand. It fits the current direction because the app is about finding room in a budget, a calendar, and a set of travel constraints.

Name check note: plain `Leeway` is not recommended as a public app name after preliminary trademark, app-store, domain, and search checks. The name has strong semantic fit, but there are exact app-name collisions and domain conflicts. See [budget-travel-leeway-name-check.md](budget-travel-leeway-name-check.md).

Naming exploration is included near the end of this document.

## One-Line Pitch

Find trips that fit your real budget, not just cheap flights.

## Product Thesis

Most travel tools start with a destination or a booking search. Budget-conscious travelers often start somewhere fuzzier:

> I have this much money. I am flexible. Where and when can I realistically go?

The MVP should help a user compare feasible trips before they start booking. It should not try to become an OTA, itinerary generator, or full travel super-app.

The useful product is a trip feasibility board:

- It compares destination options.
- It models total trip cost, not just airfare.
- It shows date flexibility and origin-airport tradeoffs.
- It explains when transit is feasible and when a rental car should be budgeted.
- It lets the user edit assumptions instead of trusting a black-box answer.
- It links out for verification instead of owning booking.

## Target User

Primary user:

- Budget-conscious leisure traveler.
- Wants value, but is not a serious couponer or deal-maximizer.
- Has some flexibility on destination, timing, or departure airport.
- Wants to avoid surprise costs.
- Is willing to verify prices, but wants the comparison work organized.

Good early use cases:

- "I have $900 and want a 4-5 day trip sometime this year."
- "I want somewhere warm, but I can travel in whichever month is cheapest."
- "I can leave from one of three nearby airports if the savings are real."
- "I do not know whether this destination is cheap if I need a car."
- "I want a shortlist of realistic trips, not 40 tabs."

Less ideal early users:

- Fixed-destination business travelers.
- People who only want luxury inspiration.
- People who expect exact live prices inside the app.
- Expert points-and-miles users.
- Users who want booking and customer support inside the product.

## MVP Principle

The MVP should answer:

> Is this trip realistically doable within my budget?

It should not answer:

> Can I book this entire trip here?

That distinction keeps the product practical for a solo builder and keeps the user promise honest.

## Core Inputs

### Budget

- Total trip budget.
- Currency.
- Number of travelers.
- Optional buffer percentage.
- Optional "hard cap" versus "preferred max."

### Trip Length

- Exact number of nights.
- Range of nights, such as 3-5 nights.
- Optional weekend or long-weekend preference.

### Time Flexibility

Dates should be optional. Users should be able to plan around budget instead of forcing the budget into fixed dates.

Modes:

| Mode | User Intent | Example |
| --- | --- | --- |
| Exact dates | User has fixed PTO or an event. | March 12-17 |
| Flexible window | User knows the rough window. | 4-6 days in October |
| Budget-first / no dates yet | User wants the cheapest realistic season or month. | Warm 5-day trip sometime this year |

Budget-first output should show:

- Cheapest months or seasons.
- Best value window.
- Weather tradeoffs.
- High-season warnings.
- "Go then, not then" recommendations.

Example:

```text
Mexico City
Best budget window: February-April
Estimated total: $760-$930
Why: moderate flights, lower lodging, strong transit, low food cost
Watch out: Easter week can spike lodging and airfare
Weather: mild, lower rain risk
```

### Departure Flexibility

Origin should not be limited to one airport. Many budget travelers can drive 30-90 minutes to save money, but the app should compare net savings instead of only showing cheaper fares.

Modes:

| Mode | User Intent | Example |
| --- | --- | --- |
| Single airport | User only wants one departure option. | ATL only |
| Nearby airports | User wants airports within a drive-time radius. | Compare airports within 60 minutes |
| Custom origin set | User knows which airports are practical. | ATL, BHM, CHA, GSP |

The app should calculate:

- Flight price difference.
- Extra driving time.
- Gas estimate.
- Parking estimate.
- Tolls if applicable.
- Net savings.
- Whether the cheaper airport is worth the tradeoff.

Example:

```text
Departure comparison
ATL: $340 flight, easiest option
BHM: $220 flight, +$70 drive and parking estimate
Net savings: about $50
Verdict: maybe worth it
```

Labels:

- Best overall.
- Cheapest.
- Not worth the drive.
- Worth it only if saving at least $X.

### Destination Constraints

- Domestic, international, or either.
- Region preferences.
- Passport required okay or not okay.
- Beach, city, nature, food, culture, event, family visit, or no preference.
- Avoid list.
- Safety or accessibility notes as manual fields at first.

### Travel Style

- Budget.
- Normal value.
- Comfortable but cost-aware.

This should influence food, lodging, activity, and buffer estimates.

### Lodging Style

- Hostel.
- Budget hotel.
- Midrange hotel.
- Apartment / vacation rental.
- Flexible.

MVP should use rough bands first. Full hotel inventory is not needed to prove the product.

### Weather Preference

- Warm.
- Mild.
- Cool.
- Avoid rain.
- Avoid extreme heat.
- No preference.

Weather should affect feasibility, especially in budget-first date mode.

### Ground Mobility Feasibility

Do not ask the user to choose "no rental car" or "rental car okay" upfront. The app should show both realities so the user can decide.

Each destination should answer:

> Can I realistically do this trip without renting a car?

The card should show:

- Public transit feasibility.
- Airport-to-lodging-area transfer estimate.
- Walkability around likely lodging areas.
- Rideshare/taxi fallback risk.
- Rental car daily estimate.
- Parking estimate.
- Car-needed verdict.

Verdicts:

- No car needed.
- Car optional.
- Car recommended.
- Car likely required.

Example:

```text
Ground mobility
Transit feasible
Public transit estimate: $42 total
Airport transfer: $8 each way
Walkability: strong
Rental car estimate: $280 total
Parking risk: medium
Verdict: skip the car unless you plan day trips
```

Example:

```text
Ground mobility
Transit weak
Public transit estimate: $95 total, but limited coverage
Airport transfer: $45 rideshare likely
Rental car estimate: $360 total
Parking risk: low
Verdict: budget as if you need a car
```

## Core Output: Destination Feasibility Cards

Each destination should have a card that summarizes the decision.

Card fields:

- Destination.
- Best time window.
- Best departure option.
- Estimated total trip cost.
- Budget fit: strong fit, possible, risky, over budget.
- Cost breakdown.
- Ground mobility verdict.
- Weather fit.
- Biggest budget risks.
- What makes this work.
- What could break the budget.
- Confidence level.
- Verification links.

Example:

```text
Chicago
Budget fit: strong fit
Best window: late September or early October
Best departure: ATL unless BHM saves $120+
Estimated total: $720-$910

Cost breakdown
Flight: $180-$280
Lodging: $105/night x 4
Food: $45/day
Transit: $30-$50 total
Activities and buffer: $120

Ground mobility
No car needed
Strong public transit, walkable neighborhoods, airport train available
Rental car estimate: $340+ with parking risk

Why this works
Good transit keeps local costs low. Flexible fall dates may avoid peak lodging.

What could break the budget
Weekend hotel prices, events, checked bags, airport choice.
```

## MVP Features

### 1. Trip Board

- Create a board for one trip search.
- Store budget, traveler count, time flexibility, departure flexibility, preferences, and notes.
- Example board name: "Warm 5-day trip under $900."

### 2. Destination Shortlist

- Start with a manually seeded list of destinations.
- Show 5-10 destination cards per board.
- Let user pin, hide, or mark destinations as verified.

### 3. Total Cost Model

Estimate:

- Flight or primary transport.
- Lodging.
- Food.
- Ground mobility.
- Activities.
- Fees and buffer.

The model should produce ranges, not false precision.

### 4. Time Flexibility Comparison

- Exact dates.
- Flexible month/window.
- Budget-first, no dates yet.
- Show cheapest or best-value months.
- Include weather tradeoffs and seasonal risk notes.

### 5. Departure Flexibility Comparison

- Single airport.
- Nearby airport radius.
- Custom origin airport set.
- Net savings calculation.
- "Worth the drive?" verdict.

### 6. Ground Mobility Feasibility

- Always show public transit and rental car paths.
- Do not force the user to pre-choose.
- Make car dependency visible as a budget risk.

### 7. Editable Assumptions

Every estimate should be editable:

- Flight.
- Lodging nightly rate.
- Food per day.
- Local transit.
- Rental car.
- Parking.
- Activities.
- Buffer.

Editing assumptions should instantly update:

- Total estimate.
- Budget fit.
- Risk label.
- Comparison ranking.

### 8. Verification Links

The app should link out instead of owning booking.

Useful links:

- Flight search.
- Lodging search.
- Weather.
- Transit or route check.
- Destination cost references.
- Notes or manual research links.

### 9. Comparison Mode

Let the user compare 3-5 pinned destinations:

- Total estimated cost.
- Cheapest plausible cost.
- Most likely cost.
- Best date window.
- Best departure airport.
- Transit feasibility.
- Rental car cost.
- Weather fit.
- Biggest risk.
- Confidence.

### 10. Saved Notes

- Add notes per destination.
- Mark facts as manually verified.
- Record last checked date.
- Track why a destination was rejected.

## AI Role

AI should be optional and subordinate to the cost model.

Good AI uses:

- Turn a messy request into structured constraints.
- Summarize why a destination fits or fails.
- Explain budget risks in plain language.
- Convert pasted research notes into structured warnings.
- Generate a short comparison summary from existing card data.

Bad AI uses:

- Inventing prices.
- Acting as the pricing source.
- Recommending bookings without verification links.
- Creating generic itineraries before feasibility is proven.

The simplest version can be built with no AI. AI can make the product easier to use later, but the core value is structured trip math.

## Data Strategy

Start lightweight:

- Seed destinations manually.
- Use rough city-level lodging and food bands.
- Let users enter flight prices manually.
- Use deep links for verification.
- Use weather APIs for date-window context.
- Use manual transit/car notes first.

Add later:

- Flight price API if cost and access are reasonable.
- Airport radius search.
- Route or transit API.
- Lodging estimate source.
- Historical seasonality data.
- Points and miles guidance.

## Non-Goals

- No booking.
- No price alerts.
- No customer support burden for travel reservations.
- No full hotel inventory.
- No full live flight inventory.
- No account sync in the first build.
- No itinerary builder in the first build.
- No social sharing in the first build.
- No points account linking.
- No claims of exact current prices unless verified.

## First Build Path

### Build 1: Manual Feasibility Board

- Trip board.
- User inputs.
- Manual destination cards.
- Editable assumptions.
- Cost model.
- Comparison mode.
- Notes and verification links.

Goal:

> Replace the spreadsheet for one real trip decision.

### Build 2: Better Discovery

- Seeded destination database.
- Budget-first date windows.
- Nearby airport comparison.
- Ground mobility labels.
- Weather fit.

Goal:

> Suggest plausible destinations before the user knows where to go.

### Build 3: Data Assist

- Weather API.
- Airport lookup.
- Route checks.
- Optional flight estimate integration.
- Better lodging and food bands.

Goal:

> Reduce manual entry without becoming a booking platform.

### Build 4: AI Assist

- Natural-language trip setup.
- Risk summaries.
- Research-note parsing.
- Plain-English comparison.

Goal:

> Make the app easier to use, not magically smarter than its data.

## Validation Questions

- Does this beat a spreadsheet for choosing between destinations?
- Does date flexibility make the recommendations meaningfully better?
- Does nearby-airport comparison change decisions?
- Do users trust cost ranges when assumptions are visible?
- Does the ground mobility verdict prevent fake-cheap trips?
- Are verification links enough, or do users expect live inventory?

## Naming Direction

Desired tone:

- Flowy.
- Fluid.
- Practical.
- Budget-aware without sounding cheap.
- Useful for regular people, not extreme deal hunters.
- Travel-adjacent, but not too generic.

Avoid:

- Coupon language.
- Luxury language.
- Overly playful names.
- Names that sound like a booking agency.
- Names that imply exact live fares or guaranteed deals.

## Name Iterations

| Name | Tone | Why It Fits | Risk |
| --- | --- | --- | --- |
| Leeway | Practical, flexible, calm | Means room to maneuver. Works for budget, dates, and origin flexibility. | May have existing usage in many categories. |
| Wayline | Modern, directional | Suggests a path through options without sounding cheap. | Slightly abstract. |
| Wayfare | Travel-forward, elegant | Combines travel and fare naturally. | Very close to Wayfair visually and phonetically. |
| Within | Minimal, budget-aware | Suggests staying within budget and constraints. | Broad and likely hard to search for. |
| Veya | Light, fluid, modern | Invented name with travel energy. | Needs explanation and clearance. |
| Roam | Minimal, travel-native | Cleanly captures movement, freedom, and open-ended travel. | Drop for public naming; heavily used across software, mobile connectivity, travel/hospitality, and luggage. |
| RoamIn | Short, casual, roam-rooted | More distinctive than plain `Roam`; suggests roaming within a budget, season, or destination constraint. | Keep as secondary candidate; can read as `Roam In`, `roamin'`, or `roaming`. |
| Roamable | Fluid, practical, possibility-focused | Says the app finds trips that are actually possible within budget, timing, airport, weather, and transit constraints. | Drop for public naming after clearance check found active exact-name travel eSIM use at `roamable.co`. |
| Roamwell | Warm, practical | Suggests traveling well without excess. | A little softer, less tool-like. |
| Routewell | Practical, directional | Suggests choosing the route that actually works. | Could sound like logistics or route-optimization software. |
| TripScope | Clear, utility-forward | Says the app scopes a trip before booking. | More tool-like than brand-like. |
| Tripspan | Flexible, range-oriented | Works for date span, budget span, and trip length span. | Less elegant as a spoken brand. |
| Pathspan | Abstract, range-oriented | Combines path and range without being booking-coded. | Less immediately travel-readable. |
| Tripwise | Clear, practical | Says smart trip decisions directly. | Less distinctive. |
| Fareline | Cost-aware, structured | Suggests fares and comparison lines. | More flight-focused than total-trip-focused. |
| OpenRoute | Practical, flexible | Good for flexible travel discovery. | Could sound like maps/logistics software. |
| Range | Simple, flexible | Works for price ranges, date ranges, airport ranges. | Very generic. |
| Goable | Plain, human | Directly says "this trip is doable." | Casual and potentially less polished. |
| Drift | Flowy, flexible | Captures open-ended travel exploration. | Less practical and may imply aimlessness. |

## Current Name Recommendation

Use `Leeway` as the internal working name only. Do not treat it as the public launch name.

Why:

- It does not sound like a coupon app.
- It captures flexible planning.
- It fits the product's real job: finding room in the user's budget and calendar.
- It can support phrasing like:
  - "Find your travel leeway."
  - "Trips with room to breathe."
  - "See where your budget can take you."

Current Xcode/project working title:

`RoamIn`

This is acceptable as a project name while the public brand is still being checked. The Xcode project, target, bundle identifier, and App Store display name can diverge later if needed.

Current public-name candidates to check next:

1. Roamwell
2. Routewell
3. RoamIn
4. Roamspan
5. Roamway
6. TripScope

Preliminary trademark, App Store, Google Play, domain, and SEO checks for `Leeway` are captured in [budget-travel-leeway-name-check.md](budget-travel-leeway-name-check.md). The `Latitude` check is captured in [budget-travel-latitude-name-check.md](budget-travel-latitude-name-check.md). The first post-Latitude batch is captured in [budget-travel-name-check-batch-1.md](budget-travel-name-check-batch-1.md). The dedicated `Roamwell` check is captured in [budget-travel-roamwell-name-check.md](budget-travel-roamwell-name-check.md). The roam-family pass is captured in [budget-travel-roam-family-name-pass.md](budget-travel-roam-family-name-pass.md). The failed `Roamable` clearance check is captured in [budget-travel-roamable-clearance-check.md](budget-travel-roamable-clearance-check.md). The plain `Roam` check is captured in [budget-travel-roam-name-check.md](budget-travel-roam-name-check.md). The `RoamIn` check is captured in [budget-travel-roamin-name-check.md](budget-travel-roamin-name-check.md).

Current naming recommendation:

Keep `Leeway` as the internal codename, but move `Roamwell` back into the lead public-name position after `Roamable` failed preliminary clearance and plain `Roam` proved too crowded. `Roamable` had the best product meaning, but active exact-name travel eSIM use at `roamable.co` makes it too risky. Plain `Roam` has broader software, mobile, hospitality, and luggage collisions. `Roamwell` is not cleared yet; it still needs direct USPTO, App Store, Google Play, WIPO, and domain registrar checks before public use.
