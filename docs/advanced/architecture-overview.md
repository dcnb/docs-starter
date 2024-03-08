---
title: Overview of Template Structure
parent: Advanced
nav_order: 9
---

# Overview of CollectionBuilder Template Directory Structure and Conventions

CollectionBuilder is a Jekyll-based project, so most of the folder structure and architecture follows the basic [directory structure of Jekyll](https://jekyllrb.com/docs/structure/).
This section provides a high-level overview of files and folders as they are used in CollectionBuilder.
*Please note* CB-GH projects may not contain all these directories.

| Directory | Description|
| --- | --- |
| `_data/` | The [Jekyll data](https://jekyllrb.com/docs/datafiles/) folder contains CSVs and YAML that can be accessed by the template to build the site. In CB "_data/" will contain your metadata CSV, the "config-" CSVs that set options for visualization pages, and "theme.yml" that sets some overall configurations. |
| `_includes/` | The [Jekyll includes](https://jekyllrb.com/docs/includes/) folder contains modular chunks of HTML and JS that are used by pages and layouts to generate content on the site. Most users will not need to edit these files, but please refer to the [CB Includes](#cb-includes) section below for more detailed information. |
| `_layouts/` | The [Jekyll layouts](https://jekyllrb.com/docs/layouts/) folder contains HTML templates used to build all the pages on the site. CB users may want to tweak some layouts, such as ["home-infographic.html"]({{ '/docs/pages/home/' | relative_url }}), to control how pages look. In CB-CSV the folder "_layouts/item/" contains the layouts that match the `display_template` used by collection items. All layouts ultimately use the "default.html" layout, which pulls together the full page structure including head, banner, nav, footer, and javascript. |
| `_plugins/` | The [Jekyll plugins](https://jekyllrb.com/docs/plugins/) folder contains extensions to Jekyll written in Ruby. CB-CSV comes with [custom CB plugins](https://github.com/CollectionBuilder/collectionbuilder-csv/blob/main/docs/plugins.md) that are required to build item pages and efficiently process metadata. |
| `_sass/` | Contains "Sass partials", modular chunks of [Sass](https://sass-lang.com/) CSS. These partials are pulled into the file "assets/css/cb.scss" when the website is built, adding CB specific styles. Users can add custom CSS that will override all Bootstrap and CB styles by editing the "_custom.scss" file. In general the other partials should not be edited. |
| `_site/` | Contains the full static site output by Jekyll on your local machine. This folder is ignored by Git, since it should not be committed to your project--so you will not see it on GitHub. After doing a `rake deploy` or `jekyll build`, the contents "_site" can be copied to a web hosting location. This is done automatically by [online deployment services]({{ '/docs/deploy/' | relative_url }}) such as GitHub Pages, Actions, or Render. |
| `.github/` |  This folder is for special files used on GitHub to configure platform features. The contents aren't a necessary part of CB, but just relate to GitHub. For example, this is where you would add a GitHub Action yml file. In CB-CSV it contains template files for Issues and PRs--you can delete those in your project if desired! |
| `.jekyll-cache` | This is a temporary folder used during the Jekyll build process. It is git ignored, and you can ignore it too! |
| `assets/` | Contains third-party libraries, as well as CB specific CSS, JS, and data used on the site. The contents of this folder do not generally need to be edited by CB users. See the [CB Assets section](#cb-assets) below for details. |
| `docs/` | Contains technical documentation specific to each template. Markdown files in this folder may help provide more technical details if you are doing advanced customization of the template. This is also a good place to put your own project documentation and notes! |
| `objects/` | Contains the digital files used in your collection, see [Collection Objects section]({{ '/docs/objects/' | relative_url }}). |
| `pages/` | Contains the Markdown stubs that will become web pages in your digital collection. Most stubs do not need to be edited as they are controlled by config options. However, users will want to [edit the About or add more interpretive pages]({{ '/docs/pages/' | relative_url }}). |
| `utilities/` | Contains the [sitemap](https://www.sitemaps.org/) and other technical outputs. This folder does not need to be edited by users. |
| `.gitignore` | [Git Ignore](https://git-scm.com/docs/gitignore) is a file that tells Git to NOT track some files or folders. CB has an ignore that follows a typical Jekyll template. Note that the "objects" directory is ignored by default on CB-CSV projects, since your collection files will be hosted somewhere else. |
| `404.html` | 404 is the response a server sends if the requested page doesn't exist. GitHub Pages and many other servers will automatically direct 404s to the file "404.html" on you site--so this page sets up your 404 message! |
| `CITATION.cff` | [Citation File Format](https://citation-file-format.github.io/) is a file for human- and machine-readable citation information for software repositories. This refers to the the CB software credits. |
| `CODE_OF_CONDUCT.md` | Open source projects are encouraged to have a code of conduct outlining the expectations for the community. This is CB's CoC, you could update the details for your own project! |
| `CONTRIBUTING.md` | Open source project are encouraged to have a "contributing" doc that outlines general conventions and expectations for how to contribute. |
| `_config.yml` | The file used to [configure the core features of your CollectionBuilder site]({{ '/docs/config/' | relative_url }}). |
| `favicon.ico` | This icon will display in the browser tab. You can add or create your own to customize your collection site. |
| `Gemfile` | Gemfiles are used to manage Ruby dependencies. CB uses a basic Jekyll Gemfile. |
| `Gemfile.lock` | The Gemfile.lock is generated by your computer to record the exact Ruby Gems used. By default CB ignores the lock for simplicity. However, for more stability you may way to commit your lock to be able to reproduce the exact environment used to build your project. |
| `LICENSE` | This MIT license applies to the CB template code and must be preserved with any CB project. You can add your own license to your content, but the CB template remains MIT. |
| `Rakefile` | Provides automated tasked writing in Ruby. CB templates come with some useful utilities written as [Rake tasks](https://github.com/CollectionBuilder/collectionbuilder-csv/blob/main/docs/rake_tasks.md). |
| `README.md` | A README describes a project and provides orientation to a repository, and will be displayed on the GitHub home page. If you are starting a CB project, you will want to delete the CB content of the README and describe your own project. |

-----------

## CB Includes 

[Jekyll includes](https://jekyllrb.com/docs/includes/) are modular chunks of HTML and JS that can be pulled into pages and layouts to generate content. 
CB templates come with a set of includes that create most of the features of the digital collection. 

Most users will not need to edit the includes, but may want to refer to documentation that is at the top of most files inside a "comment" tag.
The comments will provide guidance on how to use the include and its options.

The CB includes are grouped into folders to help keep organized:

- "cb/" contains demo content.
- "feature/" contains includes used to add components to interpretative pages. This is the most important place for users to explore! All files have comments explaining their use.
- "head/" contains chunks that write out the `<head>` section of each page. If you are using a custom analytics package, you will want to paste your tracking script into "analytics.html".
- "index/" contains components designed for the CB home page.
- "item/" contains components use on items pages in CB-CSV.
- "js/" contains modular chunks of javascript which are pulled into the bottom of visualization pages. This allows the javascript to load in the correct order.
- "/" the main template elements are in the root of the includes folder. Important files:
    - "collection-banner.html" controls the banner (i.e. the very top of the page including the title and tagline) on all pages.
    - "collection-nav.html" creates the navbar.
    - "footer.html" creates the footer featured on every page.
    - "foot.html" is added to the bottom of every page and contains all the javascript. This allows libraries and dependencies to be loaded efficiently in the correct order.

## CB Assets

Contains third-party libraries, as well as CB specific CSS, JS, and data used on the site. 
The contents of this folder are important, but do not generally need to be edited by CB users.

The contents are organized into folders to stay organized:

- "css/" contains the "cb.scss" file which pulls in the Sass partials in "_sass" at build time. This ensures that CB styles and any custom styles added by the user (in "_sass/_custom.scss") will override all Bootstrap and other library styles. Most users will not need to edit "cb.scss"--please edit "_sass/_custom.scss" instead.
- "data/" contains templates that create the data derivative outputs from your metadata. In the built out collection, these are designed for users of your site to download. It is structured following the Frictionless Data "Data Package" spec. See ["data" docs for details](https://github.com/CollectionBuilder/collectionbuilder-csv/blob/main/docs/data.md).
- "img/" contains some media used by the template. This is a good place to put extra files used in your project, such as logos.
- "js/" contains specialized js and json files used by visualization pages.
- "lib/" contains all third-party libraries used in the site. This ensures projects are full self-contained and can be run without connections to external dependencies or internet. This code is from external projects with their own licenses. These include: 
    - [Bootstrap](https://getbootstrap.com/)
    - [Bootstrap Icons](https://icons.getbootstrap.com/)
    - [DataTables](https://datatables.net/)
    - [Leaflet](https://leafletjs.com/)
    - [spotlight gallery](https://github.com/nextapps-de/spotlight)
    - [lazysizes](https://github.com/aFarkas/lazysizes)
    - [Lunr](https://lunrjs.com/)
