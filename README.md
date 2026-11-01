# 💄 RuPaul’s Drag Race Contestants – JSON Dataset

This repository contains a JSON dataset of contestants from RuPaul’s Drag Race across seasons and franchises.

I originally created this file for a personal project, but I’m sharing it here in case it can be useful to others.

As a big fan of the show, I often found myself mixing up queens — especially remembering who is who and which season they’re from. This dataset was my way of organizing that information in a clean, structured format.

## 📦 What’s Inside

- `contestants_extract.json` — structured contestant data
- Cleaned / normalized fields for programmatic use
- Root shape: `{ meta, queens }`

This repository does not contain any application code — only the resulting JSON dataset.

**v3.0.0** — 778 queens · 25 franchises · 98 season pages scraped.

### Breaking changes in 3.0.0

| Before (v2.x) | After (v3.0.0) |
|---|---|
| Root was a bare `Contestant[]` | Root is `{ meta, queens }` |
| No stable id | `id` slug (unique) on every queen |
| `miniPromoImageUrl` | `promoImageURL` (wiki page main image) |
| `imageUrl` from queen page heuristics | `imageUrl` from the season table **Photo** column (first appearance) |

### Example

```json
{
  "meta": {
    "version": "3.0.0",
    "generatedAt": "2026-11-01T00:00:00.000Z",
    "source": "https://rupaulsdragrace.fandom.com",
    "queensCount": 778
  },
  "queens": [
    {
      "id": "bebe-zahara-benet",
      "dragName": "BeBe Zahara Benet",
      "imageUrl": "https://static.wikia.nocookie.net/logosrupaulsdragrace/images/4/40/BeBeZaharaBenetS1CastMug.png",
      "wikiUrl": "https://rupaulsdragrace.fandom.com/wiki/BeBe_Zahara_Benet",
      "seasons": [
        {
          "franchise": "RuPaul's Drag Race",
          "season": "1",
          "rawPlace": "Winner",
          "places": [1],
          "mainPlace": 1,
          "isWinner": true,
          "challengeWins": 2
        },
        {
          "franchise": "RuPaul's Drag Race All Stars",
          "season": "3",
          "rawPlace": "3rd/4th",
          "places": [3, 4],
          "mainPlace": 3,
          "isWinner": false,
          "challengeWins": 2
        }
      ],
      "firstFranchise": "RuPaul's Drag Race",
      "promoImageURL": "https://static.wikia.nocookie.net/logosrupaulsdragrace/images/e/ea/BeBeAS3Promo.png",
      "totalChallengeWins": 4,
      "isWinner": true,
      "firstFranchiseCountry": "United States"
    }
  ]
}
```

### TypeScript DTOs

```typescript
type ExtractFile = {
  meta: Meta;
  queens: Contestant[];
};

type Meta = {
  version: string; // Dataset semver, e.g. "3.0.0"
  generatedAt: string; // ISO day at midnight UTC, e.g. "2026-11-01T00:00:00.000Z"
  source: string; // Wiki base URL
  queensCount: number;
  lastUpdate?: Record<string, unknown>; // Optional scrape run metadata
};

type Season = {
  franchise: string; // Franchise name for this appearance
  season: string; // Season number as string (e.g. "1", "11")
  rawPlace?: string; // Place as written on the wiki (may be missing)
  places: number[]; // Parsed place numbers (empty if unknown)
  mainPlace?: number; // Best / primary place when available
  isWinner: boolean; // Won this season
  challengeWins: number; // Maxi-challenge wins this season
};

type Contestant = {
  id: string; // Unique slug from wiki title (stable key)
  dragName: string; // Drag name (resolved wiki title)
  imageUrl?: string; // Cast photo from the season table Photo column
  wikiUrl: string; // Contestant wiki page URL
  seasons: Season[]; // All recorded season appearances
  firstFranchise: string; // Franchise of the first mapped cast
  promoImageURL?: string; // Main illustration of the queen's wiki page
  totalChallengeWins: number; // Sum of challengeWins across seasons
  isWinner: boolean; // Crowned at least once
  firstFranchiseCountry?: string; // Country of firstFranchise when mapped
};
```

## 🕸️ Web Scraping

The data in this project was sourced from:

- Wikipedia
- RuPaul’s Drag Race Fandom Wiki

After scraping the information, I used a custom script to:

- Normalize inconsistent formatting
- Clean unnecessary fields
- Keep only the data required for my project
- Structure everything into a consistent JSON schema

## ⚠️ Disclaimer

This project is a fan-made, unofficial dataset.

- It is not affiliated with, endorsed by, or connected to RuPaul’s Drag Race, World of Wonder, VH1, MTV, or any official production entity.
- The data was gathered from publicly available sources.
- While I’ve done my best to ensure accuracy, I cannot guarantee the data is complete, up to date, or error-free.
- This repository is provided “as is”, without warranty of any kind.

If you plan to use this dataset in a public or commercial project, please make sure you review the original sources and verify compliance with their terms of use.

## 💖 Huge Thanks

A massive thank you to:

- Wikipedia contributors
- [The RuPaul’s Drag Race Fandom Wiki community](https://rupaulsdragrace.fandom.com/wiki/RuPaul%27s_Drag_Race_Wiki)

Your dedication to documenting and maintaining detailed information made this dataset possible. This project would not exist without the work of those communities.

## 👑 Why This Exists

Because sometimes you love the show…

…but still forget who was on which season.

And that simply cannot happen in this house. 💅
