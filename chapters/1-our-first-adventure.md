# Our First Adventure
\label{cha:1_our_first_adventure}

Welcome to _[Squire: Learn Web Development with Node and Angular](http://http://squire-book.knightoftheoldcode.com/book)_. This, the first book in a three book series, will show how to build a starting AngularJS / NodeJS application from scratch. Throughout the process we will be forging "Squire", the software we're writing to power the Knight of the Old Code website (among others). Along the way, you'll follow along as you gain confidence in web development. You'll learn how to meld Squire to your desires, ending with a website showcasing your personal brand and serving as a professional development resume. You’ll also get some insight as to how  experienced developers iterate code to refine its functionality and avoid common pitfalls.

Subsequent books in the series expand on the concepts and techniques taught in this first book, refining your website and adding features.

However, the knowledge contained within these tomes isn't only useful for creating a personal website. It is also more broadly useful to develop a range of web applications. We can promise you'll be instantly able to swear fealty to the nearest king and offer up your amazing bug hunting talent. We can't promise that he'll toss a dozen bounties and a fat purse of coins your way (though we'd be pretty surprised if that didn't happen).

## Introduction

...

### Prerequisites

...

### Conventions

...

## Gather Your Gear

\begin{quote}
An aspiring Knight is only as good as his gear. If you run into a dragon on that road over there, well you're going to get fried, regardless, really...they are *very* vicious. _However_, if you run into weaker creatures you want to ensure you have the proper equipment to defend yourself and attack the creatures.

--- Merlin Ambrosius
\end{quote}

In an increasingly mobile world, I've slowly been moving toward Cloud platforms. All of my source code (including the source code comprising this very book) is stored in the cloud (on Github). All of my files are stored in a cloud document repository (iCloud, since I'm of the Order of Apple). All of the projects I collaborate on are stored in one cloud repository or another (Dropbox, Google Drive, etc).

The exact hardware and software you use matters less now than ever. Find hardware, software, and services that *you* like and your happiness will reward you in spades.

The development technology we will be using in this book to build your website (and ours) is fairly platform agnostic. It doesn't really matter if you're of the Order of Apple, Microsoft, or Google. All you'll need is a desktop or laptop computer (phones, tablets, and other mobile computing devices _are_ able to be used, but will suffer from some slight handicaps in the cloud environments we'll be using).

Regardless of the sentiments above, there *are* fairly significant differences in the major hardware and software platforms. In order to minimize those (and to help facilitate being able to work on projects across devices and platforms) we recommend starting out with a cloud development environment.

There is certainly value in eventually purchasing and maintaining what you consider to be your ultimate development environment. Future books will cover this subject in more detail, examining how the various Orders of hardware and software accomplish the magic of web development on highly-refined toolsets.

