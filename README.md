# bezier-input

A functional React component that renders a cubic bezier curve with control handles for click-and-drag editing. It passes an array of numbers, representing y coordinates along the curve, to a specified handler function. The handler function gets called after render and whenever the control points change. I've used it to animate properties like particle size and speed over time. More about that project [here](github.com/georgeolee/p-widge).

### Lookup Interpolation

Bezier curves are parametric functions, meaning both x and y values along the curve depend on an independent variable t. The exact relationship between t and x depends on the control points used to define the curve. You can see this in the red graph, where regular intervals of t yield different increments of x as the control points change.

In the context of animation, this means the length of time represented by each sample is not a uniform quantity. Attempting to use the sampled Y values without taking the varying x intervals into account results in a curve that has the same overall highs and lows as the original but appears squashed and stretched in the x axis. You can see this in the yellow graph.

To maintain the overall shape of the original curve, the component interpolates an approximate y value at regular intervals using the two nearest sample points. This allows handler functions to treat each array index as a constant unit, which is convenient — the tradeoff is some jaggedness, which you can see in the green graph.

You can adjust the fidelity of the lookup array by passing in a different resolution to the component. The example here has resolution set to 12 (the default is 64 samples).


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

### Canvas Dimensions And Styling

The bezier curve and control elements are drawn with the Canvas API. To keep most of the styling in one place, canvas drawing colors and control size, as well as the height and width attributes of the canvas, are set from custom CSS properties after the component renders. A ResizeObserver recomputes canvas size attributes and control point size if the canvas element or document root are resized.
