# Search History

*What does a year of searching say about me?*

**Live:** [suhxnitiwari.github.io/search-history](https://suhxnitiwari.github.io/search-history/)

## What it is

A year of my Google data, asked like a search bar. The page types "suhani is…" by itself and autocompletes into
what the data found: when I go offline each night, what I search at 3 AM, which day I get the most done, and how I
went from my first line of Python to shipping my own products.

**105,092 pages · 19,626 searches · 1,974 videos · 297 files · two Google accounts · Oct 2025 – Sep 2026**

The follow-up to [Heavy Rotation](https://suhxnitiwari.github.io/listening-galaxy/), my Spotify galaxy.

## What it answers

Thirteen autocomplete answers, each its own small data story:

- **a builder:** the dated path from a product pitch, to my first Python notebook (46 notebooks in one semester), to React, to my own data products, with visits to my own projects by quarter going 0 → 8 → 129 → 3,755
- **a night owl:** my typical offline window for each night of the week
- **most productive on thursdays:** median productive actions per weekday, and what I'm most likely doing each day
- **in beauty mode at 3 am:** my searches hour by hour with the top topic for each hour, plus a "Play my day" button that walks the clock
- **dreaming of nyc**, **a marketer**, **a networker**, **up all night for what matters**, **an artist**, **a baker**, **a published author**, **an explorer**, **always misspelling austin**

## How it's built

- **A real autocomplete.** The search box filters answers by prefix and substring as you type, bolding the part you
  haven't typed yet, like Google does.
- **"Did you mean…?"** When nothing matches, the query is compared to every answer with a Levenshtein edit-distance
  function (dynamic programming), and the closest one is offered if it is within a length-scaled threshold. Misspell an answer and it still finds you.
- **Accessible combobox.** Arrow keys, Enter and Escape drive the suggestion list, with `aria-expanded`,
  `aria-activedescendant` and `aria-selected` kept in sync. Chart bars and hour columns are focusable and
  labeled for screen readers.
- **Shareable answers.** Every result updates the URL hash (`#a-night-owl`), so a link opens straight to that answer.
- **Motion with care.** Numbers count up with `requestAnimationFrame`; the typing intro and card animations turn off
  under `prefers-reduced-motion`.
- **No framework, one file.** All of it is HTML, CSS and plain JavaScript in `index.html` (~47 KB).

## Data and privacy

Two Google Takeout exports (Chrome, YouTube, Drive file titles and dates). Nothing is shown unless it's on a
hand-written allowlist; everything else is dropped. No raw data, search text beyond the examples on the page, file
contents, store names, company names or personal documents are in this repo. "Offline" is the longest stretch each
night with no activity across my laptop and phone, not measured sleep.

## Design choices

- **The interface is the metaphor.** The data came from a search engine, so the whole site is a search box that
  answers questions about me, typing its own first query when the page loads.
- Each answer is a result card with a photo, a chart built from plain HTML and CSS, and links to every other answer, so
  browsing feels like falling down a search rabbit hole.

## Status

A working prototype: the numbers come from my analysis and are written into the page. The pipeline that generates them is next.

## Tech stack

HTML · CSS · vanilla JavaScript · GitHub Pages. Photos from [Unsplash](https://unsplash.com), credited on each card. Not affiliated with Google.

## Ownership

© 2026 Suhani Tiwari. All rights reserved. See [LICENSE](LICENSE).

Built by [Suhani Tiwari](https://suhanitiwari.com).
