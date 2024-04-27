---
layout: post
title: "BibTeX References"
date:   2024-04-20
---

This site was build using the [jekyll-scholar plugin](https://github.com/inukshuk/jekyll-scholar) (version 7.1.3):
```
$ gem list | grep scholar
jekyll-scholar (7.1.3)
```

This post describes how this plugin can be used to cite BibTeX references stored in `.bib` files on a website built with Jekyll.

## Step-by-step instructions

`1.` Install jekyll-scholar plugin:
```bash
$ gem install jekyll-scholar
```

`2.` Add `gem 'jekyll-scholar', group: :jekyll_plugins` to `./Gemfile`.

`3.` Create `./_plugins` directory and write: `require 'jekyll/scholar'` to `ext.rb` file.

`4.` Set the jekyll-scholar plugin configuration settings in `./_config.yml`, this site uses:

```yml
# jekyll-scholar plugin settings
scholar:
  style: apa
  locale: en
  sort_by: none
  order: ascending
  source: ./_bibliography
  bibliography: simple.bib
  bibliography_template: "{{reference}}"
  replace_strings: true
  join_strings:    true
  details_dir:    bibliography
  details_layout: bibtex.html
  details_link:   Details
  query: "@*"
```

`5.` Create `./_bibliography` directory and add some `.bib` files to it, for example `simple.bib`:

```BibTeX
@book{ruby,
   title     = {The Ruby Programming Language},
   author    = {Flanagan, David and Matsumoto, Yukihiro},
   year      = {2008},
   publisher = {O'Reilly Media}
}

@book{smalltalk,
   title     = {Smalltalk Best Practice Patterns},
   author    = {Kent Beck},
   year      = {1996},
   publisher = {Prentice Hall}
}
```

`6.` Finally, add some content markdown files to `_posts` directory for testing. See the post `./_posts/2024-04-23-bibtex-references.md` as an example.
