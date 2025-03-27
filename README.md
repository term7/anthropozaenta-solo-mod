# anthropozaenta-solo-mod

This is a modded version of the original [Solo theme](https://github.com/tryghost/solo) for [Ghost](https://github.com/tryghost/ghost/), and only used for theme installation!<br>
We were asked to build the theme for [ANTHROPOZAENTA](https://anthropozaenta.org) based on Solo. In the spirit of FOSS, we publish all changes that were made in this repository.<br>
If you're looking to contribute to Ghost, head over to the main repository [here](https://github.com/TryGhost/Themes).

#### IMPORTANT CHANGES:

- We removed the portal with all its signup and subscription options: no newsletter, no subscription based content
- We removed the search functionality because it leverages a third party service: [UNPKG](https://unpkg.com)
- We removed content related to twitter and facebook, yet we were asked to keep instagram
- We changed the copyright from © to a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode)
- We added jQuery
- We added Mastodon integration
- We added German & English language buttons
- We added the Anthropozänta logo as a scroll-top-to-page button

# Mastodon

To include links to your Mastodon account, use the site-wide code injection tool in settings (Ghost Admin). Change `your-username` and `your-mastodon-server` to the appropriate values in the script below, then copy it into the Site Footer:

```
<script type="text/javascript">
    $('.gh-author-github').attr('href', 'https://github.com/your-username');
    $('.gh-author-mastodon').attr('href', 'https://your-mastodon-server/@your-username');
</script>
``` 

# German / English buttons

anthropozaenta-solo-mod automatically shows and hides German/English navigation buttons if a marker for different language versions is present in a page or in a blog post. These buttons can be used to scoll the current page to a German and to an English language section. To automatically show these navigation buttons, include the following html snippet just above your German language section in your post:

```
<div id="DE"></div>
``` 

Also include this html snippet above your English language section in your post:

```
<div id="EN"></div>
``` 

PLEASE NOTE: you can only include one English snippet and one German snippet in your post. Multiple html snippets of the same kind in the same post will break the functionality of these buttons.


# AN IMPORTANT NOTICE ABOUT PRIVACY:

This is a quote from Ghost's [privacy declaration](https://github.com/TryGhost/Ghost/blob/main/PRIVACY.md):

<em>To easily load member functionality for membership features, Ghost leverages [UNPKG](https://unpkg.com) to provide a CDN for drop-in script known as Portal. If member signups are disabled, no CDN will be injected.</em>

While this is true for the Portal, in order to serch posts, tags and authors, Ghost loads UNPKG nevertheless to provide search functionality on the page. We removed all elements and buttons in our theme that are related to search functionality because we hoped in consequence the CDN also won't be injected anymore. However, the CDN still is injected into our website. If you look at the page source, it looks like this (the data key always is an individual key for each website):


```
<script defer src="https://unpkg.com/@tryghost/sodo-search@~1.0.0/umd/sodo-search.min.js" data-sodo-search="https://journal.ghost.io/" data-version="1.0.0" data-key="77fa60d37b3ada6d747320b139" crossorigin="anonymous"></script>
```

While search functionality is a nice feature, and even though UNPKG is an open source project, we don't like having to trust third parties. UNPKG still is powered by [Cloudflare](https://www.cloudflare.com/en-gb/privacypolicy/)... The injected CDN further loads additional resources (Javascript and CSS stylesheets), over which we have no direct control. For privacy reasons we want to serve all scripts, fonts, etc. locally.

In oder to stop loading [UNPKG](https://unpkg.com) you will have to host Ghost on your own VPS and change a configuration file. You can find instructions on how to install Ghost [here](https://ghost.org/docs/install/).<br>
Then, log into your VPS, enter the directory of your ghost installation and edit '/versions/5.x.x/core/shared/config/defaults.json', i.e.:

```
cd /var/www/ghost
```
```
nano versions/5.4.0/core/shared/config/defaults.json
```

Delete these lines:

```
"sodoSearch": {
    "url": "https://unpkg.com/@tryghost/sodo-search@~1.0.0/umd/sodo-search.min.js",
    "version": "1.0.0"
},
```

Then restart Ghost:

```
ghost restart
```

Thats it.<br>
We encourage you to copy, adapt, share and re-distribute!

# Copyright & License

Copyright (c) 2013-2024 Ghost Foundation [& term7] - Released under the [MIT license](LICENSE).
