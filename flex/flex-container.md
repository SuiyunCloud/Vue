**Flex is better than box model**

Properties for the Parent(flex container)
![](flex_pic/01-container.svg)

# display

This defines a flex container; inline or block depending on the given value. It enables a flex context for all its direct children.

```css
.container {
  display: flex; /* or inline-flex */
}
```

Note that CSS columns have no effect on a flex container.

# flex-direction

the four possible values of flex-direction being shown: top to bottom, bottom to top, right to left, and left to right
![](flex_pic/flex-direction.svg)

This establishes the main-axis, thus defining the direction flex items are placed in the flex container. Flexbox is (aside from optional wrapping) a single-direction layout concept. Think of flex items as primarily laying out either in horizontal rows or vertical columns.

```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

    row (default): left to right in ltr; right to left in rtl
    row-reverse: right to left in ltr; left to right in rtl
    column: same as row but top to bottom
    column-reverse: same as row-reverse but bottom to top

# flex-wrap
two rows of boxes, the first wrapping down onto the second
![](flex_pic/flex-wrap.svg)
By default, flex items will all try to fit onto one line. You can change that and allow the items to wrap as needed with this property.

```css
.container {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

    nowrap (default): all flex items will be on one line
    wrap: flex items will wrap onto multiple lines, from top to bottom.
    wrap-reverse: flex items will wrap onto multiple lines from bottom to top.

# flex-flow

This is a shorthand for the flex-direction and flex-wrap properties, which together define the flex container’s main and cross axes. The default value is row nowrap.

```css
.container {
flex-flow: column wrap;
}
```

# justify-content
![](flex_pic/justify-content.svg)

This defines the alignment along the main axis. It helps distribute extra free space leftover when either all the flex items on a line are inflexible, or are flexible but have reached their maximum size. It also exerts some control over the alignment of items when they overflow the line.

```css
.container {
justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe;
}
```

    flex-start (default): items are packed toward the start of the flex-direction.
    flex-end: items are packed toward the end of the flex-direction.
    start: items are packed toward the start of the writing-mode direction.
    end: items are packed toward the end of the writing-mode direction.
    left: items are packed toward left edge of the container, unless that doesn’t make sense with the flex-direction, then it behaves like start.
    right: items are packed toward right edge of the container, unless that doesn’t make sense with the flex-direction, then it behaves like start.
    center: items are centered along the line
    space-between: items are evenly distributed in the line; first item is on the start line, last item on the end line
    space-around: items are evenly distributed in the line with equal space around them. Note that visually the spaces aren’t equal, since all the items have equal space on both sides. The first item will have one unit of space against the container edge, but two units of space between the next item because that next item has its own spacing that applies.
    space-evenly: items are distributed so that the spacing between any two items (and the space to the edges) is equal.

Note that that browser support for these values is nuanced. For example, space-between never got support from some versions of Edge, and start/end/left/right aren’t in Chrome yet. MDN has detailed charts. The safest values are flex-start, flex-end, and center.

There are also two additional keywords you can pair with these values: safe and unsafe. Using safe ensures that however you do this type of positioning, you can’t push an element such that it renders off-screen (e.g. off the top) in such a way the content can’t be scrolled too (called “data loss”).

# align-items
demonstration of differnet alignment options, like all boxes stuck to the top of a flex parent, the bottom, stretched out, or along a baseline
![](flex_pic/align-items.svg)

This defines the default behavior for how flex items are laid out along the cross axis on the current line. Think of it as the justify-content version for the cross-axis (perpendicular to the main-axis).

```css
.container {
align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe;
}
```

    stretch (default): stretch to fill the container (still respect min-width/max-width)
    flex-start / start / self-start: items are placed at the start of the cross axis. The difference between these is subtle, and is about respecting the flex-direction rules or the writing-mode rules.
    flex-end / end / self-end: items are placed at the end of the cross axis. The difference again is subtle and is about respecting flex-direction rules vs. writing-mode rules.
    center: items are centered in the cross-axis
    baseline: items are aligned such as their baselines align

The safe and unsafe modifier keywords can be used in conjunction with all the rest of these keywords (although note browser support), and deal with helping you prevent aligning elements such that the content becomes inaccessible.

# align-content
examples of the align-content property where a group of items cluster at the top or bottom, or stretch out to fill the space, or have spacing.
![](flex_pic/align-content.svg)

This aligns a flex container’s lines within when there is extra space in the cross-axis, similar to how justify-content aligns individual items within the main-axis.

Note: this property has no effect when there is only one line of flex items.

```css
.container {
align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end | baseline | first baseline | last baseline + ... safe | unsafe;
}
```

    flex-start / start: items packed to the start of the container. The (more supported) flex-start honors the flex-direction while start honors the writing-mode direction.
    flex-end / end: items packed to the end of the container. The (more support) flex-end honors the flex-direction while end honors the writing-mode direction.
    center: items centered in the container
    space-between: items evenly distributed; the first line is at the start of the container while the last one is at the end
    space-around: items evenly distributed with equal space around each line
    space-evenly: items are evenly distributed with equal space around them
    stretch (default): lines stretch to take up the remaining space

The safe and unsafe modifier keywords can be used in conjunction with all the rest of these keywords (although note browser support), and deal with helping you prevent aligning elements such that the content becomes inaccessible.
