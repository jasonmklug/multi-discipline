---
layout: post
title: "The Making of Multi-Discipline"
published: true
category: webcraft
---

Despite having worked on and around the web since 2006, it's been a while since I've had my own personal space which I controlled soup to nuts.

Twitter has satisfied *most* of my *practical* publishing needs (low friction, low maintenance, publicly accessible, able to be individually hyperlinked), but the notion that I don't "own" my tweets is aggravating to my future-proofing sensibilities.

While I do have systems in place to capture, for example, my tweets (first via an iPhone app called [Momento](http://www.momentoapp.com/``); more recently by running a custom install of Brett Terpstra's [Slogger](http://brettterpstra.com/projects/slogger/) to add my tweets to a personal [Day One](http://dayoneapp.com/) journal), it's not the same as having posts under my complete control.

## The Problem

I'll never control the fate of my posts to Twitter, Tumblr, Facebook, or any other advertising-supported *"post here and we'll probably keep your stuff around for a few years"* platform.  But I *would* like most (if not all) of my day-to-day public writing to have the best possible chance of being around for my kids to discover when they're older.

## The Solution

I'm building out my own little corner of the web where I control the presentation, availability, and ultimate fate of my content, and which I can expand to include more forms of media (long-form posts, image galleries, video, audio, etc.) as I find uses for them.

## The Tools

+ Static Site Generator ([Jekyll](http://jekyllrb.com/))
+ VPS ([Digital Ocean](https://www.digitalocean.com/?refcode=896afa34ae98))
+ Web Server ([Nginx](http://nginx.org/))
+ Programming Language ([Ruby](https://www.ruby-lang.org/))
+ Templating Language ([Liquid](http://liquidmarkup.org/))
+ Source Control ([Git](http://git-scm.com/))

## The Process

### Tinkering With Jekyll Locally

Since I had never before used Jekyll, I limited myself to installing and running it locally on my development machine (a.k.a. "dev machine", a.k.a. "laptop") for a few days.  This gave me an opportunity to tinker with it (tweak a template, find the limits/hackability of the posting system, determine what else I could build into this) without investing a bunch of time spinning up a VPS.  Jekyll, I soon learned, could even be deployed to GitHub Pages with a few setup conformities, so that became my plan.

After tinkering with Jekyll, it was clear that while this was a solid piece of software out of the box, the *real* value it offered was its customizability and extensibility (given familiarity with Ruby and Liquid).  I work with Ruby professionally, so that was a good fit; and despite this being my first experiment with Liquid, it's a sufficiently intuitive and documented system that I picked it up quickly.

The Jekyll features I wanted to build, though, required that I change my deployment plan from [GitHub Pages](https://pages.github.com/) (which offers a free and quick way to run a stock Jekyll site) to deploying via Git to my own VPS.

### Setting Up My VPS

Configuring the DigitalOcean Droplet (their term for a VPS "unit") was straightforward; DigitalOcean's own system had me up and running with a virtual Linux (Ubuntu) "box" in no time, and I had the necessary user accounts, SSH Keys, etc. set up shortly thereafter (aided by [DigitalOcean's excellent documentation & tutorials](https://www.digitalocean.com/community/?refcode=896afa34ae98)).

**Context:** *Part of setting up this droplet involved directing web traffic from my domain name, multi-discipline.com, to my droplet's IP address.  In addition to being necessary for general web traffic, having that DNS `A Record` in place allowed me to use that hostname for other services (`ssh`, `git remote`, etc.) and have a single point of update should I move the site to a different server.*

Next up, I installed Ruby and Jekyll on the VPS, installed Git (`git-core`, in my case), and created the Git repository at which I'd be receiving my entire, un-compiled Jekyll site (pushed via Git from the repository on my laptop, where I'm building the site and writing posts).

**Context:** *Jekyll is a static site generator, meaning that the "work" of building each and every page in the site (setting the permalink address of each page; including header, footer and other page layout partials; replacing variables with the appropriate text, etc.) is done __once__ whenever I push a change to the Git repository, instead of every time someone on the web requests a page.*

The driving force of all that server-side processing is a Git `post-receive hook` on the site's repository (a.k.a. "repo") on my VPS.  You can think of this as a shell script which fires when Git receives a change to that repo.  In basic terms (neglecting a few technical steps), that script:

1. Tells Jekyll to turn my site's un-compiled content files, layout partials, and assets into a functioning and inter-linked set of web pages (in other words, makes the disparate parts into a proper web site).
2. Clones the generated `/site` folder to a particular directory on the VPS (where, in a future step, we'll tell the web server to look for the page files as they're requested).

### Setting Up Nginx As My Web Server

While I've done some basic system administration work in the past, I've never actually installed and configured my own web server (Nginx, in this case) on a clean system.

Nginx does the work of listening for requests which come in, and serving the appropriate files from my VPS back to the web browser which requested them.

As such, I needed to let Nginx know:

+ The port on which it should be listening for web requests (standard is `80`)
+ The IP address from which it is serving (the IP address of my DigitalOcean Droplet)
+ Which site(s) I'm serving, and which host name(s) I'm using for them (`multi-discipline.com www.multi-discipline.com`)
+ Where (on the VPS) it should look for each site's "root" directory (eg. `/var/www`)
+ Which file to use as the site's (or any subdirectory's) index (typically `index.html`)
+ Which pages to use for given errors (eg. `404 /404.html`)

I also needed to be sure the site configuration I did in `/sites-available/multi-discipline.com` was again expressed in that site's file in the `/sites-enabled` directory.  Since my setup is pretty straightforward (i.e. any site I have "available" should also be "enabled"), I symlinked the site file in `/sites-available` with its counterpart in `/sites-enabled`, meaning any future change to one of those files is carried through to the other.

At this point, I ran into some system-permissions-related problems.

Firstoff, I'd forgotten to make the `post-receive hook` file executable (i.e. "able to be run"), so nothing was happening when my Git repository detected changes.  I fixed this with a `chmod`.

Secondly, the `post-receive hook` script couldn't write in the destination folder (or, rather, a script *run by my user account* couldn't, and the `git remote droplet` set up on my laptop to push code to the VPS did so using my VPS user account's SSH Key), so I made my user account a member of the user group which has control over `/var/www` and its contents.  In my case (and, I believe, by default), this group was `www-data`.

**Context:** *For security and peace-of-mind reasons, I set up a user account on my VPS which I would use for day-to-day system administration, but which __was not__ the system's default `root` account, since `root` is basically god as far as the system is concerned, and can do many harmful things if accidentally or maliciously misused.*

The first time I successfully ran `git push remote droplet master` on my development laptop and found the properly compiled site being served at [http://multi-discipline.com](http://multi-discipline.com), I thrust my arms up in victory.  Success!