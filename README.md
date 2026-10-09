# Nemesis Tournament Auction

A single-page web tool for running an offline player auction. It shows one PDF page (one player) at a time in the centre of the screen, while six captain tables track every sale, each captain's remaining budget, and the maximum they can safely bid on the next player.

Everything runs in the browser from one HTML file. The PDF never leaves your computer.

## Features

- Shows one PDF page at a time, scaled to fit the centre of the screen
- Six captain tables (3 on the left, 3 on the right) with player name, bid, total spend, budget left and max for next player
- Sold, Unsold and Skip buttons with automatic round handling
- Unsold players return in the next round until every player is sold
- Undo for the last Sold, Unsold or Skip action
- Configurable wallet, base price and team size
- Progress, table entries and the loaded PDF are saved in the browser, so an accidental refresh loses nothing
- Dark maroon, gold and black theme

## Getting Started

1. Open `nemesis-auction.html` in a modern browser (Chrome, Edge, Firefox or Safari). An internet connection is needed, because the PDF viewer library (PDF.js) loads from a CDN.
2. Click **Settings** and set the wallet per captain, the base price and the team size.
3. Click **Load PDF** and choose the auction PDF. Use one page per player.
4. Run the auction.

## Running the Auction

For each slide:

1. Captains bid offline.
2. Press one of the action buttons:
   - **Sold**: the player is removed from the queue.
   - **Unsold**: the player is moved to the next round.
   - **Skip slide**: for captain slides or any page that is not a player. It is removed permanently.
3. If the player was sold, type the player's name and the winning bid into that captain's table. The tool does not read names from the PDF.

When every page in the current round has been shown, the unsold players automatically start the next round. The tool shows "Auction complete" once all players are sold.

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| S | Sold |
| U | Unsold |
| K | Skip slide |
| Z | Undo last action |

Shortcuts are disabled while typing in a table.

## Settings

| Setting | Default | Description |
|---------|---------|-------------|
| Wallet per captain | 1200 | Starting budget, the same for every captain |
| Base price | 50 | Minimum price per player |
| Team size (including captain) | 7 | Each captain bids for team size minus 1 players |

Changing the team size adds or removes rows in every table. Captain names can be edited by clicking the name in each table header.

## Max for Next Player

This value makes sure no captain goes bankrupt before filling all of their slots:

    Max bid = Balance - Base price x (slots still to fill after this one)

If a captain has no slots left, it shows 0.

Example: base price 50, balance 340, 3 slots left gives 340 - 50 x 2 = 240.

A captain's table gets a red border if their balance is negative or too low to cover their remaining slots at base price.

## Buttons

- **Load PDF**: choose the auction PDF
- **Undo**: reverses the last Sold, Unsold or Skip action
- **Settings**: wallet, base price and team size
- **Reset All**: clears all tables, progress, settings and the saved PDF (asks for confirmation)

## Data and Privacy

- All data is stored in your browser (localStorage for progress and tables, IndexedDB for the PDF).
- Nothing is uploaded to a server.
- Data is tied to the browser and device you use. Switching browsers or clearing site data starts fresh.
- Private or incognito windows may not save the PDF. If so, re-select the PDF after a refresh.
- If you load a PDF with a different page count than the saved progress, the queue restarts from Round 1.

## Tech Notes

- Plain HTML, CSS and JavaScript in a single file, with no build step
- [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 (loaded from cdnjs) renders the PDF pages

## Tips

- Use **Reset All** before starting a new auction.
- Test with a few pages first to make sure the layout works on your projector or screen.
- Keep the browser tab open on the auction page during the event, and avoid clearing browser data.
