---
title: Metadata
parent: Page Config
nav_order: 2
---

# Metadata / Item Page Configuration (config-metadata.csv)

The most important CSV (if you're measuring by the number of pages it creates!), the "_data/config-metadata.csv" controls how an item's metadata is displayed on its web page. 
It also configures the machine-readable meta markup in the underlying code. 

The columns are described below, and an [example](#example) is provided for your convenience: 

### field: 
- This variable corresponds to the field listed in the metadata for the collection. For instance, if you have a metadata field called "original-collection", you would put `original-collection` here. 

### display_name: 
- This variable is how you'd like the field to be described on the item page. So, using the example above, if you'd like the field "original-collection" to appear as "Original Archival Collection" on the item page, you'd enter `Original Archival Collection` in the second column.

### browse_link: 
- *Options*: `true` or leave blank. 
- This option controls if the element will be represented as a link from the item page back to the Browse page. It is most useful for those fields, like "subject", that often contain multiple values (separated by a semicolon). So, for instance, if you wanted to make the subjects in your "subject" field separate out into individual links, you'd enter `true` in the third column of the "_data/config-metadata.csv".

### external_link: 
- *Options*: `true` or leave blank. 
- This option controls if the element will be represented as an external link from the item page to another page elsewhere (or within the collection itself). It is most useful for those fields, like "rightsstatement", that are just links. The metadata value must only be a link -- any additional text or spacing will break the link on the page. 


------

The following two options are used by **CSV only**, and are not necessary to make the collection itself work and will not affect the display.
However, configuring these options adds rich machine readable markup to each item page, making your objects more discoverable by search engines.

### dc_map: 
- *Options:* the prefix `DCTERMS`, plus a property name from the [DC Terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/){:target='_blank' rel='noopener'} namespace, written like: `DCTERMS.term_from_terms_namespace`
- This option allows you to map your metadata field to a Dublin Core property to be added in machine readable meta markup. So, continuing with our example, if you'd like to map the "original-collection" field to be read as a [Dublin Core Source](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/#http://purl.org/dc/terms/source){:target='_blank' rel='noopener'}, you'd enter `DCTERMS.source` in the third column.
- Recommended fields to map include: 
    - `DCTERMS.title`
    - `DCTERMS.creator`
    - `DCTERMS.date`
    - `DCTERMS.description`
    - `DCTERMS.subject`
    - `DCTERMS.type`
    - `DCTERMS.rights`

### schema_map:
- *Options:* any property name from Schema [CreativeWork](https://schema.org/CreativeWork){:target='_blank' rel='noopener'} type. Copy the exact property name, as this value will be turned into schema JSON-LD markup. 
- [Schema](https://schema.org/){:target='_blank' rel='noopener'} is a standard designed to provide structured semantic markup for search engines to better understand content of web pages. This option allows you to add Schema markup in JSON-LD format to item pages driven by the object metadata.  
- Recommended fields to map include:
    - `headline` (i.e. the title)
    - `creator`
    - `dateCreated`
    - `description`
    - `keywords`
    - `contentLocation`
    - `encodingFormat` (This corresponds to the [format]({{ '/docs/metadata/gh_metadata/#format' | relative_url }}) field of CollectionBuilder items)
    - `license` (Should only be used with a standardized rights URL)

------

## Example 

```
field,display_name,browse_link,dc_map,schema_map
title,Title,,DCTERMS.title,headline
creator,Creator,,DCTERMS.creator,creator
date,Date Created,,DCTERMS.date,dateCreated
date-is-approximate,Approximated Date
description,Description,,DCTERMS.description,description
subject,Subjects,true,DCTERMS.subject,keywords
location,Location,true,,contentLocation
identifier,Source Identifier
type,Type,,DCTERMS.type
format,Format,,,encodingFormat
rightsstatement,,,DCTERMS.rights,license
```

### Browse Links 

In the case of this example, only the location and subject fields have a value (`true`) for "browse-link", so those fields will turn each individual subject and location term (delimited by semicolon in that field) into a link (e.g. browse.html#dogs) that links back to a browse page view that will only list those items that share that term. 

<div class="alert alert-green" markdown="1">

**A Note on Dublin Core and Schema Markup for SEO and Machine Reading**

The title, creator, date, description, subject, and type fields in the above example all have a `dc_map` variable, so each of them would be represented in the item page's `<head>` meta section in a way that follows the Dublin Core schema to enable better machine readability and indexing.

Similarly, the title, creator, date, description, subject, location, format, and rightstatement fields all have a `schema_map` entry, so each of these would be represented in an item page's `<head>` meta section in a way that follows [schema.org](https://schema.org/){:target="_blank" rel="noopener"} recommendations in order to enable better machine readability and indexing.

</div>
