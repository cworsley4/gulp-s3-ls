# gulp-s3-ls [![NPM version][npm-image]][npm-url]

> s3 plugin for [gulp](https://github.com/wearefractal/gulp)

## Usage

First, install `gulp-s3-ls` as a development dependency:

```shell
npm install --save-dev gulp-s3-ls
```

Setup your aws.json file
```javascript
{
  "key": "AKIAI3Z7CUAFHG53DMJA",
  "secret": "acYxWRu5RRa6CwzQuhdXEfTpbQA+1XQJ7Z1bGTCx",
  "bucket": "dev.example.com"
}
```

Then, use it in your `gulpfile.js`:
```javascript
var gulp = require("gulp");
var s3 = require("gulp-s3-ls");
var aws = require("./aws.json");

gulp.src('./dist/**')
    .pipe(s3(aws));
```

## Flags

#### --dry

To test uploading files to s3 add the --dry flag and gulp-s3-ls will print out
the files and the corresponding upload path.

```
gulp upload --dry
```

## API

#### options.headers

Type: `Array`          
Default: `[]`

Headers to set to each file uploaded to S3

```javascript
var gulp = require("gulp");
var s3 = require("gulp-s3-ls");
var aws = require("./aws.json");
var options = { headers: {'Cache-Control': 'max-age=315360000, no-transform, public'} };

gulp.src('./dist/**', {read: false})
    .pipe(s3(aws, options));
```

#### options.gzippedOnly

Type: `Boolean`          
Default: `false`

Only upload files with .gz extension, additionally it will remove the .gz suffix on destination filename and set appropriate Content-Type and Content-Encoding headers.

```javascript
var gulp = require("gulp");
var s3 = require("gulp-s3-ls");
var aws = require("./aws.json");
var gzip = require("gulp-gzip");
var options = { gzippedOnly: true };

gulp.src('./dist/**')
.pipe(gzip())
.pipe(s3(aws, options));
```

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)

[npm-url]: https://npmjs.org/package/gulp-s3-ls
[npm-image]: https://badge.fury.io/js/gulp-s3-ls.png
