---
layout: post
title:  "Move back to Jekyll from wordpress.com"
date:   2017-12-24 18:14:47 -0800
categories: jekyll update
---

## Why?

I used wordpress.com to host <http://dataninja.me> page for a while.
It was useful for quickly spinning up a site, but
I hit the limit as I was planning to put in more professional contents (python and R markdown stuff).
Overall, for my use cases, wordpress.com was too
    - slow, 
    - inflexible, and
    - ugly by default (I ) general

So, I look at github pages / Jekyll again.
Last time when I tried to use it (~3 yrs ago),
it was not pretty, and build process was clunky.
It seems the situation has changed over past couple of years.
The default theme (`minima`) is OK on the ideas and build is simpler.

I use github and markdowns daily anyway, so why not?
So, I decide to try it again.


## How?

0. Move the old github repo 
    <https://github.com/jaimyoung/jaimyoung.github.io> to 
    <https://github.com/jaimyoung/jaimyoung.github.io-old>
1. Install brew maintained `ruby` not to pollute the OSX system ruby:

        brew install ruby

2. Follow <https://jekyllrb.com/docs/quickstart/>, i.e.

        gem install jekyll bundler
        jekyll new jaimyoung.github.io
        cd jaimyoung.github.io

4. Create github repo
    <https://github.com/jaimyoung/jaimyoung.github.io> again, and
    make the `jaimyoung.github.io` directory to track the github repo:

        echo "# jaimyoung.github.io" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:jaimyoung/jaimyoung.github.io.git
        git push -u origin master

7. Serve the test site on <http://localhost:4000/>

        bundle exec jekyll serve


6. Import old wordpress.com contents per <http://import.jekyllrb.com/docs/wordpressdotcom/>.
First you need to install `jekyll-import` (<https://github.com/jekyll/jekyll-import>):

        gem install jekyll-import

    (and a couple other dependencies)
    and export the stuff at <https://statkwon.wordpress.com/wp-admin/export.php>.
    You have `datasciencefun.wordpress.2017-12-25.xml` file.
    Copy it over the the blog directory and
    import to the page like:

        ruby -rubygems -e 'require "jekyll-import";
            JekyllImport::Importers::WordpressDotCom.run({
              "source" => "datasciencefun.wordpress.2017-12-25.xml",
              "no_fetch_images" => false,
              "assets_folder" => "assets"
            })'

    and clean up the files.
    This involves some manual edit and may be a big pain if your site
    has than a dozen files.

8. Find the theme files <https://jekyllrb.com/docs/themes/> by running:

        bundle show minima
        open $(bundle show minima)

    and modify a few files.
    In my case, I had to overwrite:

    - `_includes/head.html` : to add font-awesome
    - `_includes/header.html` : to use custom navigation menu at the top
    - `_includes/footer.html` : to add linkedin contact as well

0. Fix old links via `redirect` for a few pages, per
    <https://help.github.com/articles/redirects-on-github-pages/>

0. Use `collections` to organize <따라 하며 배우는 데이터 과학> pages under
    `_ipds-kr/` directory.

0. Add back Disqus
0. Add back google analytics
0. Domain transfer per <https://help.github.com/articles/setting-up-an-apex-domain/>
