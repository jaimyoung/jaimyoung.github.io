---
layout: post
title: Routine for Starting a Data Science Project in R
date: 2017-08-23 09:51:01.000000000 -07:00
categories:
- Data science
---
<p>Routine is mostly a good thing. Morning routine, gym routine, bedtime routine, etc. Thanks to routine or good habit, one doesn't spend too much time and energy on deciding on what/how to do it, saving energy for more important questions like "why".</p>
<p>Routine is mostly a good thing for data scientist, too. Here's my routine for starting a new data science project in R, large or small:</p>
<ul>
<li>Create a github repo for the project with sensible name, all lowercase and dash, no underscore (~1min)</li>
<li><code>git clone</code> to my usual project directory (<code>~/projects/</code>) (30sec)</li>
<li>Write <code>README.md</code> for what the project is about (~1min)</li>
<li>Fire up Rstudio and create RStudio project (<code>.Rproj</code>) in the directory (~1min)</li>
<li>Write the first R script, typically named <code>initial-analysis.R</code></li>
<li>First few lines of the scripts are almost always the same, like:
<ul>
<li><code>library(tidyverse)</code></li>
<li><code>df &lt;- read_csv("datafile")</code></li>
<li><code>glimpse(df)</code></li>
<li><code>df %&gt;% ggplot(aes(x, y)) + geom_....</code> : yes... this is where things start to diverge...</li>
</ul>
</li>
</ul>
<p>So, that's about 10min to hit the ground running and start producing useful stuff.</p>
<p>Once things start rolling, daily routines are similar:</p>
<ul>
<li>Bunch of data massaging, like:
<ul>
<li><code>df %&gt;% </code></li>
<li><code>group_by(x) %&gt;% </code></li>
<li><code>filter(y %in% c("good", "fine")) %&gt;% </code></li>
<li><code>summarize(mz=median(z))</code></li>
</ul>
</li>
<li>... and visualization:
<ul>
<li><code>df %&gt;% </code></li>
<li><code>ggplot(aes(x, y)) + </code></li>
<li><code>geom_... +</code></li>
<li><code>facet_wrap(~w)</code></li>
</ul>
</li>
<li>... and reporting:
<ul>
<li><code>rmarkdown::render("that-special-markdown.Rmd")</code></li>
</ul>
</li>
<li>... and <code>git commit</code> / <code>git push</code> frequently.</li>
<li>Talk to the stakeholders for questions, news, etc.</li>
</ul>
<p>But, overall, fairly automatic, fast, and effective. Yes, routine is mostly a good thing.</p>
<p><strong>What's your routine</strong> for starting a data science project in R?</p>
<p>Very different from mine??</p>
<p>Let me (and the world) know!</p>
