# Search History

*A year of my Google searches, inside my own browser. Ask it anything about me.*

**Live:** [suhxnitiwari.github.io/search-history](https://suhxnitiwari.github.io/search-history/)

**12,460 searches · 85,443 pages · 2,047 videos · 297 files I made · two Google accounts · Oct 2025 – Oct 2026**

The follow-up to [Heavy Rotation](https://suhxnitiwari.github.io/listening-galaxy/), my Spotify galaxy.

## How it works

The page is my Chrome window. You type the questions; the data answers them. The bookmark bar is the navigation, and each bookmark wears the favicon of the site whose data drives it.

1. **Hours:** every search of the year on one clock you can drag: what I search at each hour, when I search most (9 PM) and when my last search of the night comes
2. **Days:** 365 days, one favicon each, for the site that owned the day
3. **Most visited:** sites sized by how many days I opened them, with when I open each one
4. **Travel:** a world map of 107 places I searched (home, the trips I took, where I might study abroad, everywhere else), with the trips found from airport and "near me" searches
5. **Watchlist:** 37 shows, movies and books I looked up, from searches and streaming history (Netflix never names titles, so only searched ones appear)
6. **Rabbit hole:** replay two sittings where one search led somewhere else: planning December in New York, and pricing life after graduation in three cities
7. **Mind:** psychology as a possible interest, and the 202 self-help videos I watched, as themes and counts only
8. **Learning:** my UT account's file trail, from a first Python notebook to React and a backend
9. **Career:** how a search for Oracle internships became an internship

## The data engineering

The pipeline lives on my laptop with the raw data; only its small output, `data.json`, is published.

- **Extract:** two Google Takeout exports (Chrome, YouTube, Maps reviews, Drive file titles and dates, calendar times, Chrome settings, bookmarks and synced tabs). Review text, file contents and calendar titles are never read.
- **Transform:** Austin time, de-duplication, sessions (a new one after 30 quiet minutes), questions (back-to-back searches that share a word), and repeat detection: 7,138 of 19,598 search page loads were Chrome re-logging a results page, not new searches.
- **Model:** a SQLite star schema (`fact_event` with date, query, session and question dimensions) with integrity checks.
- **Analyze:** an Obsession Index (geometric mean of log-scaled frequency, repeat days, session depth, variety and estimated time), question-chain metrics, rabbit-hole ranking, a search vocabulary, month-to-month change by Jensen–Shannon divergence, and anomaly detection that found my build sprint and my New York trip from activity counts alone.
- **Export:** `data.json` (25 KB) with counts, charts and only hand-approved searches, plus a guardrail that fails the export if any quoted search isn't word for word in my data.

## How it's built

- **166 suggested questions,** grouped by chapter, every one checked to land on a real answer: when and where, then what kind of person the data shows (taste, beauty, coffee, standards, five versions of her by hour, eras, curiosity, decisions, both things are true, what survived), ending on what Google would predict next.
- **A search bar that answers in plain English.** It reads times ("3 AM", "midnight"), dates ("Oct 26"), nights of the week, cities, any site name and topics like Oracle or React, then answers with a featured-snippet card that opens the chapter at that exact point: the clock hand on 3 AM, Oct 26 lit up in the Days grid, the Chicago trip selected.
- **It guides, it never types for you.** Suggestions filter as you type, Tab accepts an inline completion, and "People also ask" offers next questions.
- **"Did you mean…?"** When nothing matches, each word is compared to the vocabulary with a Levenshtein edit-distance function, so "chikago" still finds Chicago.
- **The clock.** 12,460 searches drawn on a canvas as a spiral (midnight at the top, the year growing outward), topic bars around it in SVG, and the favicon most typical of each hour on the rim (its share of that hour divided by its share of the year).
- **Data-driven page.** Everything renders from `data.json`, so rerunning the pipeline updates the whole site. Favicons are embedded in it, so the page makes no third-party requests for them.
- **Browser-like navigation.** Back, forward and reload work inside the page, chapters you've opened turn grey, keys 1–9 jump between chapters and `/` focuses the address bar.
- **No framework.** HTML, CSS and plain JavaScript in `index.html`, with charts in Canvas, SVG and CSS.

## Data and privacy

Nothing is shown unless it was approved by hand: no names of real people, nothing about health, religion, politics, relationships, money or IDs, no hotel names, and no company names except Oracle, which is already on my résumé. "Sleep" is the longest stretch each night with no activity across my laptop and phone, not measured sleep. Searches, pages and videos come from my personal account; files, calendar and an upload come from my UT account.

## Design choices

- **The interface is the metaphor.** The data came from my browser, so the site is my browser: tab strip, address bar, bookmark bar and new-tab page.
- **Favicons are the color.** The frame stays quiet ivory and walnut; the real favicons of the sites I use bring the color.
- **The visitor asks.** Nothing plays on its own: every chapter is something to drag, step through or click.

## Tech stack

Python and SQLite (pipeline, on my laptop) · HTML · CSS · vanilla JavaScript · SVG · GitHub Pages. Not affiliated with Google.

## Ownership

© 2026 Suhani Tiwari. All rights reserved. See [LICENSE](LICENSE).

Built by [Suhani Tiwari](https://suhanitiwari.com).
