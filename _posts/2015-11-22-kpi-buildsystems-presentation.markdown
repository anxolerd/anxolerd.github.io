---
layout: post
title:  "Buildsystems presentation"
date:   2015-11-22 04:45:05
categories: dev
author: anxolerd
image: '/images/posts/kpi-buildsystems-presentation/cover.png'
---

### Why do we need buildsystems?
Imagine you are writing your own project. When it is simple or even consists of only one source file -- it is obvious for you and other how to build it. Moreover, it is usually being compiled in one command.
But what if your project consists of hundreds of source files? And what if it has a lot of dependencies that have their own dependencies and so on and so forth? Not so easy, right?

Here is were _buildsystems_ come to the rescue

### What is buildsystem?

__Buildsystem__ is a _collection of tasks_ that automate repetitive work. In other words buildsystems are software tools designed to automate the process of program compilation.

![profit.png][profit.png]{: .responsive-image}

In two words buildsystems do a lot of things that simplify the developer's life. But first developer have to setup build system before enjoying simple life :)

### Demo project

Let setup a `gulp` buildsystem for a simple web project written in javascript. Source code of this demo is available [on GitHub][demo-gh]

What is `gulp`? Gulp is a streaming build system written in javascript. The main idea is that you put your files into stream and then apply different transformations to the stream. It is somehow similar to the idea of `bash` pipes:
{% highlight bash %}
cat input | transformation_1 | transformation_2 > output
{% endhighlight %}

First of all we have to setup gulp. Gulp must be installed both _globally_ in your system and locally as _devDependency_ of your preoject.

{% highlight sh %}
root@machine npm install -g gulp
user@machine npm install --save-dev gulp
{% endhighlight %}

Then create `gulpfile.js` file in the root of your project. It is a file where all your tasks are defined. Let define there a simple task:

{% highlight js %}
var gulp = require('gulp');

gulp.task('my-first-task', [], function() {
    console.log('Hello from gulp task!');
});
{% endhighlight %}

Here ___my-first-task___ is the name of your task, empty array means that your task has no dependencies. And when you will run this task the function's body will be executed.
You can run it by typing **`gulp my-first-task`** in your console. 

Tasks can depend on other tasks. To do that just add the name of the dependency into the array paramether of dependent task. Like that:
{% highlight js %}
var gulp = require('gulp');

gulp.task('my-first-task', [], function() {
    console.log('Hello from gulp task!');
});

gulp.task('my-dependent-task', ['my-first-task'], function() {
    console.log('My dependencies have been resolved!');
    console.log('I am so happy!');
});
{% endhighlight %}

If you have some task that you run pretty often and you do not want to type its name each time you execute it, make this task default. Then you will have to type just **`gulp`** to run this task:
{% highlight js %}
var gulp = require('gulp');

gulp.task('default', [], function() {
    console.log('If you want to call me just type "gulp"');
});
{% endhighlight %}

Well, we have learnt some basics. Let do some real job. We have the following project structure:

{% highlight sh %}
user@machine tree project
├── gulpfile.js
├── package.json
└── src
    ├── 404.html
    ├── favicon.ico
    ├── img
    │   ├── mlp-computer.png
    │   ├── mlp-google.png
    │   ├── mlp-pirate.png
    │   └── mlp-study.png
    ├── index.html
    ├── js
    │   ├── hamburger.js
    │   └── sidenav.js
    ├── resources.html
    └── stylus
        ├── _base.styl
        ├── components
        ├── _content.styl
        ├── _footer.styl
        ├── _header.styl
        ├── main.styl
        ├── _mixins.styl
        ├── _palette.styl
        └── _typography.styl
{% endhighlight %}

We have our source files in the src directory. All scripts are stored in `src/js` files We do not want to load both files in our html pages, we want to create one js file which we will load. Stylesheets are written in `stylus` so we will need to preprocess them.

First we will need to install some modules for gulp:

