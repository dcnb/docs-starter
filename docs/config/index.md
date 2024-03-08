---
title: Site Config
has_children: true
nav_order: 6
---

# Initial Site Configuration

The file "_config.yml" is used to configure the core features of your CollectionBuilder site. 
This section will take you through the configuration options you can enable by editing this file. 

CB's configuration options are made up of key-value pairs written in [YAML]({{ '/docs/glossary/#yaml' | relative_url }}). 

For example, below is the option "title":

```yaml
# title of site appears in banner
title: Example Site Title
```

First, note the line proceeded by a `#` hash in the example above--everything following the hash is a comment in YAML.
CollectionBuilder's "_config.yml" uses a bunch of comments to divide the content into sections and to explain how to fill in the values--be sure to read the comments for tips and examples!

In the example, `title:` is the "key" of the key-value pair. 
YAML keys are a string followed by a colon `:` and a space--after which follows the value. 

## Template Values

When you start fresh from the CB template, placeholder values fill all the options, providing you a working example.
So to begin configuring and customizing your site, open the "_config.yml" file in the base of your project repository and replace the placeholder values with new ones for your project, following the example. 

Some options are "commented out", i.e. have `# ` in front of them to make them inactive. 
To enable these, you would need to *uncomment* the line, which requires you to delete the `# ` and space in front of the value. 

The docs in the following pages address the details of what goes in the values.

## Common YAML Errors

YAML is *very picky* about tiny details of spaces and indentation! 
If you have incorrect YAML in your "_config.yml", your Jekyll project won't build and you'll get mysterious error messages.

Carefully check over your "_config.yml" for these common errors:

- Space in front of key -- the key needs to start the line, no spaces in front! This can be hard to see. If you *uncomment* an option, be sure to delete that extra space in front. 
- No space after colon -- the key needs to be followed by *exactly* colon + space `: `. If you don't put a space before the starting the value, you'll get an error.
- Quote values that have a colon -- if your value contains a colon `:`, be sure to put quotes `"` around the full value!

{:.alert .alert-yellow .mt-4}
The "_config.yml" file serves as the main configuration file standard in all Jekyll projects. Some values are related to technical details specific to Jekyll. 
The rest are the important values that will populate the template elements of your collection site--for example, the site title and organization name that will appear in the header and footer of every page.
