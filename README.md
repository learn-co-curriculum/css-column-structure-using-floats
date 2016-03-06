# CSS Floating Columns

## Overview

In this lesson we will discuss creating column structure using floats. We will explore the CSS float property, clear property, and layout techniques for creating columns and centering elements using margins. 

## Objectives

1. How to float elements.
2. Float behavior.
3. Troubleshooting float issues.
4. A pattern for creating column structure using floats.
5. Centering our layout with a wrapper (container).

## Building With Floats

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

See the code example on floating provided in the resource links at the bottom of this lesson.

### Clear

As mentioned previously whenever we float an element, elements located below that element will pull up next to it. This is often desirable behavior. For example if we float an image to the left and then the paragraph below it will pull up next to it.

#### HTML

```html
<img src="myimage.jpg" alt="my image">
<p>Lore ipsum...</p>
```

#### CSS

```css
img {
    float: left;
}
```

In this case the paragraph wrapping up around the image may be exactly what we were after. However in some cases an element may pull up next to a floating element when we do not wish this to be the case. For example lets say we had a footer below the paragraph and although we are happy with the paragraph wrapping up around our image, we do not want the footer to go up there. Instead we wish the footer to maintain its position down below. We can use the `clear` property to set the footer to stay below the height of anything floating above it.

#### HTML

```html
<img src="myimage.jpg" alt="my image">
<p>Lore ipsum...</p>
<footer>...</footer>
```

#### CSS

```css
img {
    float: left;
}

footer {
    clear: both;
}
```

We can set the `clear` property with the following values:

`clear: left;`

Clear left tells the element to clear past the height of anything floating to the left.

`clear: right;`

Clear right tells the element to clear past the height of anything floating to the right.

`clear: both;`

Clear both tells the element to clear past the height of anything floating to the left or the right. See the code example on clearing provided in the resource links at the bottom of this lesson.

### Clearfix

Another often unintended result of floating is that you may be surprised to see a parent element will collapse its height if all of the children inside of it are floating. Let's say for example that you had a box with wood texture and inside of it you had three floating elements. 

#### HTML

```html
<div id="wood-texture"><!-- My height is collapsed! -->
  <div class="column">
    ...
  </div>
  <div class="column">
    ...
  </div>
</div>
```

#### CSS

```css
#wood {
  background: url(wood.jpg);
}

.column {
  float: left;
}
```

You might notice that the wood texture disappears when we set all of the children elements to float. This is because floating elements do not provide their parent with a reference of their height. It is as if they are plucked from the normal document flow and although are inside their parent they seem to not register as beig there. fortunately this can be fixed by using a CSS hack that deveopers have invented. It is called a clearfix.

#### HTML

```html
<div id="wood-texture" class="clearfix">
  <div class="column">
    ...
  </div>
  <div class="column">
    ...
  </div>
</div>
```

#### CSS

```css
#wood {
  background: url(wood.jpg);
}

.column {
  float: left;
}

.clearfix:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}
```

A quick google search for CSS Clearfix returns many results. The one above is one such recipe. What's all that about though? Well, let's discuss what is happening here line by line.

On line one of the HTML we added a class of clearfix to the collapsing parent element. Then in the CSS on line 9, we create the selector for that class `clearfix:after`. The `:after` part takes us to after all the children `.column` inside of `#wood`. Then after all these children it will create some `content:` on line 10. Here we insert the text content `"."` after all the column children. Weird huh? Keep with me it will strat to make more sense as we go further. On line 11 we tell that content to `display: block` which allows it to take up all the horizontal space, then on line 12 we tell it to `clear: both` allowing the content to clear past the heihght of all the floating columns above it. This is what gives the parent `#wood` a reference for how tall to be. Great, but we do not want to see a little `.` period symbol below all our floating columns. So we set it to `visibility: hidden` on line 13, and then `height: 0` and `line-height: 0` on lines 14 and 15.

When all is said and done we can now apply this class of `clearfix` to any element that is collapsing do to having floating children within it. See the code example on clearfixes provided in the resource links at the bottom of this lesson.

### Column Structure

There are many recipes for creating column structure, but we will focus on creating a liquid column structure using percents and utilizing floats. 

#### Centering

We start out by creating a wrapper class that will wrap all elements in our layout and center them.

```html
<div class="wrapper">
  ...
</div>
```

Then next we can tell that wrapper to have a fixed width, and to center using margin on each side.

