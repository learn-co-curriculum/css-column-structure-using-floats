# CSS Column Structure Using Floats

## Overview

In this lesson we will discuss creating column structure using floats. We will explore the CSS float property, clear property, and layout techniques for creating columns and centering elements using margins. 

## Objectives

1. How to float elements.
2. Float behavior.
3. Troubleshooting float issues.
4. A pattern for creating column structure using floats.
5. Centering our layout with a wrapper (container).

## Building With Floating Elements

<iframe width="640" height="360" src="https://www.youtube.com/embed/videoseries?list=PLj148bJp5wiywPPfLywS2m2neYodtzsER" frameborder="0" allowfullscreen></iframe>

*Note: Slides for this lecture video are provided in the resources at the bottom of this lesson.*

### The Grid

Having page layouts with content all to the left side of the screen; single column isn't very adventurous is it? It would be nice to be able to position content into a grid. Then we can organize our information, and create visual relationships between two pieces of content. We can use a grid to visually lead the viewer through our content giving order to our narrative. Although the grid doesn't solve all our problems, its helps us aid better site layouts.

> “The grid system is an aid, not a guarantee. It permits a number of possible uses and each designer can look for a solution appropriate to his personal style. But one must learn how to use the grid; it is an art that requires practice.”
> —Josef Muller-Brockmann

### Float

In CSS one recipe for creating rows and columns of a grid is to use the `float` property. Let's explore how this simple mechanic works on its own, then later we will discuss how to use it to create a simple column structure. 


Applying the float property to an element not only effects the behavior and display of that element, but also all of the elements below the floating element are also effected by it. This can be the cause for some unexpected behavior, but as long as we understand how float effects other elements around it, we can plan for and prevent unwanted reactions.

Let's look at the `float` properties accepted values.

`float: left;`

Floating an element to the `left` will cause that element to slide as far to the left within its parent as it can.

`float: right;`

Floating an element to the `right` will cause that element to slide as far to the right within its parent as it can.

If no width is set on a floating element, it will start to be as wide as the content within it, although we can force the width of a floating element by using its width property. Additonally all elements written in the code after that floating element will try to pull up next to it if there is room for them to exist.

`float: none;`

Setting float to `none` is the default behavior for all elements before the float peoperty is set. You can also use this propertly to essentially turn off floating on elements that might have already been told to float. This is a common strategy in responsive media queries which we will discuss in a future lesson.

### Clear


### Clearfix

...

### Centering

...

### Column Structure

...

## Summary

- ...

## Resources

- [Presentation Slides](https://docs.google.com/presentation/d/1UTUWDczUiDZ6byuhyHv0L3zJXQjdlnZheZXhRVLOL3Q/edit?usp=sharing)
- [Simple Float Left - Code Example](http://jsfiddle.net/flatiron_school/YXBnC/3/)
- [Column Structure Using Floats - Code Example](http://jsfiddle.net/flatiron_school/VGue9/)
- [MDN - CSS - Float](https://developer.mozilla.org/en-US/docs/Web/CSS/float)
- [MDN - CSS - Clear](https://developer.mozilla.org/en-US/docs/Web/CSS/clear)
- [CSS Tricks - Clearfix](https://css-tricks.com/snippets/css/clear-fix/)
