## Why

* This is a template repo for classes I teach at the [University of San Francisco](https://www.cs.usfca.edu)
* My objectives were to 
	* Make a timeline view of the course materials
	* Integrate slide material (hat-tip to Berkeley's [CS 61a](https://cs61a.org/))
	* Create a simpler information design than I could get using Google Sites (no support for `<table>`)

## How It Works

* It uses the [Jekyll](https://jekyllrb.com/) static site generator, which can be hosted on [GitHub Pages](https://pages.github.com/) 
* I lightly modified the [Minima theme](https://github.com/jekyll/minima) to use school colors
* Each row in the timeline is a pseudo blog post, using only the [front matter](https://jekyllrb.com/docs/front-matter/)
* I used [sylshare's work](https://github.com/sylhare/Reveal-Jekyll) as a starting point for integrating Jekyll and [RevealJS](https://revealjs.com/) slides (see presentation format hints)
* To use this approach for your class site, simply create a new repo using this repo as a template

## Ruby Environment

1. Since Jekyll is written in Ruby, you'll need Ruby on your local machine
	1. Well, *someone* needs Ruby. Once you get this going, adding blog posts is easy to do without a local test/dev environment
1. I run on macOS, and use [rbenv](https://github.com/rbenv/rbenv) to avoid messing around with the system Ruby installation
	```sh
	% brew install rbenv
	% rbenv init
	% rbenv install 3.1.2
	```
1. Add to `~/.zshrc`
	```sh
	eval "$(rbenv init - zsh)"
	export PATH=~/.rbenv/shims:$PATH
	export RBENV_VERSION="3.1.2"
	```
	Remember to
	```sh
	% source ~/.zshrc
	```
1. Install the Jekyll stuff from the Gemfile
	```sh
	% cd your-site
	% bundle install
	```
1. Run the local web server to test
	```sh
	% cd your-site
	% jekyll serve --livereload
	```
1. Now you can browse to `localhost:4000` and see the web site. New and modified Markdown files are auto-recompiled and your browser auto-reloads

## GitHub Configuration

1. I create my class web site repo in my semester GitHub Classroom organization
1. GitHub Pages uses the naming convention `<org>/<org>.github.io`, e.g. `https://cs221-s22/cs221-s22.github.io`
1. Create a `master` branch in addition to the default `main` branch
1. In your repo Settings, use the Pages item in the sidebar to serve from the `master` branch at the root `/`
1. When you push changes to the `main` branch on your site, the script in `your-site/.github/workflows` will run and GitHub Pages will compile the Markdown and SCSS to HTML and CSS, committing those to the `master` branch. 
1. The compilation happens on a push, not dynamically as pages are loaded. It can take ~10 minutes to compile your changes and propagate the results to GitHub Pages.
1. Your site will be available at `https://your-site.github.io`
1. You can also set up a custom domain if you have control of your DNS, e.g. `cs221.cs.usfca.edu`
    1. You'll need to set the `CNAME` in DNS to the GitHub Pages URL
    1. You'll need to create a `CNAME` file in the root directory containing the custom URL, e.g. `cs221.cs.usfca.edu`

## Adding Content

1. We make a new small file in `_posts/` for every class meeting with the topics and materials. Jekyll combines those into the big timeline using the template in `_layouts/home.html`
	1. My TAs are Zoom co-hosts so they get notified when recordings are available, and can paste the sharable video link into a new post
1. `_config.yml` contains Jekyll collections for files in `_assignments/` and `_slides/`. Those will be compiled/templated using their respective layouts in `_layouts/` 
1. RevealJS provides [documentation](https://revealjs.com/markdown/) for authoring in Markdown
1. All of the compiled HTML and CSS assets go into `_site/`
