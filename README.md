# UpReap Equity for Claude, ChatGPT and Gemini

Use your [UpReap Equity](https://upreap.com/equity/) analyst inside the AI app you already pay for. It reads your
portfolio, net worth and cash flow from Equity, explains them in plain words, and publishes its reports back to the app.
It never places real trades: it can only trade in its own paper account.

What's here:

| | |
|---|---|
| `.mcp.json` | The connector: `https://equity.upreap.com/mcp` (you sign in to Equity and approve it) |
| `skills/upreap-equity-analyst/` | The analyst skill: which tools to use, how to write updates and reviews, and the safety rules |
| `prompts/prompts.json` | Things to ask, and scheduled tasks to paste into your AI app |
| `.claude-plugin/` | The Claude plugin and marketplace files |

Every release attaches `upreap-equity-analyst.zip` (the skill, ready to upload to Claude), `prompts.json` and
`upreap-equity-plugin.zip`. The Equity app reads the latest release, so Settings → Analyst → Skills always offers the
newest version.

## What it connects to and sends

- The plugin has no code of its own. It adds one remote connector, `https://equity.upreap.com/mcp`, run by UpReap,
  and one skill (instructions for Claude).
- You sign in to Equity and approve the connection (OAuth). Claude then reads and writes your Equity data only
  through that connector, within what you allow under Settings → Analyst → What it can reach.
- It reads your portfolios, transactions, net worth, cash flow and market data from Equity, and writes reports, notes
  and paper trades back. It changes balances, targets or goals only after showing you a preview and getting your OK,
  and it can't place real trades or move money.
- Nothing else is sent anywhere. [Privacy policy](https://equity.upreap.com/privacy) ·
  [Terms](https://equity.upreap.com/terms) · Support: hello@upreap.com

## Claude Code

```
/plugin marketplace add UpReap/equity-ai-plugin
/plugin install upreap-equity@upreap
```

The first time Claude uses the connector it opens Equity so you can sign in and approve it.

## Claude (web, desktop and mobile)

1. Add the connector: in Equity, Settings → Analyst → **Connect your AI** → **Connect to Claude**. Or in Claude open
   Customize → Connectors → Add custom connector, name it `UpReap Equity` and paste `https://equity.upreap.com/mcp`.
2. Add the skill: download `upreap-equity-analyst.zip` from the
   [latest release](https://github.com/UpReap/equity-ai-plugin/releases/latest) (don't unzip it), then upload it
   under Customize → Skills and turn it on.

## ChatGPT

ChatGPT Plus or higher. Settings → Apps & Connectors → Advanced settings → turn on Developer mode. Then Create, name it
`UpReap Equity`, paste `https://equity.upreap.com/mcp` and pick OAuth. ChatGPT has no skills, so the connector carries
the analyst's rules itself.

## Gemini

On gemini.google.com: Settings → Connected apps → Add a custom app, paste `https://equity.upreap.com/mcp`. For now
Google offers this only in some countries and account types.

## Making a release

1. Change the skill or prompts.
2. Raise `version` in `.claude-plugin/plugin.json` (e.g. 1.0.0 to 1.0.1).
3. Push to main. The Release workflow sees a version that isn't released yet, tags it `v1.0.1` and attaches the
   files. Pushes that don't change the version release nothing.

The connector itself lives in the Equity app; this repo only points to it.
