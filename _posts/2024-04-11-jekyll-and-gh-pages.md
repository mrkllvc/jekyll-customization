---
layout: post
title:  "Jekyll and Github Pages"
date:   2024-04-11
---

This Jekyll based site is build locally, source code and site are then pushed to separate branches `main` and `gh-pages` respectively. This way, non-supported Jekyll site plugins can be used. Furthermore, we don't need to wait for the site to be build on GitHub after pushing the changes to the source code. This post describes this setup. See also this [answer on stackoverflow](https://stackoverflow.com/a/28252200).

## How to

First, initialize the repository and Jekyll code base:
```bash
$ mkdir repository-name && cd repository-name
$ git init --initial-branch=main
$ git remote add origin git@github.com:user-name/repository-name.git
$ jekyll new .
```

Set `baseurl: '/repository-name'` in `_config.yml`:

```
title: Jekyll customizations
description: >- # ignore newlines until "baseurl:"
  Jekyll customizations.
baseurl: "/jekyll-customizations" # the subpath of your site
url: "" # the base hostname
github_username: user-name

# Build settings
theme: minima
plugins:
  - jekyll-feed

sass:
  quiet_deps: true # to supress warnings
```

Add `_site` to `.gitignore`, because the site will be versioned in separate gh-pages branch:
```
_site # the site will be versioned in the other branch
.sass-cache
.jekyll-cache
.jekyll-metadata
vendor
.DS_Store # macOS stuff
```

Next, to build the site and serve it locally at: `http://127.0.0.1:4000/repository-name/`, run:
```bash
$ jekyll build
$ bundle exec jekyll serve
```

Add the local repository to GitHub:
```bash
($ git init -b main) # if you haven't initialize in the first step
$ git add .
$ git commit -m "jekyll source"
```
Then run `$ gh repo create` and choose "Push an existing local repository to GitHub". Set "." for Path to local repository. Give the repository a name and description. Set visibility and add a remote.

Push Jekyll source code to the main branch:
```bash
$ git push origin main
```

Push the site to gh-pages branch:
```bash
$ cd _site
$ touch .nojekyll
$ git init
$ git branch -m gh-pages
$ git remote add origin git@github.com:user-name/repository-name.git
$ git checkout -b gh-pages
$ git add -A
$ git commit -m "jekyll first build"
$ git push origin gh-pages
```


Wait for the site to deploy and check `Settings/Pages`: Your site is live at "https://user-name.github.io/repository-name/".
