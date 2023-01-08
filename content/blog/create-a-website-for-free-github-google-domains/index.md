---
title: "Create a dev website for free"
date: 2023-01-08T13:00:00+01:00
lastmod: 2023-01-08T13:00:00+01:00
draft: false
author: "Nicola Massarenti"
authorLink: ""
description: "How I created this website, for free, using GitHub Pages and Hugo"
images: [""]

tags: ["blog"]
categories: ["blog"]

lightgallery: true

share:
  enable: false
code:
  copy: true
  maxShownLines: 50
math:
  enable: true
---

# How to create a website for Free using GitHub Pages and Google Domain

It's early 2023, I've resigned from my full-time well-paid job to start a new journey as a freelancer. The first thing to do is to open a website: something that allows me to share thoughts, projects, blog posts and to be a reference for my clients.

There are a tons of options. However, I must keep into account that:
* I have very little time available
* I have limited knowledge of front-end technologies
* I need a personal website deployed as soon as possible

In the following, I'll bring you in the journey of deploying a no cost, minimal effort and blog friendly website on a custom domain (in my case, it's [nicolamassarenti.com](https://nicolamassarenti.com/)).

## Technologies

If you're like me and if you're not a front-end/full-stack developer you'll be 
overwhelmed by the options. Just to name a few, you'll have to choose among:

* Spend time and learn a new technology
* Use a no-code platform
* Create a static site
* Create a dynamic site
  
![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/create-a-website-for-free-github-google-domains/which-path.png "")


At the beginning I was considering developing the website with [[Vue.js]], which is easy to use and has an active community. I already know it a bit: in the past I created a few dashboards (with vue.js and bootstrap), some login pages, some upload pages. However, it would have been too much of an effort. It would have required a few days of coding, my design (colors, font, etc) would have been poor and, most importantly, there was the risk of falling into the rabbit hole of learning. I couldn't take this effort: I needed a website as soon as possible.
On the other side, there was React, a popular framework that has a steep learning curve. It may have been a good choice, but again, no time. I had to move on.

The second option was to use some no-code platforms such as [Squarespace](www.squarespace.com) or [Wix](wix.com), which have the following drawbacks:
* they're not free
* I would be limited to the design they offer... Yes, I know, there are A LOT of templates.. But hey, I am a developer, and I want to have freedom ;) 
* I would be dependent forever on a specific vendor

