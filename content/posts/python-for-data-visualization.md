+++
title = "Python for Data Visualization"
date = "2023-07-07"
description = "Guide to getting started with Python for Data Visualization"
tags = [
    "Python",
    "Data Visualization"
]
series = ["Python"]
+++

# Getting Started With Matplotlib

Matplotlib is a third-party library that you’ll need to install first. You can refer to the section Installing Third-Party Modules in the Chapter about using NumPy, which has detailed instructions on the options available to install modules. You can either use your IDE’s in-built tools or type the following in the Terminal:

`pip install matplotlib`
or

`python -m pip install matplotlib`

You’ve already installed NumPy when working on a previous Chapter that introduced this module. However, if you hadn’t already done so, installing Matplotlib will also install NumPy.

# Plotting your first figure
Later in this Chapter, you’ll read about the two interfaces you can use in Matplotlib to plot figures. For now, you’ll use the simpler option:

``` python
import matplotlib.pyplot as plt
days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
steps_walked = [8934, 14902, 3409, 25672, 12300, 2023, 6890]
plt.plot(steps_walked)
plt.show()
```

You start by importing matplotlib.pyplot and use the alias plt, which is the alias used by convention for this submodule. Matplotlib is a library that contains several submodules such as pyplot.

After defining the two lists days and steps_walked, you use two of the functions from matplotlib.pyplot. The plot() function plots a graph using the data in its argument. In this case, the data are the numbers in steps_walked.

When writing code in a script, as in the example above, plot() by itself is not sufficient to display the graph on the screen. show() tells the program that you want the plot to be displayed. When using an interactive environment such as the Console, the call to show() is not required. In the Snippets section at the end of this Chapter you can also read about Jupyter, another interactive coding environment used extensively for data exploration and presentation.

When you run the code above, the program will display a new window showing the following graph:

!["Matplotlib chart](/images/python-data-vis/chart01.png)

When you run the code above, the program will display a new window showing the following graph:

!["Matplotlib chart](/images/python-data-vis/chart02.png)

