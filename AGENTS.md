# AGENTS.md

This repo holds Patrick Huesler's public websites. Right now there is only one:
`huesler.io/`, a personal blog built with Jekyll. Its last real activity was in
2015 to 2018, so treat the toolchain as legacy.

## Layout

```
huesler.io/
  _config.yml      Jekyll config (redcarpet markdown, pygments highlighter, pretty permalinks, paginate: 5)
  _posts/          Published posts, named YYYY-MM-DD-slug.md
  _drafts/         Unpublished drafts (shown only by `rake server`)
  _layouts/        default.html (shell + sidebar toggle JS), post.html, page.html
  _includes/       head.html, sidebar.html
  index.html       Paginated post list (jekyll-paginate)
  about.md, archive.md, 404.html, atom.xml
  public/          Static assets: css/ (poole, lanyon, syntax), images/, js/countdown.js
  Rakefile         build / server / deploy / release tasks
```

The theme is [Lanyon](https://github.com/poole/lanyon) (built on Poole), with
`theme-base-08` set on `<body>`. `huesler.io/README.md` is the stock Lanyon
README, not documentation for this site.

## Commands

Run these from `huesler.io/`:

- `bundle install`: install gems (Jekyll 3.6.x, jekyll-paginate, jekyll-gist, pygments.rb, redcarpet)
- `rake server`: `jekyll server --drafts --watch` for local preview
- `rake build` (the default): `jekyll build`, output goes to `_site/`
- `rake deploy`: rsync `_site/` to `$deploy_user@$deploy_server:/home/$deploy_user/www/huesler.io/`
- `rake release`: build, then deploy

`Gemfile.lock` pins Jekyll 3.6.2 and Bundler 1.16.2, and nothing pins a Ruby
version (the 2.3.3 pin was removed). These old gems, pygments.rb in particular
(which needs Python), may not install or run on a modern Ruby such as 3.3. If
the build fails, say so. Don't upgrade dependencies unless you're asked to.

Never run `rake deploy` or `rake release` unless the user explicitly asks. They
publish the site to the live server.

## Content conventions

- Post front matter is just `layout: post` and `title: "..."`. The date comes from the filename.
- Pages that should appear in the sidebar nav use `layout: page` and need a `title`.
- For code blocks, use Liquid `{% highlight lang %} ... {% endhighlight %}` (Pygments), not fenced blocks, to match the existing posts.
- Put post images under `public/images/posts/` and reference them by absolute path (`/public/images/...`).
- The site has no analytics, comments or donation widgets. Google Analytics, Disqus and Flattr were removed on purpose, so don't add them back.

## Style

`.editorconfig` sets 2-space indentation, LF line endings, UTF-8, trimmed
trailing whitespace and a final newline.
