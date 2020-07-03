# The BarPlot class

Barplots are distributions of gene expression for a particular gene, in a particular sample, across a single cell type.
Expression data is stored in the PopAlign object as log-scaled counts of mRNA transcripts; there is one such datapoint
per individual cell per gene. Barplots are created by sorting the cells into bins based on their expression of a certain gene,
and then normalixing the cell count in each bin based on the total `ncells` in a sample.

## Initialization

Barplots can be created using the `BarPlot` class, which takes the following arguments upon initialization. Note that
all argumentes are keyword arguments, with the exception of `pop`.

* `pop` **[dict]** The PopAlign object.
* `samples` **[str, list, None]** The sample or list of samples for which plots will be created. If `None`, all samples
    will be used (see `plot._init_samples()`). If multiple samples are specified, a grid of barplots is created.
* `celltype` **[str]** The celltype for which the plot(s) will be created. One of `Myeloid`, `B-cell`, or `T-cell`
* `gene` **[str]** The gene for which the plot(s) will be created. The inputted string must be a valid gene name, 
    i.e. in the list `pop['filtered_genes']`.
* `nbins` **[int]** The number of bins into which the gene expression data will be sorted. The default number is 25.

## Usage

Barplots can be generated using the code below. Colors can be specified using a two-tuple, where the tuple
elements are strings representing valid `matplotlib` [colors](https://matplotlib.org/2.0.2/api/colors_api.html).

```python
from plotpop import barplot # Import the barplot module.

bar = barplot.BarPlot(pop, samples='ALL CYTO', celltype='T cell', gene='CD3D')
bar.plot() # The default colors are `salmon` and `turquoise`

grid = barplot.BarPlot(pop, samples=None, celltype='T cell', gene='CD3D')
grid.plot(color=('magenta', 'yellow')) 
```

The code above produces the following graphs: 

<img src="https://github.com/pipparichter/plotpop/blob/master/docs/example_barplot.png" width="300" height="300">

<img src="https://github.com/pipparichter/plotpop/blob/master/docs/example_barplot_grid.png" width="300" height="300">

After figures have been generated by `plot()` and stored in the `figure` attribute, the barplots can be saved. If 
no filenames are specified, the default filenames `barplot.png` and `barplot_grid.png` are used. Saving multiple barplots
without specifying a different filename will result in them being overwritten.

```python
bar.save(filename='example_barplot.png')
grid.save(filename='example_barplot_grid.png')
```
