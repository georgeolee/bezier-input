# bezier-input-react

A cubic Bezier component with interactive control points. When the user moves a point, the component creates a lookup table for the new curve and passes it to an `onChange` function. 

The lookup table is just a standard javascript array of numbers, representing the (approximate) height of the curve at regular intervals across the width of the graph. The default lookup `resolution` is 64 entries. 

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

Typical uses for a curve input involve modifying some y according to x – changing speed over time, for example, or remapping one range of colors to another. Parametric curves like Beziers, however, are defined in terms of t rather than x, which is inconvenient for that sort of thing.

To approximate something like an f(x) function, the component takes a set of curve points that are equally spaced in the t axis (red graph) and uses it to interpolate another set of points that are equally spaced in the x axis (green graph).

This lets us represent the curve with a 1D array of `resolution` y values for 0 $\le$ x $\le$ 1. Traversing the curve horizontally is easy because the change in x is a constant `1 / (resolution - 1)` from one index to the next.

It's not a perfectly accurate representation, but it gets reasonably close for a slider-type input. You can bump up `resolution` to get a more accurate approximation. The example above uses a crunchy 12 just for clarity :slightly_smiling_face:.

### Control Point Constraints

You can set initial control points other than the default ones as long as they fit the constraints below. The graph area spans from (0, 0) in the bottom left to (1, 1) in the top right. If any coordinate falls outside the permitted range for some reason, the component will try to scale/translate the curve to fit the graph area. 

Note that P<sub>0</sub> and P<sub>3</sub> are drawn differently to avoid obscuring the ends of the curve. Because of this, they won't appear to line up with P<sub>1</sub>/P<sub>2</sub> even when their coordinates are identical. The difference is visual only!

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
