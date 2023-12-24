# Visualization code example

Data visualization:
1. Line plot
2. Bar plot
3. Scatter plot
4. Box plot
5. Sequence of pictures (matrix)
6. Vertical bar sequence
7. Geographical visualization

Process thinking visualization
1. Flowchart
2. Model schematic

## Tips
### Matplotlib
1. Use `_` as preceeding character before labels to prevent it from showing multiple times (see Bar color demo)
2. Figsize can be set by using few following commands:
```python
plt.figure(figsize=(width, height))

fig, ax = plg.subplots(row, col, figsize=(width, height))

fig.set_figheight(height)
fig.set_figwidth(width)
```
3. Bar chart can be stacked vertically with one another. Make sure to specify the same x.
```python
# Product price components
d = [10, 5, 7]
l = ['screen', 'battery', 'others']
s = 0
w = 0.4

_, ax = plt.subplots()
for d_, l_ in zip(d, l):
    h = ax.bar('price_components', d_, w, label=l_, bottom=s)
    ax.bar_label(h, label_type='center')
    s += d_
plt.legend()
plt.show()
```

This way, bar of screen, battery, and others would be stacked with one another. 

4. Use `barh` to create a horizontal bar.
5. Pass `xerr` params to the bar function to add errors
6. Use `invert_yaxis` or `invert_xaxis` to flip the order. The scale and data orders would inverted. This would interfere with `set_xlim` or `set_ylim` functions, as they need to be adjusted based on the left/right, top/bottom manner.
7. The default `bar_label` positioning is `edge`. You can set to `center` by passing `label_type` param duing `bar_label` function call.
8. Instead of calling the `set_title`, `set_ylabel`, `set_xlabel` etc one-by one, we can call `set` function and passing `title`, `ylabel`, `xlabel`, `ylim`, etc in a single function call.
9. Use `fmt` param in function call (especially for label-like things) to format the result. `{:.0f}` to set decimal value. `:` to state current value, `f` to state that we formatting the float/decimal digits. `.0`, dot followed by any whole number.

> Read more about numbers classification in https://www.mometrix.com/academy/numbers-and-their-classifications/


|Pointer|Numbers classification|
|---|-------|
|a|Natural/Counting (1,2,3,4,5, ...): We usually count with it.|
|b|Whole Numbers (0,1,2,3, ...): Natural, including 0.|
|c|Integers (..., -3, -2, -1, 0, 1, 2, 3, ...): Positive & negative whole numbers.|
|d|Rational numbers (2/1, 0.5, 3/10, 2.957, ...): Can be expressed as the division of integers.|
|e|Irrational numbers (pi, root of 2, e): Cannot be written as a simple fraction or decimal.|
|f|Real numbers: All numbers from a to f.|
|g|Imaginary numbers: expressed as the sum of a real part and an imaginary part (i)|

10. Use `constrained` layout to avoid decorations overlap. Calliing `tight_layout` would turn off constrained option.
11. Bar chart is basically a mix & match thing that we can leverage by specifying the coordinate & length of the bar. Specify the `bottom` parameter to shift the bar upwards. Or using a shifted `x` param to simulate as if they were different, but grouped together. Pass the returned `Axes` object to the `bar_label` function to specify the label, either on the `edge` or the `center`.
12. To draw annotation with a text pointing to specific part of the chart, use `Axes.annotate`. In simple terms, we just specify the `text` and the `target coordinate`. If an arrow is needed, pass `xytext` and `textcoords`. With them we can *shift* the text to any position that we want. The gap between our new shifted text and previously target coordinate would filled with an arrow that we can specify using `arrowprops` param. Other params like `fontsize`, `horizontalalignment` and `verticalalignment` can be used to customize more.
13. Regarding confusion of subplots & figsize, I think the better explanation is, a `subplots` constructed and defined as a matrix, with $rows,columns$. In the other hand, `figsize` constructed and defined in cartesian coordinate, which using $x,y$ to move and measure within the plane.
14. Set the chart aspect ratio using `set` param.
15. We can increase the visibility of data points on the axis using `EventCollection` module in `matplotlib.collections`. This way, we can add visible vertical/horizontal bar (based on specified orientation), just like 'bleed cutting points' in printing industry.
16. The `eventplot` chart is a unique one. I still thinking the possible use cases for this particular chart. I think, scatter plot `.plot()` can achieve the same thing (more versatile). The only exception is, this chart-type can be used to simplify recursion and provide a cleaner code.
17. To fill a polygon, just use `.fill()` while passing x and y points. Further costumization like `facecolor`, `edgecolor`, and `linewidth` can be used. Any polygon can be filled-up. Workaround over the open-boundary, using the first & last points to connect and create a closed shape.
18. `fill_betweenx` can be used to invert the fill area of `fill_between`. The params are identical, with a flip on x and y.

## Module notes
1. Discrete distribution as horizontal bar chart.
Utilize `barh` along with `left` param to stack one another.

The question: 
- How to make sure they are drawn in absolute value?
- How to draw a different data label if the one used for drawing are different with the actual data? (this one arise because of the absolute nature of the drawing)

2. Costumizing dashed line styles
Instead of using predefined styles using `ls` param, we can create our own line style.

**$1^st$ option:** Get return handler after plotting with `b = ax.plot()`, then format them with function `b.set_dashes()`. Pass a list with even length. It will be interpreted as line/break/line/break/etc. sequence.

**$2^nd$ option:** Using `dashes` param during `.plot()` function call. Pass a similar iterable just like on the 1st option.

`dash_capstyle` and `gapcolor` are the other option that we can use to further costumize the line style.

3. Lines with a ticked patheffect
Add tick along the line. Use `path_effects` param, and pass `patheffects,withTickedStroke()` inside a iterable.

4. Linestyles
Similar to `dashes`, `linestyle` can achieve the same thing. The only difference is, linestyle provide an additional param, an offset. `(offset, (on, off, ..., ...))` instead of just an on/off sequence.

5. Marker reference
Add additional visibility to data points using various symbols. Four major categories: unfilled, filled, TeX, Paths.

6. Markevery Demo
Pass a valid value to `markevery` param during `.plot()` function call.
Refer to https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D.set_markevery for complete documentation.
In simple words, you can costumize the marker by any means: every-n, start, stop, shift, specific points, T/F values, fractional spacing



