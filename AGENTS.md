# AGENTS.md

This repo holds Patrick Huesler's public websites. Right now there is only one:
`huesler.io/`, a personal blog built with [Hugo](https://gohugo.io). It was
migrated from Jekyll in 2026, and git history holds the Jekyll version.

## Layout

```
huesler.io/
  hugo.toml          Site config: permalinks, pagination, Atom output, sidebar menu
  .tool-versions     Pinned Hugo extended version (installed via asdf)
  content/posts/     Blog posts, one Markdown file per post
  content/about.md   Sidebar pages (listed in [menus] in hugo.toml)
  content/archive.md Uses layouts/archive.html
  layouts/           Hand-rolled Lanyon port, no external theme
    baseof.html      Shell: head, sidebar, masthead, sidebar toggle JS
    home.html        Paginated post list
    page.html        Posts and plain pages
    home.atom.xml    Feed served at /atom.xml
    _partials/       head.html, sidebar.html
  static/public/     CSS (poole, lanyon, syntax), images, js; served at /public/...
  Makefile           build / server / deploy / release / clean
```

The theme is a port of [Lanyon](https://github.com/poole/lanyon), with
`theme-base-08` set on `<body>`.

## Commands

Run these from `huesler.io/`:

- `make server`: `hugo server --buildDrafts` for local preview at http://localhost:1313
- `make build`: `hugo --gc --minify`, output goes to `public/` (gitignored)
- `make deploy`: rsync `public/` to `$deploy_user@$deploy_server:/home/$deploy_user/www/huesler.io/`
- `make release`: clean, build, then deploy

Never run `make deploy` or `make release` unless the user explicitly asks. They
publish the site to the live server.

## Things that must not break

- **Post URLs** are `/YYYY/MM/DD/slug/`, matching the old Jekyll site. They
  come from `date` and `slug` in the front matter, so don't change either on
  an existing post.
- **The feed lives at `/atom.xml`.** Entry `<id>`s copy the old Jekyll format
  (`http://www.huesler.io/YYYY/MM/DD/slug`) so feed readers don't re-announce
  old posts. `baseURL` stays `http://` for that reason.
- **Static assets keep their paths** under `/public/`. Posts link to them by
  absolute path.

## Content conventions

- New post: `content/posts/<slug>.md` with front matter `title`, `date` (YYYY-MM-DD) and `slug`. Add `draft: true` for unpublished posts.
- Use fenced code blocks with a language. Chroma emits Pygments-style classes that `static/public/css/syntax.css` styles.
- Raw HTML in Markdown is allowed (`markup.goldmark.renderer.unsafe`), and old posts depend on it for gists, iframes and tweets.
- Put post images under `static/public/images/posts/`.
- The site has no analytics, comments or donation widgets. Google Analytics, Disqus and Flattr were removed on purpose, so don't add them back.

## Style

`.editorconfig` sets 2-space indentation, LF line endings, UTF-8, trimmed
trailing whitespace and a final newline.
