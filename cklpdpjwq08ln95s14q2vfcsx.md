## Must-have style-lint basic rules 🎨

## What is style-lint? 👀

[style-lint](https://stylelint.io/) is a linter that helps you avoid errors and enforce conventions in your CSS syntax file or CSS-like syntaxes like SCSS, Sass, Less and SugarSS.

## Why i don't use `stylelint-config-recommended`?

[stylelint-config-recommended](https://github.com/stylelint/stylelint-config-recommended) turns on all the possible errors rules within stylelint, includes:

- `selector-pseudo-element-no-unknown`: Disallow unknown pseudo-element selectors.
- `selector-type-no-unknown`: Disallow unknown type selectors.

This rules don't know about created `element` `type` from Angular template and you get unexpected errors.

So i decided to choose rules, one by one.

## Must-have basic rules 👇

### TL;DR

My `.stylelintrc.json`:

```json
{
  "ignorePatterns": [
    "coverage/**/*",
    "e2e/**/*",
    "media/**/*"
  ],
  "rules": {
    "indentation": 2,
    "color-hex-case": "upper",
    "color-hex-length": "long",
    "color-no-invalid-hex": true,
    "declaration-block-no-duplicate-properties": true,
    "no-duplicate-at-import-rules": true,
    "font-family-no-duplicate-names": true,
    "comment-no-empty": true,
    "string-quotes": "single",
    "value-keyword-case": "lower",
    "max-empty-lines": 1,
    "max-line-length": 80,
    "no-eol-whitespace": true,
    "property-no-unknown": true,
    "block-no-empty": true,
    "selector-pseudo-class-no-unknown": true
  }
}
```

### indentation

Because CSS file usually has one or two levels of indentation, so i chose `2` spaces.

### color-hex-case

Upper `color-hex` (`#FFFFFF`, not `#ffffff`) are easy to read, but with editor color-text visualization extensions, that is not problem.

Some developer don't want to using `shift` key too much.

### color-hex-length

Shorter is easier to coding, but i don't like to see `short` color in same column with `long` color.

### No invalid, no empty, no unknown and no duplication rules

```JSON
  {
    "color-no-invalid-hex": true,
    "declaration-block-no-duplicate-properties": true,
    "no-duplicate-at-import-rules": true,
    "font-family-no-duplicate-names": true,
    "comment-no-empty": true,
    "no-eol-whitespace": true,
    "property-no-unknown": true,
    "block-no-empty": true,
    "selector-pseudo-class-no-unknown": true,
    "value-keyword-case": "lower"
  }
```

### string-quotes

`single` quotes are faster because they don't require `shift` key. 😸

### max-empty-lines

I don't need more than `1` line between each class.

### max-line-length

`80` is enough for most case except `url` and `font-family`.

## Image source

Photo by [Hiren Lad from Pexels](https://www.pexels.com/photo/passports-camera-battery-charger-watches-and-cables-on-brown-wooden-surface-3031670/)
