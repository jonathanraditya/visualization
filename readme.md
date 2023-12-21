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

