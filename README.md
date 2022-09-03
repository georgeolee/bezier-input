# bezier-input-react

A cubic Bezier curve with interactive control points. It generates a lookup array of approximate y values along the curve. You can specify a handler function to be called when the curve changes.

Here's an [example](github.com/georgeolee/p-widge) that uses it for animation curves.

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Graph Values

Lookup values are interpolated at regular intervals along the x axis from a set of initial sample points. Compare the green graph (interpolation) to the red one (raw samples) to see what I'm talking about. 


![bezier_comparison_compressed](https://user-images.githubusercontent.com/62530485/169634721-63925d24-38a2-4b42-864e-a6f092776711.gif)

I'm sacrificing a little accuracy for convenience here. This way, whatever function handles the graph output can traverse the array and treat each index as a fixed unit of width. Otherwise, the handler function would have to contend with the changing horizontal distances between samples seen in the red graph. 

The yellow graph shows what happens if you don't do either and just use the sampled y values – you get a curve, but not quite the same one. 


### Constraints
All four control points have their x and y coordinates clamped to the 0 - 1 range. The start and end points are restricted to  x = 0 and x = 1, respectively. If initial control points that fall outside this range are specified, the curve will be resized to fit.

### Props

`resolution` – the number of lookup values to output; defaults to 64\
`onChange` – a function to handle the lookup array\
`points` – the initial control points in the format [x<sub>0</sub>, y<sub>0</sub>, x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub>]\
`labelTop` `labelX` `labelY` - graph title and axis labels
