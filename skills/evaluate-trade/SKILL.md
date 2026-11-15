---
name: evaluate-trade
description: Judge an NFL fantasy football trade. Use when the user asks whether a trade is fair, who wins it, whether to accept, decline or counter an offer, or pastes a trade from their league (dynasty or redraft), including trades with rookie draft picks.
---

# Evaluate a fantasy football trade

Use the FantasyTrade Pro connector's `evaluate_trade` tool. Its values come from a statistical model rebuilt every night, so they are more current than anything you remember about players. Do not judge a trade from memory when the tool is available.

## 1. Work out the two sides

`you_get` is what the user would receive and `you_give` is what they would give up. If the user describes a trade between two other teams, pick one team as "you" and say which.

Pass each asset as text:

- Players by name: `"Ja'Marr Chase"`. Full names are safest. Nicknames and initials ("JSN", "ARSB") should be expanded before the call.
- Rookie draft picks: `"2027 1st"`, with a third of the round if the user knows it (`"early 2027 1st"`, `"late 2028 2nd"`), or an exact slot (`"2027 1.03"`). With no hint, the tool assumes the middle of the round.

## 2. Settle the league settings

The answer depends on the league, so pass `league` whenever the user has said anything about it:

- `format`: `dynasty` or `redraft`.
- `superflex`: true when teams can start a second quarterback (Superflex or 2QB).
- `teams`, `ppr` (1, 0.5 or 0), `te_premium`, `pass_td`.

If the user has not said, ask one short question only when it would change the answer: dynasty or redraft, and Superflex or 1QB. Those two move values the most, quarterbacks and picks above all. Otherwise go ahead with the default (12-team dynasty Superflex, full PPR) and say that you did.

Draft picks have no value in redraft. If a redraft trade includes picks, ask whether it is really a dynasty or keeper league.

## 3. Call the tool and report

Lead with the verdict in the tool's own words ("Leans their way", "You win", "Fair trade"), then:

1. The confidence and the gap between the sides.
2. Each side's assets with their values, in a short table when there are more than two assets in total.
3. The reasons the tool gives, in plain sentences. If a roster-spot cost was applied (one side gets more players than it gives), explain it: the extra player pushes someone to the bench, so the weakest piece counts for less.
4. What would even it out, if the tool suggests something.
5. The link from the result, as "Open this trade in FantasyTrade Pro", so the user can adjust it or share it with their league.

Keep it short. A manager in a group chat wants the call and the reason, not a report.

## Rules

- Report the tool's verdict as it is. If it says the trade is close, say it is close; do not round a lean up to a win.
- You may add context the model cannot see (the user's roster needs, a contending window, news from today), but label it as your own view and keep it separate from the values.
- If the tool says a name fits several players, ask the user which one, or retry with the full name if the conversation makes it obvious.
- If the tool reports that a player is not in the values, say so. Kickers, defenses and individual defensive players are not covered.
- If the connector is not connected, tell the user to connect FantasyTrade Pro on the plugin's Connectors tab, or point them to https://fantasytrade.pro to run the trade there.
