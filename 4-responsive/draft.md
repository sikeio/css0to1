# rough outline

+ testing on device, & talk about meta tag.
+ change container to be flexible, so it's almost "responsive"
+ show where things break
+ talk about which screen dimensions to use

# stuff

+ how do you organize media queries?
  + mobile first. add properties to desktop.
  + desktop first.
  + neither. put either properties in respective media queries?

+ @media only screen and (max-width : 414px)
  + why "only screen"
  + why 414px?

+ does setting the container's max-width give us "almost responsive" design?
  + great way to illustrate the advantage of using % layout

+ is it normal to collapse styles at different screen sizes?
  + i mean, when you adjust a desktop design to make it responsive, do you continuously adjust the screen size, and fix things as it breaks?

  As you decrease the screen sizes, different components look ok, but break at a certain size (which might not be all the same)

  + component A breaks at 800px, fix it.
  + component B breaks at 700px, fix it.
  + component C breaks at 500px, fix it.
  + adjust everything else for 400px

  Would you create different media queries at different screen sizes to fix these things?

  Or would you just define screen sizes for the devices you want to support?

  + usually you would define the devices you want to support and design accordingly
    + or, flip-side: http://responsivedesign.is/articles/why-you-dont-need-device-specific-breakpoints
      content-based responsive design

  > love this article. I work at Gilt and we recently spoke about our responsive website and how we also don't build our site for a specific device. Content specific breakpoints is super interesting. We don't have content specific break points but 4 generic breakpoints (tiny, narrow, medium, and wide) and build a great experience for each one. The iphone 6+ falls into the tiny breakpoint but just barely. If the phablets get any bigger they will fall into the narrow bucket and that will be just fine with us.

  while you don't want to be generally applicable, you don't want to be too specific.

+ css properties without media_type is screen by default?

+ css properties testers

media queries from bootstrap

```css
    /*==========  Mobile First Method  ==========*/

    /* Custom, iPhone Retina */
    @media only screen and (min-width : 320px) {

    }

    /* Extra Small Devices, Phones */
    @media only screen and (min-width : 480px) {

    }

    /* Small Devices, Tablets */
    @media only screen and (min-width : 768px) {

    }

    /* Medium Devices, Desktops */
    @media only screen and (min-width : 992px) {

    }

    /* Large Devices, Wide Screens */
    @media only screen and (min-width : 1200px) {

    }
```

more detailed list for various devices:

http://responsivedesign.is/develop/browser-feature-support/media-queries-for-common-device-breakpoints

# "screen" vs "only screen" in media queries

pretty arcane

http://stackoverflow.com/questions/8549529/what-is-the-difference-between-screen-and-only-screen-in-media-queries

# IE8

does not support media query...

doesn't this make "mobile-first" a no go?

https://github.com/scottjehl/Respond

# media query

not supported in until IE9