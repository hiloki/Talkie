Talkie.js - HTML/CSS/JavaScript Slide library
====================

[![Licence](http://img.shields.io/badge/license-MIT-000000.svg?style=flat-square)](https://npmjs.org/package/Talkie)
[![Version](http://img.shields.io/npm/v/Talkie.svg?style=flat-square)](https://npmjs.org/package/Talkie)

This library written in es6 JavaScript & [baconjs/bacon.js](https://github.com/baconjs/bacon.js). Also serve as a practice of es6 and functional reactive programming.

For more information about dependency Please look at the [package.json](package.json).

## Feature

- [x] Markdown support
- [x] Code highlighting
- [ ] CSS transitions
- [ ] Layout attributes (WIP)
- [x] keyboard control
- [x] touch control
- [x] Responsive scaling (4:3, 16:9)
- [x] FullScreen mode
- [x] Background image & filter
- [x] Pointer attention
- [ ] Rehearsal mode
- [ ] Presenter note
- [x] Progress indicator
- [ ] PDF download

## Getting started

Talkie.js contains one of the CSS and one of JavaScript.

- dist/talkie.min.css
- dist/talkie.min.js

Next code is the simplest sample.

```html
<html>
<head>
  <link rel="stylesheet" href="./dist/talkie.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.4/styles/monokai_sublime.min.css">
</head>
<body>

<!-- put your slides -->

<section layout>
  <h1>Slide 1</h1>
</section>

<script layout type="text/x-markdown">
# Slide 2
</script>

<script layout type="text/x-markdown">
\```javascript
function hello(str) {
  alert('Hello ' + str);
}
hello('World!')
\```
</script>

<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/8.4/highlight.min.js"></script>
<script src="./dist/talkie.js"></script>
<script>Talkie();</script>
</body>
</html>
```

If you use the code highlighting, you must load these files.

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.4/styles/monokai_sublime.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/8.4/highlight.min.js"></script>
```

### Slide ratio

The default slide 16:9 (width: 1366px, height 768px). In the following code ratio 4:3 (width 1024px, height 768px) you will.

```javascript
Talkie({wide: false});
```

### Backface image & filter

You can add `backface` attribute into each slides. Image path that you specify in the backface attribute will be the background of when the slide is displayed.

```html
<section layout
         backface="background-image.jpg"
         backface-filter="blur(1px) brightness(.8)">

  <h1>Title</h1>
  <p>foo, bar, baz, qux...</p>

</section>
```

`backface-filter` attribute is applied to the background image as [CSS Filters](http://css-tricks.com/almanac/properties/f/filter/).

### All options

```javascript
/**
 * @typedef {Object} TalkieOptions
 * @property {Boolean} [api]
 * @property {Boolean} [wide]
 * @property {Boolean} [control]
 * @property {Boolean} [pointer]
 * @property {Boolean} [progress]
 * @property {Boolean} [backface]
 */
```

### FullScreen mode

When you press the **"f"** key will be a full-screen mode. "f" or "Esc" key Press and then exit.

### Pointer mode

When you press the **"b"** key pointer appears, disappears when you release.

### Custom key binding & control

`Talkie()` returns an object with initialization. This object has some of the control bus and functionality.

```javascript
/**
 * @typedef {Object} TalkieExport
 * @param {Object.<Function>} control
 * @param {Bacon.EventStream} changed
 * @param {Bacon.Bus} next
 * @param {Bacon.Bus} prev
 * @param {Bacon.Bus} jump
 */
var talkie  = Talkie({wide:false});
```

You can define any key bindings.

```javascript
talkie.next.plug(talkie.control.key('space'));
talkie.next.plug(talkie.control.key('s'));
talkie.next.plug(talkie.control.key('n'));
talkie.prev.plug(talkie.control.key('a'));
talkie.prev.plug(talkie.control.key('p'));
```

It is also possible to control these functions in the program.

```javascript
window.next = function() {
  talkie.next.push();
};
window.prev = function() {
  talkie.prev.push();
};
window.jump = function(num) {
  talkie.jump.push(num);
};
```

## Internal API

If you want to using Talkie internal api. Like this and will get Talkie api object.

```javascript
var talkie = Talkie({api: true});
```

Look at the [index.js](src/index.js) you will see how to use the internal API. You referring to [index.js](src/index.js), can build a slide in its own UI.

## License

The MIT License (MIT)