My current favorite platforms are [Nitrous.io](https://www.nitrous.io) and [Cloud9](https://c9.io). As a Page working your way to Knighthood, the differences between the two are fairly minor.

Regardless of which cloud provider you choose, they all should have really good support for Node.js (the basic foundation of JavaScript flavored web development). At the moment, I'll leave getting started with your cloud provider as an exercise to you. You should be able to find decent tutorials for getting Node setup with [either](https://www.nitrous.io/stacks/nodejs/) [service](https://docs.c9.io/v1.0/docs/create-a-workspace).

[This will actually be fleshed out before the final version of the book with enough to get up and running. We'll include some basic setup information for each cloud service, a few screenshots, and links to further information.]

*(I would love feedback as to any challenges you may have run into so that I can help clarify any "sticking points" without fully re-documenting stuff that those providers can more easily document).*

## Hello, Nurse!

Now that Node is installed, we can create a basic Node application.

```console
$ mkdir squire
$ cd squire
$ npm init
```

```console
name: (squire)
version: (1.0.0)
description: Squire attends your website content so you
can focus on important subjects like ale and swordplay.
entry point: (index.js) server.js
test command:
git repository:
keywords:
author: Tricorius
license: (ISC) MIT
```

```console
$ touch server.js
```

### Terminal Care

```
console.log(‘Hello, Nurse’);
```

In terminal:

```console
$ node server.js
$ Hello, Nurse!
```

package.json

\begin{codelisting}
\codecaption{npm start}
\label{code:npm-start}
```javascript
  "scripts": {
    "start": "node server.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
\end{codelisting}

```
```

```console
$ npm start

> squire@1.0.0 start /Users/curtis/code/knightoftheoldcode/squire
> node server.js

Hello, Nurse!
```

[determine when is the best time to introduce nodemon]

### Browser Care

```console
$ npm install —save express
```

\begin{codelisting}
\codecaption{server.js}
\label{code:server.js}
```javascript
var express = require('express');

var app = express();

app.set('port', (process.env.PORT || 5000));

app.get('*', function(req, res, next) {
  console.log('Hello, Nurse!');
  res.send('Hello, Nurse!');
});

app.listen(app.get('port'), function() {
  console.log('Node app is running on port: ', app.get('port'));
});
```
\end{codelisting}

In Browser:

- http://localhost:5000/
- http://localhost:5000/hello
- http://localhost:5000/nurse

[This functionality will become important later for SEO. In order for HTML5 pushState to properly function, you need to be able to send your Angular application back to the browser to respond to any route from the server.]


### World Wide Wabbits

```console
$ mkdir app
$ touch app/index.html
```


\begin{codelisting}
\codecaption{app/index.html}
\label{code:app/index.html}
```html
<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8">

  <title>Squire</title>

</head>

<body>
  Hello, Nurse!
</body>
</html>
```
\end{codelisting}

\begin{codelisting}
\codecaption{server.js}
\label{code:server.js}
```javascript
app.get('*', function(req, res, next) {
  console.log('sending index file');
  res.sendFile('index.html', { root: __dirname + '/app' });
});
```
\end{codelisting}

### Git

At Knight of the Old Code we use git; the version control system that Mr. Linus Torvolds created for his little open source project "linux" (you might have heard of it).

Git tracks the content of your project files and intelligently merges changes together. This is really nice for a solo developer, it's essential for a team of developers.

Operating Systems, platforms, languages, and frameworks often utilize a series of metadata files, caches, and other non-essential (rebuildable) directories. These (and secure information such as API access and encryption keys) should not be stored in a code reepository. We will investigate all of these situations as they arise, but the immidiate issue we have is that Node and Angular include various files that don't need to be stored in your source code repository.

Thankfully, these structures are well-documented. We've found that the best clearinghouse for this information is the predefined .gitignore files which Github releases on their platform.

[Sidebar: https://github.com/github/gitignore. The github/gitignore project is Github's collection of .gitignore file templates. The project README explains the project, how to contribute, and links to a few resources to further explore the .gitignore concept.]

At this point, we are interested in the Angular and Node .gitignore templates. Since are using Angular and Node in our project, these templates make a great starting point.

[Sidebar: Github doesn't have an official Angular .gitignore template? Whaaaaaa? Well, Angular, being a framework, doesn't have as many ignorable files as Node, which is a language platform. That's ok...we can just take the .gitignore from the official Angular project (https://github.com/angular/angular.js/blob/master/.gitignore) and use that as a starting point. This gives more than we really need, and also has some duplication from the Node .gitignore, but it's good enough for now. We'll clean it up later. Remember, developing is largely about shipping working software. It doesn't do much good to have perfect, pristine code that the Academics would spend months marveling over if the code isn't running somewhere.]

[Explain Github's "raw" button to show how to copy / paste code out.]

At the root of your project, create a .gitignore file. Note that the ```.``` at the beginning of the file is important [describe why].

```console
$ touch .gitignore
```

\begin{codelisting}
\codecaption{.gitignore}
\label{code:.gitignore}
```
# Node #

# Logs
logs
*.log
npm-debug.log*

# Runtime data
pids
*.pid
*.seed

# Directory for instrumented libs generated by jscoverage/JSCover
lib-cov

# Coverage directory used by tools like istanbul
coverage

# Grunt intermediate storage (http://gruntjs.com/creating-plugins#storing-task-files)
.grunt

# node-waf configuration
.lock-wscript

# Compiled binary addons (http://nodejs.org/api/addons.html)
build/Release

# Dependency directory
# https://docs.npmjs.com/misc/faq#should-i-check-my-node-modules-folder-into-git
node_modules

# Angular #

/build/
/benchpress-build/
.DS_Store
gen_docs.disable
test.disable
regression/temp*.html
performance/temp*.html
.idea/workspace.xml
*~
*.swp
angular.js.tmproj
/node_modules/
bower_components/
angular.xcodeproj
.idea
*.iml
.agignore
.lvimrc
libpeerconnection.log
npm-debug.log
/tmp/
/scripts/bower/bower-*
```
\end{codelisting}

With this file in place, subsequent steps to initialize git and add source files to our repository will properly ignore files we don't want to store in the cloud. We are going to be pushing this to a public repoistory, so you want to be very careful what you push. If you push files that are suppose to be secure, you can compromise your accounts and allow "hackers" easy access to jack you up.

#### Git initialize

In order to initialize a git repository, all we need is git (which should be preinstalled on most modern operating systems and cloud development environments) and a simple command in the root of our project directory.

```console
$ git init
Initialized empty Git repository in /Users/curtis/code/knightoftheoldcode/squire/.git/
```

#### Git config

[Add discussion of git config, local vs global, and what email address you should use.]

#### Git add

In order to track files properly, we have to indicate to git that we'd like it to be aware of them. We can determine which files git sees and what status it considers them to be in with the command git status.

```console
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
	README.md
	app/
	package.json
	server.js

nothing added to commit but untracked files present (use "git add" to track)
```

The above results indicate that git has found some files and a directory to be untracked. We want to add these to git's tracking sine they are all valid source code files. In order to add all files, I prefer the command git add --all.

```console
$ git add --all
```

After we add these files to git, it will properly report them with a git status command:

```console
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .gitignore
	new file:   README.md
	new file:   app/index.html
	new file:   package.json
	new file:   server.js
```

#### Git commit

We can now "commit" these files to git's caring hands by executing the "git commit" command:

```console
$ git commit -m "initial commit"
[master (root-commit) 467992b] initial commit
 5 files changed, 101 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 app/index.html
 create mode 100644 package.json
 create mode 100644 server.js
```

The -m flag allows us to directly pass a commit comment into the commit command. If we excluded it, then git would pull up our system editor to prompt us for a more detialed commit message. We will discuss more about proper commit messages later.

After the commit, git status should show a clean working directory.

```console
$ git status
On branch master
nothing to commit, working directory clean
```

#### Github

Github is a very friendly place where you can store your open source code for free. You can also pay a small monthly fee to store private repositories safe from the prying of eyes.

We will store your personalized version of Squire in a public repository for now. If there comes a time when you want to add top-secret features to your website, feel free to convert your repository to a private one.

Create an account on Github. Then click the "+ New Repository" button. Fill in the name of the project "squire" and a descrption. At this point you don't need to initialize the repository with a README, .gitignore, or license (although you're encouraged to eventually determine an applicable license. Squire is licensed as MIT which essentially means you can do whatever you want with the code...) We will explore these files in more detail throughout the course of this tutorial. Then click "Create repository".

[Sidebar: For further information, you can check out the following Github tutorial (https://help.github.com/articles/set-up-git/). Also link to the Github series on Knight of the Old Code.]

#### Git remote

We now have a project created in the cloud, on Github, to house your source code. (We will be able to do many future magical things with this cloud code.) We need to link the code in your project to this storage location. The mechanism in git to do so is called a "remote".

You can examine your projecct's defined "remotes" by executing the command (the -v flag stands for "verbose" mode):

```console
$ git remote -v
```

At the moment, this shouldn't return any results. This is perfectly fine as we haven't yet added any.

The success page in Github should suggest to you our next course of action..."or push an existing repository from the command line". We want to execute the code in this block in our project's root directory.

```console
$ git remote add origin git@github.com:[account]/[repository-name].git
```

[Sidebar: In order to make this happen without security error messages, you'll need to generate (if it doesn't exist) and add your secure token (called an SSH key) from your development computer or cloud development environment to your Gibhub account. This is actually easier to do than it sounds, and mose platofrms have some excellent documentation for how to do so. (Link to a few)]

Now git remote should show us some meat.

```console
$ git remote -v
origin	git@github.com:knightoftheoldcode/squire.git (fetch)
origin	git@github.com:knightoftheoldcode/squire.git (push)
```

That's better. If you examine the earlier git remote add command and the results of git remote -v you'll notice the word "origin" repeated. This is the common term for the primary location of your code, otherwise its "origin". This will, in most circumstances, be your primary source code repository server (be it Github, Bitbucket, Gitlab, or your own local network server).

#### Git push

At this point, we are ready to push our code to the cloud. The second of the two recommended commands from Github will (if your security tokens are correctly configured) push the code from your machine to the cloud.

```console
$ git push -u origin master
Counting objects: 8, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (8/8), 1.49 KiB | 0 bytes/s, done.
Total 8 (delta 1), reused 0 (delta 0)
To git@github.com:knightoftheoldcode/squire.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

Refreshing your Github project should now show the commit succeeded, it should show your README below the code results.

Over time, we'll be adding additional features to your repository and additional information to your README. Utilizing a series of services and information available on the web, we can provide a lot of insight into your code.

### Heroku

A typical working session with git involves branching your repository code (to protect you from yourself or random evil magic in your general vicinity), modifying the code to your heart's content, then committing, merging, and pushing your code when your tests are greeen and you're satisfied with the results.

Allow us to practice this git workflow with a sparring session against Heroku. (Trust us, although the Knights Heroku are mighty warriors, they are very honorable and will be very gentile with those starting their journey.)

[Sidebar: We'll be essentially following Heroku's Getting Started with Node guide. (https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction)]

You'll first need to create a heroku account to be able to push. You'll also have to add your SSH keys (created earlier for Github) to Heroku to be able to push changes.

You'll want to download and install the heroku toolbelt (preinstalled in many operating systems and cloud development platforms).

[Sidebar: Recommendations for various Operating Systems.]

#### Heroku Login

The first step is to authenticate your account with Heroku toolbelt. (I recommend setting up two-factor authentication at your earliest convenience all *all* development accounts. If anyone gets ahold of these accounts your day is going to become VERY bad VERY quickly.)

```console
$ heroku login
Enter your Heroku credentials.
Email: zeke@example.com
Password:
```

#### Add a few files

Although our code should technically deploy at this point, we should add a file to provide Heroku the information it needs to properly drive your application.

#### Git workflow

I prefer to use a very simple branching workflow with git. (If you're part of a large team, you may have a more complex workflow, but I prefer to keep things as simple as they can be and as complex as they need to be.)

```console
$ git checkout -b add-heroku-files
```

Git checkout is primarily responsible for checking out code from your repository. It can also be used to switch between branches (separate sets of code useful for isolating and testing new features before general release into the codebase) and create new branches.

The above command should create and switch to the new branch "add-heroku-files".

```console
$ touch Procfile
```

The capitalization is important in the file name, because: programming.

\begin{codelisting}
\codecaption{Procfile}
\label{code:Procfile}
```
web: node server.js
```
\end{codelisting}

This declares a single process type, web, and the command needed to run it. The name web is important here. It declares that this process type will be attached to the HTTP routing stack of Heroku, and receive web traffic when deployed.

Procfiles can contain additional process types. For example, you might declare one for a background worker process that processes items off of a queue.

```console
$ git status
On branch add-heroku-files
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	Procfile

nothing added to commit but untracked files present (use "git add" to track)
```

```console
$ git add --all
$ git status
On branch add-heroku-files
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   Procfile
```

```console
git commit -m "add Procfile for heroku deploy"
[add-heroku-files e4d3f1f] add Procfile for heroku deploy
 1 file changed, 1 insertion(+)
 create mode 100644 Procfile
```

We are satisfied with our changes...so we'll now merge them back into the master branch. (We will eventually explore a much fancier version of merging called Pull Requests. This allows others to get involved in a merge and is often used in production with professional software development.)

Before you merge you always want to make sure your working directory is clean (meaning you're now tracking and committed all files in the current branch).

```console
$ git status  
On branch add-heroku-files
nothing to commit, working directory clean
```

In order to merge, we want to travel back to the branch which we want to update. In this case, we just got done working with the add-heroku-files branch. We now want to merge that back into master for pushing up to Github (origin) and heroku (heroku).

```console
$ git checkout master
```

If you ever need to align your bearings with branches, you can use the git branch command.

```console
$ git branch
  add-heroku-files
* master
```

It will indicate with the asterisk which branch you're currently working on. We are on master, so we want to merge add-heroku-files.

```console
$ git merge add-heroku-files
Updating 467992b..e4d3f1f
Fast-forward
 Procfile | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 Procfile
```

The above output indicates a single insertion (+) in the Procfile.

```console
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean
```

Git status shows that this merge is committed and we are ahead of origin/master by 1 commit. This essentially means that we have one commit on our local system that isn't pushed to origin yet (which makes sense...we haven't pushed yet).

```console
$ git push origin master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 305 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To git@github.com:knightoftheoldcode/squire.git
   467992b..e4d3f1f  master -> master
```

#### Heroku local

Now that we have defined a Procfile we can try launching the application in "local" mode with the heroku toolbelt. This will give us the closest emulation as possible to the same environment it will be running with on live. Although you'll likely be developing in a diffetent mode (with nodemon which automatically monitors for code changes and refreshes your application) it's good to test heroku local as part of your standard pre-deploy checklist.

```console
$ heroku local
forego | starting web.1 on port 5000
web.1  | Node app is running on port:  5000
web.1  | sending index file
```

#### Heroku create

We're now ready to create the heroku application. By default new apps on Heroku are in the "free" tier, which gives you a free application with some really great features at the cost of needing to sleep for at least six hours a day. (This is generally not a huge deal, even with some production apps. Though I recommend figuring out a way to potentially monotize your app / website before you drive enough random traffic to violate the sleeping rules.)

```console
$  heroku create
Creating sharp-rain-871... done, stack is cedar-14
http://sharp-rain-871.herokuapp.com/ | https://git.heroku.com/sharp-rain-871.git
Git remote heroku added
```

#### Heroku push

Heroku create has created an application and added a git remote called "heroku". You can deploy code updates by pushing code to this remote using a standard git push heroku master command.

```console
$ git push heroku master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 305 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Node.js app detected
remote:
remote: -----> Creating runtime environment
remote:        
remote:        NPM_CONFIG_LOGLEVEL=error
remote:        NPM_CONFIG_PRODUCTION=true
remote:        NODE_ENV=production
remote:        NODE_MODULES_CACHE=true
remote:
remote: -----> Installing binaries
remote:        engines.node (package.json):  unspecified
remote:        engines.npm (package.json):   unspecified (use default)
remote:        
remote:        Resolving node version (latest stable) via semver.io...
remote:        Downloading and installing node 4.2.1...
remote:        Using default npm version: 2.14.7
remote:
remote: -----> Restoring cache
remote:        Loading 2 from cacheDirectories (default):
remote:        - node_modules
remote:        - bower_components (not cached - skipping)
remote:
remote: -----> Building dependencies
remote:        Pruning any extraneous modules
remote:        Installing node modules (package.json)
remote:
remote: -----> Caching build
remote:        Clearing previous node cache
remote:        Saving 2 cacheDirectories (default):
remote:        - node_modules
remote:        - bower_components (nothing to cache)
remote:
remote: -----> Build succeeded!
remote:        └── express@4.13.3
remote:        
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote:
remote: -----> Compressing... done, 11.5MB
remote: -----> Launching... done, v4
remote:        https://squire-book-page.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/squire-book-page.git
   467992b..e4d3f1f  master -> master
```

```console
$ heroku ps
=== web (Free): `npm start`
web.1: idle 2015/10/17 13:33:33 (~ 8m ago)
```

If the above command doesn't indicate that a web dyno is running, then scale your web dynos to 1 (anymore will kick into production mode and cost you money...be *very* cautious of this setting).

```console
$ heroku ps:scale web=1
Scaling dynos... done, now running web at 1:Free.
```

It is wise to take an additional step and check your Heroku logs.

```console
$ heroku logs --tail
2015-10-17T18:56:31.955290+00:00 heroku[api]: Enable Logplex by tricorius@knightoftheoldcode.com
2015-10-17T18:56:31.955290+00:00 heroku[api]: Release v2 created by tricorius@knightoftheoldcode.com
2015-10-17T18:58:37.130134+00:00 heroku[api]: Scale to web=1 by tricorius@knightoftheoldcode.com
2015-10-17T18:58:37.198837+00:00 heroku[api]: Release v3 created by tricorius@knightoftheoldcode.com
2015-10-17T18:58:37.198837+00:00 heroku[api]: Deploy 467992b by tricorius@knightoftheoldcode.com
2015-10-17T18:58:37.269464+00:00 heroku[slug-compiler]: Slug compilation started
2015-10-17T18:58:37.269475+00:00 heroku[slug-compiler]: Slug compilation finished
2015-10-17T18:58:39.880682+00:00 heroku[web.1]: Starting process with command `npm start`
2015-10-17T18:58:41.726231+00:00 app[web.1]:
2015-10-17T18:58:41.948299+00:00 app[web.1]: Node app is running on port:  23074
2015-10-17T18:58:41.726229+00:00 app[web.1]: > squire@1.0.0 start /app
2015-10-17T18:58:41.726230+00:00 app[web.1]: > node server.js
2015-10-17T18:58:41.726212+00:00 app[web.1]:
2015-10-17T18:58:42.155003+00:00 heroku[web.1]: State changed from starting to up
2015-10-17T18:58:49.806927+00:00 heroku[router]: at=info method=GET path="/" host=squire-book-page.herokuapp.com request_id=5623024b-73fc-48b5-b077-db6f6d1d345b fwd="75.169.221.46" dyno=web.1 connect=1ms service=29ms status=200 bytes=427
2015-10-17T18:58:49.785985+00:00 app[web.1]: sending index file
2015-10-17T18:58:50.628297+00:00 heroku[router]: at=info method=GET path="/favicon.ico" host=squire-book-page.herokuapp.com request_id=fdcceef3-1be2-4300-b630-189719b69122 fwd="75.169.221.46" dyno=web.1 connect=0ms service=8ms status=200 bytes=427
2015-10-17T18:58:50.622940+00:00 app[web.1]: sending index file
2015-10-17T19:33:34.456965+00:00 heroku[web.1]: Idling
2015-10-17T19:33:34.458166+00:00 heroku[web.1]: State changed from up to down
2015-10-17T19:33:39.756962+00:00 heroku[web.1]: Stopping all processes with SIGTERM
2015-10-17T19:33:41.251741+00:00 app[web.1]: Error waiting for process to terminate: No child processes
2015-10-17T19:33:42.189240+00:00 heroku[web.1]: Process exited with status 22
2015-10-17T20:06:53.753528+00:00 heroku[slug-compiler]: Slug compilation started
2015-10-17T20:06:53.753537+00:00 heroku[slug-compiler]: Slug compilation finished
2015-10-17T20:06:53.683331+00:00 heroku[api]: Deploy e4d3f1f by tricorius@knightoftheoldcode.com
2015-10-17T20:06:53.683331+00:00 heroku[api]: Release v4 created by tricorius@knightoftheoldcode.com
```

Remember to ctrl-c out of heroku logs when you are done. Heroku spins up dynos when you run heroku comands. This counts against your hours (since it costs them money to spin up servers for you to interact with your application). This can end up costing you money if you forget to terminate hyour dynos.

#### Heroku open

You can now visit your application on the web to verify that it's running live.

```console
$ heroku open
```

The above command should trigger your browser and load a new tab pointing to your deployed, running code.

It may not be very fancy, but it will be very awesome. And congratulations, you won your sparring match with Knights Heroku.
