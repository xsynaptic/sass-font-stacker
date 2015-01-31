# SASS FONT STACKER

This Sass micro-library provides a simple way to work with a pre-defined set of font stacks, web-safe and otherwise. A single function and mixin provide a bit of syntactic sugar to make it easier to prepend any of the existing fonts stacks with an arbitrary number of fonts.

What this library won't do is output an `@import` declaration for web fonts. For that you'll want to turn to something like [Sass Web Fonts](https://github.com/penman/Sass-Web-Fonts) but be warned: [imports are an anti-pattern](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/), good for the developer and bad for performance.



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

Note that the only *required* argument is the *last* argument which should be one of the pre-defined font stacks.



## Font stacks

The font stacks themselves result from a combination of research, experience, and idle whim. I don't pretend to be an expert in these matters, nor can I cite my sources any longer (I've been working with most of these stacks long enough that the original blogs I adapted them from no longer exist). Luckily you aren't locked into what I've thrown together!

Want to define your own font stacks on a per-project basis? Add to the `$k-font-stacks` global:

```scss
$k-font-stacks: map-merge($k-font-stacks, (
  helvetica-only: (Helvetica, sans-serif)
));
```



## License

MIT/GPLv3.
