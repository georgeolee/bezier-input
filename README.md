# bezier-input-react

A cubic Bezier curve with interactive control points. It generates a lookup array of approximate y values along the curve. You can specify a handler function to call when the user changes the control points.

Here's an [example](github.com/georgeolee/p-widge) that uses it for animation curves.

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

Lookup values (green) are interpolated from an initial sample set of points on the curve (red). The sample points don't have a fixed horizontal spacing because Bezier curves are parametric. With the interpolated values, each entry is a fixed distance from the next, so it's easy to traverse the curve with just length and index like you would any other array. You can bump up the resolution to mitigate the accuracy loss if needed.


![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

*Comparison of sampled points (x and y), sampled y values, and interpolated y values*


### Constraints
All four control points have their x and y coordinates clamped to the 0 - 1 range. The start and end points are restricted to  x = 0 and x = 1, respectively. If initial control points that fall outside this range are specified, the curve will be resized to fit.

### Props

`resolution` – the length of the lookup array  (default 64)\
`onChange` – a handler function, called with lookup array as an argument when the curve changes\
`points` – the initial control points in the format [x<sub>0</sub>, y<sub>0</sub>, x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub>]\
`labelTop` `labelX` `labelY` - graph title and axis labels
