---
name: player-values
description: Look up fantasy football trade values and rankings. Use when the user asks what an NFL player or rookie draft pick is worth, compares players, asks who to keep or who is rising or falling, or wants dynasty or redraft rankings overall or for quarterbacks, running backs, wide receivers or tight ends.
---

# Player values, rankings and pick values

Use the FantasyTrade Pro connector. Values are on one scale from 0 to 10,000, where the most valuable player in the user's league format is 10,000. They are rebuilt every night, so use them in place of anything you remember.

| The user asks | Tool |
|---|---|
| What is a player worth, or which of these players is worth more | `get_player_values` with up to ten names |
| Rankings, top players at a position, who to target | `get_rankings`, with `position` for one of QB, RB, WR, TE |
| What a rookie pick is worth, or which veteran equals a pick | `get_rookie_pick_values` (dynasty only) |

Pass `league` whenever the user has described their league: `format` (dynasty or redraft), `superflex`, `teams`, `ppr`, `te_premium`, `pass_td`. The same player can be worth very different amounts in dynasty and redraft, or in Superflex and 1QB, so if the format is unknown and the question depends on it (any quarterback, any rookie, any older player), ask, or state the default you used: 12-team dynasty Superflex, full PPR.

## Reporting

- **One player:** the value, the likely range, the position rank ("WR7"), and the change over the last week when it is given. Add the availability note if the result has one: it means the player is expected to miss games.
- **A comparison:** put the players side by side with value and position rank, then say who is worth more and by roughly how much. When two ranges overlap heavily, say they are close; do not declare a winner on a small gap.
- **Rankings:** a numbered list with value and position rank. The tool returns 25 at a time; use `offset` for the next page when the user wants more.
- **Picks:** the value with its range, and the veteran of similar value the tool names, which is the quickest way to make a pick's worth concrete.

Include the link from the result (the player's page, the rankings page or the pick chart) so the user can see the full picture, including the week-by-week chart on player pages.

## Rules

- Value is trade value, not a projection for this week. For start-or-sit questions, say the tool does not answer them, though projected points per game is in the result.
- Only quarterbacks, running backs, wide receivers and tight ends are covered.
- If a name fits several players, the tool lists the candidates. Ask which one, or retry with the full name.
- Never quote a value that did not come from a tool result in this conversation.
