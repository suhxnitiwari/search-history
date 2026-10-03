# 8,730 Questions

*If all you had was my search history, could you figure out who I am?* **An attempt to reconstruct one person from the questions she asked the internet.**

**Live:** [suhxnitiwari.github.io/search-history](https://suhxnitiwari.github.io/search-history/)

**8,730 questions · 12,460 searches · 85,443 pages · 2,047 videos · 297 files I made · two Google accounts · Oct 2025 – Oct 2026**

The follow-up to [Heavy Rotation](https://suhxnitiwari.github.io/listening-galaxy/), my Spotify galaxy.

## The investigation

Fourteen questions, each one earning the next. Every chapter has a **More info** panel with its data sources, methods and a privacy rating.

1. **The interrogation:** the evidence, and a search bar that takes you to any question
2. **What's on my browser?** My pink theme (decoded from Chrome settings), 473 open tabs, a bookmark bar built from my data, and the apps I favorite vs. the ones I use
3. **What gets my attention?** An Obsession Index, not a top-10 list
4. **How do I get curious?** Real question chains, typos included
5. **How deep is deep?** Anatomy of a 9h 54m rabbit hole
6. **When am I me?** Guess my bedtime, then watch my day hour by hour
7. **Can search history identify my roles?** Evidence boards you can vote on
8. **What would Google get wrong?** Real mistakes made while analyzing this data
9. **So what does a search reveal?** My search vocabulary
10. **Can you watch me learn?** From my first Python notebook to my own projects
11. **Which searches escaped the browser?** A summer at Oracle, five trips and a map of eleven I only searched flights for
12. **Can Google watch someone change?** Month by month, and life events found without being told
13. **You think you know me? Prove it.** What did I search next?
14. **So… could you?**

## The data engineering

The pipeline lives on my laptop with the raw data; only its small output, `data.json`, is published.

- **Extract:** two Google Takeout exports (Chrome, YouTube, Maps reviews, Drive file titles and dates, calendar times, Chrome settings, bookmarks and synced tabs). Review text, file contents and calendar titles are never read.
- **Transform:** Austin time, de-duplication, sessions (a new one after 30 quiet minutes), questions (back-to-back searches that share a word), and repeat detection: 7,138 of 19,598 search page loads were Chrome re-logging a results page, not new searches.
- **Model:** a SQLite star schema (`fact_event` with date, query, session and question dimensions) with integrity checks.
- **Analyze:** an Obsession Index (geometric mean of log-scaled frequency, repeat days, session depth, variety and estimated time), question-chain metrics, rabbit-hole ranking, a search vocabulary, month-to-month change by Jensen–Shannon divergence, and anomaly detection that found my build sprint and my New York trip from activity counts alone.
- **Export:** `data.json` (25 KB) with counts, charts and only hand-approved searches, plus a guardrail that fails the export if any quoted search isn't word for word in my data.

## How it's built

- **A search bar that answers questions.** The box filters the investigation's questions by title and keywords as you type, so "sleep" or "oracle" finds the right chapter.
- **"Did you mean…?"** When nothing matches, the query is compared to every question and keyword with a Levenshtein edit-distance function (dynamic programming), and the closest one is offered if it's within two edits. Misspell "oracle" and it still finds you.
- **Accessible combobox.** Arrow keys, Enter and Escape drive the suggestion list, with `aria-expanded`, `aria-activedescendant` and `aria-selected` kept in sync. Chart bars and hour columns are focusable and labeled for screen readers, and every More info panel is a native `<dialog>`.
- **Data-driven page.** Every chapter is rendered from `data.json`, so rerunning the pipeline updates the whole site.
- **Motion with care.** Numbers count up with `requestAnimationFrame`, charts grow in as they scroll into view, question chains type themselves out and the trip arcs draw themselves; all of it turns off under `prefers-reduced-motion`.
- **No framework.** HTML, CSS and plain JavaScript in `index.html`, with the charts and the map built from plain HTML, CSS and SVG.

## Data and privacy

Nothing is shown unless it was approved by hand: no names of real people, nothing about health, religion, politics, relationships, money or IDs, no hotel names, and no company names except Oracle, which is already on my résumé. "Sleep" is the longest stretch each night with no activity across my laptop and phone, not measured sleep. Searches, pages and videos come from my personal account; files, calendar and an upload come from my UT account.

## Design choices

- **The interface is the metaphor.** The data came from a search engine, so the investigation opens on a search bar, and the browser chapter is drawn in my own pink Chrome theme.
- **An investigation, not a dashboard.** Each chapter answers a smaller question that earns the next one, and the story breaks its own model in "What would Google get wrong?" before it reaches a conclusion.
- **Episodes.** The navigation and the More info panels borrow the shape of a streaming app's episode pages: what it's about, who's in it (the data), what genre it is (the methods) and its rating (what it keeps private).

## Tech stack

Python and SQLite (pipeline, on my laptop) · HTML · CSS · vanilla JavaScript · SVG · GitHub Pages. Not affiliated with Google.

## Ownership

© 2026 Suhani Tiwari. All rights reserved. See [LICENSE](LICENSE).

Built by [Suhani Tiwari](https://suhanitiwari.com).
