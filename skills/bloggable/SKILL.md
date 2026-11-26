---
name: bloggable
description: Set up and run a Bloggable blog through the Bloggable MCP server — create a blog that matches a website's brand and voice, import existing posts, plan topics, write, edit and publish posts, and connect a subdomain. Use when the user wants to start, set up or manage a blog with Bloggable, or to plan, write, edit or publish posts on one.
---

# Bloggable

Bloggable hosts the blog and writes posts in the brand's voice with AI. You work through the Bloggable MCP tools; the
user signs in, approves, and chooses a plan in their browser. Full guide: https://getbloggable.com/agents/onboarding.md

## Connect

The tools come from the MCP server `https://getbloggable.com/api/mcp`. If they are not available, add it — Claude Code:
`claude mcp add --transport http bloggable https://getbloggable.com/api/mcp`; Claude: the Bloggable connector. The first call opens a browser to
sign in — free, no card.

## Start

Call `get_account`. If `live` is false the workspace is in setup: everything you configure is free and private, and
publishing and AI writing wait until the user chooses a plan at the go-live link. Then `list_blogs`.

## Set up a blog

Gather the brand first: name, website, a one-line description, audience, colours, logo URL, how the site talks, and any
existing articles.

- In a code repository, read them from the code: the Tailwind config or CSS variables, `content/`, `posts/`, `*.md`.
- In a chat, ask for the website, read it if you can fetch pages, and confirm what you found with the user rather than
  guessing.

1. `create_blog` (name, websiteUrl, description, niche, targetAudience, primaryColor, logoUrl) → `list_themes` →
   `update_blog` with a `themeId` and a `voiceProfile` taken from the site's own copy.
2. `import_posts` for existing articles — up to 8 per call, plain Markdown, absolute image URLs, keep each slug, set
   `canonical` to where it lives today.
3. `add_planned_topics` with a handful of post ideas (free).
4. Optional: `set_custom_domain` with a subdomain such as blog.example.com (no /blog paths) and give the user the DNS
   record it returns.
5. `finish_setup`, then show the user the go-live link and the preview link.

## Run the blog

- **Read:** `list_posts` for posts, `list_planned_topics` for ideas (a topic is not a post), `get_post` for one in full.
- **Edit:** `update_post` — title, body, excerpt, tags, SEO, byline. Send only what changes.
- **Write with AI (PAID):** `draft_posts` turns planned topics into posts, `suggest_topics` researches new ideas,
  `rewrite_posts` regenerates or refreshes existing posts. Quote `estimate_credits` first, then follow the work with
  `list_jobs` — it takes minutes per post.
- **Publish:** `publish_post` now, or later with `scheduledAt`; `unpublish_post` takes a post back to draft.

## In a code repository: the posts in the user's app

To list the blog's posts in the user's own site, read the RSS feed (`<blog address>/feed.xml`) or the posts API and
link each post to the blog. For instant updates the user adds an event webhook and you write the endpoint. Full guide,
section 6.

## Don't

- Publish, unpublish, or call a PAID tool unless the user asked for it.
- Guess ids — take them from `list_blogs`, `list_posts` and `list_planned_topics`.
- Rebuild the blog's pages in the user's app (a list of posts linking to the blog is fine), or write an API key or a
  webhook's signing secret into a repository.
