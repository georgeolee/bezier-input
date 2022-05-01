# bezier-input

A cubic bezier curve with handles for click-and-drag editing. It outputs an array of numbers, representing y coordinates along the curve, that can be used to control an arbitrary value. I've used it to animate properties like particle size and speed over time. More about that project [here](github.com/georgeolee/p-widge).

### Lookup Interpolation

Because bezier curves are parametric functions, `(x,y)` points along the curve depend on an independent variable `t`. Evenly stepped values for `t` don't necessarily imply the same for `x`. This makes something like animation using the raw sample values a little tricky, because each sample represents a different step size for `x` — or a different length of time, in the context of animation.

To get around this, the component interpolates a `y` value at evenly spaced increments of `x` using the two nearest sample points. This is handy for animation because it means each element of the output array represents an equal slice of time, but it does introduce some discrepancy between the output and the "real" y values along the curve. This is mostly noticeable at  very low sample sizes when the slope of the curve changes rapidly. For a closer approximation (or a really jagged line) you can pass a different `resolution` into the component.

### Control Point Range

0 to 1

### Output Range

Output values are in the 0 - 1 range.

### props

`resolution` – the number of lookup values to output\
`func` – a function to handle the lookup array\
`points` – the initial control point coordinates ; 8 numbers or 4 (x, y) vector objects\
`labelTop` `labelX` `labelY` - graph title and axis labels

### styling

The bezier curve and control elements are drawn using the Canvas API. To keep all the styling in one place, most of the canvas color values are set from custom CSS properties after the component renders.
