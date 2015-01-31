# SASS FONT STACKER

This Sass micro-library provides a simple way to work with a pre-defined set of presumably web-safe font stacks. A single function and mixin provide a bit of syntactic sugar to make it easier to prepend any of the existing fonts stacks with an arbitrary number of fonts.

What this library *won't* do is output an `@import` declaration for web fonts. For that you'll want to turn to something like [Sass Web Fonts](https://github.com/penman/Sass-Web-Fonts) but be warned: [imports are an anti-pattern](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/), good for the developer and bad for performance.



## Installation

Download/clone this repo or install with Bower: `bower install sass-font-stacker -D`.



## Usage

```scss
body {
  @include k-font-family("PT Serif", "PT Serif Pro", georgia);
}
```

This will render:

```css
body {
  font-family: "PT Serif", "PT Serif Pro", Georgia, "Palatino Linotype", Palatino, "URW Palladio L", "Book Antiqua", "Times New Roman", serif;
}
```

You can also get a little closer to the base metal:

```scss
body {
  font-family: k-font-stack(georgia);
}
```

Which will output:

```css
body {
  font-family: Georgia, "Palatino Linotype", Palatino, "URW Palladio L", "Book Antiqua", "Times New Roman", serif;
}
```

Note that the only *required* argument is the *last* argument which should be one of the pre-defined font stacks. This way you can prepend an arbitrary number of web fonts using syntax that doesn't stray too far from what you'd be doing otherwise.



## Font stacks

The font stacks themselves result from a combination of research, experience, and idle whim. I don't pretend to be an expert in these matters but nor are you locked into what I've thrown together. Want to define your own font stacks on a per-project basis? Add to the `$k-font-stacks` global:

```scss
$k-font-stacks: map-merge($k-font-stacks, (
  helvetica-only: (Helvetica, sans-serif)
));
```



## Credits

I don't know where a bunch of the font stacks I've included came from (as I've been using a few of those in my own projects for a few years already) but several originate with [this post by Michael Tuck](http://www.sitepoint.com/eight-definitive-font-stacks/) (2009), [this post on A Way Back](http://www.awayback.com/revised-font-stack/), and a cursory inspection of [Dan's Tools](http://www.cssfontstack.com/).



## License

MIT/GPLv3.
