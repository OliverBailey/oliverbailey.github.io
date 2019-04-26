# Space Jekyll

A simple and elegant Jekyll theme based on Spacemacs. Public site for Oliver Bailey

# Site/User Settings

customize your site in ``_config.yml``

```ruby

# Site settings
description: A blog about lorem ipsum
baseurl: "" # the subpath
url: "" # the base hostname &/|| protocol for your site

# User settings
username: Lorem Ipsum
user_description: Lorem Developer
user_title: Lorem Ipsum
email: lorem@ipsum.com
twitter_username: loremipsum
github_username:  loremipsum
gplus_username:  loremipsum
disqus_username: loremipsum

```

See more about project and links in [_config.yml](./_config.yml)

## How to create a post ?

_posts create a file .md with structure:

```md
---
layout: post
title: "Lorem ipsum speak.."
date: 2016-09-13 01:00:00
image: '/assets/img/post-image.png'
description: 'about tech'
tags:
- lorem
- tech
categories:
- Lorem ipsum
twitter_text: 'How to speak with Lorem'
---
```

## How to insert new links on menu navigation ?

You should open `_config.yml` and change/add `links` section:

```yaml
links:
  section_1: # you can use any name
    - title: home # show on menu
      url: / #link
      key_trigger: 1 # link shortcut and show on the left of the title
    - title: my posts
      url: /posts
      key_trigger: 2
    - title: series
      url: /series
      key_trigger: 3
    - title: tags
      url: /tags
      key_trigger: 4
    - title: about me
      url: /about
      key_trigger: 5
```

Frontend Technologies
---------------------
* [Gulp](https://gulpjs.com/): The streaming build system.
* [Stylus](http://stylus-lang.com/): expressive, dynamic, robust CSS.
* [BrowserSync](https://www.browsersync.io/): Time-saving synchronised browser testing.
* [Rupture](https://github.com/jescalan/rupture): Simple media queries for stylus.
* [Kouto-Swiss](http://kouto-swiss.io/): A complete CSS framework for Stylus.
* [Jeet](http://jeet.gs/): A grid system for human.
* [Zepto.js](http://zeptojs.com/): The aerogel-weight jQuery-compatible JavaScript library.

## How can I modify the theme ?

First, install [jekyll](https://jekyllrb.com/) and [node.js](https://nodejs.org/).

1. Fork the theme with your username, example: `charlie.github.io`
2. Clone repository to your computer
3. run `npm install`
4. run `gulp`
5. Be happy by modifying the files

**Space Jekyll** uses the [Stylus](http://stylus-lang.com/) to process his css, then modifies the style of the theme in [this folder](https://github.com/victorvoid/space-jekyll-template/tree/master/src/styl).

You can go in the [variable.styl](https://github.com/victorvoid/space-jekyll-template/blob/master/src/styl/_variables.styl) and modify the colors. 
