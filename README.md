# trondbordewich.com

Personal blog, built with [Hugo](https://gohugo.io) and deployed to GitHub Pages by GitHub Actions on every push to `master`.

## Writing

```sh
brew install hugo                           # once
hugo new content blog/my-new-post.md        # creates a draft in content/blog/
hugo server -D                              # preview at http://localhost:1313, drafts included
```

Remove `draft: true` from the front matter when the post is ready, then commit and push.

- Posts live in `content/blog/` and are served at `/blog/<filename>/`.
- `summary` in the front matter is shown on the front page; leave it empty to use the first paragraph.
- Link to another post by its filename: `[text](other-post.md)`. External links are regular Markdown links.
- Images: make the post a folder (`hugo new content blog/my-post/index.md`), put `photo.jpg` next to it and write `![Alt text](photo.jpg)`. Shared images can go in `static/`.
- Code blocks: regular fenced blocks with a language, e.g. ```` ```swift ````.
- Video: `{{< youtube ID >}}` or `{{< vimeo ID >}}`.

## Layout

No theme dependency — the templates in `layouts/` and the CSS in `assets/css/` are the whole design.

- Logo and favicon: `static/logo.svg` (switches colours in dark mode). The PNG/ICO icons in `static/` are rendered from it with `rsvg-convert`.
- Syntax highlighting colours: `assets/css/syntax.css`, generated with `hugo gen chromastyles`.
- The CI pins the Hugo version in `.github/workflows/hugo.yml`. Bump it there when you upgrade Hugo locally.
