# Minimizing Regret

A website for the Google Princeton AI and the Hazan Lab @ Princeton University.

## Getting started

### Editing the website directly from GitHub (easier)
Navigate to the file you'd like to edit or click the drop-down `Add file` and start typing. Click the green button once you're done editing to commit your changes.

### Running the website on your laptop (harder)
Clone this repository and then run `./scripts/install` from this directory. Depending on your setup, you may need `sudo`.

## FAQ

### How to add a person / author
1. Edit `_data/people.yml`.
2. Add an appropriate entry modeled after existing entries (note the `status` attribute e.g., current, former).

Example: the following will create someone named `First Last` in the [People](https://minregret.github.io/people) page. If you'd like to add a headshot, save it as `people/first-last.png` to automatically load it. `first` will be the author slug used in writing new posts.
```yaml
first:
  name: First Last
  title: Grand Poobah
  website: https://grand.Poobah
  status: current
```

### How to add a new posts
1. Create a new file with a name in the format `YYYY-MM-DD-post-name.md` in `_posts`.
2. Copy and paste the following at the beginning
```yaml
---
title: "A great post on an even greater subject"
authors: [elad, cyril]
---
```
3. Write your post using [Markdown](https://www.markdownguide.org/basic-syntax/).

4. If you would like to use `MathJax`, you just surround your usual MathJax with double `$` like so: `$$\in 8$$`.
