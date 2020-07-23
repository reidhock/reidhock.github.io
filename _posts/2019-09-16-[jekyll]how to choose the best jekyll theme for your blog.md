---
title: "[Jekyll] How to install the best Jekyll theme for your blog - part 1"
subtitle: "For people who want to make a personal blog..."
categories: [jekyll]
tags:
  - jekyll [지킬]
  - github [깃허브]
published: false
---

***
Those of you who speak Korean might have realized that I only have been posting about python algorithm quiz. When I started this blog, I wanted my blog to be informative to people who are living outside of my country as well. So from now on, I will try to write some future posts in English.

I didn't learn programming in English. So my terminology might not be perfect or very professional. A bright side is if you aren't a programmer it might be easier to understand since I don't throw out professional terms haha.

***

## What is Jekyll?
Our friend, wikipedia says
> "Jekyll is a **simple**, **blog-aware**, **static site generator** for personal, project, or organization sites. Written in Ruby by Tom Preston-Werner, GitHub's co-founder, it is distributed under the open source MIT license."

Basically, people use Jekyll because it is light and easy to use. When I first used Jekyll, I didn't know anything about it. But after 1~2 weeks, I found myself making this blog.

If you aren't a programmer, follow this post and explore later. It will be challenging but eventually you will get it. At the end of this post you will have your own blog!

## Preparation 
By following this post, you are going to post and update a blog by using some tools(SourceTree, Atom, Github) that help you manage your blog easier. Don't get scared by new tools. They are user-friendly and easy-to-use tools. (Maybe not Github...maybe...)
In this part, I am going to go through the following and explain one by one.

1. Do I even like Jekyll themes?
2. Create GitHub Account
3. Install a theme and Jekyll
4. Tools(Atom, SourceTree)

### Jekyll themes
First, you need to see if you even want to use Jekyll to make your own blog. Go visit the following links and see if there is a template that you want to use first.

[http://jekyllthemes.org](http://jekyllthemes.org/)

[https://jekyllthemes.io](https://jekyllthemes.io/)

In my case, I wanted a simple and easy-to-use theme. A theme, [Kiko_Now](https://aweekj.github.io/kiko-now/), is what I am currently using for my blog. I chose this because I didn't have to mess with a new programming language, `Ruby`, and it's easy to navigate throughout the pages.

So from here, I will continue this post based on Kiko_Now theme.

### GitHub
GitHub is commonly used to host open source projects among many programmers. I understood it as programmers' facebook/Google Drive. They share their codes and applications they've built and comment on each other's work through GitHub. Lastly, they can save their work in Github repository. In our case, we are going to use GitHub for free repositories and a free blog domain name. If you want to know more, click the following youtube video link that GitHub provides.

[Introduction to GitHub Pages](https://youtu.be/2MsN8gpT6jY)

So now we know what theme we want to use. The next step is creating a new Github account. if you already have an account, you can skip this part.
Go to [GitHub](https://github.com/) and create a new account.

I highly recommend to read all the tutorials and guides. You don't have to understand but just get a sense of it. That is enough for now.

Once you successfully make a new account(GitHub might make you create a new repository. Don't get scared. Just make one for them haha), next step is going to a `fork` Kiko_Now theme. `fork` is an action that you copy all the files and folders from a repository that you want to copy to your repository. Go to [https://github.com/AWEEKJ/kiko-now](https://github.com/AWEEKJ/kiko-now). Then you will see this.

![_config.yml]({{ site.baseurl }}/images/2-jekyll-2019-09-16.png)

Click `fork`. Then it will copy this repository to yours. Now if you go to your own repository, you will see the exact same title and contents on your repository.


**This is a very important part.** click the repository that you just forked then you will see this.

![_config.yml]({{ site.baseurl }}/images/3-jekyll-2019-09-16.png)

Now we are going to change the name(`Kiko_Now`) to `your account name`. Go to settings and change your repository name as (USERNAME.github.io). In my case, it will be `reidhock.github.io`. This will be your blog address!

![_config.yml]({{ site.baseurl }}/images/4-jekyll-2019-09-16.png){: width="50%"}

If you followed everything, it is going to look like this. It is up to you how you are going to write new posts. You can either edit on github or you can download on your computer and edit locally. In this post, we are going to use tools such as Sourcetree and Atom that help you to upload your works from your computer to Github repository. They are free tools and you can easily download online. here are the links to download those two tools.

[SourceTree](https://www.sourcetreeapp.com/)

[Atom](https://atom.io)

Now you are ready to download your repository to your local computer.

![_config.yml]({{ site.baseurl }}/images/5-jekyll-2019-09-16.png)

Click `clone or download` and `open in desktop` and download the repository in your local computer. Github will ask you if you want to open it with sourcetree. click `open sourcetree`. if you see this window, you did everything right so far(I already have my own blog folder, so it might look little different).

![_config.yml]({{ site.baseurl }}/images/6-jekyll-2019-09-16.png)

Then you are ready to write a new post on your laptop!

If you followed till here, well done! You haven't given up! I didn't realize when I started this post, it is going to be this long. So I am thinking to separate this post into two or three. Until the next post, it would be good for you to explore Github and study how the system works.

Thank you!
