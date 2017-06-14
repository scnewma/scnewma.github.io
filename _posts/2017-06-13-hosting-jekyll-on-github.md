---
title: Hosting Jekyll blogs for free!
description: This post explains how to host your Jekyll-based blog on GitHub for free.
date: 2017-06-13
---
[In our last post we got a new blog setup with Jekyll.]({{ site.baseurl }}{% post_url 2017-06-10-blogging-with-jekyll %})  But, what good is a blog if you can't share it with the world?  Today, we are going to take `super-awesome-blog` and host it on GitHub...for free!

> In this post, I'm going to assume that you have a basic understanding of git.  If you don't know what git is.  [This article](https://www.liquidlight.co.uk/blog/article/git-for-beginners-an-overview-and-basic-workflow/) should teach you everything you need to know.

## But how?
GitHub Pages is an awesome feature that _all_ GitHub project get __automatically__.  On top of that, GitHub will automatically build and publish your website for you as soon as you push your changes into the repository.  How awesome is that?  Let's get `super-awesome-blog` published already!

## Setting up your project
If you followed along from the [last post]({{ site.baseurl }}{% post_url 2017-06-10-blogging-with-jekyll %}) you already have a blog running locally, but we don't have a git repository set up for it.  Let's create one.

> If you didn't go through the previous post and want to get started here anyway.  Go ahead and [fork `super-awesome-blog` on GitHub](https://github.com/scnewma/super-awesome-blog) to get started.  You can skip the initializing git section.

### Initializing Git
Run the following commands in your project folder to get your local git repository set up.
```bash
# your current directory should be /super-awesome-blog

git init

# The _site directory will be built by GitHub so we don't want to commit it
echo "_site" >> .gitignore

# For OS X
echo ".DS_Store" >> .gitignore

echo "# Super Awesome Blog" >> README.md
```

### Creating a remote repository
Next, you need to [create a new repository on GitHub](https://github.com/new) for your blog.  ___Do not initialize it with a README file (we already did that).___

![New repository]({{ site.url }}/assets/img/hosting-jekyll-on-github/new-repo.png){:width="500px"}

### Linking your repositories
We have a local git repository, and an empty remote repository.  We need to link them up.  Running the following commands will link the two repositories and put your code on GitHub.

```bash
# You can find your exact url on your GitHub project page under clone
git remote add origin https://github.com/<username>/<project>.git

git add --all
git commit -m "first commit"

git push -u origin master
```

Now you should be able to go to your project in GitHub and see your files.

## Setting up GitHub site
So, we have our project files on GitHub.  Now we have to tell GitHub that it can use those project files to build a site for us.
We do this in the project settings. In settings, scroll down to the section called _GitHub Pages_ and set your source to the master branch and hit save.

![Pages on Master Branch]({{ site.url }}/assets/img/hosting-jekyll-on-github/github-pages-setting.png){:width="500px"}

> GitHub can also build your website from the `/docs` folder on the master branch.  This is useful when you want to create a website for another project that you have on GitHub.  Maybe some awesome library your made?

After a few minutes (the first time can take 15-20 minutes) you should be able to load your blog by going to `http://<username>.github.io`

## So now what?
Now anytime you push changes to your remote repository GitHub will automatically build your website and publish it for you, and you didn't pay anything!  That's pretty cool, right?

### Try it out
Go ahead and create a new post for your blog and push it to the remote repository.  It will appear in the post list on the homepage within a few minutes.

### With great power comes a blogging responsibility
Now you have the power to not only create a blog, but to publish it to the internet for the whole world to see.  I'm sure you'll have some really great content to share.  I will be back soon to discuss another exciting, blog-worthy topic.
