# CLAUDE.md

## Local build

CI uses `bundle exec jekyll build`. Locally `bundle exec` is broken (repo pins Ruby 3.3.7 via `.ruby-version`, local Homebrew Ruby is 4.0.9, gems missing), so use:

```sh
JEKYLL_NO_BUNDLER_REQUIRE=true jekyll build
```

Do NOT try to fix with `gem pristine --all` or `bundle install` under Ruby 4.x — it churns the shared Homebrew toolchain without fixing the version mismatch. The `Ignoring ... extensions are not built` warnings are harmless.

## Visual check

```sh
JEKYLL_NO_BUNDLER_REQUIRE=true jekyll build && ~/.claude/bin/shot _site /tmp/shot
# → /tmp/shot/full-1440.png, /tmp/shot/fold-1440.png, /tmp/shot/full-390.png, /tmp/shot/fold-390.png
```

`shot <dir-or-html> <outdir> [width ...]` serves the dir on localhost, waits for fonts/animations, takes full-page + fold PNGs (default widths 1440 390).
