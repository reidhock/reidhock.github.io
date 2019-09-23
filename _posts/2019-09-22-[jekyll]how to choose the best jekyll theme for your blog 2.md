---
title: "[Jekyll] How to install the best Jekyll theme for your blog - part 2"
subtitle: "For people who want to make a personal blog..."
categories: [jekyll]
tags:
  - jekyll [지킬]
  - github [깃허브]
published: true
---

***
We are going to pick up what was left in the [last post(How to choose the best jekyll theme for you blog - part 1)](https://reidhock.github.io/jekyll-how-to-choose-the-best-jekyll-theme-for-your-blog/). As I said, it might be tough if it is your first time to use all the tools I introduced or I will. However, the key is go through the difficulties and play with new tools. I guarantee that you will get it eventually. Even I did it. haha Let jump in.

***

Now you have your repository in your laptop and a tool to edit the repository(Atom) and help you upload local changes to Github(Sourcetree).

Let's open Atom you download since last post. If you don't know what Atom is go to the their [website](https://atom.io/) and explore. If you are too lazy to read everything, just think that it is basically a tool that helps you to write and edit files and navigate a folder.

Let's find your repository in your computer. go to `file` and `open...` and find where you downloaded the repository in your laptop. Then you will look at this.

![_config.yml]({{ site.baseurl }}/images/1-jekyll-2019-09-22.png)

Before we touch anything here, you need to download a plugin that allows you to use `terminal` in Atom. Go to preferences. Then, you will see install menu and type and install platformio-ide-terminal. After installing the plugin, you will be able to find litte `+` button on the left bottom.
![_config.yml]({{ site.baseurl }}/images/2-jekyll-2019-09-22.png)

if you click the `+` button. you will see terminal in Atom. you don't have to download the plugin but I find it useful.

![_config.yml]({{ site.baseurl }}/images/3-jekyll-2019-09-22.png)

Now, if you don't know what terminal is and you think this terminal window seems scary just copy and paste what I wrote here. In order to use Jekyll, of course you need to install jekyll and we are going to do that in terminal.
type `gem install github-pages`. This install plugins like Jekyll, Sass, etc.
Now you can see the changes on the repository folder by typing `jekyll serve`.
I will explain more about this later but it is faster and easier to see the changes right away instead commit and push to github respository and then see the changes.

Now, let's explore the folder/kiko_now theme based blog.

![_config.yml]({{ site.baseurl }}/images/4-jekyll-2019-09-22.png){: width="50%"}

The folder names speak for theirselves. I will briefly explain these folders.

`_includes` is a folder that is used for many pages so the creator of this theme put them separately to avoid repeating the code.

`_layout` is a folder that determines how the page would look.

`_post` is where everything happens. You will write new post here, using `markdown` format. Markdown is basically is one of markup languages that help you to write and add some features easily on web. By using this, you don't have to know all that jazz about html language.

`_sass` is a folder that makes your blog fancier with lots of colors and fonts.

`_site`, `.sass-cache`, `.git` are not necessarily important to know so I will skip.

`archive`, `theme`, `tags` will be shown in menu navigation. you can delete `theme` folder. Actually you should haha. if you click it, you will know why.

`images` is where you store all the images for you post.

if you look down, you will see `config.yml` file. It is like root of your blog. It takes care of basic settings. For now, let's just leave how it is and change it later.

As I shortly mentioned, you can check your blog locally by typing `jekyll serve` in `terminal`. Click `+`button on the left bottom of Atom window and type 'jekyll serve'. You should see this.

![_config.yml]({{ site.baseurl }}/images/6-jekyll-2019-09-22.png)

Now open your browser and in address menu type `localhost:4000`.

![_config.yml]({{ site.baseurl }}/images/7-jekyll-2019-09-22.png)

then you should be able to see the kiko_now theme blog in your browser.

***
It is actually taking a lot of effort to cover all the stuff to make a blog. So I will stop it here. who knows, it will have part-3000. haha if you have any questions please leave a comment. I will answer it as soon as I can.

***
