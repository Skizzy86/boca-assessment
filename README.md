# BOCA - Business Owner Capacity Assessment

Guide-facing assessment tool for The Breakthrough Year.

## Files

- `index.html` - the whole application. No build step, no dependencies.
- `CNAME` - custom domain for GitHub Pages.

## How it is used

The client reads a printed one-page questionnaire. The Guide scores the 25
statements in this web app, presses Run Test, and prints the two-page report
to PDF for the client.

## Backend

Scores POST to a Google Apps Script web app. The URL lives in the `ENDPOINT`
constant at the top of the script block in `index.html`. Redeploying the Apps
Script project produces a new /exec URL that has to be pasted back in.

Apps Script stores rows and returns them by ID. It generates no report copy:
the 20 pillar paragraphs live in `COPY.pillar` here and are selected in the
browser at render time.

## Scoring

All scoring lives in `CONFIG`. Per-item weights must sum to exactly 5.0 within
each pillar, which keeps the weighted pillar maximum at 15 and leaves the band
thresholds and demotion floors valid. Weighted scores are continuous, so floor
comparisons use `< n + 1` rather than `<= n`; using `<=` lets a weighted 7.3
slip past a floor that a raw 7 would trip.
