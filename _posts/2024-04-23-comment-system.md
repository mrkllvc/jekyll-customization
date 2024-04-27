---
layout: post
title: "Comment System"
date:   2024-04-23
---

One way to enable comments on a fully static Jekyll website is via Node.js application called [staticman](https://github.com/eduardoboucas/staticman). For this, we have to run the instance of staticman either on our own infrastructure or by using a service such as Heroku. However, in 2022 Heroku shut down their free tier.

This post explains how to develop a simple comment system for Jekyll website via contact forms. There are many free options for contact forms for static websites, such as [staticforms](https://www.staticforms.xyz/) and [web3forms](https://web3forms.com/). 

You provide an email address and they give you an api address, for example: 

> https://api.staticforms.xyz/submit

and an access key such as:

> e44fc5d0-0b52-4cb1-9f79-fefc3800d89c

Form submissions can be received directly through email without the need for server or back-end code. An email alias is recommended for privacy and security reasons. For more security, some other method should be used.

The staticman templates written in liquid can be adapted to replace the Node.js application with contact forms. The following short instructions can help to recreate this simplified comment system.

## Instructions

`1.` The given api address and access key can be saved to `_config.yml` for easy access. 

`2.` Write a `comment_form.html` in `./_includes` directory. For example:
```html
<form method="post" action="{{ site.comments.action }}">
  <input type="hidden" name="accessKey" value="{{ site.comments.token }}">

  <!-- form inputs -->
</form>
```
In the form inputs should be the textarea for the comment, name and submit button. You can define some hidden inputs in order to send the time and date when the comment was submitted and the name of the blog post. For example here via `staticforms` this custom inputs can be defined as:

```html
  <input type="hidden" name="$Date" value="{{ site.time | date: '%s' }}">
  <input type="hidden" name="$BlogPost" value="{{ page.title }}">
```

This way, when someone submits a comment, you get an email with the comment, name, submission date and name of the blog post. 

`3.` Write this data to `_data/comments/post-name` directory in a YAML file. For example this is the data for the first comment on this page. Date and time is in [unixtimestamp](https://www.unixtimestamp.com/) format:

```yaml
_id: 1
_parent: 'jekyll-customization/comment-system'
replying_to_uid: ''
message: 'This is just a test'
name: 'Lambda'
date: 1714228019
```

`4.` Add a `comment.html` in `./_includes` directory that reads such YAML file and outputs the html. 

`5.` Add a `comments.html` that goes over all posts and all comments including (calling) `comment.html` for each YAML file. At the end it should also include `comment_form.html` for adding new comments.

`6.` Include `comments.html` in `post.html` layout in `./_layouts` directory:
```html
  <!-- ./_posts/post.html -->
  <div>
     <!-- include comments.html  -->
  </div>
```

This way each blog post site will have the past comments included (sorted by date) and at the bottom there will be a form for adding new comments.

For more information, check the source code of this site: [jekyll-customization](https://github.com/mrkllvc/jekyll-customization). In particular the files: `./_posts/post.html`, `./_includes/comments.html`, and `./_data/comments/post-name/` YAML files with comment data. You can also try adding a comment on this site.


