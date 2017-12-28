---
layout: post
title:  "Move back to Jekyll from wordpress.com"
date:   2017-12-24 18:14:47 -0800
categories: jekyll update
---

## 1. Why?

I used wordpress.com to host <http://dataninja.me> page for a while.
It was useful for quickly spinning up a site, but
I hit the limit as I was planning to put in more professional contents (python and R markdown stuff).
Overall, for my use cases, wordpress.com was too
- slow (heavy overhead), 
- ugly (espeically Korean and highlighted codes), and
- inflexible (e.g. cannot change fonts; adding custom pages are hard).

So, I look at github pages / Jekyll again.
Last time when I tried to use it (~3 yrs ago),
it took some work to make it look pretty, and build process was clunky.
It seems the situation has changed over past couple of years.
Now, the default theme (`minima`) looks OK and build is simpler and faster.

I use github and markdowns daily anyway, so why not?
So, I decide to try it again.


## 2. How?

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
    - github help page is a bit unclear; google is your friend here, which gives you
        a more thorough instructions on, say for namecheap.com,
        <https://www.namecheap.com/support/knowledgebase/article.aspx/9645/2208/how-do-i-link-my-domain-to-github-pages>


## 3. Netlify for HTTPS!

Now everything *sort of* works.
But it turned out that github pages doesn't support HTTPS for custom domain.
This is a huge problem since

1. there already are quite a few
**https:**//dataninja.me domain names on the network.
1. Chrome browser doesn't handle https to http change easily: 
    <https://superuser.com/questions/565409/chrome-how-to-stop-redirect-from-http-to-https>
1. Google search engine indexing values https a lot higher than http sites, and
1. there doesn't seem to be a plan to support this in github.
    <https://github.com/isaacs/github/issues/156>

So, <https://www.netlify.com/> comes to the rescue.
(It is mentioned in the above github thread).
It took ~5min to set up netlify and hook it up to github repo and start building.

Initially, the build failed (of course) but it was easy to troubleshoot 
thanks to the build logs like this:
```
6:55:18 PM: ruby_dep-1.5.0 requires ruby version >= 2.2.5, which is incompatible with the
current version, ruby 2.1.2p95
```
So, that's a lot more transparent than github (+1).
Thanks to the logs, I could track the build failure to the wrong ruby version.
To fix, I added `.ruby-version` with `2.4.2` per
<https://www.netlify.com/blog/2016/10/18/how-our-build-bots-build-sites/>
and the build succeeded.
Now, the page is up and running at <https://${random_words}.netlify.com/>.

Next step is set up DNS.
Netlify provides their own nameservers, so it was pretty simple to follow their
directions.

Final step is, the original requirement, to get HTTPS working.
Again, this was super simple and HTTPS certificate was up and running in a few minutes.

### Making disqus working again
The newly deployed page doesn't have disqus comments activated.
It was this code snippet of minima theme checks
if `jekyll.environment == "production"`:
<https://github.com/jekyll/minima/blob/master/_includes/disqus_comments.html>
It seems github pages set up the env variable, but netlify doesn't.
This is an easy fix: following <https://jekyllrb.com/docs/configuration/>,
set this environment variable in the setting:
<https://app.netlify.com/sites/pensive-keller-afeae1/settings/deploys#build-environment-variables>
`JEKYLL_ENV=production`

Voilà, now the comments works.
