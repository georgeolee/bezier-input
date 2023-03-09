# bezier-input-react

A cubic Bezier component with interactive control points. When the user moves a point, the component creates a lookup table for the new curve and passes it to `props.onChange`. 

The lookup table is a standard js array of numbers representing the (approximate) height of the curve at regular intervals across the x axis of the graph. The default lookup `resolution` is 64 entries. 

![bezier-output](https://user-images.githubusercontent.com/62530485/169880265-a6972892-68af-4e2b-96ab-c6d74fdc8355.gif)


### Control Point Constraints

The graph area spans from (0, 0) in the bottom left to (1, 1) in the top right.

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
