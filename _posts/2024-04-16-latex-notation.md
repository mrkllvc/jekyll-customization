---
layout: post
title:  "LaTeX Notation"
date:   2024-04-16
---

LaTeX notation can be enabled through the [MathJax](https://github.com/mathjax/MathJax) JavaScript display engine.

This post describes how MathJax can be used with Jekyll.

## Instructions
First, define the structure and look of the site, by creating:

* `custom-head.html`, `footer.html`, `header.html` etc. in `./_includes` directory.

* `base.html`, `home.html`, `post.html` etc. in `./_layouts` directory.


Next, in `base.html`, define the MathJax configuration, for example:
```html
<script type="text/javascript">
    window.MathJax = {
    tex: {
        packages: ['base', 'ams', 'newcommand'],
        inlineMath: [['$', '$'], ['\\(', '\\)']],
        tags: 'ams'
    },
    loader: {
        load: ['ui/menu', '[tex]/ams', '[tex]/newcommand']
    }
    };
</script>
```

And after this, add the CDN snippet in `base.html`:
```html
<script type="text/javascript" id="MathJax-script" async
    src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>
```

Finally, test the inline and display modes. The text that follows:
```Latex
$\LaTeX$ test. When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
```

should be formatted as:

$\LaTeX$ test. When $a \neq 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$