# logseq-better-zotero-plugin

## A fully local and improved Zotero-Itegration for Logseq using BetterBibTeX JSON

This is a plugin for [Logseq](https://logseq.com/) that allows you to search your literature in [Zotero](https://www.zotero.org/) and creates customizable literature pages.
These use the [Nunjucks syntax](https://mozilla.github.io/nunjucks/templating.html) and allow for maximum customization on your side.
No API or internet connection is required, making it truly local!

* import your literature from Zotero as you need it
* customize the appearance of literature pages according to your needs
* modify data with Nunjucks

## Usage

[!usageVideo](https://github.com/arcusamicus/logseq-better-zotero-plugin/assets/90210405/c83e45ca-8510-476a-8900-28be74ae0d03)

## Installation

1. download this repository
2. enable Developer mode in Logseq
![developerMode](https://github.com/arcusamicus/logseq-better-zotero-plugin/assets/90210405/08287d22-150a-4338-bde8-4da5d0d14b15)
3. in the Plugins window in Logseq click on `Load unpacked plugin` and select the downloaded repository
4. export your Zotero library in BetterBibTeX JSON format (with keep updated enabled)
![zoteroSetup](https://github.com/arcusamicus/logseq-better-zotero-plugin/assets/90210405/c71b93dc-765e-4c4a-86b4-ab17e5a07fba)
5. copy the full path to this BetterBibTeX JSON file into the plugin settings
6. use the Slash-Command `/better Zotero` in a block in Logseq and start searching for literature

## customization
* set up the name of the slash-command, the path to the BetterBibTeX-JSON-file, the title-template and the page-template parentblock-ID in the plugin settings
![pluginSettings](https://github.com/arcusamicus/logseq-better-zotero-plugin/assets/90210405/17f9a7c5-fc2b-48bd-b8ac-c3010bd66ee3)

Examples for further Title-Template: {{date}}-{{title}}, {% if authors[0].firstName and authors[0].lastName %}{{authors[0].firstName}} {{authors[0].lastName}}{% elif authors[0].name %}{{authors[0].name}}{% endif %}-{{title}}  → look at [Nunjucks Docs](https://mozilla.github.io/nunjucks/templating.html) for full explanation

Example for as simple Page-Template:
![pageTemplate](https://github.com/arcusamicus/logseq-better-zotero-plugin/assets/90210405/a18c169c-b8e3-4bdd-8e2e-557664ffb546)

The default Page-Template is the following:
```jinja2
{% if tags.length > 0 %}zotero-tags:: {{tags | join(", ", "tag")}}{% endif %}
{% if date %}date:: {{date}}{% endif %}
{% if ISSN %}issn:: {{ISSN}}{% endif %}
{% if issue %}issue:: {{issue}}{% endif %}
{% if DOI %}doi:: {{DOI}}{% endif %}
{% if pages %}pages:: {{pages}}{% endif %}
{% if volume %}volume:: {{volume}}{% endif %}
{% if itemType %}item-type:: {{itemType}}{% endif %}
{% if accessDate %}access-date:: {{accessDate}}{% endif %}
{% if title %}original-title:: {{title}}{% endif %}
{% if language %}language:: {{language}}{% endif %}
{% if url %}url:: {{url}}{% endif %}
{% if runningTime %}running-time:: {{runningTime}}{% endif %}
{% if shortTitle %}short-title:: {{shortTitle}}{% endif %}
{% if publicationTitle %}publication-title:: {{publicationTitle}}{% endif %}
{% if series %}series:: {{series}}{% endif %}
{% if seriesNumber %}series-number:: {{seriesNumber}}{% endif %}
{% if seriesTitle %}series-title:: {{seriesTitle}}{% endif %}
{% if blogTitle %}blog-title:: {{blogTitle}}{% endif %}
{% if creators %}authors:: {% for author in creators %}{% if author.firstName and author.lastName %}{{author.firstName}} {{author.lastName}}{% elif author.name %}{{author.name}}{% endif %} ({{author.creatorType}}){% if not loop.last %}, {% endif %}{% endfor %}{% endif %}
{% if libraryCatalog %}library-catalog:: {{libraryCatalog}}{% endif %}
{% if select %}links:: [Local library]({{select}}){% endif %}

{% if abstractNote %}Abstract{% endif %}

{% if abstractNote %}{{abstractNote | safe}}{% endif %}

{% if attachments.length > 0 %}Attachments{% endif %}

{% if attachments.length > 0 %}
{% for att in attachments %}  
[{{att.title}}]({{att.uri}}) {{'{{'}}zotero-imported-file {{att.select.split('/') | last}}, "{{att.path.split('\\') | last}}"{{'}}'}}
{% endfor %}
{% endif %}
```
Tip: copy this default Page-Template to a jinja2-codeblock in Logseq and simply modify it there according to your wishes

## Acknowledgements

**inspired by:** the default Zotero-integration in Logseq, [logseq-logtero-plugin](https://github.com/vyleung/logseq-logtero-plugin)
**used tools:** [svelte](https://github.com/sveltejs/svelte), [@logseq/libs](https://www.npmjs.com/package/@logseq/libs), [fuse.js](https://github.com/krisk/Fuse), [nunjucks](https://github.com/mozilla/nunjucks)