{% highlight sh %}
user@machine npm i gulp-concat gulp-stylus gulp-uglify --save-dev
{% endhighlight %}

We will start from just copying files from one directory to another. To do that we source our input files and then apply `gulp.dest` to them:

{% highlight js %}
var gulp = require('gulp');
gulp.task('copy-file', [], function(){
    gulp.src('path/to/my/file')
    .pipe(gulp.dest('destination/path/here'))
});
{% endhighlight %}

We can source multiple files at once. To do that we can use `globs`. If you are not familiar with globs take a look [here][globs].

{% highlight js %}
var gulp = require('gulp');
gulp.task('copy-file', [], function(){
    gulp.src('my/**/*.glob')
    .pipe(gulp.dest('destination/path/here'))
});
{% endhighlight %}

In demo project we do not have a lot of javascript. However there are a lot of javascript code in big projects. In order to speed up page load time javascript is often being minified. To do that we have **`gulp-uglify`** plugin.

{% highlight js %}
var gulp = require('gulp');
var uglify = require('gulp-uglify);

gulp.task('scripts', [], function(){
    gulp.src('src/**/*.js')
    .pipe(uglify())
    .pipe(gulp.dest('build/js'))
});
{% endhighlight %}

Now we have two minified javascript files in our output directory. But as we remember we do not want to load two files. We want to have one javascript file, which includes the contents of that two. Here comes **`gulp-concat`** to the rescue!
{% highlight js %}
var gulp = require('gulp');
var uglify = require('gulp-uglify);
var concat = require('gulp-concat);

gulp.task('scripts', [], function(){
    gulp.src('src/**/*.js')
    .pipe(concat('bundle.js'))
    .pipe(uglify())
    .pipe(gulp.dest('build/js'))
});
{% endhighlight %}

During development process we often need to rebuild ou javascript as we change the source code. It is not convenient to do it manually, so maybe there is gulp plugin for that? The answer is

> Gulp can do that out of the box. Without any plugins!

Here is code we need to watch changes in our source files and rebuild project as we detect them:

{% highlight js %}

...

gulp.task('watch', ['scripts'], function(){
    gulp.watch('src/js/**/*.js', ['scripts'])
});

gulp.task('default', ['scripts', 'watch']);
{% endhighlight %}

Now it is time to build styles for our project. We use [stylus][stylus] in our demo project. Hence we need **`gulp-stylus`** plugin to build our styles:

{% highlight js %}
var stylus = require('gulp-stylus');

...

gulp.task('styles', [], function(){
    gulp.src('src/stylus/main.styl')
    .pipe(stylus())
    .pipe(gulp.dest('build/css'));
});

...

// Do not forget to add watcher
gulp.task('watch', ['scripts', 'styles'], function() {
    gulp.watch('src/stylus/**/*.styl', ['styles'])
    gulp.watch('src/js/**/*.js', ['scripts'])
});

...

gulp.task('default', ['scripts', 'styles', 'watch']);
{% endhighlight %}

### To sum up
We have followed the process of setting up gulp buildsystem. Of course there are still a lot of things to improve in our build system like stopping watch task as build fails or optimizing images... You can find some of that steps done in [demo repository][demo-gh]. Also check my [slides][slides] for cute pony pictures.
You can check out this awesome [video tutorial][youtube-tutorial] about setting up gulp.
 
![final.jpg][final.jpg]{: .responsive-image}


[profit.png]: /public/images/posts/kpi-buildsystems-presentation/profit.png
[demo-gh]: https://github.com/anxolerd/kpi-buildsystems-demo
[globs]: https://github.com/isaacs/node-glob#glob-primer
[stylus]: https://learnboost.github.io/stylus/
[slides]: http://anxolerd.github.io/kpi-slides-buildsystems
[youtube-tutorial]: https://goo.gl/7KN5gP
[final.jpg]: /public/images/posts/kpi-buildsystems-presentation/final.jpg
