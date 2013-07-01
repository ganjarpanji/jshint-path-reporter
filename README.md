# jshint-path-reporter

[![Build Status](https://secure.travis-ci.org/Bartvds/jshint-path-reporter.png?branch=master)](http://travis-ci.org/Bartvds/jshint-path-reporter) [![Dependency Status](https://gemnasium.com/Bartvds/jshint-path-reporter.png)](https://gemnasium.com/Bartvds/jshint-path-reporter) [![NPM version](https://badge.fury.io/js/jshint-path-reporter.png)](http://badge.fury.io/js/jshint-path-reporter)

> JSHint reporter that displays absolute error path with row/column on one line

A console reporter similar to the default output except the report displays absolute file paths with the row/column appended in a parsable format. 

This allows convenient use of [JSHint](http://jshint.com) from within tools that apply a filter RegExp to console views to turn error lines into clickable links to instantly navigate to the error location.

Tested and actively used in WebStorm with [grunt-contrib-jshint](https://github.com/gruntjs/grunt-contrib-jshint) (be sure to have a filter configured).

## Usage

Install from NPM
````
 $ npm install jshint-path-reporter
````

Then pass **the path to the module** as the reporter option (see the [JSHINT docs](http://jshint.com/docs)). It's a bit odd but this is how JSHINT finds the module. I'm trying to get a fix for this in JSHint.

### grunt-contrib-jshint

````js
grunt.initConfig({
	//..
	jshint: {
		options: {
			jshintrc: '.jshintrc',
			reporter: './node_modules/jshint-path-reporter'
		}),
		source: {
			//..
		}
	}
});
````
If `grunt-contrib-jshint` doesn't share `'.jshintrc'` options over multiple target then you need to get it manually and extend or default:

````js
grunt.initConfig({
	//..
	jshint: {
		options: grunt.util._.defaults({
			reporter: './node_modules/jshint-path-reporter'
		}, grunt.file.readJSON('.jshintrc')),
		source: {
			options: {
				//override jshint options
			} 
			//..
		},
		minified : {
			options: {
				//override
			} 
			//..
		}
	}
});
````
## Options

### Globally disable ANSI colouring

For low-tech displays and pure text.
````js
require('jshint-path-reporter').color(false);
````

## Example output

> WebStorm (with link filter and darcula theme):
> ![webstorm darcula](https://raw.github.com/Bartvds/jshint-path-reporter/master/media/example_output_webstorm.png)

## History

* 0.1.1 - Split display per file, inlined colors.js, fixed 'too many errors' bug
* 0.1.0 - First release

## Build

Install development dependencies in your git checkout:
````
$ npm install
````

You need the global [grunt](http://gruntjs.com) command:
````
$ npm install grunt-cli -g
````

Build and run tests:
````
$ grunt
````

See the `Gruntfile` for additional commands.

## License

Copyright (c) 2013 Bart van der Schoor

Licensed under the MIT license.

