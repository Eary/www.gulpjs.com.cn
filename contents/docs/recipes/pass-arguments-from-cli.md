# 用命令行传递arguments

```js
// npm install --save-dev gulp gulp-if gulp-uglify minimist

var gulp = require('gulp');
var gulpif = require('gulp-if');
var uglify = require('gulp-uglify');

var minimist = require('minimist');

var knownOptions = {
  string: 'env',
  default: { env: process.env.NODE_ENV || 'production' }
};

var options = minimist(process.argv.slice(2), knownOptions);

gulp.task('scripts', function() {
  return gulp.src('**/*.js')
    .pipe(gulpif(options.env === 'production', uglify())) // only minify in production
    .pipe(gulp.dest('dist'));
});
```

然后通过如下运行gulp:

```sh
$ gulp scripts --env development
```
