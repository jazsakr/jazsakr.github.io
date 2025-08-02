---
title:  "How I set up my GitHub Pages site with Jekyll" 
excerpt: "This tutorial includes installing prerequisites, creating a GitHub repo and adding new Jekyll theme."
categories:
  - website
tags:
  - tutorial
toc: true
toc_sticky: true
number: 1
---

This is how I set up this website using GitHub pages and the Minimal Mistakes Jekyll theme. I like to look at and edit my files on my mac computer and commit the changes through GitHub Desktop. Familiarity with navigating the command line through the Terminal is very helpful. If you do not feel comfortable, check out the video version of this tutorial.

SIMPLE tutorial version: [(not ready, check back later)](){: .btn .btn--danger}

## **Before you start**

I would add a SSH key to your GitHub account first, then build the site. This is optional but that way you don't have to enter your password every time you make changes to your remote GitHub repository (“repo” for short). A "[remote repository](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories)" just means the place on GitHub (not your local computer) where your stuff is. Your stuff is saved in a folder (called a “repository”) and the location of this folder on GitHub is designated by an address.

There are two types of URL addresses:
- An HTTPS URL like `https://github.com/user/repo.git`
- An SSH URL, like `git@github.com:user/repo.git`

GitHub has some recommendations for [authentication](https://docs.github.com/en/get-started/git-basics/set-up-git#authenticating-with-github-from-git), but what do we need?
- <u>Do I need GitHub CLI or Git Credential Manager?</u>
You don’t need it if you just want to simply `git push/pull/clone` without typing a password every time. You need it if you want to use HTTPS instead of SSH or if you want to do more involved GitHub stuff from the terminal like viewing issues or managing repos/actions
- <u>Do I need to use SSH agent forwarding?</u>
You don’t need SSH agent forwarding just to push/pull directly from GitHub. You need it if you are using a remote-server as a middle-man, like this: your-device → (ssh into) → remote-server → (tries to push to) → GitHub

To run `git` commands without typing a password every time:
1. Make a key if needed
2. Add your SSH key to GitHub
`cat ~/.ssh/id_rsa.pub` then go to https://github.com/settings/keys → Click "New SSH key" → give it a name like `my-laptop` or `work-macbook` → Paste your public key into the box → Click "Add SSH key"
3. Test connection (on the command line) by running
`ssh -T git@github.com` and you will see something like this: `Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.`

## **Create a GitHub Pages site with Jekyll**

To do this, we will follow this [tutorial from GitHub Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-a-repository-for-your-site).

### **Install prerequisites**

GitHub lists some [prerequisites](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#prerequisites) we need before we can use Jekyll. 

We will need [Ruby](https://www.ruby-lang.org/en/), a programming language, before installing [Jekyll](https://jekyllrb.com). We will do this by following this [tutorial from the Jekyll website](https://jekyllrb.com/docs/installation/macos/)

Since I am on a Mac, I installed it using [Homebrew](https://brew.sh), the package manager for macOS. 

To install `ruby` with `homebrew`, run:
```bash
brew install chruby ruby-install
ruby-install ruby 3.4.1
```

*A lot* of messages will be printed to the terminal for about a minute and will end with a message that looks something like:

```
>>> Successfully installed ruby 3.4.1 into /Users/jazsakr/.rubies/ruby-3.4.1
```

Next we need to configure our shell to use `chruby`. The following will add lines to the end of your user config file:
```bash
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc 
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc 
echo "chruby ruby-3.4.1" >> ~/.zshrc

source ~/.zshrc
```

Check the ruby version by running `ruby -v`

Install Jekyll by running:
```bash
gem install jekyll
```

### **Create a repository**

Since we are using Github pages to create the site, we need to have a GitHub repository. Create a new repository on the GitHub website by clicking "New repository" after logging in and call it whatever you want (for example `jazsakr_website.github.io`) under “Repository name”.

Leave everything else at the defaults and click “Create repository”.

### **Create your site**

Next we are going to make the site, but first we have to have a local copy of the repository we created for the site. First, in the terminal, go to the folder where you want to keep the local copy. I have a folder called `GitHub` in my home directory were I keep all my local copies of my GitHub repos.

```bash
mkdir GitHub
cd GitHub
git init jazsakr_website.github.io
```

You will get a message that looks something like this: 
```
Initialized empty Git repository in /Users/jazsakr/GitHub/jazsakr_website.github.io/.git
```

Next you are going to go into the folder you have just initialized and create a new Jekyll site by running:
```bash
cd jazsakr_website.github.io
jekyll new --skip-bundle .
```

You will get a message that looks something like this: 
```
New jekyll site installed in /Users/jazsakr/GitHub/jazsakr_website.github.io
Bundle install skipped
```

If you list the contents of this folder now, you should see: `404.html`, `Gemfile`, `_config.yml`, `_posts`, `about.markdown`, and `index.markdown`

Next we have to edits some files and we can do this quickly using [Nano](https://www.nano-editor.org), a text editor for Unix-like operating systems using a command line interface. We will edit two files by running `nano` followed by the file name. But before we edit any files, we have to know the latest supported version of the `github-pages`gem so we can add the version number into the file we will edit. You can find this version here: [GitHub Pages - Dependency versions](https://pages.github.com/versions/).

1. Edit the `Gemfile` file by:
	- Comment out the line the starts with `gem "jekyll",` by adding the `#` at the very beginning of the line. 
	- Edit the line `gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins` by replacing `GITHUB-PAGES-VERSION` with the version number we saw in the [Dependency versions](https://pages.github.com/versions/) page.
	- Save the `Gemfile`

Then run:
```bash
bundle install
```

A lot of messages will be printed to the terminal and will end with some “Post-install” messages.

2. Edit the `.gitignore` file by:
	- Add a line for `Gemfile.lock`  
	- Add another line for`.DS_Store`
	- Save the `.gitignore`

### **Commit, build, and deployment**

Since these changes were made locally, we need to update the remote copy of the repo on the GitHub website and begin version control using git, a version control system. We will do this by adding and committing what edits we just did before pushing them to the GitHub website. An **add** marks the things where the changes will be tracked (in this case, all the files that were generated after `jekyll new --skip-bundle .`). A **commit** captures these **changes** and therefore tracks the **differences** between the current version of the repo and the previous one (in this case, we are establishing the first version of our files). A **push** sends these commits to the GitHub website.

In the repo for your GitHub pages site, run:
```bash
git commit -m "Initial Github pages site with Jekyll"
git add .
git commit -m "Add files"
```

You should see the list of files that you created, something like this:
```
[main (root-commit)] Add files
 7 files changed, 173 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 404.html
 create mode 100644 Gemfile
 create mode 100644 _config.yml
 create mode 100644 _posts/2024-08-11-welcome-to-jekyll.markdown
 create mode 100644 about.markdown
 create mode 100644 index.markdown
```

Next we have to push these commits, but first lets check if we have remote access.

You can do this by running:
```bash
ssh -T git@github.com
```

If this is the first time you test your SSH connection to GitHub, you will most likely get a message that says something like `The authenticity of host 'github.com' can't be established.` and will ask `Are you sure you want to continue connecting (yes/no/[fingerprint])?`. Type `yes`, press enter and then it should say something like:
```
Warning: Permanently added 'github.com' to the list of known hosts.
Hi jazsakr! You've successfully authenticated, but GitHub does not provide shell access. 
```

We also need to name the branch we are working on. A branch is a **copy of your code** at a certain point in time (the version of your code that exists at the moment you created the branch). The default branch of all repos is called `main`. Making branches is useful if you want to try things without breaking your code.

Name your branch then connect your local repo to the remote repo GitHub website by running:
```bash
git branch -M main
git remote add origin git@github.com:jazsakr/jazsakr_website.github.io.git
```

Check to make sure the connection has been established between the local and remote repo by running `git remote -v` and you should see something like this:
```bash
origin	git@github.com:jazsakr/jazsakr_website.github.io.git (fetch)
origin	git@github.com:jazsakr/jazsakr_website.github.io.git (push)
```

Now we are ready to push the changes to the remote repo by running:
```bash
git push -u origin main
```

Now the local repo on your local computer should be identical with the remote repo on the GitHub website.

The last few steps will be done in the web browser on the GitHub website. 
1. Go the the GitHub pages website repo and click the “Settings” tab near the top. 
2. In the panel on the left-hand side, go to the “Pages” section.
3. In the drop down menu for “Branch,” change from “None” to “main” and click “Save”
4. Refresh the page, then you will see a “Visit site” button near the top.

Now your GitHub pages website is live!

## **Add Minimal Mistakes Jekyll theme**

The Jekyll theme that I am using is called [Minimal Mistakes ](https://mmistakes.github.io/minimal-mistakes/) and we will follow this [Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/). According to [Adding a theme to your GitHub Pages site using Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll), we need to follow the “[Remote theme method](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remote-theme-method)” and “[Starting from `jekyll new`](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#starting-from-jekyll-new)” sections.

What’s the difference between a regular theme and a remote theme?
<u>Theme: (Gem-based theme)</u>
- Uses a Ruby gem (installed via Gemfile) to bring in the theme.
- Install the gem locally (bundle install), and GitHub Pages only supports a few pre-approved themes
- Add it to `_config.yml` like this: `theme: minimal-mistakes-jekyll`
- Works for local builds and fully offline workflows.

<u>Remote_theme: (GitHub-based theme)</u>
- Loads the theme directly from a GitHub repo, no gem install needed.
- Use with custom themes or those not officially supported by GitHub Pages.
- GitHub fetches it automatically when building your site.
- Add it to `_config.yml` like this: `remote_theme: mmistakes/minimal-mistakes`
- Works for hosted builds (like GitHub Actions or GitHub Pages).

The developers of the theme made a super simple starter GitHub repo called “[Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter/blob/master/README.md)” to use as an example or more directly as a template. 

Overall, to add this theme, we will need to edit a few files in the repo. I like to do this through the [GitHub Desktop](https://github.com/apps/desktop) rather than continuing through the terminal. 

### **Add repo to GitHub Desktop**

First download and install GitHub Desktop. Next we need to add the GitHub pages site repo. 

Since we have a local copy of the repo:
1. Click on “Add an Existing Repository from your Local Drive” on the list of options on the left-hand side. Then 
2. Click “Choose” to find the location of the repo. If you saved it like I did, it would be in “GitHub” folder you made in your home home directory. 
3. Click “Add Repository”

After adding the repo, it should say “No local changes“. This will change when we start editing files.  Now we can edit the files using any text editor and GitHub Desktop will track the changes. 

### **Edit files**

We can use any text editor. We can use the preinstalled TextEditor on macOS. If a file does not open with any text editor by default, you could select one by following the prompts or right click on the file and choose the software using “Open with”.

1. Edit the `Gemfile` by:
	- Delete the contents in your own `Gemfile` 
	- Replace with the contents of the [`Gemfile` in Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter/blob/master/Gemfile).

2. Edit the `_config` file by:
	- Delete the contents in your own `_config` 
	- Replace with the contents of the [`_config` in Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter/blob/master/_config.yml). 
	- Fill in the information you want to share about yourself (otherwise delete that line in the file). 
	- I would also add the line`markdown_ext: "markdown,mkdown,mkdn,mkd,md"` like in this [`_config` for the Minimal Mistakes GitHub repo](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml). This defines which file extensions should be recognized as Markdown files, which are the type of files you will create when you make things like blog posts.

3. Create a new file called `index.html` 
	- You can directly download the [`index.html` in Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter/blob/master/index.html) and add it to your repo. 

4. Deleted the `about.markdown` and `index.markdown` files
5. Lastly, we need to change the layout for the automatically generated post  `0000-00-00-welcome-to-jekyll.markdown`. Go into the `_post` folder and edit `layout` from `post` to `single` at the very top. 
It will look something like this:
```
---
layout: single
title:  "Welcome to Jekyll!"
date:   2025-07-05 20:11:46 -0700
categories: jekyll update
---
```

After we finish all the editing we need to do, we have to commit and push the changes as we did earlier when we created the site. This time we will be doing it through GitHub Desktop. Now if you go back to the Desktop app, you should see the exact edits per file and the edit status of all files listed.  

1. Fill in the “Summary” section on the left-hand side with a simple description of the changes. In this case, it can be called “add Minimal Mistakes theme“.
2. Click the commit button at the bottom of the panel on the left-hand side (will say something like “Commit 6 files to main“)
3. Click “Push to origin” toward the right-hand side. When it is done, it will go back to displaying “No local changes”

Now check out your website, it should have a new look!