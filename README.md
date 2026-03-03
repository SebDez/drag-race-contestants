# 💄 RuPaul’s Drag Race Contestants – JSON Dataset

This repository contains a JSON output of all contestants from RuPaul’s Drag Race across the different seasons and franchises.

I originally created this file for a personal project, but I’m sharing it here in case it can be useful to others.

As a big fan of the show, I often found myself mixing up queens — especially remembering who is who and which season they’re from. This dataset was my way of organizing that information in a clean, structured format.

## 📦 What’s Inside

- A JSON file containing structured data about contestants
- Cleaned and normalized fields
- Only the relevant data needed for programmatic use

This repository does not contain any application code — only the resulting JSON dataset.

```json
{
   {
    "dragName": "A'Keria C. Davenport",
    "imageUrl": "https://static.wikia.nocookie.net/logosrupaulsdragrace/images/8/80/A%27keriaChanelDavenportAS6.png",
    "wikiUrl": "https://rupaulsdragrace.fandom.com/wiki/A'Keria_C._Davenport",
    "seasons": [
      {
        "franchise": "RuPaul's Drag Race",
        "season": "11",
        "rawPlace": "3rd/4th",
        "places": [
          3,
          4
        ],
        "mainPlace": 3,
        "isWinner": false,
        "challengeWins": 2
      },
      {
        "franchise": "RuPaul's Drag Race All Stars",
        "season": "6",
        "rawPlace": "8th",
        "places": [
          8
        ],
        "mainPlace": 8,
        "isWinner": false,
        "challengeWins": 0
      }
    ],
    "firstFranchise": "RuPaul's Drag Race",
    "miniPromoImageUrl": "https://static.wikia.nocookie.net/logosrupaulsdragrace/images/6/65/AkeriaS11Promo.jpg",
    "totalChallengeWins": 2,
    "isWinner": false,
    "firstFranchiseCountry": "United States"
  }
}
```

```typescript
type Season = {
  franchise: string; // This season franchise name
  season: number; // This season number (for this franchise)
  rawPlace: string; // The place raw string
  places: number[]; // All the places (if more than one)
  mainPlace: number; // The higher place
  isWinner: boolean; // As the contestant won this season
  challengeWins: number; // Number of challenges won in this season
};

type Contestant = {
  dragName: string; // The contestant drag name
  imageUrl?: string; // The contestant main image, if found
  wikiUrl: string; // The wiki url
  seasons: Season[]; // All the seasons the contestant went to
  firstFranchise: string; // The first franchise of the first cast
  miniPromoImageUrl?: string; // The contestant mini promo image, if found
  totalChallengeWins: number; // Total amount of challenges won, all seasons count
  isWinner: boolean; // Was crown at least one time
  firstFranchiseCountry: string; //The country of the first cast
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
