## 04 - 00 Introduction to Matplotlib
Matplotlib is probably the single most used Python package for 2D-graphics. It provides both a very quick way to visualize data from Python and publication-quality figures in many formats. We are going to explore matplotlib in interactive mode (i.e. for Jupyter notebooks/ ipython environments) covering most common cases.

The matplotlib code is conceptually divided into three parts: 
- the `pylab` interface is the set of functions provided by `matplotlib.pylab` which allow the user to create plots with code quite similar to `MATLAB` figure generating code. 
- The matplotlib frontend or matplotlib API is the set of classes that do the heavy lifting, creating and managing figures, text, lines, plots and so on. This is an abstract interface that knows nothing about output. 
- The backends are device-dependent drawing devices, aka renderers, that transform the frontend representation to hardcopy or a display device.

### Gallery
I'm sure that at some point you'll say, "I want to make a plot that has X with Y in the same figure, but it needs to look like Z". Good luck getting an answer from a web search with that query. This is why the [`Gallery`](http://matplotlib.org/gallery.html "Matplotlib Gallery") is so useful. Matplotlib Gallery showcases the variety of ways one can make plots. Browse through the gallery, click on any figure that has pieces of what you want to see the code that generated it. Soon enough, you will be like a chef, mixing and matching components to produce your masterpiece!
