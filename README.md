[![Build Status](https://travis-ci.org/woodyrew/metalsmith-json-to-files.svg)](https://travis-ci.org/woodyrew/metalsmith-json-to-files)

# Metalsmith json to files
Creates files from supplied JSON

A [Metalsmith](https://github.com/segmentio/metalsmith) plugin that lets you generate files from `JSON`.

## Features
- Many `JSON` files can be located in one directory for processing
- Filename is configurable and generated from `JSON` source file
- Permalink style filenames make for pretty URLs

## Installation
```bash
$ npm install metalsmith-json-to-files
```

## Usage

### Initialise plugin
```js
var json_to_files = require('metalsmith-json-to-files');

metalsmith.use(json_to_files({
    source_path: '../path/to/json_files/'
}));
```

### Use plugin
```md
---
name: My Posts
template: posts.hbs
json_files:
    source_file: posts
    filename_pattern: posts/:date-:fields.slug
    as_permalink: true
    template: post.hbs

---

Take a look...
```

Any extra metadata within the `json_files` object will be passed through to the files it generates as `data.`

The `data` object can be renamed by passing `rename_data_to` in the front matter:
```md
---
name: My Posts
template: posts.hbs
json_files:
    rename_data_to: itemData
---
```

### Passing data directly into the page

By default JSON data is wrapped in a `data` object in the page, but sometimes we want to pass it into the page unwrapped as if we'd written it in front matter (eg. it might be handy to pass `tags` for use by other plugins).

This can be achieved by using `passhrough`, an array of objects each containing:
- the key of the object we wish to pass directly (`from`)
- the name we want to use in the page (`to`)

So the following example will pass `tags` and retain the name. It will also pass `date` into the page as `publishedDate`: 
```md
---
name: My Posts
template: posts.hbs
json_files:
    passthrough:
      - from: tags
        to: tags
      - from: date
        to: publishedDate
---

## Examples
See the [metalsmith-json-to-files CLI example](https://github.com/toddmorey/metalsmith-json-to-files-example)


## License
GPL-2.0
