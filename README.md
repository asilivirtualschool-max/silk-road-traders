# Silk Road Traders

A Grade 5 multiplayer trading game adapted from a Silk Road simulation. Play it at https://asilivirtualschool-max.github.io/silk-road-traders/

## Setup

## 1. Try it first (no setup)
Open the game link in Chrome and tick **Test mode**. Click **Create game**. The teacher screen shows six buttons that open each group in its own tab.

## 2. Firebase rules
The file already points at your existing **finding-out-expedition** Realtime Database. Games are saved under `/silkroad/{CODE}`.

In the Firebase console, go to **Realtime Database → Rules**. Add this block next to your existing `rooms` rule (inside `"rules"`), then click **Publish**:

```json
"silkroad": {
  "$code": {
    ".read": true,
    ".write": "!data.exists() || data.child('meta/created').val() > now - 86400000",
    ".validate": "$code.length === 4"
  }
}
```

Anyone with a 4-letter code can play that game. A game stops accepting changes 24 hours after it was created.

To use a different database, change `FIREBASE_DB_URL` near the top of the `<script>` in the HTML file.

## 3. Host it
It is hosted on GitHub Pages from this repo. Open the page, leave Test mode off and click **Check connection**. It should say "All good".

## 4. In class
1. Teacher: open the page, click **Create game** and project the screen.
2. Each group: open the same page on one device, type the code and pick its region.
3. Teacher: press the big button to move through the game: Round 1 → Round 2 → News #2 → Round 3 → News #3 → Results.

Groups agree on deals out loud first. Then one group sends the offer on its device and the other group accepts it. The app handles who can trade with whom, the hidden disease cards, the news cards and the scoring.

## Changes from the original activity
- **Trade zones:** West = Byzantium + Arabia, Middle = Persia + India, East = Central Asia + China.
- **Round 1:** no trading. Groups explore their cards instead, because each group shares one device.
- **Cards:** 12 cards per region, sorted into four kinds: food, goods, technology and belief. Wording is simplified for Grade 5.
- **Card swaps:** wine became grapes, and ammonium chloride became "Metalwork salts".
- **Arabia:** starts with no food, so it has to trade for some.
- **Scoring:**
  - +1 for each card from another region.
  - +2 for holding all four kinds of card.
  - You need 2 food cards (3 for Central Asia and India after News #2), or you lose 3 points.
  - −2 for each disease card.
  - The news cards change some of these rules.
