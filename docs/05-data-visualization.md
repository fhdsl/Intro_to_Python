

# Data Visualization

In our final to last week together, we learn about how to visualize our data.

There are several different data visualization modules in Python:

-   [matplotlib](https://matplotlib.org/) is a general purpose plotting module that is commonly used.

-   [seaborn](https://seaborn.pydata.org/) is a plotting module built on top of matplotlib focused on data science and statistical visualization. We will focus on this module for this course.

-   [plotnine](https://plotnine.org/) is a plotting module based on the grammar of graphics organization of making plots. This is very similar to the R package "ggplot".

To get started, we will consider these most simple and common plots:

Distributions (one variable)

-   Histograms

Relational (between 2 continuous variables)

-   Scatterplots

-   Line plots

Categorical (between 1 categorical and 1 continuous variable)

-   Bar plots

-   Violin plots

[![Image source: Seaborn's overview of plotting functions](https://seaborn.pydata.org/_images/function_overview_8_0.png)](https://seaborn.pydata.org/tutorial/function_overview.html)

Why do we focus on these common plots? Our eyes are better at distinguishing certain visual features more than others. All of these plots are focused on their position to depict data, which gives us the most effective visual scale.

[![Image Source: Visualization Analysis and Design by [Tamara Munzner](https://www.oreilly.com/search?q=author:%22Tamara%20Munzner%22)](https://www.oreilly.com/api/v2/epubs/9781466508910/files/image/fig5-1.png)](https://www.oreilly.com/library/view/visualization-analysis-and/9781466508910/K14708_C005.xhtml)

Let's load in our genomics datasets and start making some plots from them.


``` python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt


metadata = pd.read_csv("classroom_data/metadata.csv")
mutation = pd.read_csv("classroom_data/mutation.csv")
expression = pd.read_csv("classroom_data/expression.csv")
```

## Distributions (one variable)

To create a histogram, we use the function [`sns.displot()`](https://seaborn.pydata.org/generated/seaborn.displot.html) and we specify the input argument `data` as our dataframe, and the input argument `x` as the column name in a String.


``` python
sns.displot(data=metadata, x="Age")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-3-1.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-3-2.png){width=200%}

(The `plt.figure()` and `plt.show()` functions are used to render the plots on the website, but you don't need to use it for your exercises.)

A common parameter to consider when making histogram is how big the bins are. You can specify the bin width via `binwidth` argument, or the number of bins via `bins` argument.


``` python
sns.displot(data=metadata, x="Age", binwidth = 10)
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-4-5.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-4-6.png){width=200%}

Our histogram also works for categorical variables, such as "Sex".


``` python
sns.displot(data=metadata, x="Sex")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-5-9.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-5-10.png){width=200%}

**Conditioning on other variables**

Sometimes, you want to examine a distribution, such as Age, conditional on other variables, such as Age for Female, Age for Male, and Age for Unknown: what is the distribution of age when compared with sex? There are several ways of doing it. First, you could color variables by color, using the `hue` input argument:


``` python
sns.displot(data=metadata, x="Age", hue="Sex")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-6-13.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-6-14.png){width=200%}

It is rather hard to tell the groups apart from the coloring. So, we add a new option that we want to separate each bar category via `multiple="dodge"` input argument:


``` python
sns.displot(data=metadata, x="Age", hue="Sex", multiple="dodge")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-7-17.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-7-18.png){width=200%}

Lastly, an alternative to using colors to display the conditional variable, we could make a subplot for each conditional variable's value via `col="Sex"` or `row="Sex"`:


``` python
sns.displot(data=metadata, x="Age", col="Sex")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-8-21.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-8-22.png){width=200%}

You can find a lot more details about distributions and histograms in [the Seaborn tutorial](https://seaborn.pydata.org/tutorial/distributions.html).

## Relational (between 2 continuous variables)

To visualize two continuous variables, it is common to use a scatterplot or a lineplot. We use the function [`sns.relplot()`](https://seaborn.pydata.org/generated/seaborn.relplot.html) and we specify the input argument `data` as our dataframe, and the input arguments `x` and `y` as the column names in a String:


``` python
sns.relplot(data=expression, x="KRAS_Exp", y="EGFR_Exp")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-9-25.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-9-26.png){width=200%}

To conditional on other variables, plotting features are used to distinguish conditional variable values:

-   `hue` (similar to the histogram)

-   `style`

-   `size`

Let's merge `expression` and `metadata` together, so that we can examine KRAS and EGFR relationships conditional on primary vs. metastatic cancer status. Here is the scatterplot with different color:


``` python
expression_metadata = expression.merge(metadata)

sns.relplot(data=expression_metadata, x="KRAS_Exp", y="EGFR_Exp", hue="PrimaryOrMetastasis")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-10-29.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-10-30.png){width=200%}

Here is the scatterplot with different shapes:


``` python
sns.relplot(data=expression_metadata, x="KRAS_Exp", y="EGFR_Exp", style="PrimaryOrMetastasis")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-11-33.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-11-34.png){width=200%}

You can also try plotting with `size=PrimaryOrMetastasis"` if you like. None of these seem pretty effective at distinguishing the two groups, so we will try subplot faceting as we did for the histogram:


``` python
sns.relplot(data=expression_metadata, x="KRAS_Exp", y="EGFR_Exp", col="PrimaryOrMetastasis")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-12-37.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-12-38.png){width=200%}

You can also conditional on multiple variables by assigning a different variable to the conditioning options:


``` python
sns.relplot(data=expression_metadata, x="KRAS_Exp", y="EGFR_Exp", hue="PrimaryOrMetastasis", col="AgeCategory")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-13-41.png){width=200%}![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-13-42.png){width=200%}

You can find a lot more details about relational plots such as scatterplots and lineplots [in the Seaborn tutorial](https://seaborn.pydata.org/tutorial/relational.html).

## Categorical (between 1 categorical and 1 continuous variable)

A very similar pattern follows for categorical plots. We start with [sns.catplot()](https://seaborn.pydata.org/generated/seaborn.catplot.html) as our main plotting function, with the basic input arguments:

-   `data`

-   `x`

-   `y`

You can change the plot styles via the input arguments:

-   `kind`: "strip", "box", "swarm", etc.

You can add additional conditional variables via the input arguments:

-   `hue`

-   `col`

-   `row`

See categorical plots [in the Seaborn tutorial.](https://seaborn.pydata.org/tutorial/categorical.html)

## Basic plot customization

You can easily change the axis labels and title if you modify the plot object, using the method `.set()`:


``` python
plt.figure()
exp_plot = sns.relplot(data=expression, x="KRAS_Exp", y="EGFR_Exp")
exp_plot.set(xlabel="KRAS Espression", ylabel="EGFR Expression", title="Gene expression relationship")
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-14-45.png)<!-- -->

``` python
plt.show()
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-14-46.png)<!-- -->![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-14-47.png)<!-- -->

You can change the color palette by setting adding the `palette` input argument to any of the plots. You can explore available color palettes [here](https://www.practicalpythonfordatascience.com/ap_seaborn_palette):


``` python
plt.figure()
sns.displot(data=metadata, x="Age", hue="Sex", multiple="dodge", palette=sns.color_palette(palette='rainbow')
)
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-15-51.png)<!-- -->

``` python
plt.show()
```

![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-15-52.png)<!-- -->![](resources/images/05-data-visualization_files/figure-docx/unnamed-chunk-15-53.png)<!-- -->

## Exercises

Exercise for week 5 can be found [here](https://colab.research.google.com/drive/1kT3zzq2rrhL1vHl01IdW5L1V7v0iK0wY?usp=sharing).
