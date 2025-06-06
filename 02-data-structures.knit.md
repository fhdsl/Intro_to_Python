

# Working with data structures

In our second lesson, we start to look at two **data structures**, **Lists** and **Dataframes**, that can handle a large amount of data for analysis.

## Lists

In the first exercise, you started to explore **data structures**, which store information about data types. You explored **lists**, which is an ordered collection of data types or data structures. Each *element* of a list contains a data type or another data structure.

We can now store a vast amount of information in a list, and assign it to a single variable. Even more, we can use operations and functions on a list, modifying many elements within the list at once! This makes analyzing data much more scalable and less repetitive.

We create a list via the bracket `[ ]` operation.


``` python
staff = ["chris", "ted", "jeff"]
chrNum = [2, 3, 1, 2, 2]
mixedList = [False, False, False, "A", "B", 92]
```

### Subsetting lists

To access an element of a list, you can use the bracket notation `[ ]` to access the elements of the list. We simply access an element via the "index" number - the location of the data within the list.

*Here's the tricky thing about the index number: it starts at 0!*

1st element of `chrNum`: `chrNum[0]`

2nd element of `chrNum`: `chrNum[1]`

...

5th element of `chrNum`: `chrNum[4]`

With subsetting, you can modify elements of a list or use the element of a list as part of an expression.

### Subsetting multiple elements of lists

Suppose you want to access multiple elements of a list, such as accessing the first three elements of `chrNum`. You would use the **slice** operator `:`, which specifies:

-   the index number to start

-   the index number to stop, *plus one.*

If you want to access the first three elements of `chrNum`:


``` python
chrNum[0:3]
```

```
## [2, 3, 1]
```

The first element's index number is 0, the third element's index number is 2, plus 1, which is 3.

If you want to access the second and third elements of `chrNum`:


``` python
chrNum[1:3]
```

```
## [3, 1]
```

Another way of accessing the first 3 elements of `chrNum`:


``` python
chrNum[:3]
```

```
## [2, 3, 1]
```

Here, the start index number was not specified. When the start or stop index is *not* specified, it implies that you are subsetting starting the from the beginning of the list or subsetting to the end of the list, respectively. Here's another example, using negative indicies to count from 3 elements from the end of the list:


``` python
chrNum[-3:]
```

```
## [1, 2, 2]
```

You can find more discussion of list slicing, using negative indicies and incremental slicing, [here](https://towardsdatascience.com/the-basics-of-indexing-and-slicing-python-lists-2d12c90a94cf).

## Objects in Python

The list data structure has an organization and functionality that metaphorically represents a pen-and-paper list in our physical world. Like a physical object, we have examined:

-   What does it contain (in terms of data)?

-   What can it do (in terms of functions)?

And if it "makes sense" to us, then it is well-designed.

The list data structure we have been working with is an example of an **Object**. The definition of an object allows us to ask the questions above: *what does it contain, and what can it do?* It is an organizational tool for a collection of data and functions that we can relate to, like a physical object. Formally, an object contains the following:

-   **Value** that holds the essential data for the object.

-   **Attributes** that hold subset or additional data for the object.

-   Functions called **Methods** that are for the object and *have to* take in the variable referenced as an input.

This organizing structure on an object applies to pretty much all Python data types and data structures.

Let's see how this applies to the list:

-   **Value**: the contents of the list, such as `[2, 3, 4].`

-   **Attributes** that store additional values: Not relevant for lists.

-   **Methods** that can be used on the object: `chrNum.count(2)` counts the number of instances 2 appears as an element of `chrNum`.

Object methods are functions that does something with the object you are using it on. You should think about `chrNum.count(2)` as a function that takes in `chrNum` and `2` as inputs. If you want to use the count function on list `mixedList`, you would use `mixedList.count(x)`.

Here are some more examples of methods with lists:

| Function method                                                              | What it takes in             | What it does                                                          | Returns                          |
|------------------------------------------------------------------------------|------------------------------|-----------------------------------------------------------------------|----------------------------------|
| [`chrNum.count(x)`](https://docs.python.org/3/tutorial/datastructures.html)  | list `chrNum`, data type `x` | Counts the number of instances `x` appears as an element of `chrNum`. | Integer                          |
| [`chrNum.append(x)`](https://docs.python.org/3/tutorial/datastructures.html) | list `chrNum`, data type `x` | Appends `x` to the end of the `chrNum`.                               | None (but `chrNum` is modified!) |
| [`chrNum.sort()`](https://docs.python.org/3/tutorial/datastructures.html)    | list `chrNum`                | Sorts `chrNum` by ascending order.                                    | None (but `chrNum` is modified!) |
| [`chrNum.reverse()`](https://docs.python.org/3/tutorial/datastructures.html) | list `chrNum`                | Reverses the order of `chrNum`.                                       | None (but `chrNum` is modified!) |

## Methods vs Functions

**Methods** *have to* take in the object of interest as an input: `chrNum.count(2)` automatically treat `chrNum` as an input. Methods are built for a specific Object type.

**Functions** do not have an implied input: `len(chrNum)` requires specifying a list in the input.

Otherwise, there is no strong distinction between the two.

## Dataframes

A Dataframe is a two-dimensional data structure that stores data like a spreadsheet does.

The Dataframe data structure is found within a Python module called "Pandas". A Python module is an organized collection of functions and data structures. The `import` statement below gives us permission to access the "Pandas" module via the variable `pd`.

To load in a Dataframe from existing spreadsheet data, we use the function [`pd.read_csv()`](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html):





















