# SASS FONT STACKER

This Sass micro-library provides a simple way to work with a pre-defined set of presumably web-safe font stacks. Two functions and a single mixin provide a bit of syntactic sugar to make it easier to prepend any of the existing fonts stacks with an arbitrary number of fonts.

What this library *won't* do is output an `@import` declaration for web fonts. For that you'll want to turn to something like [Sass Web Fonts](https://github.com/penman/Sass-Web-Fonts) but be warned: [CSS imports are an anti-pattern](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/), good for the developer and bad for performance.

[Read the announcement on my blog](http://synapticism.com/a-sass-micro-library-for-web-safe-font-stacks/).



## Installation

Download/clone this repo or install with Bower: `bower install sass-font-stacker -D`. This project has no dependencies. Requirements: Sass 3.3+.



## Usage

This library defines a mixin and a utility function that accept an arbitrary list of fonts. The last items in the list (or the only item, as the case may be) *must* be the name of one of the font stacks included in the `$k-font-stacks` map variable (browse source for a full list).

```scss
@mixin k-font-family($fonts...)
@function k-font-stack($fonts...)
```

An example with two leading fonts:

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

Note that the only *required* argument is the *last* argument which should be one of the pre-defined font stacks. This way you can prepend an arbitrary number of web fonts using syntax that doesn't stray too far from what you'd be doing otherwise. If something goes horribly wrong there is a backup defined by `$k-font-stack-default` which is currently set to `courier` (so it'll be readily apparent that you've requested a stack that could not be found).

The second utility function returns a font stack without the generic term (e.g. `sans-serif`, `monospace`, etc.) at the end. The purpose of this is to allow for font stacks to be welded together as needed (with an eye toward international font sets). For instance:

```scss
body {
  font-family: k-font-stack("Noto Sans", k-font-stack-trim(helvetica), k-font-stack-trim(zh-sans), sans-serif);
}
```

This will return a declaration that includes Chinese fonts at the end.



## Font stacks

The font stacks themselves result from a combination of research, experience, guesswork, and idle whim. I don't pretend to be an expert in these matters but then again, who is? Most of the articles written about web-safe font stacks are five years old and usage data is lousy and poorly sourced. I have at least gone to the trouble of sprinkling most font stacks with a few free and open source alternatives so as to not ignore Linux users the way some designers do.

At any rate, you aren't locked into using what I have compiled here. Want to define your own font stacks on a per-project basis? Add to the `$k-font-stacks` global:

```scss
$k-font-stacks: map-merge($k-font-stacks, (
  helvetica-only: (Helvetica, sans-serif)
));
```

Sane pull requests are also welcome!



## Credits

Many of these font stacks are modifications of font stacks I've collected over the years. Many of my sources are no longer online. Among those that are: [this post by Michael Tuck](http://www.sitepoint.com/eight-definitive-font-stacks/), [this post on A Way Back](http://www.awayback.com/revised-font-stack/), [this post on Mighty Meta](http://www.mightymeta.co.uk/web-safe-fonts-cheat-sheet-v-3-with-font-face-fonts-and-os-breakdown/), some tips about Futura and Century Gothic on [Intavent](http://intavant.com/), a cursory inspection of [Dan's Tools](http://www.cssfontstack.com/), and [the Wayback Machine](https://webcache.googleusercontent.com/search?q=cache:http://www.visibone.com/font/FontResults.html&gws_rd=cr&ei=CazNVMvABsT38QWgjYD4CQ).



## License

MIT/GPLv3.
