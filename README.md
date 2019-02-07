# GitBook PlantUml Plugin with Cloud and Language Support

This is a plugin for Gitbook to support PlantUML diagrams inside Markdown/Asciidoc documents.
It doesn't need a local java running process. It does a call to a PlantUML server to render the graph.

Added new parameters: language, host's port and output format
* Added support for asciidoc.
* Added support for plantuml running in another server's port
* Added support for other output format (generated file extension)

Package published at [gitbook-plugin-plantuml-cloud-languages](https://www.npmjs.com/package/gitbook-plugin-plantuml-cloud-languages)

* inspired by [romanlytkin/gitbook-plantuml](https://github.com/romanlytkin/gitbook-plantuml)
* forked from [dy93/gitbook-plugin-plantuml-cloud](https://github.com/dy93/gitbook-plugin-plantuml-cloud)
* forked from [rodgalvao/gitbook-plugin-plantuml-cloud](https://github.com/rodgalvao/gitbook-plugin-plantuml-cloud)

The plugin now supports two APIs for generating PlantUML diagrams:
* [bitjourney/plantuml-service](https://github.com/bitjourney/plantuml-service)
* [PlantUML Server](http://www.plantuml.com/plantuml/)

## NPM Installation

```$ npm install gitbook-plugin-plantuml-cloud-languages```

## Gitbook Installation

* Add the plugin to your book.json

```js
{
  "plugins": ["plantuml-cloud-languages"]
}
```

* Install the plugin to you gitbook

```$ gitbook install```

* No additional steps required

## Configuration

* If you do not add a plugin configuration to your book.json, then the following defaults will be used:

| Configuration option | Description | Default |
| -------------------- | ----------- | ------- |
| umlPath | Path to a directory where the generated images for the diagrams will be cached. | "assets/images/uml" |
| type | Determines the type of the server side API | "plantuml-service" |
| host | Host for the diagramming service | "plantuml-service.herokuapp.com" |
| port | Host's port | "80" |
| protocol | https or http | "https" |
| path | URL Fragment which will be appended to the host part | "/svg/" |
| blockRegex | Regular expression to select the diagramming text blocks. | ^```uml((.*\n)+?)?```$ |
| language | Which language will be generated. Supports "asciidoc" | "markdown" |
| format | File output format. Examples: "svg" or "png". You may have to sync with the path parameter above. | "svg" |

* If want to use the PlantUML Server API the following changes need to be made to the plugin configuration in your book.json:

```js
{
  "plugins": ["plantuml-cloud-languages"],
  "pluginsConfig": {
    "plantuml-cloud-languages": {
      "protocol": "http",
      "type": "plantuml-server",
      "host": "www.plantuml.com",
      "port": "80",
      "path": "/plantuml/svg/",
      "language": "asciidoc",
      "format": "svg"
    }
  }
}
```

> The PlantUML Server API on plantuml.com expects the diagram text blocks in a special encoding. [Look here for more information.](http://plantuml.com/pte)
> To make this encoding work in this plugin it was necessary to include some code for the deflate operations. [Look here for more information.](https://github.com/johan/js-deflate)

* [x] Make the plugin work with nodejs zlib deflate implementation and remove the duplicated deflate code.
