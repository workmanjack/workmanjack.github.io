# www.jackcworkman.com

Also available from [workmanjack.github.io](workmanjack.github.io)

## Jekyll

### Getting Started With GitHub Pages & Jekyll:

1. Purchase domain from [Google Domains](https://domains.google)
2. Setup a [Github Pages](https://pages.github.com/) repo ([tutorial](http://www.curtismlarson.com/blog/2015/04/12/github-pages-google-domains/))
3. Install [Jekyll on Windows](https://jekyllrb.com/docs/installation/windows/)
4. Change your mind and use Hugo instead because apparently [it is way faster](https://forestry.io/blog/hugo-and-jekyll-compared/)

### Additional resources that might be helpful for navigating the Pages & Jekyll ecosystem:

* https://medium.com/@tordable/github-pages-as-blogging-platform-320524b1fffa
* https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/

### Here are some Jekyll themes that I think look neat:

* https://github.com/Sylhare/Type-on-Strap
* https://jekyller.github.io/jasper2/

## Hugo

### Getting Started

1. To [install Hugo](https://gohugo.io/getting-started/installing), I used [Chocolatey](https://chocolatey.org/). Note that I had never used Chocolatey before, but it was a breeze.
2. Follow [Hugo's quickstart guide](https://gohugo.io/getting-started/quick-start/). I had a local site up and running in minutes!
3. Follow [Hugo's GitHub Pages guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/).

Two notes on the Pages guide that confused me at first:

* Their provided git submodule command uses ssh instead of https. My local git is not properly configured to work with ssh, so I needed to switch the command to https. So, instead of `git submodule add -b master git@github.com:<USERNAME>/<USERNAME>.github.io.git public`, I ran `git submodule add -b master https://github.com/<USERNAME>/<USERNAME>.github.io.git public`.
* By default, hugo does not render the static site files to your disk when running `hugo serve`. To enable this, run `hugo serve --renderToDisk`.

### Publishing Hugo to a Subdirectory of Your GitHub Pages Site

In [Hugo's GitHub Pages guide]((https://gohugo.io/hosting-and-deployment/hosting-on-github/), they assume that your hugo site is also the root of your personal site. For me, that was not the case. I had a custom landing page and wanted my blog (which I used hugo for) to live behind it.

To push hugo to a subdir, you need to do the following:

1. Create a subdir in your personal website GitHub Pages repo. I called mine `blog`.
2. When building your hugo site, don't just call hugo. Call `hugo --destination public\blog`. This puts all rendered files into your subdirectory.
3. And the final step is to modify your config's base url. Open up your site's config.toml, and change `baseURL` to `"http://www.jackcworkman.com/blog"` (but replace with your actual site).

Here is the script they provide in their guide adapted to push to a subdirectory (note that this example assumes you want to render files to public\blog):

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo --destination public/blog # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```

Note: if your personal website (now submodule) has changes not yet pulled, you will need to pull them manually. The above bash script might fail silently otherwise (it did for me executing in Windows). To pull them manually, `cd public && git pull`.

### Some Hugo themes that have caught my eye

* https://themes.gohugo.io/theme/gohugo-theme-ananke/
* https://themes.gohugo.io/airspace-hugo/
* https://themes.gohugo.io/theme/startbootstrap-clean-blog/
* https://themes.gohugo.io/manis-hugo-theme/
* https://themes.gohugo.io/theme/hugo_theme_pickles/
* https://themes.gohugo.io/theme/steam/
* https://themes.gohugo.io/theme/cactus/

## Website Goals

I realized I'm looking for a landing page that I can break out into my big three

    1. Data Science
    2. Music
    3. Reading
    4. Running
