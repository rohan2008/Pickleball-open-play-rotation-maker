# Open-Play Rotation Maker

A free web app for running pickleball open play. Check players in, enter their DUPR ratings, and press **Next round**. It puts people on courts with balanced teams, keeps sit-outs even, and keeps partners changing. It also runs round robins and single-elimination brackets.

**Try it:** https://rohannamdhari.com/open-play-rotation-maker/

No sign-up, no server, no tracking. Everything runs in your browser.

## What it does

### Open play
- **Fair sit-outs.** When there are more players than spots, the people who have played the most sit first, and ties go to whoever sat longest ago.
- **Balanced teams.** Each court is split into the fairest teams it can find using DUPR, shown as a gap on each court (Even, Close, Lopsided).
- **Fresh partners and opponents.** Repeat partners and repeat opponents are penalized, so you keep meeting new people.
- **Mix levels or group by level.** Let anyone land on any court, or keep similar ratings together.
- **Doubles or singles**, and 1 to 30 courts.
- **Hidden courts.** Courts start face-down so players don't crowd the board. Tap one to flip it, or reveal them all at once.
- **Round timer** (12, 15 or 20 minutes) with a "Time!" alert.
- **Late arrivals and early leavers.** Late players get credited so they aren't scheduled for a pile of catch-up games. Check people out when they leave.
- **Fairness table and history.** See who sat, who played and how many partners each person has had. Copy any round for your group chat.

### Tournaments
- **Round robin.** Everyone plays everyone once. Standings rank by wins, then point difference.
- **Bracket.** Single elimination, seeded by rating, with byes when the field isn't a power of two.
- **Pool + bracket.** Play a round robin first, then the top finishers are seeded into a bracket.
- **Randomized or picked teams** for doubles, with optional team names and colors.
- **Score check.** Optionally flag scores that aren't a finished game (game to 11, 15 or 21, win by 2).
- **Late teams** can join pool play with catch-up matches.
- **Copy results** for the group chat.

## Using it

1. Add players with a name and (optionally) a DUPR from 2.00 to 8.00. You can paste a whole list, one per line, like `Maya Chen, 4.21`. Players without a rating are treated as mid-pack.
2. Check in whoever is here.
3. Pick your format and number of courts.
4. Press **Next round**.

The app starts with example players so you can see how it works. Press **Clear examples** to start your own.

## Run it locally

It's plain HTML, CSS and JavaScript with no build step and no dependencies. Download the repo and open `open-play-rotation-maker/index.html` in a browser.

To bundle everything into a single self-contained HTML file (handy for sharing):

```
cd open-play-rotation-maker
node build.js
```

That writes `dist/open-play-rotation-maker.html`.

## How it works

Files in `open-play-rotation-maker/js/` load in this order, since each uses things defined in the ones before it:

| File | Job |
| --- | --- |
| `config.js` | Fixed settings, example players, team colors |
| `utils.js` | Small helpers and the toast message |
| `state.js` | Session state and saving to the browser |
| `ratings.js` | DUPR validation and the 0 to 1 skill scale |
| `rotation.js` | Who sits, who plays where, who partners whom |
| `tournament.js` | Round robin, bracket and seeding logic |
| `render.js` | Draws open play, the roster, fairness and history |
| `tournament-render.js` | Draws tournament setup, pool play and the bracket |
| `events.js` | Wires buttons and inputs to the state |
| `main.js` | Startup |

For each round the app tries about 900 random lineups and keeps the one with the lowest cost: uneven teams, repeat partners and repeat opponents all add cost.

## Your data

Sessions are saved in your browser's local storage on your own device. Nothing is sent anywhere. Clearing your browser's site data erases the saved session. The page loads two fonts (Big Shoulders Display and Archivo) from Google Fonts.

## Contributing

Issues and pull requests are welcome.
