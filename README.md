```
                                  ___  ______  _____  ___
                                 / _ \ | ___ \|  ___|/ _ \
                                / /_\ \| |_/ /| |__ / /_\ \
                                |  _  ||  __/ |  __||  _  |
                                | | | || |    | |___| | | |
                                \_| |_/\_|    \____/\_| |_/

                                      ____  ___
                                     |___ \/ _ \
                                       __) | | | |
                                      / __/| |_| |
                                     |_____|\___/

```

**APEX** is a front-end fan portal for the 2026 FIA Formula 1 World Championship. It brings together live timing, session streams, championship standings, driver profiles, race calendar, circuit guides, and team data in a dark, data-forward interface inspired by F1 pit-wall timing screens.

---

## Design Direction

The interface is built around a single question: *What if the F1 timing screen became a web UI?*

| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0d1014` | Page background |
| `--bg-elevated` | `#151a20` | Cards, surfaces |
| `--red` | `#e10600` | F1 brand accent |
| `--teal` | `#00d2be` | Data accent (timing screen green) |
| `--display` | Barlow Condensed | Headings, large numerals |
| `--body` | Inter | Body text |
| `--mono` | JetBrains Mono | All data, timing, labels |

Typography choices are deliberate: Barlow Condensed for compact, impactful headlines; JetBrains Mono for the timing strip and data tables to match broadcast graphics; Inter for readable body text.

---

## Pages

| Page | Path | Content |
|---|---|---|
| **Live** | `index.html` | Hero, live streams with multi-source player, weekend schedule, standings preview, highlights grid with video modal, telemetry data cards |
| **Standings** | `standings.html` | Full driver (22) + constructor (11) championship tables with proportional points bars |
| **Drivers** | `drivers.html` | 22-driver card grid, hash-routed detail pages with bio, career stats, race results, and highlights |
| **Calendar** | `calendar.html` | 22-round calendar with session schedules, sprint labels, and status indicators |
| **Tracks** | `tracks.html` | 22 circuit cards with track maps and technical specifications |
| **Teams** | `teams.html` | 11 constructor cards, tyre compound display, DRS info, points reference |

---

## Architecture

```
f1-stream.html          (original single-file prototype, preserved for reference)
index.html               homepage — streams, schedule, standings, highlights
standings.html           full championship tables
drivers.html             driver grid + detail views
calendar.html            race calendar with session times
tracks.html              circuit directory
teams.html               constructor + tyre + rules reference
style.css                shared design system and component styles
data.js                  all F1 2026 structured data
f1-logo.svg              F1 logotype
```

- **Zero build step.** Open any `.html` file directly in a browser.
- **No frameworks, no bundlers, no npm.** Pure HTML, CSS, and JavaScript.
- **Shared design system.** `style.css` defines all tokens and component styles consumed by every page.
- **Inline page logic.** Each HTML page contains its own `<script>` block for page-specific rendering, sharing data from `data.js`.
- **External API.** Live session streams are fetched from `streamed.pk/api` with F1-specific filtering and multi-source fallback.

---

## Signature Feature — The Timing Strip

A persistent top-10 driver positions ticker inspired by the F1 live timing broadcast graphic. Fixed below the nav on every page. Displays position number, team color dot, driver abbreviation, and gap time. Hidden on mobile (<680px). This is the deliberate aesthetic risk of the project — no other F1 fan site renders a telemetry-style timing strip as a persistent navigation element.

---

## Accessibility

- Skip-to-content link on every page
- ARIA roles and states on all tab interfaces (`role="tablist"`, `role="tab"`, `aria-selected`)
- `aria-live` regions on dynamic timing strip content
- Keyboard-activatable tab controls (Enter key)
- `prefers-reduced-motion` support disabling all animations
- `:focus-visible` outlines with teal highlight
- Responsive down to mobile breakpoints at 680px and 900px
- Touch targets minimum 44px at mobile breakpoints

---

## Data

All championship data, driver profiles, circuit specs, and calendar information for the 2026 season is hardcoded in `data.js`. Driver photos are served from the official F1 media CDN with Wikimedia Commons fallbacks. Track map images are sourced from Wikimedia Commons. Highlight video thumbnails use YouTube's thumbnail API.

---

## Running Locally

```bash
# Serve with any static file server, for example:
npx serve .
# or
python -m http.server 8000
# or
npx live-server
```

Open the served URL in a browser and navigate between pages via the top nav.
