# bezier-input-react

A cubic Bezier curve with interactive control points. It generates a 1D lookup array of approximate y values along the curve. You can specify a handler function to be called when the curve changes.

Here's an [example project](github.com/georgeolee/p-widge) that uses it for interactive animation curves.

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Lookup Interpolation

Lookup values are interpolated at regular intervals along the x axis to allow easy indexing through the array. The interpolation is necessary because Bezier curves are parametric – see the GIF below for an illustration. 


![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

- *blue*: the rendered component
- *red*: initial sampling of 12 points x<sub>n</sub>y<sub>n</sub> on the curve at regular intervals of parameter t
- *yellow*: horizontal distortion that arises when stepping linearly through the array [y<sub>1</sub>, ..., y<sub>12</sub>]
- *green*: interpolating new y values to allow linear indexing through the array without losing the overall shape of the curve

### Constraints
All four control points have their x and y coordinates clamped to the 0 - 1 range. The start and end points are restricted to  x = 0 and x = 1, respectively. If initial control points that fall outside this range are specified, the curve will be resized to fit.

### Props

`resolution` – the number of lookup values to output; defaults to 64\
`onChange` – a function to handle the lookup array\
`points` – the initial control point coordinates\
`labelTop` `labelX` `labelY` - graph title and axis labels