```css
.wrapper {
  width: 960px;
  margin: 0 auto;
}
```

To center, we are setting the wrapper to `margin: 0 auto;`. The first number sets zero pixels for the top and bottom of the wrapper and auto (automatic) ammount for the left and right sides of the element. By giving the element automatic amount of space on the left and right it will center the wrapper within the body. Note that in order to see the auto margin the element must have a set width.

#### Rows

Next we will cerate an element that will act as a row always stacking vertically and separating the space of one row to another. Since the columns within our rows will be floating we want to tell the rows to always clear past each other to maintain their row like behavior.

```html
<div class="wrapper">
  <div class="row">
    ...
  </div>
  <div class="row">
    ...
  </div>
</div>
```

Here we created two rows by giving each div a class of `row`. Next in the CSS we need to tell rows to clear each other and prevent them from collapsing their height using our clearfix code.

```css
.wrapper {
  width: 960px;
  margin: 0 auto;
}

.row {
  clear: both;
}

.row:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}
```

Here on line 7 we set rows to `clear:both` so  they will display vertically regardless of any floating elements above them. On line 10 we use our clearfix hack to prevent rows themself from collapsing their height regardless of having floating children inside them.

#### Columns

Now we are ready to insert our columns into each row. Let's say that we wish to have three columns in the first row and two columns in the bottom row, one that takes up two-thirds the space and the other taking up one-third.

```html
<div class="wrapper">
  <div class="row">
    <div class="col-4">...</div>
    <div class="col-4">...</div>
    <div class="col-4">...</div>
  </div>
  <div class="row">
    <div class="col-8">...</div>
    <div class="col-4">...</div>
  </div>
</div>
```

I used the name `col-4` to indicate columns that take up one-third of our grid, and `col-8` for columns taking up two-thirds of our grid. There are many different grid recipes online you can use, this one follows the convention of giving our grid 12 units. Thus one-third of our twelve units is four, hence the name `col-4` and two-thirds of our twelve units is eight, hence the name `col-8`. Its less important what we name our column classes though and most important how they are sized, any margin, and floating.

Let's set their CSS to float, we will give them (2%) two percent margin on their left side, except the first column which will have (0) zero margin. This is again a recipe for making space btween all the columns except on the beginning and ending of each row. 

```css
.wrapper {
  width: 960px;
  margin: 0 auto;
}

.row {
  clear: both;
}

.row:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}

[class*="col-"] {
  float: left;
  margin-left: 2%;
}

[class*="col-"]:first-child {
  margin-left: 0;
}
```

Here on line 19, we are using an attribute selector `[class*="col-"]` this selects any elements with the letter "col-" in their class name. In our case, this applies to both our columns `col-4` and `col-8`. neat huh, we just wrote a single selector that adresses all our column classes regardless of the number on the end of the class name. We wil make use of these numbers later on... Next, we applied code to float all our columns and give them 2% margin on their left side. On line 24, `[class*="col-"]:first-child` we select only columns that happen to be the first one on the left inside their parent `.row`. We did this using the `:first-child` on the selector. Then we set these first children columns to have zero margin on their left side. What this does is create space to the left of each column except the first. Now we have spacing between each column, yet the first column is right up against the edge of our row and thus aligned with the side of the wrapper as well.

#### Math

Now we need to size the coluns so they fit side by side. remember earlier we discussed how floating elements will fit other content side by side only when there is room. IF our math is off fo rthe widths of our columns one or more may not fit and be pushed below. We will start by figuring out the width of the columns taking up one-third. To factor our math as percent, let's take the of the measure total available space within the parent row, (100%) one hundred percent. Then we will subtract the margin, with three columns there will be margin inbetween the left and center column as well as between the center and right column. At two percent margin and with two places where we have margin thats (4%) four percent total margin.

> 100 - 4 = 96

That equals (96%) ninety six percent of space left over for the width of the three columns. Now we can divide that width by the three coluns

> 96 / 3 = 32

That equals a width of (32%) thirty two percent for each of the `col-4` columns. Now we just need to calculate the width of our `col-8`. Well, let's see. first lets take (100%) of space minus (2%) margin between the col-8 and col-4. That is 98 minus the col-4 width we already know is thrirty two.

> 100 - 2 - 32 = 66

This equals (66%) sixty six percent for the width of our col-8. The important thing here is we made sure our columns plus our margins are all adding up to 100 percent. This will insure that as floating elements they will all fit side by side within our rows. Let's apply these calculated widths into our CSS,

