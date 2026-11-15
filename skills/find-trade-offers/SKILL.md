---
name: find-trade-offers
description: Build a fair fantasy football trade offer or counter-offer. Use when the user asks what they could get for a player or pick, what they should offer to acquire someone, how to counter an offer, or what to add to make a lopsided trade fair.
---

# Find a fair offer

Use the FantasyTrade Pro connector. Three tools matter here:

- `suggest_fair_trade_returns`: given one side of a trade, lists fair returns for it (straight swaps, two-player packages, a player with a pick, picks only).
- `evaluate_trade`: checks a specific offer and says what would even it out.
- `get_rookie_pick_values`: what each rookie pick is worth, for dynasty leagues.

Settle the league settings first, as for any trade question: dynasty or redraft, Superflex or 1QB, then team count and scoring if the user has given them. Pass them as `league` on every call so all the numbers are on the same scale.

## "What can I get for X?" or "What should I offer for X?"

1. Call `suggest_fair_trade_returns` with the known side in `assets`.
2. The returns are drawn from the whole player pool, not from the other manager's roster. If the user has told you who is on the other team, keep only the returns that team could actually send, or use the values to build one from their players.
3. Present up to four options, one line each: the assets and their total against the value of what the user gives. Say which you would lead with and why, in one sentence.
4. Give the result's link so the user can open the first option in the analyzer.

## Countering or fixing a lopsided trade

1. Call `evaluate_trade` on the offer as it stands.
2. If it is not fair, the result names an asset that would even it out. Offer that, or a pick of similar value from `get_rookie_pick_values` in a dynasty league.
3. Call `evaluate_trade` again on the adjusted offer and confirm it now reads as fair before recommending it. Do not recommend an adjustment you have not checked.

## Rules

- Two lesser players are not equal to one better player just because their values add up. The tool already counts the cost of the extra roster spot, so trust its adjusted totals over your own sums.
- Say when nothing fair exists: a low-value player may not be worth any single asset, and a top player may be worth more than any two.
- An offer the other manager would never accept is not useful. Prefer a package with one real centrepiece over several bench players.
- Do not invent values. Every number you give must come from a tool result in this conversation.
