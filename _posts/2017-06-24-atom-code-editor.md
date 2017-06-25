---
title: "Code Editor Preferences: Atom"
description: The customizations that I make to the Atom code editor to make it work the best for me.
date: 2017-06-24
tags:
  - atom
---
Whenever I'm working with Javascript, HTML, CSS, or anything else web related, I'm usually using the [Atom editor](https://atom.io/).  I prefer Atom because it is fast, works on all platforms, and has an extensive library of plugins to make it fit your needs.  I'm going to go over some of the preferences that I have setup in Atom to make it even better for me and maybe you will appreciate some of them too.

## Theming
Like most other editors, Atom is fully customizable.  I really like _(maybe a little bit obsessed)_ with the [solarized color theme](http://ethanschoonover.com/solarized) _(Solarized Dark to be exact)_.  I have it on everything that I can, even my entire Ubuntu desktop.  Anyway, it's built into Atom, so, that makes it super easy.

You can change the color scheme in preferences > themes. Solarized dark is a syntax theme, but it also colorized your editor as well.

## Editor settings
These are the essential settings that I turn on in the editor preferences.

#### Scroll Past End
I personally hate working towards the end of the file.  I like my current work to be in the middle of the screen.  With this enabled you can scroll past the end of the document without needing to put extra line breaks at the end of the document.
![Scoll past end]({{ site.url }}/assets/img/atom-code-editor/scroll-past-end.png){:width="500px"}

#### Show Indentation Guide
If you are working in code with a lot of nesting (tends to happen to me a lot in HTML) this makes it easy to determine the starting and ending blocks.  Also makes it easy to keep your code or markup clean.
![Indentation Guide Example]({{ site.url }}/assets/img/atom-code-editor/indentation-guide.png){:width="500px"}

#### Use Soft Tabs
Spaces are better than tabs :).  Anyway, I prefer spaces, so I make atom use spaces instead of tabs.  This is up to you.

## Hide Files in Tree View
One of the other essentials is to hide the files that you don't need to see in the tree view.  If you go to your packages, search for `tree-view` then click settings, you can select the options "Hide Ignored Names" and "Hide VCS Ignored Files".  The "Ignored Names" are setup in the general settings in Atom, while "Hide VCS Ignored Files" will automatically read your `.gitignore` and hide those files in the tree-view.

Since you don't need to access these files often it declutters your workspace, making it easier to find what you are looking for.  If you need to view these files for some reason (maybe `node_modules`) you can quickly toggle this feature by focusing the tree-view (`ctrl-0`) and then hitting `i` (on macOS anyway).

## Disable Unneeded Packages
Packages are why Atom is so awesome, but it comes with a few too many by default (at least for me).  I suggest going into packages and disabling the packages that you don't need.  This will help with performance and start-up time.

I always disable the following:
- about
- background-tips
- welcome
- wrap-guide _(removes the vertical line from the editor which I don't like)_
- language-* _packages for the languages that I don't use (perl, php, etc)_

## Installing Awesome Packages
Currently these are the packages that I use all of the time.  I often try out new packages to see what works and what doesn't.  This is a list of the ones that I'm always using.  They have a special place in my workflow.

#### Emmet
[Emmet](https://atom.io/packages/emmet) is my favorite plugin by far.  Basically, Emmet does expansion, making it easy to compose HTML very quickly.  For example I can type `ul.nav>li.nav-item*4` hit `tab` and it will create the following structure.  It's very powerful.

```html
<ul class="nav">
  <li class="nav-item"></li>
  <li class="nav-item"></li>
  <li class="nav-item"></li>
  <li class="nav-item"></li>
</ul>
```
> [Learn more about Emmet expansions](https://docs.emmet.io/actions/expand-abbreviation/).

#### File-Icons
The [file-icons package](https://atom.io/packages/file-icons) makes the tree-view look a little better by replacing the standard file icon with icons depending on the type of files that are there.  It's mostly aesthetic, but it can make it a little easier to find the file you are looking for.

![Tree View with Icons]({{ site.url }}/assets/img/atom-code-editor/file-icons.png){:width="300px"}

#### Open in Browser
[Open in Browser](https://atom.io/packages/open-in-browser) is useful if you are testing something on a basic HTML page, or have a site that doesn't have dev server, then this plugin can make it a lot easier to launch your site in the browser.  If you are inside of an HTML page you can right-click and open the page in your default browser.

#### Pigments
[Pigments](https://atom.io/packages/pigments) adds some color to your CSS.  It will change the background color of your hex, rgb, and rgba colors to the color depicted making it easy to see what colors your site has.  Another awesome perk is that it works with SASS variables and the `lighten` and `darken` functions so you can tell what colors are going to be produced without needing to go to your browser.

![Pigments Example]({{ site.url }}/assets/img/atom-code-editor/pigments.png){:width="500px"}

> To get the dots on the right instead of the background-color behind the text visit the pigment package's settings and change the `marker-type` to either `dot` or `native-dot`.

## Conclusion
The Atom editor is great out of the box, but you should definitely customize it to fit your needs/preferences.  You will be much for efficient, and it will be a more pleasant experience.

Also, there are plenty of packages that I didn't cover in this short post, make sure to go and check out the [Atom package repository](https://atom.io/packages) to see what will help improve your coding experience.