So, I ended up choosing the third option: building a website using a framework for static websites. After some googling I stumbled upon [[hugo]], which provides many themes, supports Markdown and content organization through the use of taxonomies (e.g., categories, tags). One of the coolest theme I stumbled upon is [PaperMod](https://github.com/adityatelange/hugo-PaperMod), a minimal theme suited for a blog. However, the documentation wasn't great and it didn't seem straightforward to modify the homepage.

So I did a deeper search and came across [LoveIt](https://hugoloveit.com/), a theme quite similar to PaperMod, with a better documentation, with recent commits and with an easy way of customizing the home page.

Once I chose the website, it was time for the interesting part: **developing**.

## How to create a website

First of all, you have to install [[hugo]], the link to the installation is [here](https://gohugo.io/installation/).

Then, create your project.
```shell
hugo new site my-website
cd my-website
git init #initializing the folder as a repository
```

 Now install the theme. The straightforward way is to add the theme repository as a sub-module.
```shell
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

## Customization
The configurations are stored in the file `config.toml`. The content of my website is the following:

```toml
baseURL = "https://nicolamassarenti.com/"

# Change the default theme to be use when building the site with Hugo
theme = "LoveIt"

# website title
title = "Nicola Massarenti"

# language code ["en", "zh-CN", "fr", "pl", ...]
languageCode = "en"
# language name ["English", "简体中文", "Français", "Polski", ...]
languageName = "English"
# whether to include Chinese/Japanese/Korean
hasCJKLanguage = false

# default amount of posts in each pages
paginate = 12
# google analytics code [UA-XXXXXXXX-X]
googleAnalytics = ""
# copyright description used only for seo schema
copyright = ""

# whether to use robots.txt
enableRobotsTXT = true
# whether to use git commit log
enableGitInfo = true
# whether to use emoji code
enableEmoji = true

# ignore some build errors
ignoreErrors = ["error-remote-getjson", "error-missing-instagram-accesstoken"]

# Author config
[author]
  name = "Nicola Massarenti"
  email = "nicola.massarenti@gmail.com"
  link = ""

# Menu config
[menu]
  [[menu.main]]
    weight = 1
    identifier = "blog"
    pre = ""
    post = ""
    name = "Blog"
    url = "/blog/"
    title = "The blog"
  [[menu.main]]
    weight = 2
    identifier = "about"
    pre = ""
    post = ""
    name = "About"
    url = "/about/"
    title = "The about page"

[params]
  # site default theme ["auto", "light", "dark"]
  defaultTheme = "dark"
  # public git repo url only then enableGitInfo is true
  gitRepo = "https://github.com/nicolamassarenti/nicolamassarenti.com"
  #  which hash function used for SRI, when empty, no SRI is used
  # ["sha256", "sha384", "sha512", "md5"]
  fingerprint = ""
  #  date format
  dateFormat = "02/01/2006"
  # website title for Open Graph and Twitter Cards
  title = "Nicola Massarenti's website"
  # website description for RSS, SEO, Open Graph and Twitter Cards
  description = "The personal website of Nicola Massarenti"
  # website images for Open Graph and Twitter Cards
  images = ["/logo.png"]

  # Header config
  [params.header]
    # desktop header mode ["fixed", "normal", "auto"]
    desktopMode = "auto"
    # mobile header mode ["fixed", "normal", "auto"]
    mobileMode = "auto"
    #  Header title config
    [params.header.title]
      # URL of the LOGO
      logo = ""
      # title name
      name = "Nicola Massarenti"
      # you can add extra information before the name (HTML format is supported), such as icons
      pre = ""
      # you can add extra information after the name (HTML format is supported), such as icons
      post = ""
      #  whether to use typeit animation for title name
      typeit = false

  # Footer config
  [params.footer]
    enable = true
    #  Custom content (HTML format is supported)
    custom = ''
    #  whether to show Hugo and theme info
    hugo = false
    #  whether to show copyright info
    copyright = true
    #  whether to show the author
    author = true
    # Site creation time
    since = 2023
    # ICP info only in China (HTML format is supported)
    icp = ""
    # license info (HTML format is supported)
    license = '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'

  #  Section (all posts) page config
  [params.section]
    # special amount of posts in each section page
    paginate = 20
    # date format (month and day)
    dateFormat = "02-01"
    # amount of RSS pages
    rss = 10

  #  List (category or tag) page config
  [params.list]
    # special amount of posts in each list page
    paginate = 20
    # date format (month and day)
    dateFormat = "02-01"
    # amount of RSS pages
    rss = 10

  #  App icon config
  [params.app]
    # optional site title override for the app when added to an iOS home screen or Android launcher
    title = "Nicola Massarenti's website"
    # whether to omit favicon resource links
    noFavicon = false
    # modern SVG favicon to use in place of older style .png and .ico files
    svgFavicon = ""
    # Android browser theme color
    themeColor = "#ffffff"
    # Safari mask icon color
    iconColor = "#5bbad5"
    # Windows v8-10 tile color
    tileColor = "#da532c"

  #  Search config
  [params.search]
    enable = true
    # type of search engine ["lunr", "algolia"]
    type = "lunr"
    # max index length of the chunked content
    contentLength = 4000
    # placeholder of the search bar
    placeholder = ""
    #  max number of results length
    maxResultLength = 10
    #  snippet length of the result
    snippetLength = 30
    #  HTML tag name of the highlight part in results
    highlightTag = "em"
    #  whether to use the absolute URL based on the baseURL in search index
    absoluteURL = false
    [params.search.algolia]
      index = ""
      appID = ""
      searchKey = ""

  # Home page config
  [params.home]
    #  amount of RSS pages
    rss = 10
    # Home page profile
    [params.home.profile]
      enable = true
      # Gravatar Email for preferred avatar in home page
      gravatarEmail = ""
      # URL of avatar shown in home page
      avatarURL = "/images/NicolaMassarenti.jpg"
      #  title shown in home page (HTML format is supported)
      title = "Nicola Massarenti"
      # subtitle shown in home page (HTML format is supported)
      subtitle = "Freelance AI/ML Engineer"
      # whether to use typeit animation for subtitle
      typeit = true
      # whether to show social links
      social = true
      #  disclaimer (HTML format is supported)
      disclaimer = ""
    # Home page posts
    [params.home.posts]
      enable = false
      # special amount of posts in each home posts page
      paginate = 6
      #  replaced with hiddenFromHomePage in params.page
      # default behavior when you don't set "hiddenFromHomePage" in front matter
      defaultHiddenFromHomePage = false

  # Social config about the author
  [params.social]
    GitHub = "nicolamassarenti"
    Linkedin = "nicola-massarenti/?locale=en_US"
    Twitter = ""
    Instagram = ""
    Facebook = ""
    Telegram = "@nicolamassarenti"
    Medium = "@nicola-massarenti"
    Gitlab = ""
    Youtubelegacy = ""
    Youtubecustom = ""
    Youtubechannel = ""
    Tumblr = ""
    Quora = ""
    Keybase = ""
    Pinterest = ""
    Reddit = ""
    Codepen = ""
    FreeCodeCamp = ""
    Bitbucket = ""
    Stackoverflow = ""
    Weibo = ""
    Odnoklassniki = ""
    VK = ""
    Flickr = ""
    Xing = ""
    Snapchat = ""
    Soundcloud = ""
    Spotify = ""
    Bandcamp = ""
    Paypal = ""
    Fivehundredpx = ""
    Mix = ""
    Goodreads = ""
    Lastfm = ""
    Foursquare = ""
    Hackernews = ""
    Kickstarter = ""
    Patreon = ""
    Steam = ""
    Twitch = ""
    Strava = ""
    Skype = ""
    Whatsapp = ""
    Zhihu = ""
    Douban = ""
    Angellist = ""
    Slidershare = ""
    Jsfiddle = ""
    Deviantart = ""
    Behance = ""
    Dribbble = ""
    Wordpress = ""
    Vine = ""
    Googlescholar = ""
    Researchgate = ""
    Mastodon = ""
    Thingiverse = ""
    Devto = ""
    Gitea = ""
    XMPP = ""
    Matrix = ""
    Bilibili = ""
    Discord = ""
    DiscordInvite = ""
    Lichess = ""
    ORCID = "0000-0002-8882-4252"
    Pleroma = ""
    Kaggle = ""
    MediaWiki= ""
    Plume = ""
    HackTheBox = ""
    RootMe= ""
    Phone = ""
    Email = "nicola.massarenti@gmail.com"
    RSS = true # 

  #  Page global config
  [params.page]
    #  whether to hide a page from home page
    hiddenFromHomePage = false
    #  whether to hide a page from search results
    hiddenFromSearch = false
    #  whether to enable twemoji
    twemoji = false
    # whether to enable lightgallery
    lightgallery = false
    #  whether to enable the ruby extended syntax
    ruby = true
    #  whether to enable the fraction extended syntax
    fraction = true
    #  whether to enable the fontawesome extended syntax
    fontawesome = true
    # whether to show link to Raw Markdown content of the content
    linkToMarkdown = true
    #  whether to show the full text content in RSS
    rssFullText = false
    #  Table of the contents config
    [params.page.toc]
      # whether to enable the table of the contents
      enable = true
      #  whether to keep the static table of the contents in front of the post
      keepStatic = true
      # whether to make the table of the contents in the sidebar automatically collapsed
      auto = true
    #  KaTeX mathematical formulas
    [params.page.math]
      enable = true
      #  default inline delimiter is $ ... $ and \( ... \)
      inlineLeftDelimiter = ""
      inlineRightDelimiter = ""
      #  default block delimiter is $$ ... $$, \[ ... \], \begin{equation} ... \end{equation} and some other functions
      blockLeftDelimiter = ""
      blockRightDelimiter = ""
      # KaTeX extension copy_tex
      copyTex = true
      # KaTeX extension mhchem
      mhchem = true
    #  Code config
    [params.page.code]
      # whether to show the copy button of the code block
      copy = true
      # the maximum number of lines of displayed code by default
      maxShownLines = 50
    #  Mapbox GL JS config
    [params.page.mapbox]
      # access token of Mapbox GL JS
      accessToken = ""
      # style for the light theme
      lightStyle = "mapbox://styles/mapbox/light-v10?optimize=true"
      # style for the dark theme
      darkStyle = "mapbox://styles/mapbox/dark-v10?optimize=true"
      # whether to add NavigationControl
      navigation = true
      # whether to add GeolocateControl
      geolocate = true
      # whether to add ScaleControl
      scale = true
      # whether to add FullscreenControl
      fullscreen = true
    #  social share links in post page
    [params.page.share]
      enable = true
      Twitter = true
      Facebook = true
      Linkedin = false
      Whatsapp = false
      Pinterest = false
      Tumblr = false
      HackerNews = true
      Reddit = false
      VK = false
      Buffer = false
      Xing = false
      Line = true
      Instapaper = false
      Pocket = false
      Flipboard = false
      Weibo = true
      Blogger = false
      Baidu = false
      Odnoklassniki = false
      Evernote = false
      Skype = false
      Trello = false
      Mix = false
    #  Comment config
    [params.page.comment]
      enable = true
      # Disqus comment config
      [params.page.comment.disqus]
        # 
        enable = false
        # Disqus shortname to use Disqus in posts
        shortname = ""
      # Gitalk comment config
      [params.page.comment.gitalk]
        # 
        enable = false
        owner = ""
        repo = ""
        clientId = ""
        clientSecret = ""
      # Valine comment config
      [params.page.comment.valine]
        enable = false
        appId = ""
        appKey = ""
        placeholder = ""
        avatar = "mp"
        meta= ""
        pageSize = 10
        # automatically adapt the current theme i18n configuration when empty
        lang = ""
        visitor = true
        recordIP = true
        highlight = true
        enableQQ = false
        serverURLs = ""
        #  emoji data file name, default is "google.yml"
        # ["apple.yml", "google.yml", "facebook.yml", "twitter.yml"]
        # located in "themes/LoveIt/assets/lib/valine/emoji/" directory
        # you can store your own data files in the same path under your project:
        # "assets/lib/valine/emoji/"
        emoji = ""
      # Facebook comment config
      [params.page.comment.facebook]
        enable = false
        width = "100%"
        numPosts = 10
        appId = ""
        # automatically adapt the current theme i18n configuration when empty
        languageCode = ""
      #  Telegram comments config
      [params.page.comment.telegram]
        enable = false
        siteID = ""
        limit = 5
        height = ""
        color = ""
        colorful = true
        dislikes = false
        outlined = false
      #  Commento comment config
      [params.page.comment.commento]
        enable = false
      #  utterances comment config
      [params.page.comment.utterances]
        enable = false
        # owner/repo
        repo = ""
        issueTerm = "pathname"
        label = ""
        lightTheme = "github-light"
        darkTheme = "github-dark"
      # giscus comment config (https://giscus.app/)
      [params.page.comment.giscus]
        # You can refer to the official documentation of giscus to use the following configuration.
        enable = false
        repo = ""
        repoId = ""
        category = "Announcements"
        categoryId = ""
        # automatically adapt the current theme i18n configuration when empty
        lang = ""
        mapping = "pathname"
        reactionsEnabled = "1"
        emitMetadata = "0"
        inputPosition = "bottom"
        lazyLoading = false
        lightTheme = "light"
        darkTheme = "dark"
    #  Third-party library config
    [params.page.library]
      [params.page.library.css]
        # someCSS = "some.css"
        # located in "assets/"
        # Or
        # someCSS = "https://cdn.example.com/some.css"
      [params.page.library.js]
        # someJavascript = "some.js"
        # located in "assets/"
        # Or
        # someJavascript = "https://cdn.example.com/some.js"
    #  Page SEO config
    [params.page.seo]
      # image URL
      images = []
      # Publisher info
      [params.page.seo.publisher]
        name = ""
        logoUrl = ""

  #  TypeIt config
  [params.typeit]
    # typing speed between each step (measured in milliseconds)
    speed = 100
    # blinking speed of the cursor (measured in milliseconds)
    cursorSpeed = 1000
    # character used for the cursor (HTML format is supported)
    cursorChar = "|"
    # cursor duration after typing finishing (measured in milliseconds, "-1" means unlimited)
    duration = -1

  # Site verification code config for Google/Bing/Yandex/Pinterest/Baidu
  [params.verification]
    google = ""
    bing = ""
    yandex = ""
    pinterest = ""
    baidu = ""

  #  Site SEO config
  [params.seo]
    # image URL
    image = "https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.com/main/assets/images/NicolaMassarenti.jpg"
    # thumbnail URL
    thumbnailUrl = "https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.com/main/assets/images/NicolaMassarenti.jpg"

  #  Analytics config
  [params.analytics]
    enable = false
    # Google Analytics
    [params.analytics.google]
      id = ""
      # whether to anonymize IP
      anonymizeIP = true
    # Fathom Analytics
    [params.analytics.fathom]
      id = ""
      # server url for your tracker if you're self hosting
      server = ""
    # Plausible Analytics
    [params.analytics.plausible]
      dataDomain = ""
    # Yandex Metrica
    [params.analytics.yandexMetrica]
      id = ""

  #  Cookie consent config
  [params.cookieconsent]
    enable = true
    # text strings used for Cookie consent banner
    [params.cookieconsent.content]
      message = ""
      dismiss = ""
      link = ""

  #  CDN config for third-party library files
  [params.cdn]
    # CDN data file name, disabled by default
    # ["jsdelivr.yml"]
    # located in "themes/LoveIt/assets/data/cdn/" directory
    # you can store your own data files in the same path under your project:
    # "assets/data/cdn/"
    data = ""

  #  Compatibility config
  [params.compatibility]
    # whether to use Polyfill.io to be compatible with older browsers
    polyfill = false
    # whether to use object-fit-images to be compatible with older browsers
    objectFit = false

# Markup related config in Hugo
[markup]
  # Syntax Highlighting
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNos = true
    lineNumbersInTable = true
    # false is a necessary configuration
    # (https://github.com/dillonzq/LoveIt/issues/158)
    noClasses = false
  # Goldmark is from Hugo 0.60 the default library used for Markdown
  [markup.goldmark]
    [markup.goldmark.extensions]
      definitionList = true
      footnote = true
      linkify = true
      strikethrough = true
      table = true
      taskList = true
      typographer = true
    [markup.goldmark.renderer]
      # whether to use HTML tags directly in the document
      unsafe = true
  # Table Of Contents settings
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 6

# Sitemap config
[sitemap]
  changefreq = "weekly"
  filename = "sitemap.xml"
  priority = 0.5

# Permalinks config
[Permalinks]
  # posts = ":year/:month/:filename"
  posts = ":filename"

# Privacy config
[privacy]
  #  privacy of the Google Analytics (replaced by params.analytics.google)
  [privacy.googleAnalytics]
    # ...
  [privacy.twitter]
    enableDNT = true
  [privacy.youtube]
    privacyEnhanced = true

# Options to make output .md files
[mediaTypes]
  [mediaTypes."text/plain"]
    suffixes = ["md"]

# Options to make output .md files
[outputFormats.MarkDown]
  mediaType = "text/plain"
  isPlainText = true
  isHTML = false

# Options to make hugo output files
[outputs]
  # 
  home = ["HTML", "RSS", "JSON"]
  page = ["HTML", "MarkDown"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML", "RSS"]
  taxonomyTerm = ["HTML"]

```

### Favicons
I used [this]() picture and generated the different formats using [realfavicongenerator](https://realfavicongenerator.net/) . 

## Skeleton structure

Setting up the skeleton (menu bar, header, footer) is fairly simple.  
```toml
# Menu config
[menu]
  [[menu.main]]
    weight = 1
    identifier = "blog"
    pre = ""
    post = ""
    name = "Blog"
    url = "/blog/"
    title = "The blog"
  [[menu.main]]
    weight = 2
    identifier = "about"
    pre = ""
    post = ""
    name = "About"
    url = "/about/"
    title = "The about page"

[params]
  # site default theme ["auto", "light", "dark"]
  defaultTheme = "dark"
  # public git repo url only then enableGitInfo is true
  gitRepo = "https://github.com/nicolamassarenti/nicolamassarenti.com"
  #  which hash function used for SRI, when empty, no SRI is used
  # ["sha256", "sha384", "sha512", "md5"]
  fingerprint = ""
  #  date format
  dateFormat = "02/01/2006"
  # website title for Open Graph and Twitter Cards
  title = "Nicola Massarenti's website"
  # website description for RSS, SEO, Open Graph and Twitter Cards
  description = "The personal website of Nicola Massarenti"
  # website images for Open Graph and Twitter Cards
  images = ["/logo.png"]

  # Header config
  [params.header]
    # desktop header mode ["fixed", "normal", "auto"]
    desktopMode = "auto"
    # mobile header mode ["fixed", "normal", "auto"]
    mobileMode = "auto"
    #  Header title config
    [params.header.title]
      # URL of the LOGO
      logo = ""
      # title name
      name = "Nicola Massarenti"
      # you can add extra information before the name (HTML format is supported), such as icons
      pre = ""
      # you can add extra information after the name (HTML format is supported), such as icons
      post = ""
      #  whether to use typeit animation for title name
      typeit = false

  # Footer config
  [params.footer]
    enable = true
    #  Custom content (HTML format is supported)
    custom = ''
    #  whether to show Hugo and theme info
    hugo = false
    #  whether to show copyright info
    copyright = true
    #  whether to show the author
    author = true
    # Site creation time
    since = 2023
    # ICP info only in China (HTML format is supported)
    icp = ""
    # license info (HTML format is supported)
    license = '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'
```

It sets the menu, the footer and the header configurations. There are two sections: `blog`, that contains my articles, and `about`, a page with my work experiences.

## Home page

To setup the home page is necessary to save the avatar in folder `assets/images`.  The configurations are:
```toml
  [params.home]
    rss = 10
    [params.home.profile]
      enable = true
      gravatarEmail = ""
      avatarURL = "/images/NicolaMassarenti.jpg"
      title = "Nicola Massarenti"
      subtitle = "Freelance AI/ML Engineer"
      typeit = true
      social = true
      disclaimer = ""
    [params.home.posts]
      enable = false
      paginate = 6
      defaultHiddenFromHomePage = false

  [params.social]
    GitHub = "https://github.com/nicolamassarenti"
    Linkedin = "https://www.linkedin.com/in/nicola-massarenti/"
    Telegram = "@nicolamassarenti"
    Medium = "https://medium.com/@nicola-massarenti"
    ORCID = "https://orcid.org/0000-0002-8882-4252"
    Email = "nicola.massarenti@gmail.com"
    RSS = true # 
```

## Setting up CI/CD 

Setting up the *CI/CD* on GitHub is fast: you can automate your deployments by using the default action for `hugo` applications. The `yml` is provided by GitHub and is the following:

```yml
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: true

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.108.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Install Dart Sass Embedded
        run: sudo snap install dart-sass-embedded
      - name: Checkout
        uses: actions/checkout@v3
        with:
          submodules: recursive
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v2
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```


## Setting up GitHub Pages and Google Domains

First of all, you have to enable GitHub pages for your profile by going on your *profile settings* and enabling Pages. Then, you have to [configure an apex domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain), add your desired custom domain and save the configurations.

Now it's time to move to Google Domains and click on *Manage* to the website you want to use as a custom domain.

![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/create-a-website-for-free-github-google-domains/domains-1.png "")

Then, add the Host Name records as shown in the picture below.

![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/create-a-website-for-free-github-google-domains/domains-2.png "")

## Conclusions

The process of creating a website can be daunting, especially if you have limited time and knowledge of front-end technologies. However, as demonstrated in this post, it is possible to create a professional, blog-friendly website with minimal effort by using a framework for static websites such as Hugo and a suitable theme. By following the steps outlined in this post, you can have your own website up and running in no time and for free.

I hope you found this post helpful and informative. If you have any questions or comments, please don't hesitate to leave them below or to reach out to me on my [LinkedIn account](https://www.linkedin.com/in/nicola-massarenti/?locale=en_US). I would love to hear from you.