```css
.wrapper {
  width: 960px;
  margin: 0 auto;
}

.row {
  clear: both;
}

.row:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}

[class*="col-"] {
  float: left;
  margin-left: 2%;
}

[class*="col-"]:first-child {
  margin-left: 0;
}

.col-4 { width: 32%; }
.col-8 { width: 66%; }
```

Let's say we wanted the flexibility to set a column to any size within our twelve unit grid? Then we just have to calculate the math the same as we did before by subtracking margin from 100% and dividing up the remaining soace for each column width. here are those widths assuming a two percent margin,

```css
.col-1  { width: 6.5%;  }
.col-2  { width: 15%;   }
.col-3  { width: 23.5%; }
.col-4  { width: 32%;   }
.col-5  { width: 40.5%; }
.col-6  { width: 49%;   }
.col-7  { width: 57.5%; }
.col-8  { width: 66%;   }
.col-9  { width: 74.5%; }
.col-10 { width: 83%;   }
.col-11 { width: 91.5%; }
.col-12 { width: 100%;  }
```

Pretty great! I could now link to this CSS in any web site and make use of the row, and column classes to achieve any float based column structure I wish. We have essentially created a reusable grid system.

### Adding Padding and Border to Floating Elements

What is we dared to now add some border or padding to our floating columns? Well as we discussed in a prior lesson. Different browsers use different box models. If we wish to include padding and borders within our columns without upsetting our math for their widths, we could set or `box-sizing` to `border-box`. Here is the full finished code below:

```css
* { box-sizing: border-box; }

.wrapper {
  width: 960px;
  margin: 0 auto;
}

.row {
  clear: both;
}

.row:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}

[class*="col-"] {
  float: left;
  margin-left: 2%;
}

[class*="col-"]:first-child {
  margin-left: 0;
}

.col-1  { width: 6.5%;  }
.col-2  { width: 15%;   }
.col-3  { width: 23.5%; }
.col-4  { width: 32%;   }
.col-5  { width: 40.5%; }
.col-6  { width: 49%;   }
.col-7  { width: 57.5%; }
.col-8  { width: 66%;   }
.col-9  { width: 74.5%; }
.col-10 { width: 83%;   }
.col-11 { width: 91.5%; }
.col-12 { width: 100%;  }
```

### Pre-Built Grid Systems

This last example is a simple grid system you can use, it is always good to understand floating from the ground up and be able to write your own code from scratch. It is worth mentioning here however, that there are many different prebuilt CSS grid systems that you can download and use. This does take a lot of the headache out of creating floating column structure, but still you will be glad you know how they work and how to build your own if neccesary!

## Summary

- Floating an element to the `float: left` or `float: right` will slide the element in that direction until it reaches the edge of its parent element.
- Elements located below floating elements will try to pull up next to them if there is room for them to exist. ELements that won't fit will wrap down below to the next line.
- If we do not wish an element to pull up next to a floating element we can give it the `clear: both` value.
- When we float all the children within a parent it will collapse its height. To remedy this we can use a CSS Clearfix hack.
- We can build column structure by floating elements and setting their width to fit side by side.
- There are many recipes for grid systems using floating columns. You can build your own or download, link, and use the class names used in the pre-built grid file.

## Resources

- [Presentation Slides](https://docs.google.com/presentation/d/1UTUWDczUiDZ6byuhyHv0L3zJXQjdlnZheZXhRVLOL3Q/edit?usp=sharing)
- [Simple Float Left - Code Example](http://jsfiddle.net/flatiron_school/YXBnC/3/)
- [Clearfix - Code Example](http://jsfiddle.net/flatiron_school/eQRJM)
- [Column Structure Using Floats - Code Example](http://jsfiddle.net/flatiron_school/VGue9/)
- [MDN - CSS - Float](https://developer.mozilla.org/en-US/docs/Web/CSS/float)
- [MDN - CSS - Clear](https://developer.mozilla.org/en-US/docs/Web/CSS/clear)
- [CSS Tricks - Clearfix](https://css-tricks.com/snippets/css/clear-fix/)
- [CSS - Light Grid Example](https://github.com/jongrover/css-light-grid/blob/master/css/light-grid.css)
- [Site Point - Understanding Grid Systems](http://www.sitepoint.com/understanding-css-grid-systems/)
