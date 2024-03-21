# FreeTAKServer-User-Docs
FreeTAKServer documentation for end users

<https://freetakteam.github.io/FreeTAKServer-User-Docs/>

## Notes for documentation updates

### `awesome-pages`

The documentation uses the `awesome-pages` plugin which allows a
finer control of the document navigation. 
The official documentation for `awesome-pages` is located in the [project repo](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin).

In short, one may create a `.pages` file with in the directory hierarchy
to manipulate how the navigation structure is created. 
This file should contain the `nav:` structure for just that directory. 
If the `.pages` file does not exist 
then `mkdocs` will generate the navigation according to its internal rules.
Generally, a `.pages` should be provided and not fall to the internal rules.

This plugin won't do anything if the `mkdocs.yml` defines a `nav` or `pages` entry.

### `mike`
The documentation uses the `mike` plugin to provide support for multiple versions.
The official documentation for `mike` is located in the [project repo](https://github.com/jimporter/mike/).

Use of `mike` is not yet fully enabled.
Advice as to its proper use is appreciated.


### `section-index`
The documentation uses the `section-index` plugin which enables clickable sections leading to an index page. 
The official documentation for `section-index` is located in the [project repo](https://github.com/oprypin/mkdocs-section-index/).


### `search`
The documentation uses the `search` built in plugin which allows your users to search your documentation. 
The official documentation for `search` is located in the [project repo](https://squidfunk.github.io/mkdocs-material/plugins/search/#configuration).


### `pdf-export`
The documentation uses the `pdf-export` plugin which constructs a PDF file of the documentation. 
The official documentation for `pdf-export` is located in the [project repo](https://github.com/zhaoterryy/mkdocs-pdf-export-plugin).

This only happens if the `ENABLE_PDF_EXPORT` environment variable it true.


### `markdown-include`
The documentation uses the `markdown-include` plugin which constructs a PDF file of the documentation. 
The official documentation for `markdown-include` is located in the [project repo](https://github.com/cmacmackin/markdown-include).

This reduces errors when text is to be injected into the document.
For example, here is an excerpt from the LICENSE file.
```text
{!LICENSE!lines=1  3 8-10  2}
```


### `attr_list`
The documentation uses the `attr_list` extension which
adds a syntax to define attributes on the various HTML elements in markdown’s output. 
The official documentation for `attr_list` is located in the [project repo](https://python-markdown.github.io/extensions/attr_list/).

Some uses:

* resizing images
* associating classes with elements


### `mkdocs-mermaid2-plugin`
The documentation uses Mermaid2 to make network-deployment-diagrams.

### `mkdocs_puml`
The documentation uses PlantUML to make network-deployment-diagrams.
This tooling supports more of C4 and UML but does not work as well with the IDE and mkdocs.


