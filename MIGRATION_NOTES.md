# Academic Pages Migration Notes

This folder contains the Academic Pages/Jekyll version of Diego Almonacid-Almarza's academic website.

## What Was Migrated

- Site identity, author profile, portrait, email, ORCID, Google Scholar, and PhilPapers profile.
- CV PDF at `files/Almonacid-Almarza_CV.pdf`.
- Publications as Markdown files in `_publications/`.
- Talks as Markdown files in `_talks/`.
- Teaching entries as Markdown files in `_teaching/`.
- Navigation reduced to Publications, Talks, Teaching, and CV.
- A light customization layer in `assets/css/main.scss` using the chosen palette:
  - `#34344a` space indigo
  - `#80475e` vintage berry
  - `#bcabae` lilac ash
  - `#fbfbfb` white
  - `#258ea6` pacific cyan

## PDFs and Handouts

- Put article PDFs in `files/papers/`.
- Put presentation handouts in `files/handouts/`.
- To show a download link, add a field like this to the relevant Markdown file:

```yaml
paperurl: "/files/papers/example-paper.pdf"
```

For talks/handouts:

```yaml
slidesurl: "/files/handouts/example-handout.pdf"
```

## Local Preview

The macOS system Ruby is too old for the current Academic Pages dependency stack. Use Homebrew Ruby 3.3 for local preview.

Recommended setup:

```bash
cd academicpages-site
export PATH="/opt/homebrew/opt/ruby@3.3/bin:/opt/homebrew/lib/ruby/gems/3.3.0/bin:$PATH"
bundle config set --local path vendor/bundle-ruby33
bundle install
bundle exec jekyll serve --host 127.0.0.1 --port 4000
```

Then open:

```text
http://127.0.0.1:4000/
```
