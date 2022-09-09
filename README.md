# bezier-input-react

A cubic Bezier component with interactive control points. When the user moves a point, the component creates a lookup table for the new curve and passes it to an `onChange` handler. 

The lookup table is just a standard javascript array of numbers, representing the height of the curve at regular intervals across the width of the graph. The default lookup `resolution` is 64 entries. 

Note that values are approximate – my original use case was controlling instance properties in a particle system, so accuracy took a backseat in favor of keeping computations simple. See details below.

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

Bezier curves are parametric, which is inconvenient for stuff like animation curves where you want x to be your independent variable. To get something a little closer to an f(x) representation, the component plugs a number of values for t into the Bezier equation and uses the resulting points to interpolate the value of y at regular x intervals. 

This lets us represent the curve with a simple 1D array of `resolution` y values for 0 $\le$ x $\le$ 1. Looking up y in terms of x is straightforward because the x increment between indices stays a constant `1 / (resolution - 1)` even as the control points change.

It's not a perfectly accurate solution, but it should work well enough for a slider-style input. You can bump up `resolution` to get a more accurate approximation. The example above uses a crunchy 12 just for clarity :slightly_smiling_face:.

### Control Point Constraints

You can set initial control points other than the default ones as long as they fit the constraints below. The graph area spans from (0, 0) in the bottom left to (1, 1) in the top right. If any coordinate falls outside the permitted range for some reason, the component will try to scale/translate the curve to fit the graph area. 

Note that P<sub>0</sub> and P<sub>3</sub> are drawn slightly differently to avoid obscuring the ends of the curve, so they won't appear to line up with P<sub>1</sub>/P<sub>2</sub> even when their coordinates are identical. This difference is visual only.

| point | x | y | default |
| --- | --- | --- | --- |
| P<sub>0</sub> | 0 | 0 to 1 | (0, 0) |
| P<sub>1</sub> | 0 to 1 | 0 to 1 | (0, 1) |
| P<sub>2</sub> | 0 to 1 | 0 to 1 | (1, 0) |
| P<sub>3</sub> | 1 | 0 to 1 | (1, 1) |

### Props

| name | type | description|
| --- | --- | --- |
| `resolution` | number | length of the lookup array |
| `onChange` | function | handler to call on control point change; also called once after initial render |
| `points` | array | initial control points in the format [ x<sub>0</sub>, y<sub>0</sub>, x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub> ] |
| `labelTop`<br/>`labelX`<br/>`labelY` | string | graph labels |
