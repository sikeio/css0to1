
你应该给绝对定位的元素标明 width


let me see how i can summarize the usage...

1. percentage is always the container's width and height
2. if using using positioning to push something outside a container, always specify a height, otherwise you'd get surprising effects.
3. it's easy if the dimensions are known before hand, but you might need to use javasript to calculate size if you want the positioned container to adjust its size to content.



{
just talk about this particular usage, and not getting into the nitty gritty of absolute positioning, like

+ "static position" when left/right/top/bottom is auto
+ how width and height are calculated

}

# blah blah blah

+ it's really about using left, right, top, bottom to calculate the size of a box INSIDE a container. Great wonkiness if underspecified.

+ illustrate wonkiness if width is not specified.

+ if the absolutely positioned element may have variable width or height, it usually requires JavaScript to calculate the positions. Especially for centering.

+ useful for vertical alignment, as long as the height is known.

i should probably find a way to illustrate the idea of using 100% and 50% of container width to shift something down entirely.

could probably illustrate with a dropdown menu-esque layout. then reader figoure the horizontal thing.

+ find a reasonable absolute position tutorial.

+ the default position is the "stataic" position, where it would be had it not been positioned at all
  http://stackoverflow.com/a/19969046

+ why can't I set height as percentage if box is relative
  + can do it if box positioning is absolute

+ ok... I need a strategy to talk about this.

I think you can make the available width arbitrarily large by using negative left (or right), and use margin to push things out...

In general things behave weirdly if width is not set. I could set the positioned element's width to 100% to simplify the examples, I guess...

