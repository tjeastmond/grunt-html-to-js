# grunt-html-to-js

> Converts html templates to JavaScript

** THIS IS A FORK OF A FORK!**

This is a fork of the [grunt-html-convert repo](https://github.com/soundstep/grunt-html-convert), the original grunt task converts html to angular modules. This fork convert html to vanilla javascript.

## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-html-convert --save-dev
```

One the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-html-convert');
```

## The "htmlConvert" task

### Overview

This plugin converts a group of html files to JavaScript and assembles them into an vanilla javascript.

Note that this plugin does *not* compile the templates.  It simply caches the template source code.

### Setup

```js
grunt.initConfig({
  htmlConvert: {
    options: {
      // custom options, see below
    },
    mytemplate: {
      src: ['src/**/*.tpl.html'],
      dest: 'tmp/templates.js'
    },
  },
})
```

Result:

```
var mytemplate = {};
mytemplate['tile-item.tpl.html'] = '<div data-id="{{data.id}}">\n' +
	'	{{data.title}}\n' +
	'	<img data-src="{{data.img}}" />\n' +
	'	<button data-click="remove()"></button>\n' +
	'</div>';
```

Note that you should use relative paths to specify the template URL, to
match the keys by which the template source is cached.

### Gotchas

The `dest` property must be a string.  If it is an array, Grunt will fail when attempting to write the bundle file.

### Options

#### options.base
Type: `String`
Default value: `'src'`

The prefix relative to the project directory that should be stripped from each template path to produce a module identifier for the template.  For example, a template located at `src/projects/projects.tpl.html` would be identified as just `projects/projects.tpl.html`.

#### options.target
Type: `String`
Default value: `'js'`

Language of the output file. Possible values: `'coffee'`, `'js'`.

#### options.module
Type: `String`
Default value: the task name

#### options.rename
Type: `Function`
Default value: `none`

A function that takes in the module identifier and returns the renamed module identifier to use instead for the template.  For example, a template located at `src/projects/projects.tpl.html` would be identified as `/src/projects/projects.tpl` with a rename function defined as:

```
function (moduleName) {
  return '/' + moduleName.replace('.html', '');
}
```

#### options.quoteChar
Type: `Character`
Default value: `"`

Strings are quoted with double-quotes by default.  However, for projects
that want strict single quote-only usage, you can specify:

```
options: { quoteChar: '\'' }
```

to use single quotes, or any other odd quoting character you want

#### indentString
Type: `String`
Default value: `    `

By default a tab indent is used for the generated code. However,
you can specify alternate indenting via:

```
options: { indentString: '    ' }
```

#### indentGlobal
Type: `String`
Default value: ``

By default there's global indentation. However, if all the generated code must indented,
you can specify it via:

```
options: { indentGlobal: '    ' }
```

#### fileHeaderString:
Type: `String`
Default value: ``

If specified, this string  will get written at the top of the output
Template.js file. As an example, jshint directives such as
/* global soma: false */ can be put at the head of the file.

### Usage Examples

See the `Gruntfile.js` in the project source code for various configuration examples.

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History

0.0.2 bug fix for coffee script
0.0.1 convert the angular grunt task to vanilla javascript
