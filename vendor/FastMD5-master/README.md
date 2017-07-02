FastMD5
=======

## Fast JavaScript MD5 library

The goal of this project is to create an extremely fast MD5 implementation.<br>
It's based on a [Joseph Myers's high-performance md5](http://www.myersdaily.org/joseph/javascript/md5-text.html).<br>
See latest [jsPerf MD5 comparison](http://jsperf.com/md5-shootout/63).

## Usage

Grab the [library](https://raw.githubusercontent.com/iReal/FastMD5/master/build/md5.min.js) and include it.

```html
<script src="path_to/md5.min.js"></script>
```

Then use it:

```js
var string, hash;

string = "abc";
hash = md5(string);

console.log(hash); // -> "900150983cd24fb0d6963f7d28e17f72"
```

#### Optional

`md5`(`data`, `[ascii]`, `[arrayOutput]`);

- `ascii` - set `true` if `data` consists only of ASCII chars to improve performance
- `arrayOutput` - if `true`, then the result is an array of chars (not a string)
