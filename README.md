# [gulp](http://gulpjs.com/)-wt

[![NPM version][npm-image]][npm-url]

[![NPM](https://nodei.co/npm/gulp-wt.png?downloads=true&stars=true)](https://nodei.co/npm/gulp-wt/)

> Compile Sass to CSS with gulp!

[npm-url]: https://www.npmjs.org/package/gulp-wt
[npm-image]: http://img.shields.io/npm/v/gulp-wt.svg
[downloads-image]: http://img.shields.io/npm/dm/gulp-wt.svg

## Requirements

`gulp-wt` has dependencies on wellington. This is provided by `wellington-bin`.

Please refer the [user guide](http://getwt.io/docs/usage/)

## Installation

Install with [npm](https://npmjs.org/package/gulp-wt)

```
$ npm install gulp-wt
```

## Usage

set your project path.

```javascript
var wt = require('gulp-wt'),
  path = require('path');

gulp.task('wt', function() {
  gulp.src('./src/*.scss')
    .pipe(wt({
      project: path.join(__dirname, 'assets'),
      css: 'css',
      sass: 'sass'
    }))
    .pipe(gulp.dest('app/assets/temp'));
});
```

set your wt settings.

```javascript
var wt = require('gulp-wt'),
  minifyCSS = require('gulp-minify-css');

gulp.task('wt', function() {
  gulp.src('./src/*.scss')
    .pipe(wt({
      css: 'app/assets/css',
      sass: 'app/assets/sass',
      image: 'app/assets/images'
    }))
    .pipe(minifyCSS())
    .pipe(gulp.dest('app/assets/temp'));
});
```

Support multiple require option

```javascript
var wt = require('gulp-wt'),
  minifyCSS = require('gulp-minify-css');

gulp.task('wt', function() {
  gulp.src('./src/*.scss')
    .pipe(wt({
      css: 'app/assets/css',
      sass: 'app/assets/sass',
      image: 'app/assets/images',
      require: ['susy', 'modular-scale']
    }))
    .pipe(minifyCSS())
    .pipe(gulp.dest('app/assets/temp'));
});
```

Support return the output of the Wt as the callback

```javascript
var wt = require('gulp-wt'),
  minifyCSS = require('gulp-minify-css');

gulp.task('wt', function() {
  gulp.src('./src/*.scss')
    .pipe(wt({
      css: 'app/assets/css',
      sass: 'app/assets/sass',
      image: 'app/assets/images'
    }))
    .on('error', function(error) {
      // Would like to catch the error here
      console.log(error);
      this.emit('end');
    })
    .pipe(minifyCSS())
    .pipe(gulp.dest('app/assets/temp'));
});
```

`gulp-wt` with [gulp-plumber](https://github.com/floatdrop/gulp-plumber)

```javascript
var wt = require('gulp-wt'),
  plumber = require('gulp-plumber'),
  minifyCSS = require('gulp-minify-css');

gulp.task('wt', function() {
  gulp.src('./src/*.scss')
    .pipe(plumber({
      errorHandler: function (error) {
        console.log(error.message);
        this.emit('end');
    }}))
    .pipe(wt({
      css: 'app/assets/css',
      sass: 'app/assets/sass',
      image: 'app/assets/images'
    }))
    .on('error', function(err) {
      // Would like to catch the error here
    })
    .pipe(minifyCSS())
    .pipe(gulp.dest('app/assets/temp'));
});
```

## Configuration

### Configuration Options

#### style

**default:** nested

**description:** The output style for the compiled css.
One of: nested, expanded, compact, or compressed.

#### comments

**default:** false

**description:** Show line comments or not.

#### relative

**default:** true

**description:** Are assets relative.

#### css

**default:** css

**description:** The target directory where you keep your css stylesheets. It is relative to the ``project`` option.

#### sass

**default:** sass

**description:** The source directory where you keep your sass stylesheets. It is relative to the ``project`` option.

#### javascript

**default:** js

**description:** The directory where you keep your javascripts. It is relative to the ``project`` option.

#### font

**default:** font

**description:** The directory where you keep your fonts. It is relative to the ``project`` option.

#### project

**default:** your project base

**description:** The location where all your assets are store.

#### logging

**default:** true

**description:** show/hide compile log message.

#### import_path

**default:** false

**format:** ``string`` or ``array``

**description:** The directory where you keep external Wt plugins or extensions that you would like to make available using the `@import` function. Common use case would be setting this to your `bower_components` directory for example. It is relative to the ``project`` option.

#### require

**default:** false

**format:** ``string`` or ``array``

**description:** Require the given Ruby library before running commands. This is used to access Wt plugins without having a project configuration file.

#### load_all

**default:** false

**description:** Load all the frameworks or extensions found in the FRAMEWORKS_DIR directory.

#### sourcemap

**default:** false

**description:** Generate standard JSON source maps.

PS. Past wt versions (prior to 1.0.0) do not support `--sourcemap` flag, please update sass and wt as the following version.

```
* sass (3.3.3)
* wt (1.0.2)
```

#### time

**default:** false

**description:** Display compilation times.

#### debug

**default:** false

**description:** Turns on sass's debuging information.

#### environment

**description:** The environment mode can also be `development` or `production`.

#### http_path

**default:** false

**description:** Set this to the root of your project when deployed.

#### generated_images_path

**default:** false

**description:** GENERATED_IMAGES_PATH. Support `--generated-images-path` parameter.

#### task

**default:** compile

**description:** Support wt primary commands: compile or watch.


## Running tests

```
$ npm i
$ npm test
```
