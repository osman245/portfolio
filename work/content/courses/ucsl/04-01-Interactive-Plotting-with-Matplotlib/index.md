[![Collab Link](https://miro.medium.com/proxy/1*g_x1-5iYRn-SmdVucceiWw.png)](https://colab.research.google.com/github/Mohitsharma44/ucsl17/blob/master/notebooks/04-01%20Interactive%20Plotting%20with%20Matplotlib.ipynb) 

> Click above image to access the interactive version of this notebook



## Interactive Plotting with Matplotlib
One can use Jupyter notebook as a browser-based interactive data analysis tool to combine narrative, code, graphics, and much more into a single executable document.

Plotting interactively within a notebook can be done with the `%matplotlib inline` command and then importing `pyplot` from `matplotlib`


```python
%matplotlib inline
import matplotlib.pyplot as plt
```

Before we get into learning some stuff, lets set up the `style` of our plots. Starting from Matplotlib v1.5, you have many different plotting `styles` to chose from. To get all the list of supported ones, run


```python
plt.style.available
```




    ['seaborn-dark',
     'seaborn-darkgrid',
     'seaborn-ticks',
     'fivethirtyeight',
     'seaborn-whitegrid',
     'classic',
     '_classic_test',
     'fast',
     'seaborn-talk',
     'seaborn-dark-palette',
     'seaborn-bright',
     'seaborn-pastel',
     'grayscale',
     'seaborn-notebook',
     'ggplot',
     'seaborn-colorblind',
     'seaborn-muted',
     'seaborn',
     'Solarize_Light2',
     'seaborn-paper',
     'bmh',
     'tableau-colorblind10',
     'seaborn-white',
     'dark_background',
     'seaborn-poster',
     'seaborn-deep']



Personally, I prefer using `seaborn-darkgrid` but you are free to chose from whatever you like


```python
plt.style.use('seaborn-darkgrid')
```

## 04 - 02 pyplot
The pyplot module is where everything in matplotlib comes together. It is the launching point for 

- preparing your figures, 
- making plots, and 
- doing any modifications and decorations you want. 

It all comes together here. Let us take a look at those three catagories of pyplot functions.

### Plotting Preparation

Function          | Description                                                                                
:-----------------|:----------------------------------------------------------
`autoscale`       | Autoscale the axis view to the data (toggle).
`axes`            | Add an axes to the figure.                                                                 
`axis`            | Convenience method to get or set axis properties.
`cla`             | Clear the current axes.                                                                    
`clf`             | Clear the current figure.                                                                  
`clim`            | Set the color limits of the current image.                                                 
`delaxes`         | Remove an axes from the current figure.                                                    
`locator_params`  | Control behavior of tick locators.                                                         
`margins`         | Set or retrieve autoscaling margins.
`figure`          | Creates a new figure.                                                                      
`gca`             | Return the current axis instance.                                                          
`gcf`             | Return a reference to the current figure.                                                  
`gci`             | Get the current colorable artist.                                                          
`hold`            | Set the hold state.                                                                        
`ioff`            | Turn interactive mode off.                                                                 
`ion`             | Turn interactive mode on.                                                                  
`ishold`          | Return the hold status of the current axes.                                                
`isinteractive`   | Return status of interactive mode.                                                         
`rc`              | Set the current rc params.                                                                 
`rc_context`      | Return a context manager for managing rc settings.                                         
`rcdefaults`      | Restore the default rc params.                                                             
`savefig`         | Save the current figure.                                                                   
`sca`             | Set the current Axes instance.                                                     
`sci`             | Set the current image.                                                                     
`set_cmap`        | Set the default colormap
`setp`            | Set a property on an artist object
`show`            | Display a figure
`subplot`         | Return a subplot axes positioned by the given grid definition.                             
`subplot2grid`    | Create a subplot in a grid.                                                                
`subplot_tool`    | Launch a subplot tool window for a figure.                                                 
`subplots`        | Create a figure with a set of subplots already made.                                       
`subplots_adjust` | Tune the subplot layout.                                                                   
`switch_backend`  | Switch the default backend.                                                                
`tick_params`     | Change the appearance of ticks and tick labels.                                            
`ticklabel_format`| Change the ScalarFormatter used by default for linear axes.           
`tight_layout`    | Automatically adjust subplot parameters to give specified padding.                         
`xkcd`            | Turns on [XKCD](http://xkcd.com/) sketch-style drawing mode.                             
`xlabel`          | Set the *x* axis label of the current axis.                                                
`xlim`            | Get or set the *x* limits of the current axes.                                             
`xscale`          | Set the scaling of the *x*-axis.                                                           
`xticks`          | Get or set the *x*-limits of the current tick locations and labels.                        
`ylabel`          | Set the *y* axis label of the current axis.                                                
`ylim`            | Get or set the *y*-limits of the current axes.                                             
`yscale`          | Set the scaling of the *y*-axis.                                                           
`yticks`          | Get or set the *y*-limits of the current tick locations and labels.                        

## Plotting Functions

Function          | Description
:-----------------|:--------------------------------------------
`acorr`           | Plot the autocorrelation of *x*
`bar`             | Make a bar plot
`barbs`           | Plot a 2-D field of barbs
`barh`            | Make a horizontal bar plot
`boxplot`         | Make a box and whisker plot
`broken_barh`     | Plot horizontal bars
`cohere`          | Plot the coherence between *x* and *y*
`contour`         | Plot contours
`contourf`        | Plot filled contours
`csd`             | Plot cross-spectral density
`errorbar`        | Plot an errorbar graph
`eventplot`       | Plot identical parallel lines at specific positions
`fill`            | Plot filled polygons
`fill_between`    | Make filled polygons between two curves
`fill_betweenx`   | Make filled polygons between two horizontal curves
`hexbin`          | Make a hexagonal binning plot
`hist`            | Plot a histogram
`hist2d`          | Make a 2D histogram plot
`imshow`          | Display an image on the axes
`loglog`          | Make a plot with log scaling on both the *x* and *y* axis
`matshow`         | Display an array as a matrix in a new figure window
`pcolor`          | Create a pseudocolor plot of a 2-D array
`pcolormesh`      | Plot a quadrilateral mesh
`pie`             | Plot a pie chart
`plot`            | Plot lines and/or markers
`plot_date`       | Plot with data with dates
`polar`           | Make a polar plot
`psd`             | Plot the power spectral density
`quiver`          | Plot a 2-D field of arrows
`scatter`         | Make a scatter plot of x vs y
`semilogx`        | Make a plot with log scaling on the *x* axis 
`semilogy`        | Make a plot with log scaling on the *y* axis
`specgram`        | Plot a spectrogram
`spy`             | Plot the sparsity pattern on a 2-D array
`stackplot`       | Draws a stacked area plot
`stem`            | Create a stem plot
`step`            | Make a step plot
`streamplot`      | Draws streamlines of a vector flow
`tricontour`      | Draw contours on an unstructured triangular grid
`tricontourf`     | Draw filled contours on an unstructured triangular grid
`tripcolor`       | Create a pseudocolor plot of an unstructured triangular grid
`triplot`         | Draw a unstructured triangular grid as lines and/or markers
`xcorr`           | Plot the cross-correlation between *x* and *y*

## Plot modifiers

Function          | Description                                                                                
:-----------------|:---------------------------------------------------------------------
`annotate`        | Create an annotation: a piece of text referring to a data point
`arrow`           | Add an arrow to the axes
`axhline`         | Add a horizontal line across the axis
`axhspan`         | Add a horizontal span (rectangle) across the axis
`axvline`         | Add a vertical line across the axes
`axvspan`         | Add a vertical span (rectangle) across the axes
`box`             | Turn the axes box on or off
`clabel`          | Label a contour plot
`colorbar`        | Add a colorbar to a plot
`grid`            | Turn the axes grids on or off
`hlines`          | Plot horizontal lines
`legend`          | Place a legend on the current axes
`minorticks_off`  | Remove minor ticks from the current plot
`minorticks_on`   | Display minor ticks on the current plot
`quiverkey`       | Add a key to a quiver plot
`rgrids`          | Get or set the radial gridlines on a polar plot
`suptitle`        | Add a centered title to the figure
`table`           | Add a table to the current axes
`text`            | Add text to the axes
`title`           | Set a title of the current axes
`vlines`          | Plot vertical lines
`xlabel`          | Set the *x* axis label of the current axis
`ylabel`          | Set the *y* axis label of the current axis

Don't get bogged down by the enourmous list. We will look at some of them throughout the remaining UCSL coursework and slowly these options will start to *click* as you do more and more plotting.

Lets start with the very basics

### Figure
All plotting is done through the [`Figure`](http://matplotlib.org/api/figure_api.html#matplotlib.figure.Figure) object. You can create as many figures as you need. Figures can't do much by themselves, but no plotting can happen without them. They are, literally, the *canvas* of your plot.

#### Figure Properties
The figure properties include the figure size (figsize) and the resolution (dpi).

- figsize is a tuple of integers. It most often includes width and height in inches.
- dpi is resolution of the figure. It is given as an integer representing (predictably) dots per inch. 

So to create an empty figure of size 10,4, we would type: 


```python
fig = plt.figure(figsize=(10, 4))
# Now plot
plt.plot()
```




    []




    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_8_1.png)
    


This lets you create a figure with specified aspect ratio. If arg is a number, use tIn the above code, it’s the line plt.plot() that actually generates the figure. 

A really useful function is [`figaspect`](http://matplotlib.org/api/figure_api.html?highlight=figaspect#matplotlib.figure.figaspect)

Figaspect lets you create a figure with specified aspect ratio. If arg is a number, use that aspect ratio. If arg is an array, figaspect will determine the width and height for a figure that would fit the array while preserving aspect ratio.

Use it to create a plot that is twice as wide as it is high by adding the “plt.figaspect” line below: hat aspect ratio. If arg is an array, figaspect will determine the width and height for a figure that would fit array preserving aspect ratio.


```python
# Twice as wide. Ratio of Height/ Width
fig = plt.figure(figsize=plt.figaspect(0.5))
plt.plot()
```




    []




    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_10_1.png)
    


If we want to save the plot, we can call the method `plt.savefig(<filename>)`. The default format in which the image is saved is `png`. There are many other formats supported. To get a list of all the formats, you can use this function: 


```python
fig.canvas.get_supported_filetypes()
```




    {'ps': 'Postscript',
     'eps': 'Encapsulated Postscript',
     'pdf': 'Portable Document Format',
     'pgf': 'PGF code for LaTeX',
     'png': 'Portable Network Graphics',
     'raw': 'Raw RGBA bitmap',
     'rgba': 'Raw RGBA bitmap',
     'svg': 'Scalable Vector Graphics',
     'svgz': 'Scalable Vector Graphics'}



### Axes
Notice that in the previous plot, Matplotlib automatically created the axis for us. Since all plotting is done with respect to an Axes, we can use Matplotlib to change the axes.

An Axes is made up of Axis objects (and many other things). An Axes object must belong to a particular Figure (and only one Figure). Most commands you will ever issue will be with respect to this Axes object.

For example, let’s manually add an axis for X: 


```python
# Lets manually add axis for x axis
import numpy as np
fig = plt.figure()
ax = fig.add_subplot(111) 
theta = np.linspace(-np.pi, np.pi, 100)
plt.plot(theta, np.sin(theta))
```




    [<matplotlib.lines.Line2D at 0x107689390>]




    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_14_1.png)
    


Here’s how to create a subplot: 

In the line above: ax = fig.add_subplot(111)

In this case, Fig.add_subplot. This function accepts numrows numcols fignum as parameters. You already know what rows and columns are. Fignum represents the subplot number and ranges from 1 to the maximum number of rows and columns (numrows*numcols).

If you want to place an axes manually, i.e., not on a rectangular grid, use the axes() command, which allows you to specify the location as axes([left, bottom, width, height]) where all values are in fractional (0 to 1) coordinates.

Each figure can contain as many axes and subplots as your heart desires

### Linestyles
Line styles are about as commonly used as colors. There are a few predefined linestyles available to use. Note that there are some advanced techniques to specify some custom line styles. Below you’ll see an example of a custom dash pattern. You can click [`here`](http://matplotlib.org/1.3.0/examples/lines_bars_and_markers/line_demo_dash_control.html) to see the code. 

linestyle          | description
-------------------|------------------------------
'-'                | solid
'--'               | dashed
'-.'               | dashdot
':'                | dotted
'None'             | draw nothing
' '                | draw nothing
''                 | draw nothing

To generate a "dashdot" linestyle, add the proper command to your plt line:


```python
fig = plt.figure()
ax = fig.add_subplot(111) 
theta = np.linspace(-np.pi, np.pi, 100)
# combining `-` and `.`
plt.plot(theta, np.sin(theta), ls='-.')
```




    [<matplotlib.lines.Line2D at 0x1076f0f60>]




    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_17_1.png)
    


### Limits and autoscaling
By default, matplotlib will attempt to determine limits for you that encompasses all the data you have plotted. This is the autoscale feature.

Continuing with the above example, now let’s set limits on the x-axis:



```python
fig = plt.figure()
ax = fig.add_subplot(111) 
theta = np.linspace(-np.pi, np.pi, 100)
plt.plot(theta, np.sin(theta))
# Set limits on X-axis
ax.set_xlim(-np.pi, np.pi/2)
```




    (-3.141592653589793, 1.5707963267948966)




    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_19_1.png)
    


As you’ll likely have noticed, the limit caused the plot to be truncated at value of x=np.pi/2 which is at x position of ~ 1.57

### Labels and Legends
You can label just about anything in mpl. You can provide a label to your plot, which allows your legend to automatically build itself. A legend is like the legend on a map: a key to the symbols and colors the visualization is using to communicate. The X and Y axis can also be labeled, as well as the subplot itself via the title.

In the example below, we take the temperature “string” obtained from the [nasa.gov](https://data.giss.nasa.gov/gistemp/) for the years 1880 - 2018. We then load the temperature string as a numpy array using numpy’s fromstring method and create another array for the years between 1880 and 2018. 


```python
# Temperature data obtained from NASA: https://data.giss.nasa.gov/gistemp/
surface_temp_change = '-0.29,-0.1,0.11,-0.33,-0.18,-0.64,-0.42,-0.65,-0.42,-0.2,-0.47,-0.46,-0.25,-0.68,-0.55,-0.43,-0.22,-0.22,-0.06,-0.17,-0.39,-0.28,-0.18,-0.27,-0.63,-0.38,-0.3,-0.43,-0.45,-0.69,-0.43,-0.62,-0.26,-0.42,0.02,-0.18,-0.17,-0.46,-0.42,-0.2,-0.14,-0.03,-0.33,-0.25,-0.23,-0.32,0.21,-0.28,-0.02,-0.47,-0.29,-0.1,0.14,-0.34,-0.26,-0.36,-0.28,-0.1,0.0,-0.12,-0.15,0.13,0.26,0.0,0.41,0.13,0.15,-0.13,0.05,0.09,-0.3,-0.35,0.16,0.09,-0.28,0.11,-0.16,-0.14,0.39,0.06,-0.01,0.07,0.08,-0.03,-0.06,-0.09,-0.16,-0.06,-0.23,-0.11,0.09,-0.03,-0.24,0.28,-0.15,0.07,0.0,0.18,0.08,0.14,0.3,0.56,0.09,0.52,0.3,0.21,0.29,0.36,0.56,0.15,0.4,0.42,0.45,0.37,0.3,0.5,0.27,0.32,0.61,0.48,0.26,0.44,0.75,0.73,0.59,0.71,0.58,0.96,0.25,0.62,0.73,0.51,0.46,0.68,0.73,0.82,1.13,0.9'
surface_temp_change_arr = np.fromstring(surface_temp_change, sep=",")
surface_temp_year = np.array(range(1880, 2018))
```

Next, we plot the temperature array and pass the label for the temperature plot as “Global Surface Temp Change”


```python
fig = plt.figure(figsize=plt.figaspect(0.5))
ax = fig.add_subplot(111)
ax.plot(surface_temp_year, surface_temp_change_arr, label='Global Surface Temp Change')
ax.set_ylabel('Temperature (deg C)')
ax.set_xlabel('Month of January')
ax.set_title("A tale of Global Warming")
ax.legend()
```




    <matplotlib.legend.Legend at 0x1079a27f0>




    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_24_1.png)
    


### "Twinning" axes
Sometimes one may want to overlay two plots on the same axes, but the scales may be entirely different. You can simply treat them as separate plots, but then twin them.

Please note: As we move forward in this unit, we’re going to shift more exclusively to commenting in the #hashtag in-code format that you will see in your CUSP courses and you will use in your own courses. It takes some getting used to, but it is critical to learn. 


```python
# CO2 data obtained from http://cdiac.ornl.gov/CO2_Emission/timeseries/global
co2_emission_str = '865.412,891.081,938.752,997.424,1008.425,1015.759,1030.427,1081.765,1199.109,1199.109,1305.452,1364.124,1371.458,1356.79,1404.461,1488.802,1536.473,1613.48,1705.155,1859.169,1958.178,2024.184,2075.522,2262.539,2288.208,2431.221,2592.569,2874.928,2750.25,2878.595,3003.273,3065.612,3223.293,3457.981,3116.95,3072.946,3303.967,3501.985,3432.312,2955.602,3417.644,2944.601,3098.615,3556.99,3531.321,3575.325,3604.661,3894.354,3905.355,4198.715,3861.351,3446.98,3105.949,3274.631,3567.991,3766.009,4143.71,4433.403,4187.714,4371.064,4763.433,4891.778,4921.114,5100.797,5071.461,4253.72,4539.746,5104.464,5386.823,5203.473,5977.21,6479.589,6582.265,6750.947,6838.955,7488.014,7983.059,8324.09,8544.11,8998.818,9420.523,9460.86,9849.562,10388.611,10982.665,11477.71,12057.096,12442.131,13076.522,13861.26,14862.351,15430.736,16046.792,16919.538,16952.541,16853.532,17836.288,18393.672,18606.358,19644.119,19438.767,18841.046,18679.698,18610.025,19281.086,19864.139,20472.861,20993.575,21767.312,22244.022,22354.032,22629.057,22405.37,22383.368,22764.736,23263.448,23802.497,24161.863,24095.857,24051.853,24667.909,25250.962,25470.982,27014.789,28364.245,29427.675,30461.769,31125.496,32042.246,31686.547,33505.379,34865.836,35463.557,35848.592'
co2_emissions_arr = np.fromstring(co2_emission_str, sep=",")
```


```python
fig = plt.figure(figsize=plt.figaspect(0.5))
ax = fig.add_subplot(111)
ax.plot(surface_temp_year, surface_temp_change_arr, label='Global Surface Temp Change')
# Share x axis
ax2 = ax.twinx()
ax2.plot(surface_temp_year[:-4], co2_emissions_arr, label='CO2 emission', color='orange')
ax2.set_ylabel('Million Tons of $CO_2$')
ax.set_ylabel('Temperature (deg C)')
ax.set_xlabel('Month of January')
ax.set_title("A tale of Global Warming")
ax.legend(loc="upper left")
ax2.legend(loc="lower right")
# turn off grids for CO2
ax2.grid(False, which='both')
```


    
![png](./04-01%20Interactive%20Plotting%20with%20Matplotlib_27_0.png)
    


This is a peek into how easy it is to visualize the data. In the next few sub-modules, we will look at ways of using subplots, annotating plots, plotting a histogram and more.
