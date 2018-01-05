---
layout: post
title:  "Moving from WordPress.com to Github Pages to Netlify"
categories: jekyll update
---
**TL;DR: I migrated my homepage from
WordPress.com to GitHub Pages for speed and flexibilty,
then to Netlify for HTTPS support.**

| | WordPress.com | GitHub Pages | Netlify |
|-|:-------------:|:-------------:|:-----:|
| Easy to Use? | Yes | Use Git+Markdown | Use Git+Markdown |
| Cost | Free for basic | Free for basic | Free for basic |
| Load Speed? | Slow | Fast| Fast |
| Flexibility | Low | Very flexible | Very flexible |
| HTTPS for Custom Domain | Yes | No | **Yes** |
| Build logs | NA | No | **Yes** |

Table: Comparison of the 3 platforms.


## 1. From Wordpress.com ...

I have been using [WordPress.com](https://wordpress.com) to host my homepage at
<http://dataninja.me> for almost a year.
It was a good solution for quickly spinning up the site, but
I hit the limit as I was planning to put in more professional contents (python and R markdown stuff).
Overall, for my use cases, WordPress.com was too:
- slow (heavy overhead), 
- ugly (espeically Korean and highlighted codes), and
- inflexible (e.g. cannot change fonts easily; adding custom pages are hard).



## 2. Moving to Github Pages ...

So, I considered [GitHub Pages](https://pages.github.com/) / [Jekyll](https://jekyllrb.com/) again.
Last time when I tried to use it (~3 yrs ago),
the static site build process was clunky and it took some work to make the site look pretty.
It seems the situation has changed a lot over past couple of years.
Now, the default theme ([minima](https://github.com/jekyll/minima))
looks OK and the build process is simpler and faster.
So, unlike WordPress.com, GitHub page is:
- fast to load,
- pretty by default,
- flexible, and
- free.

I use GitHub and [Markdowns](https://daringfireball.net/projects/markdown/syntax),
especially, [R Markdown](http://rmarkdown.rstudio.com/),
almost daily anyway. So why not??
So, I decide to switch back.
The process looked like this on OSX.
(Replace <https://github.com/jaimyoung/jaimyoung.github.io> with your own GitHub Pages repo.)

0. Backup the old GitHub Pages repo, if you had one already. 
    - (In my case, this meant
        moving <https://github.com/jaimyoung/jaimyoung.github.io> to 
        <https://github.com/jaimyoung/jaimyoung.github.io-old>)

1. Install brew-maintained ruby not to pollute the OSX system ruby
(Of course, your OSX must have [homebrew](https://brew.sh/) installed already):

        brew install ruby

2. Install Jekyll per [Jekyll Quickstart Guide](https://jekyllrb.com/docs/quickstart/), i.e.

        gem install jekyll bundler
        jekyll new jaimyoung.github.io
        cd jaimyoung.github.io

4. Create github page repo
    <https://github.com/jaimyoung/jaimyoung.github.io>, and
    make the `jaimyoung.github.io` directory to track the github repo:

        echo "# jaimyoung.github.io" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:jaimyoung/jaimyoung.github.io.git
        git push -u origin master

7. Serve the test site on <http://localhost:4000/> by running:

        bundle exec jekyll serve


6. Import old WordPress.com contents per [WordPress.com to Jekyll import guide](http://import.jekyllrb.com/docs/wordpressdotcom/).
    1. First you need to install `jekyll-import` (<https://github.com/jekyll/jekyll-import>):

            gem install jekyll-import

        and a couple other dependencies.
    2. Then, export the old WordPress.com contents per direction to some xml file.
        (In my case, I exported from <https://statkwon.wordpress.com/wp-admin/export.php>
        to `datasciencefun.wordpress.2017-12-25.xml`).
    3. Copy it over the the blog directory and
        import to the page like:

            ruby -rubygems -e 'require "jekyll-import";
                JekyllImport::Importers::WordpressDotCom.run({
                  "source" => "datasciencefun.wordpress.2017-12-25.xml",
                  "no_fetch_images" => false,
                  "assets_folder" => "assets"
                })'

    4. Browse the imported files (mostly under `_pages` folder in my case),
        clean them up as needed,
        and move them to correct folders or collections.


8. Modify theme files as needed.
    - In my case, I had to overwrite:
        - `_includes/head.html` : to add font-awesome
        - `_includes/header.html` : to use custom navigation menu at the top
        - `_includes/footer.html` : to add linkedin contact as well
    
    - Find the theme files <https://jekyllrb.com/docs/themes/> by running:

            bundle show minima
            open $(bundle show minima)

        copy the files to your repo, and make necessary changes.
        See my github repo for the changes I made to above files.

0. Use [Jekyll Collections](https://jekyllrb.com/docs/collections/)
    to organize "따라 하며 배우는 데이터 과학" (my Korean data science book)
    pages under
    `_ipds-kr/` directory.

0. Set up redirect for a few pages,
    using [Redirects on GitHub Pages](https://help.github.com/articles/redirects-on-github-pages/).
    In my case, I wanted to move `ipds-kr-slides-ppt` to `ipds-kr/slides-ppt`, etc.


0. Set up and add [Disqus](https://disqus.com/) for comments.

0. Set up and add [Google Analytics](https://analytics.google.com) for site analytics.

0. Transfer `dataninja.me` custom domain from WordPress.com to
    GitHub Pages per [directions](https://help.github.com/articles/setting-up-an-apex-domain/).
    - github help page is a bit unclear; google is your friend here, which gives you
        a more thorough instructions on specific name provider.
        For namecheap.com for example, [this page](https://www.namecheap.com/support/knowledgebase/article.aspx/9645/2208/how-do-i-link-my-domain-to-github-pages) was helpful.


## 3. Then to Netlify...

Now everything *almost* works.
But it turned out that **github pages doesn't support HTTPS for custom domain.**
This is a huge problem for me since:

1. There already are quite a few
    **https:**//dataninja.me domain names on the Facebook, LinkedIn, etc.,
1. Chrome browser doesn't handle [https to http change easily](https://superuser.com/questions/565409/chrome-how-to-stop-redirect-from-http-to-https),
1. Google search engine indexing values https a lot higher than http sites, and
1. there seems to be [no plan to support https for custom domtain in github](https://github.com/isaacs/github/issues/156)

Now, Netlify(<https://www.netlify.com/>) comes to the rescue.
It is mentioned in the [above github thread](https://github.com/isaacs/github/issues/156),
as a great (free) solution that provides HTTPS support for custom domains.
I also found it mentioned in some R markdown/bookdown/blogdown sites, so it looked reputable.

The process was pretty simple and took ~10 minutes:
1. Set up netlify account and hook it up to github repo and start building.
    1. Initially, the build failed (of course) but it was easy to troubleshoot 
        thanks to the build logs like this:

            6:55:18 PM: ruby_dep-1.5.0 requires ruby version >= 2.2.5, which is incompatible with the
            current version, ruby 2.1.2p95

        So, that's a lot more transparent than github (+1).
    1. Thanks to the logs, I could track the build failure to the wrong ruby version.
    To fix, I added `.ruby-version` with `2.4.2` per [help page](https://www.netlify.com/blog/2016/10/18/how-our-build-bots-build-sites/)
    and the build succeeded.
    1. Now, the page is up and running at <https://${random_words}.netlify.com/>.
2. Set up DNS.
    Netlify provides their own nameservers, so it was pretty simple to follow their
    directions.
3. Final step is, the original requirement, to get HTTPS working.
    Again, this was super simple and HTTPS certificate was up and running in a few minutes.

After these, the site is now up and running at <https://dataninja.me/>.
Pretty sweet!

### Making Disqus comments working on Netlify
To use Disqus comments, one adds the following line in `_config.yml`:

    disqus:
      shortname: dataninja-me

This works in github pages, but Netlify version doesn't activate the comments.
It is because minima theme has the [following lines](https://github.com/jekyll/minima/blob/master/_includes/disqus_comments.html)

    if `jekyll.environment == "production"`:

until it activate disqus comments. 
The environment is set by Github Pages when the site builds,
but Netlify doesn't, hence no Disqus comments.
To fix it, per [Netlify config directions](https://jekyllrb.com/docs/configuration/),
set this environment variable in the site deploy setting:

    `JEKYLL_ENV=production`

(The URL looks like <https://app.netlify.com/sites/pensive-keller-afeae1/settings/deploys#build-environment-variables> in my case). 

Voilà, now the comments works on Netlify.

## Conclusions
I described how I migrated my homepage from
WordPress.com to GitHub Pages for speed and flexibilty,
then to Netlify for HTTPS support.

## References
- [Getting started with Jekyll - Series](https://learn.cloudcannon.com/jekyll/why-use-a-static-site-generator/) by
    CloudCannon
