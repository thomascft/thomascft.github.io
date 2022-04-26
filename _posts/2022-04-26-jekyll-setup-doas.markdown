---
layout: post
title:  "Setting up Jekyll with opendoas"
date:   2022-04-26 14:05:26 -0600
categories: jekyll update
---

## The Story

I recently bought a domain, and decided to setup a blog with github pages. During setup I ran into some interesting problems with doas, a minimal replacment for sudo. Bundle the ruby package manager kept trying to install gems to system directories, and when trying to call `sudo -K` failed due to the fact that I symlinked my sudo binary to doas, and doas dosen't have that specific flag. The fix, well upon reading currently github-pages dosen't support ruby 3.0.0, so I installed rbenv from the aur. [Rbenv](https://github.com/rbenv/rbenv) manages ruby versions and paths, and by following the [install](https://github.com/rbenv/rbenv#installation) guide you can fix the problems with ruby versions.

## The Actual Fix

### Prerequsites

- rbenv
- text editor
- some patience

### Ok...

So.. Now the good stuff. Create a repo on GitHub named `your-username.github.io`, and clone it to a local directory with:  
`git clone https://github.com/your-username/your-username.github.io`  
Once that's complete, run `rbenv install version` with version being a version of ruby (I used 2.7.6). Then set the project specific ruby version by typing `ruby local 2.7.6`. This creates a .ruby-version file and sets the local version. Now that you have ruby install Jekyll and Bundler with `gem install jekyll bundle` in your project root. After they install create a new Jekyll site with `jekyll --skip-bundle new .`. and open the `Gemfile` in your choice of editor. Comment the line that says `Gem jekyll ...` and uncomment the line contaning `Gem github-pages`. Close that file and open `_config.yml` and edit accordingly. Once you're finished install and serve the site locally with `bundle install` and `bundle exec jekyll serve`. If you visit http://localhost:4000/ you should see your site. Now to edit your first post, open the file in _posts, and write. Jekyll uses [markdown](https://www.markdownguide.org/basic-syntax/) for creating posts. To publish the site to Github Pages, type `git add .`, `git commit -m 'Message',` and `git push`.  
Now that that's done go to github and open the repository we created and click the repository settings, and navigate to the pages option. Click publish and you're good to go. If you navigate to `https://your-username.github.io` you should see your site.
