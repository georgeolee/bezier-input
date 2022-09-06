# bezier-input-react

A cubic Bezier component with interactive control points. It generates a lookup table for the  current curve and updates it as you move the points around.  You can set an `onChange` function to handle the lookup data. 

The lookup table is just a standard javascript array of numbers, representing the height of the curve at different points along the x axis. The entries go from left to right across the width of the graph. The default number of lookup entries is 64, but it can be set explicitly via the `resolution` prop.

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

Lookup values (green in the GIF below) are interpolated from an initial sampling of points on the curve (red). 

The sample points don't have a fixed horizontal spacing because Bezier curve equations are parametric and the control points are constantly shifting. 

The interpolated values, however, can be calculated at regular intervals along the x axis. This makes the interpolated curve easier to work with, because you can throw out one set of coordinate data and just traverse the curve horizontally by index.

There's an accuracy tradeoff here, but it is a slider-style input after all :slightly_smiling_face:. You can bump up `resolution` if your curve is looking too jagged.

![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

*Comparison of sampled points (x and y), sampled y values, and interpolated y values – shown here at 12 resolution*


### Control Point Constraints

You can set initial control points other than the default ones as long as they fit the following constraints:

| point | x | y | default |
| --- | --- | --- | --- |
| P<sub>0</sub> | 0 | 0 to 1 | (0, 0) |
| P<sub>1</sub> | 0 to 1 | 0 to 1 | (0, 1) |
| P<sub>2</sub> | 0 to 1 | 0 to 1 | (1, 0) |
| P<sub>3</sub> | 1 | 0 to 1 | (1, 1) |

The points (0, 0) and (1, 1) correspond to the bottom left and top right corners of the graph, respectively. All ranges are inclusive. If any coordinate falls outside the permitted range for some reason, the component will attempt to scale/translate the curve to fit the graph area.

### Props

| name | type | description|
| --- | --- | --- |
| `resolution` | number | length of the lookup array |
| `onChange` | function | handler to call on control point change; also called once after initial render |
| `points` | array | initial control points in the format [ x<sub>0</sub>, y<sub>0</sub>, x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub> ] |
| `labelTop`<br/>`labelX`<br/>`labelY` | string | graph labels |
