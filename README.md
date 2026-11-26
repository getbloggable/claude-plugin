# Bloggable for Claude

[Bloggable](https://getbloggable.com) hosts your blog and writes posts in your brand's voice with AI. This plugin lets Claude set up and
run a Bloggable blog for you: create a blog that matches your website, import your existing posts, plan topics, write,
edit and publish posts, and connect a subdomain.

## What's inside

- **The Bloggable connector** (`.mcp.json`): Bloggable's remote MCP server at `https://getbloggable.com/api/mcp`.
- **The `bloggable` skill** (`skills/bloggable/SKILL.md`): how Claude uses those tools — what to set up first, what
  is free, and what waits until you ask for it.

The plugin contains no code and runs nothing on your computer.

## Getting started

1. Install the plugin from Claude's directory. In Claude Code you can also install it from this repository:
   `claude plugin marketplace add getbloggable/claude-plugin`, then
   `claude plugin install bloggable@bloggable`.
2. Ask Claude to set up a blog ("Set up a Bloggable blog for example.com") or to work on the one you have ("Draft
   my next three planned posts").
3. The first time Claude uses Bloggable, your browser opens so you can sign in with Google or an email link and
   approve the connection. A new account opened this way is free, with no card: nothing is public and AI writing is
   off until you choose a plan.

## What it sends, and where

Everything goes to one place: Bloggable's MCP server at `https://getbloggable.com/api/mcp`, over HTTPS, signed in as you. Claude sends what
you ask it to work on — blog settings, posts, post ideas, images to upload by their URL — and reads back your blogs,
posts and the progress of AI work. Sign-in is OAuth: Claude never sees your password, and you can disconnect it at any
time in Bloggable under Settings → AI agents.

Writing with AI spends your account's credits. The skill tells Claude to use those tools, and to publish, only when
you ask, and to quote the cost first for anything large.

## Privacy

Bloggable's privacy policy: https://getbloggable.com/legal/privacy. Terms of service: https://getbloggable.com/legal/terms.

## Support

Help centre: https://getbloggable.com/help · Email: hello@support.getbloggable.com

## License

MIT — see [LICENSE](LICENSE).
