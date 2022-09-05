# bezier-input-react

A cubic Bezier curve with interactive control points. You can specify an `onChange` function to handle changes to the curve. The handler gets called with a lookup array of approximate y values along the curve as its sole argument.

Here's an [example](https://github.com/georgeolee/p-widge) that uses it for animation curves.

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

Lookup values (green in the GIF below) are interpolated from an initial sample set of points on the curve (red). The sample points don't have a fixed horizontal spacing because Bezier curves are parametric. With the interpolated values, on the other hand, each entry is a uniform slice of the overall curve. This makes it easy to traverse the curve with just length and index like you would a typical array. You can get a smoother and more accurate (or less, as below) approximation by passing in a <code>resolution</code> other than the default 64.


![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

*Comparison of sampled points (x and y), sampled y values, and interpolated y values – shown here at 12 resolution*


### Control Point Constraints

You can set initial control points other than the default:

| point | x | y | default |
| ----- | - | - | ------- |
| P<sub>0</sub> | 0 | 0 to 1 | (0, 0) |
| P<sub>1</sub> | 0 to 1 | 0 to 1 | (0, 1) |
| P<sub>2</sub> | 0 to 1 | 0 to 1 | (1, 0) |
| P<sub>3</sub> | 1 | 0 to 1 | (1, 1) |

All ranges are inclusive. If any coordinate falls outside the permitted range for some reason, the entire curve will be translated and/or scaled to fit. This transformation will carry over to the lookup array.

### Props

| name | type | description|
| - | - | - |
| `resolution` | number | length of the lookup array |
| `onChange` | function | handler to call on control point change; also called once after initial render |
| `points` | array | initial control points in the format [ x<sub>0</sub>, y<sub>0</sub>, x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub> ] |
| `labelTop`<br/>`labelX`<br/>`labelY` | string | graph labels |
