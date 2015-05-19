
# implement "education & experience"

+ choosing between float and absolute
  + float is easierdemo
+ illustrate BFC。 gurantees that things don't wrap around floated elements.
+ limit width of image to 180px (or whatever)

# photos

+ talk about box model
  + show chrome inspector's box model illustration
    + what color is what
+ change default box model to border-box (from content-box)
+ use float
+ each li 25%
+ img should be 100% to fill the li
  + if 25% is applied to img, it's 25% of the image itself.
+ use border-box to add padding: 10px

```
html {
  box-sizing: border-box;
}

/* 切换了 box-sizing 子元素也会切换 */
*, *:before, *:after {
  box-sizing: inherit;
}
```

vs

```
* {
  box-sizing: border-box;
}
```

# implement get in touch.

nothing new here. just do it on your own

# implementing form

+ center the forms
+ use absolute to offset labels to the right of the form
  + text-align + padding to move the label to align with the form
+ luin explicitly sets line-height for label and input, so they have fixed height regardless of what the global typography is.
  + talk about line-height to precisely control the form sizing
+ the `left -100%, width: 100%` technique
  + this gurantees it just touching the left edge

+ how dou you get this to work for vertical?

+ absolute suitable for dropdown menu, tooltip
  + anything that's obviously outside of document flow

+ most of the time use float or inline-block
+ if an element kinda "belogns" to the same component, you can use absolute
  + badge decoration
  + tooltip
  + dropdown menu


