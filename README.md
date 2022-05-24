# bezier-input

A functional React component that renders a cubic bezier curve with control handles for click-and-drag editing. It passes an array of numbers, representing y coordinates along the curve, to a specified handler function. The handler function gets called after render and whenever the control points change. I've used it to animate properties like particle size and speed over time. More about that project [here](github.com/georgeolee/p-widge).

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

Bezier curves are parametric functions. In most cases, the points obtained by sampling an arbitrary curve P(t) at regular intervals of t **(red)** will not be evenly distributed in the x axis. 

Using the sampled y values without accounting for this uneven horizontal distribution effectively creates a new curve **(yellow)** that has the same vertical range as the original but is squashed and stretched horizontally.

To simplify output handling, this component uses the original sample points to interpolate a new array of approximate y values **(green)** at regular x intervals along the curve. This is more convenient in a lot of cases – if you want to lerp through array values over time, say – because each index can be treated as a fixed unit of equal weight, without the need to consider variations in sample width.

There are a couple tradeoffs to this approach:

#### Inaccuracy

Except for the start and end points, sample values represent approximations rather than actual points along the curve. This is probably not a huge deal in the type of situation where you'd consider using a click and drag input.

#### Information Loss

This is probably the bigger tradeoff. You can see in the green graph areas where many tightly packed points from the original sampling get flattened out into a line. You can mitigate the effects of undersampling by passing in a higher resolution to the component if needed. 

(12 samples are shown here for clarity, but the default resolution is 64.)


![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

- blue: the rendered component appearance
- red: sampled points along the curve at evenly spaced intervals of t
- yellow: sampled y values, evenly distributed along the x axis
- green: interpolated y values, to correct for x axis stretching; this is what gets passed to the handler function

### Constraints

To keep the curve from failing the [vertical line test](https://en.wikipedia.org/wiki/Vertical_line_test), control points P0 and P3 are restricted to  x = 0 and x = 1, respectively. All four control points have their x and y coordinates clamped to the 0 - 1 range. If the initial control points passed in cross outside of this range, they are normalized to fit.


### Output Range

Output values are in the 0 - 1 range.

### Props

`resolution` – the number of lookup values to output\
`func` – a function to handle the lookup array\
`points` – the initial control point coordinates ; 8 numbers or 4 (x, y) vector objects\
`labelTop` `labelX` `labelY` - graph title and axis labels

### Canvas Styling

The bezier curve and control elements are drawn with the Canvas API. To keep styling in one place, canvas drawing colors and control point size are set from custom CSS properties after the component renders. 
