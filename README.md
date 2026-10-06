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
3. Teacher: press the big button to move through the game. Short on time? Use **Skip Round N** or **Jump to results**.

| Step | What happens |
|---|---|
| Round 1 | Know your region. No trading. Choose a Translator. |
| Round 2 | Trade inside your zone. |
| News #2 | Each region's news card (China pays tax). |
| Round 3 | Trade with next-door zones. Translator needed for other zones. |
| News #3 | News cards that change end-of-game scoring. |
| Round 4 | Trade with anyone. Translator needed for far regions. |
| News #4 | War comes to the Silk Roads. |
| Round 5 | Trade or battle. Up to 3 battles per group. |
| Results | Scores, disease trail, Arabic phrasebook. |

### Arabic and the Translator
Every card shows its Arabic word and how to say it. Each round adds new words (hello, thank you, numbers, trader, war, peace...).
For deals with another zone, the Translator must pick the right Arabic word before an offer is sent, and must work out the Arabic in an offer from far away before it can be accepted. A wrong answer means a 10-second wait. Arabia speaks Arabic already, so it never needs a challenge.

### Battles (Round 5)
A group picks a region to attack. Both groups get the same question (Arabic word or Silk Road fact). The first correct answer wins one random card from the other group, and each battle won is worth 1 point. If nobody is right in 30 seconds, it is a draw.

## Changes from the original activity
- **Trade zones:** West = Byzantium + Arabia, Middle = Persia + India, East = Central Asia + China.
- **Five rounds** instead of three, with Arabic language, Translators and battles added.
- **Cards:** 12 cards per region, sorted into food, goods, technology and belief, with simple wording for Grade 5.
- **Card swaps:** wine became grapes, and ammonium chloride became "Metalwork salts".
- **Arabia:** starts with no food, so it has to trade for some.
- **Scoring:** +1 per card from another region, +2 for all four kinds, food needed (2, or 3 for Central Asia and India after News #2) or −3, −2 per disease card, +1 per battle won. News cards change some rules.
