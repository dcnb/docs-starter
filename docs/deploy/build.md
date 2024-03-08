---
title: Jekyll Build
parent: Deploy
nav_order: 3
---

# Build Locally and Self Host

The most common way to build your CB-CSV site is to use Jekyll on your local computer (which can also be done with CB-GH if desired!).

Jekyll build is a bit different than [using the development server]({{ '/docs/repository/generate/' | relative_url }}) because it outputs all the URLs used in the site to match your final deployment location based on your [configuration options]({{ '/docs/config/url/' | relative_url }}).
The build version will include real URLs, swapping out the development links starting with `http://localhost:4000/` used by `jekyll s` with the production url value you have configured, e.g. `https://example.org`.

## Build with Rake Deploy

If you are running a development server (jekyll s), stop the server by typing `Ctrl + C` in the terminal.
Otherwise, open a terminal window in your project repository (usually the integrated terminal in your text editor). 
Then give the command:

```
rake deploy
```

This will run the Jekyll build command which may take quite a bit longer than Jekyll serve (for details to why, see below). 
Once finished, your complete site will be output in the "_site" directory.

*P.S.* `rake deploy` is short hand for the full command `JEKYLL_ENV=production bundle exec jekyll build` which we thought was too long to remember!

## Move the Files

With the build complete, the files in "_site" are your digital collection, ready to go to their final home! 
The full contents of "_site" need to be copied to your web server.

How you move the files will depend on the access set up for your server. 
For static servers, some common options include:

- **Network drive / Shared folder:** your organization's IT may provide a network drive that you can use just like a normal folder on your computer. Open "_site", select everything (`Ctrl + A`), and copy (`Ctrl + C`). Open the web folder in the location you want to deploy and paste (`Ctrl + V`) the contents of "_site" in.
- **SFTP:** many traditional servers have FTP access. Use an FTP client to upload the contents of "_site" to your server in the location you want to deploy.
- **cPanel:** many hosts (such as Reclaim) provide cPanel as a web based interface to your server. Click on "File Manager" to upload files via the web interface. Your server will generally have a folder named something like "public_html" that represents the root of your website. 

*Tip:* If you don't have a server, it is possible to build and host all CB projects via GitHub Pages. 
This works well if your objects are hosted elsewhere since you won't encounter size limits in your repository.
Check [GitHub Actions]({{ '/docs/deploy/actions/' | relative_url }}) and [Third party build services]({{ '/docs/deploy/thirdparty/' | relative_url }}) for more info.

{:.alert .alert-yellow}
The files in "_site" will use URLs based on what you set in "_config.yml".
Some features and navigation may be broken if your ["URL variables"]({{ '/docs/config/url/' | relative_url }}) do not match the actual location deployed!

--------------

# Details of the Build Process

During the build process, Jekyll knits together the data, configuration, Markdown, and modular components of the template to output a complete site.
The output is the web like it's 1999--a folder of HTML, CSS, and JS files that make up a static website.

During both Jekyll serve and build, your project code is processed and output into the "_site" folder.

When you're generating a test site using `bundle exec jekyll s`, Jekyll automatically builds all the pages with links based on the development server, by default using urls that start with `http://127.0.0.1:4000/` or `http://localhost:4000/`. 

For deployment, the command `bundle exec jekyll build` builds the site using links based on the production URLs configured in "_config.yml".

However, to build out *EVERYTHING* you need to add one more option--the Jekyll ["production" environment](https://jekyllrb.com/docs/configuration/environments/){:target="_blank" rel="noopener"}.
Some features (meta tags and analytics) are *only* added to your CollectionBuilder site when built in the "production" environment.
This saves time during development and avoids false analytics data.

The production ENV adds:

- **Meta markup:** adds rich machine readable markup to the `<head>` of every page, including [Open Graph](https://opengraphprotocol.org/){:target='_blank' rel='noopener'}, [Dublin Core](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/){:target='_blank' rel='noopener'}, and [Schema](https://schema.org/){:target='_blank' rel='noopener'} as configured in ["config-metadata.csv"]({{ '/docs/customization/config-metadata/' | relative_url }}).
- **Analytics:** adds the include "_includes/head/analytics.html" to every page. This adds your [analytics snippet if configured]({{ '/cb-docs/docs/advanced/analytics/' | relative_url }}). Waiting until final deployment to add analytics prevents false hits during testing.

The environment can be added before the Jekyll command, like `JEKYLL_ENV=production bundle exec jekyll build`. 
To make it easier, CollectionBuilder provides the `rake deploy` command as an alternative.
It is also the environment used by the automatic build on GitHub Pages!
