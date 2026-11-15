# FantasyTrade Pro

Judge NFL fantasy football trades from a conversation with Claude. Ask in your own words whether a trade is fair and get a verdict, a confidence level, the value of every player and rookie pick, the reasons behind the call, and what would even it out. It works for dynasty and redraft leagues, Superflex and 1QB, and uses your league's size and scoring.

The values are FantasyTrade Pro's own model, rebuilt every night from public NFL statistics. The method is published at https://fantasytrade.pro/methodology/.

## What is in the plugin

- **A connector** to FantasyTrade Pro's server, with five read-only tools: evaluate a trade, get player values, get rankings, suggest fair returns for one side of a trade, and get rookie pick values.
- **Three skills** that tell Claude how to use those tools well:
  - `evaluate-trade`: is this trade fair, who wins, should I accept.
  - `find-trade-offers`: what can I get for a player, what should I offer, how do I counter.
  - `player-values`: what a player or pick is worth, comparisons, and rankings.

## Use it

1. Add the plugin, then connect **FantasyTrade Pro** on the plugin's Connectors tab. There is no account and no sign-in.
2. Ask a question the way you would in your league chat:
   - "I give Bijan Robinson and a 2027 2nd and get Ja'Marr Chase. 12-team Superflex dynasty. Fair?"
   - "What could I ask for in return for Brock Bowers?"
   - "Top 15 dynasty tight ends in a 1QB league."
   - "What is a late 2027 1st worth?"
3. Mention your league's format when it is not a 12-team Superflex dynasty league with full PPR, which is the default.

Each answer includes a link that opens the same trade, player or rankings page on fantasytrade.pro.

## Data

The plugin sends the player names, draft picks and league settings from your question to `https://fantasytrade.pro/api/mcp` so the values can be worked out. It does not send your conversation, your name or anything about your Claude account. The server stores none of it, and every tool only reads: nothing in your league or on the site can be changed. The plugin runs no code on your computer and contains only Markdown and JSON files.

Privacy policy: https://fantasytrade.pro/privacy/

## Limits

- Quarterbacks, running backs, wide receivers and tight ends only. No kickers, defenses or individual defensive players.
- Values are estimates with a range, and close trades are called close.
- The plugin cannot see your league or roster. League import is available on the website.

## Support

Documentation: https://fantasytrade.pro/mcp/

Questions and problems: support@fantasytrade.pro or https://fantasytrade.pro/contact/

FantasyTrade Pro is not affiliated with the NFL or any fantasy platform.

## License

MIT. See `LICENSE`. The license covers the files in this plugin, not the FantasyTrade Pro website, its data or its value model.
