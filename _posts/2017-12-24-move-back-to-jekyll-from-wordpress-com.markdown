---
layout: post
title:  "Move back to Jekyll from wordpress.com"
date:   2017-12-24 18:14:47 -0800
categories: jekyll update
---

Why?

1. Wordpress.com is great while it lasts, but it's slow, not free, and inflexible.
2. I use github daily already.

How?

0. Move the old github repo `jaimyoung.github.io` to `jaimyoung.github.io.old`
1. Install brew maintained `ruby` not to pollute the OSX system ruby:

        brew install ruby

2. Follow <https://jekyllrb.com/docs/quickstart/>, i.e.

        gem install jekyll bundler

3. Do:

        jekyll new jaimyoung.github.io
        cd jaimyoung.github.io

4. Create `jaimyoung.github.io` github repo.
5. Make the `jaimyoung.github.io` directory to track the github repo:

        echo "# jaimyoung.github.io" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:jaimyoung/jaimyoung.github.io.git
        git push -u origin master

6. Import old wordpress.com contents per <http://import.jekyllrb.com/docs/wordpressdotcom/>.
First you need to install `jekyll-import` (<https://github.com/jekyll/jekyll-import>):

        gem install jekyll-import

and export the stuff at:

        <https://statkwon.wordpress.com/wp-admin/export.php>


7. Serve the test site on <http://localhost:4000/>

        bundle exec jekyll serve


TODO:
1. Add back disqus
2. More cleanup