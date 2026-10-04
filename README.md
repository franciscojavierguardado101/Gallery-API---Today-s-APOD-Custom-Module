# Gallery API — Today's APOD Custom Module

A Next.js frontend module that displays NASA's Astronomy Picture of the Day (APOD) as an interactive gallery component, built for the Francisco Guardado Book 1 headless Drupal site.

## What it does

- Fetches and displays today's APOD (image or video) on page load
- Shows a random gallery of past APOD entries as clickable thumbnails below the main panel
- Clicking any thumbnail swaps the main panel to that entry
- Includes a Refresh button to load a new random gallery set
- A "Back to today" link reappears whenever you are viewing a past entry

## Data source

Pulls from NASA's public WordPress REST API with no API key required:

```
https://science.nasa.gov/wp-json/wp/v2/apod-basic
```

## File structure

```
src/
  app/
    api/
      apod/
        route.ts           # Next.js API route — proxies NASA, reads gallery count from Drupal config
  components/
    paragraphs/
      apod/
        ApodDisplay.tsx    # Main React component (today panel + gallery thumbnails)
        types.ts           # TypeScript interfaces for APOD data shape
        index.ts           # Barrel export
```

## How the API route works

`route.ts` accepts two modes via query param:

| `?mode=`  | Behavior |
|-----------|----------|
| `today`   | Returns the single most recent APOD entry |
| `random`  | Returns multiple entries (count pulled from Drupal config, default 6) |

The gallery count is configurable from the Drupal CMS admin without touching code.

## Stack

- Next.js 16 (App Router)
- TypeScript
- Drupal 11 headless backend (Pantheon)
- Deployed on Vercel
