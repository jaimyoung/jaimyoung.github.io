---
layout: post
title: Data Science DevOps and Docker
date: 2017-08-05 22:58:36.000000000 -07:00
categories:
- Data science
tags:
- devops
- docker
- R
---
<p>Data scientists sometimes have to (help) “productionize” their work, i.e. integrate data analysis, dashboard, and predictive modeling into a larger process or software pipeline. For example, imagine a system that (1) monitors for a data change, (2) triggers data analysis process whenever a change happens, and (3) takes the output of the analysis to show a webpage and/or store output parameters in a database for other systems to use.</p>
<p>Data scientists typically work in part (2), prototyping bunch of R or python codes. But when it’s time to build and deploy the system, integrating such data science codes is not trivial. A big challenge is that Data scientists' work environment (e.g. Macbook laptop with R and many, many, many R packages) is typically very different from a “deployment” environment (e.g. linux box in AWS EC2 or corp VMs). Installing R and bunch of dependency R libraries on the machine is frowned upon by ops and software engineers, since it’s usually a painful, fragile process.</p>
<p>In an ideal world, R / python codes data scientist developed on their laptop would “just work” when dropped on the deployment server(s). Too good to be true?? Well, that ideal world is here already thanks to the fantastic technology called “<a href="https://www.docker.com/">Docker</a>”. Using Docker, data science analysis and prototype could become super close to something that could be deployed very fast and efficiently. Just like devops helped developers productionize and operationalize their work better. We can even call it “data science devops”.<img class=" size-full wp-image-509 alignright" src="{{ site.baseurl }}/assets/vertical_large.png" alt="vertical_large" width="286" height="237" /></p>
<p>Essentially, the first step to achieve data science devops consist of two practices:</p>
<ol>
<li><strong>Make the R codes into a command line script</strong> that could be executed via <a href="https://stat.ethz.ch/R-manual/R-devel/library/utils/html/Rscript.html">Rscript</a>, preferably with advanced option parsers like <a href="https://cran.r-project.org/web/packages/argparse/index.html">R argparse</a>. This has the added benefit of forcing <a href="https://en.wikipedia.org/wiki/Reproducibility">reproducibility</a>. Also data scientists are forced to think more in terms of API way and “<a href="https://en.wikipedia.org/wiki/Unix_philosophy">do one thing well</a>” (UNIX philosophy) mentality that lead to cleaner code structure.</li>
<li><b>Dockerize the R application</b>. Start with, e.g. <a href="https://hub.docker.com/r/rocker/verse/">rocker/verse</a> and <a href="https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/">add/modify</a><a href="https://github.com/rocker-org/rocker-versioned">Dockerfile</a> as needed.</li>
</ol>
<p>With the above two practices, on any machine with Docker installed, the app could be "deployed" like:</p>
<pre>$ docker pull your-org/my-r-app</pre>
<p>and could be run like:</p>
<pre>$ docker run your-org/my-r-app ARG1, ARG2, ...</pre>
<p>The beauty is that, it will run in ANY environment where Docker is installed: your Mac or Windows laptop, EC2 linux host, Your corp VM, and so on.</p>
<p>Is it actually easy? NO. You actually need to spend good ~100 hours or so to be at home writing your own Dockerfile with confidence. Is learning how to dockerize R app helpful? YES, very much so. Once you make the habit of developing your R analysis pipeline in a Dockerized, reproducible setting, your codes will be cleaner, more reproducible, and super easy to deploy. Your dev / ops coworkers will thank you. You and your team’s productivity will improve (YMMV).</p>
<p>So, dear fellow data scientists --- <a href="https://docs.docker.com/engine/installation/">install Docker</a> and <a href="https://docs.docker.com/get-started/">start learning how to use it;</a> Welcome to data science devops.</p>
<p>&nbsp;</p>
