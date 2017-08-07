gulp-cmdcompile ![NPM version](https://img.shields.io/npm/v/gulp-cmdcompile.svg?style=flat)
====================================================================================================================================================

By Shawn Li &lt;shawn@shawnli.org&gt; 

gulp-cmdcompile is a gulp plugin designed to bring flexible file compilation with command line tools to gulp build ecosystem.


Installation
--------------
### NPM
```bash
$ npm install --save-dev gulp-cmdcompile
```
### Yarn
```bash
$ yarn add -dev gulp-cmdcompile
```

Example
-------
```js
const path = require('path');
const gulp = require('gulp');
const changed = require('gulp-changed');
const cmdcompile = require('gulp-cmdcompile');

gulp.task('build-file', function () {
    return gulp.src('*.cc', {read:false})
        .pipe(changed('build', {
            transformPath: p => path.join(path.dirname(p), path.basename(p, '.cc'))
        }))
        .pipe(cmdcompile('g++', [], {
            print_build: true, 
            filename_transform: 'stripext'
        }))
        .pipe(gulp.dest('build'));
});
```

Documentation
-------------
### cmdcompile(program [, prog_arglist] [, options])
Calling cmdcompile will return a stream object suitable to feed in pipe line of gulp construct. It accept at most three
arguments, while only the first one(program) is required.

#### program
*Type: String*  
the program name this plugin should invoke to process source files. In most cases, command line compiler program should
fit, like `g++` and `clang` or even `tc`(Typescript compiler) if you mean it.

#### prog_arglist
*Type: Array of String*  
List of arguments that would passed to compiler through command line. You can specify any optimization, compiling macros
and linked libraries here.

#### options
*Type: Object*  
Currently two options are supported.  
**print_debug** :  _true|false_  
whether output compiler tool's stdout and stderr


**filename_transform** : _none|stripext|&lt;function&gt;_  
Default to none(no transformation). Providing stripext will strip output file's extension, commonly used in C/C++ program.
You can also customize transformation rule by providing a function that accept single argument as source file name and
return target file name in any way you wish.





MIT License
----------------------------
Copyright (c) 2017 Shawn Li &lt;shawn@shawnli.org&gt;

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the &quot;Software&quot;), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED &quot;AS IS&quot;, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
