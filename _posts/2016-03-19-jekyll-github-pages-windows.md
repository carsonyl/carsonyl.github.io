---
layout: post
title:  "Set up Jekyll for GitHub Pages, on Windows"
categories: web jekyll
---

It's fairly easy to set up a Windows [Jekyll] environment for [GitHub Pages], even though Jekyll doesn't officially support Windows. It's even easier if you've got [chocolatey] installed. Here's how.

First, install chocolatey if you don't already have it. Open an elevated Command Prompt and run:

~~~
C:\> @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
~~~

Restart Command Prompt. Install Ruby, GitHub Pages' Jekyll bootstrapper, and its dependencies. You may need to restart Command Prompt again after installing Ruby so that it'll appear in your path.

~~~
C:\> choco install ruby ruby2.devkit -y
C:\> gem install github-pages
~~~

`github-pages` includes Jekyll and all the gems available in GitHub Pages. Keep up with the state of GitHub Pages by keeping this gem up to date. `ruby2.devkit` is needed to build dependencies such as RedCloth.

If you've already cloned the repository for your GitHub Pages site, and haven't already set up Jekyll in it, `cd` into the directory and initialize Jekyll with `jekyll new . --force`.

`jekyll serve` will serve your site and automatically detect changes as you go. Really old versions of Jekyll need a separate gem to detect file changes on Windows.

[Visual Studio Code] is a fairly good editor to use with Jekyll. It has syntax highlighting and preview for Markdown, too.

[Jekyll]: https://jekyllrb.com/
[GitHub Pages]: https://pages.github.com
[chocolatey]: https://chocolatey.org
[Visual Studio Code]: https://code.visualstudio.com
