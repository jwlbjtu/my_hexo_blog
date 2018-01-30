---
title: Get back on blogging
date: 2018-01-13 16:26:50
categories: 
- [Life] 
tags:
- other 
---

It has been a while since I posted my last blog. Today I finally find sometime setting up this new blog site that has a nice looking theme. Now I am feeling so existed to start the new blogging journey!! 

As the first post, let's talk a little about how I create this blog site. 
<!-- excerpt -->
### Hexo - Blog Framework
[Hexo](https://hexo.io/) is a NodeJS based blog framework. The set up is very easy, the only two things you need are NodeJS and Git. Once you have it installed and initialized, you can start blogging right away. Hexo is a complete package by itself. 

All the posts are writen by MarkDown (*.md) files, and later Hexo will traslate them into static HTML files during the process of pulishing. The vanilla Hexo already has Post, Archive, Categorize and Tags fundctions. By installing themes on Hexo you could also get Searching and Comment widgets. Hexo also has plugins like Google Analytics, Swiftype, Disqus e.g. So you would get anything you need to start a blog with Hexo. 

The best thing is all the plugins and widgets above are easyly configured in one _config.yml file. No code writing at all! 

**Useful Links**
- [Hexo Doc](https://hexo.io/docs/)
- [Hexo Theme](https://hexo.io/themes/)

### Hosting the blog on GitHub Page
I hosted my blog site by using GutHut Pages. It is a free and easy way to host a web application. Hexo has a deploy plugin for automatically deploy the blog onto GitHub. Details please check out the deployment section of Hexo Doc. Below are the links I found are very helpful:
- [GitHub Pages](https://pages.github.com/)
- [How to setup a blog on github with Hexo](https://zirho.github.io/2016/06/04/hexo/)
- [Setting up a custom domain](https://help.github.com/articles/quick-start-setting-up-a-custom-domain/)

**Tips:** GitHub Pages requires you to create a repository with name like {username}.github.io, username is your GitHub username. Once you have the repositoy created, please **DO NOT** try to push all the Hexo source code into that repo. How Hexo works is that it will generate static web content based on the local source code and then push only the static content to the repo. And GitHub will scan the repo and set up a host for it. 

So after you create the repository please leave it empty, and then follow the [document](https://hexo.io/docs/deployment.html) to configue the _config.yml file. After that just execute the command below Hexo will handle everything for you. After the command is done you should see that static contents are pushed into your repository. 
``` bash
$ hexo deploy
```

****
Here is the link to my old blogs [Old blogs](https://jiangwl.wordpress.com/2013/12/09/interact-with-mongodb-by-java/)
