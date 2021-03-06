# procreate-swatch-generator
[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Test coverage][coveralls-image]][coveralls-url]

> Generate a Procreate swatches file from a list of colors


## Install

```
$ npm install --save procreate-swatch-generator
```


## Usage

```js
var procreateSwatchGenerator = require('procreate-swatch-generator');

procreateSwatchGenerator(['#000', 'rgb(128, 128, 128)'], 'Goth Drab').pipe(fs.createWriteStream('./Goth Drab.swatches'));
//=> will write ./Goth Drab.swatches
```

## CLI

```
$ npm install --global procreate-swatch-generator
```
```
$ procreate-swatch-generator --help

  Usage
    procreate-swatch-generator [...colors]

  Example
    procreate-swatch-generator '#000' 'rgb(128, 128, 128)'
    // Writes ./My Awesome Swatch.swatches

    procreate-swatch-generator '#000' 'rgb(128, 128, 128)' -f "$HOME/Dropbox/Goth Drab"
    // Writes $HOME/Dropbox/Goth Drab.swatches

    procreate-swatch-generator '#000' 'rgb(128, 128, 128)' -f 'Goth Drab' -o "$HOME/Dropbox"
    // Writes ~/Dropbox/Goth Drab.swatches

    // Also supports piping output to another process or destination
    procreate-swatch-generator '#000' 'rgb(128, 128, 128)' -f 'Goth Drab' > './Goth Drab.swatches'
    // Writes ~/Dropbox/Goth Drab.swatches

  Options
    -f, --filename Filename (without extension) of the swatch to use for the swatch. Autogenerated if not specified.
    -o, --output Path of the directory where the swatch file will be written. Default: (inferred from the filename if not passed, or the the current directory otherwise).
```


## API

### procreateSwatchGenerator(colors, [options])

`procreateSwatchGenerator` returns a PassThrough stream object that can be piped to another destination.

#### colors

*Required*
Type: `Array`

An array of valid color strings (hex, rgb(a), hsl(a), or hsv(a)). Any colors passed that use an alpha channel (such as rgba or hsla), will have the alpha channel dropped, since Procreate swatches don't consider the opacity of the colors (that can be set using the Layer Opacity tool).

Since Procreate's swatches only support up to 30 colors, any colors beyond 30 than that will be ignored (though I may add auto-splitting/creating of the swatches in a future release).

#### name

*Required*
Type: `String`

The name you wish to give to the swatch as it appears in Procreate.



## License

MIT © [Nate Cavanaugh](http://alterform.com)

[npm-image]: https://img.shields.io/npm/v/procreate-swatch-generator.svg?style=flat-square
[npm-url]: https://npmjs.org/package/procreate-swatch-generator
[travis-image]: https://img.shields.io/travis/natecavanaugh/procreate-swatch-generator/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/natecavanaugh/procreate-swatch-generator
[coveralls-image]: https://img.shields.io/coveralls/natecavanaugh/procreate-swatch-generator/master.svg?style=flat-square
[coveralls-url]: https://coveralls.io/r/natecavanaugh/procreate-swatch-generator?branch=master