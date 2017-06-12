---
title: "How to start blogging with Jekyll"
description: "Get up and running with Jekyll.  This post explains how to install Jekyll and how to get a simple blog up and running."
date: 2017-06-10
---

## What is Jekyll
[Jekyll](https://jekyllrb.com/) is a framework for building static websites.  It allows you to create templates to code your websites dynamically while only serving static content.  This means that you don't have a backing datastore to store all of your assets, it's stored right in the directory structure.

If all you are providing is static web pages, this paradigm is going to help you build the fastest websites possible!  Everything is built at compile-time.  Obviously, the lacking datastore is a limitation, but there are a lot of websites ___(like blogs!)___ that do not need this.

## Installing Jekyll
This is a quick explanation on how to get Jekyll installed locally using Ruby and RubyGems.  If you don't have Ruby installed, and are on OS X, I would suggest [installing via Homebrew](https://www.ruby-lang.org/en/documentation/installation/#homebrew).  Doing so will give you everything you need.

So, to install the Jekyll RubyGems dependencies run the following:
```
gem install jekyll bundler
```

That installs both the Jekyll and the Bundler RubyGems and should give you everything you need.  You can verify
that your installation worked successfully by checking your Jekyll version.
```
jekyll --version
```

If you have any issues, you should check out the [Jekyll troubleshooting guide](https://jekyllrb.com/docs/troubleshooting/).

### Windows
Follow the [Jekyll on Windows installation instructions](https://jekyllrb.com/docs/windows/).

## Starting your blog
Jekyll gives us a simple command to create a new blog using the default template.  Let's do that now.
```
jekyll new super-awesome-blog --blank
```

That will create a new `super-awesome-blog` directory in your current directory.  _We use the `--blank` flag because by default Jekyll installs a theme for us.  For learning purposes, we are going to create our own "theme"._
Open it up and see what it gives us.
```
super-awesome-blog
+-- _drafts		
+-- _layouts
+-- _posts		
+-- index.html
```

Quick explanation of the files we get above.  
- `_drafts` is where your draft blog posts will go.  _For brevity, I'm not going to cover this directory in this post_
- `_layouts` is where the your...LAYOUTS!... will go.
- `_posts` is where all of your blog posts will be housed.
- `index.html` is the default file that will load.

We will go more into these in a minute, but first, let's see what our new blog looks like by running `jekyll build` from the `super-awesome-blog` directory and then opening `/_site/index.html` in your browser.

> ___What did I do wrong?! There is nothing there!___

That's because we didn't put anything in the `index.html` file.  Go ahead and put the following in there now.
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Super Awesome Blog</title>
  </head>
  <body>
    <h1>Welcome to my Super Awesome Blog!</h1>
  </body>
</html>
```

Run `jekyll build` again and refresh your browser.  Now we have a functional(ish) website.

> It would get really annoying if we had to run `jekyll build` every time we made a change to our page.  Luckily Jekyll provides a couple of different options to make this easier.  1) You can run using `jekyll build --watch` and Jekyll will automatically rebuild your site everytime you save a file.  2) The better option, would be to run a local server so that it's served as a webpage just like when you put it on the internet.  You can do that with the following `jekyll serve`.  This does the same as `jekyll build --watch` with the added benefit of serving your site on `localhost:4000`.  This is what I'm going to assume you are doing for the remainder of this post.

## Basic page layout
Now let's create a basic page layout.  If you don't understand what's going on here, just keep following along.  It will make more sense in a minute.

Create a new file `_layouts/default.html` and move your the content from `index.html` in there.  Then in `index.html` replace everything with:
```yaml
---
layout: default
---
```

> This section is what Jekyll calls _front-matter_ and is designated by a block of `yaml` surrounded by `---` at the top of a page.  This front-matter is metadata about your page.  It can be used for a variety of different things, which we will explore soon.

If you refresh you browser, everything should look as before.  This is where the power of Jekyll starts to shine.  We just created a reusable layout that can be used on any page we create.  

Let's go ahead and style that template a little bit and explore this a bit more.  After styling this is our `_layouts/default.html`.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Super Awesome Blog</title>

    <style>
      /* mini reset */
      html, body {
        padding: 0;
        margin: 0;
      }
      /* end reset */

      nav {
        width: 100%;
        background-color: #ccc;
        padding: 1rem;
      }
    </style>
  </head>
  <body>
    <nav>
      <h1>Super Awesome Blog!</h1>
    </nav>
  </body>
</html>
```

## First post
Now we can create our first blog post, and we can utilize the layout that we just created.  Create a new file `_posts/2017-06-10-first-post.md` and put the following inside of it:
```md
---
layout: default
---

# Welcome
This is my first post on this awesome blog that I just created.

## What to expect
Expect more awesome blogs coming in the future.
```

Also add the following below the `<nav>` element in `_layouts/default.html`.
```html{% raw %}
<div class="content">
  {{ content }}
</div>
{% endraw %}```

Now you can load the blog post in your browser by going to `localhost:4000/2017/06/10/first-post`

Ok.  This requires a little bit of explanation.  First your post.  The format that we named our file is a requirement by Jekyll, so if you don't follow that format, it's not included in your site.  Go ahead, try it.  So, Jekyll requires your post names to be in the following format.
```
YEAR-MONTH-DAY-title.MARKUP
```

Second, you noticed that we were able to use markdown files (`.md`) directly and Jekyll converts it directly to HTML.  That's pretty awesome.  By default Jekyll uses kramdown for markdown support.  On top of markdown support, Jekyll can directly output textile and asciidoc as well.  [Learn more about Jekylll converters.](https://jekyllrb.com/docs/plugins/#converters-1)

Finally, remember that we had to add `{% raw %}{{ content }}{% endraw %}` to the default template.  This tells Jekyll that this part of the page will be provided by a sub-page (like our blog post).  The page that uses the default layout will now be able inject content into the layout.  The `content` that we are talking about is literally everything that appears after the front-matter (`---` block).

## More variables
So, we say that we can use the `content` variable to inject the page content into our template, but what if we need to inject more than one piece of information.  Let's have our blog post control the website title so that our users can easily distinguish our blog posts when they have multiple open.

In `_layouts/default.html` update the `<title>` element to `<title>{{ page.title }}</title>`.  Now, in your blog post add a title property to your front-matter, like so:
```yaml
---
layout: default
title: "First Post"
---
```

Now when you refresh your blog post, you will see the title update.  You can do this with almost anything.  We will explore this concept in more detail in the future.

## Better Home Page
So, we can create blog posts in Markdown and our users can navigate to them in the browser, but how are they going to find them?  We need a page where our user's can view a catalog of all of the awesome posts we have written.

Open up `index.html` and add the following as your `content`.
```html
<div class="container">
  <h1>Blog Post Archive</h1>

  {% for post in site.posts %}
    <a href="{{ post.url }}" class="post">
      <p class="title">
        {{ post.title }}
      </p>
      <p class="subtitle">
        {{ post.date | date: "%B %d, %Y" }}
      </p>
    </a>
  {% endfor %}
</div>
```

And add the following styles to the default layout.
```css
.container {
  padding: 2rem 5rem;
}

.post {
  display: block;
  padding: 1rem;
  background-color: #ccc;
  border-radius: 1.5rem;
  color: #000;
  text-decoration: none;
}

.post .title {
  margin: .25rem 0;
  font-size: 1.5rem;
}

.post .subtitle {
  margin: .25rem 0;
  font-size: 1.25rem;
}
```

Navigating to `localhost:4000` you should see a list of blog posts (which is just the singular blog post right now).  And you can click on the post, and it will navigate you directly to the blog post, just as you would expect.

There is a little more "magic" here that needs explanation.
```liquid
{% raw %}
  {% for post in site.posts %}
{% endraw %}
```
This is the [Liquid templating system](https://github.com/Shopify/liquid/wiki) syntax for looping.  The real magic is that you are able to access all of the blog posts via the `site` variable.  Jekyll does this automatically because we put all of our posts in the `_posts` directory.  Also, we can access variables that exist in the front-matter of the post like this `{{ post.title }}` or `{{ post.date }}`.  

> But what about `{% raw %}{{ post.url }}{% endraw %}`?  We didn't define that in the front-matter.

Jekyll automatically adds a couple of variables to our post for us.  One of these is `url`.  These variables can save us a lot of work, so make sure to utilize them.  [Read more about Jekyll page variables.](https://jekyllrb.com/docs/variables/#page-variables)

## Wrapping Up
We have covered a lot of information in this first post about Jekyll.  There will be more posts about Jekyll here in the future to expand on these topics and cover even more powerful features in Jekyll.  Most of the following blog posts will be much shorter, so they can be consumed much easier.

You can see the final code for `super-awesome-blog` on my [GitHub](https://github.com/scnewma/super-awesome-blog).
