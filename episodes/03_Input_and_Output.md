---
title: "Input and Output"
teaching: 10 # teaching time in minutes
exercises: 2 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is a function?
- How do we read data from a file?
- How can we graph data?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understanding how to build and use functions
- Learning how to open files and read data from them
- Beginning to plot numerical data

::::::::::::::::::::::::::::::::::::::::::::::::

## Reusable Code with Functions

Often we come across situations where we would want to do the same type of calculation several times in a single program. Many of the Python modules provide functions for doing just this (and some of you will have used the `math.sqrt()` function earlier). However, you can define your own functions if you want. This can be done anywhere in your program, but is usually done at the beginning. In any case, the important thing is that you define a function before you try to use it in your program.

As a trivial example, here is a function definition which squares a number:

```python
def square(x):
    return x*x
```

When Python comes across this in your program, it does nothing. Only when you call it does it produce any effect. The `x` in the `def` line is called an argument, and acts as a placeholder for whatever (in this case) you want to square. Once the function is defined, you can call it using anything in place of the `x`, for example to square the number `3`, you would use:

```python
square(3)
```

```output
9
```

If you wanted to store the result in a variable, you could use:

```python
y = square(3)
```

and you could also pass a variable into the function, so after:

```python
z = square(y)
```

`z` would have the value `81`.

Functions are incredibly versatile and many arguments can be passed into a single function, they can contain more than one line of code, and can do anything that you can do in other parts of a Python program. Parcelling up code like this means that it is not repeated in your program, so that if you need to change it, it will only have to be changed once.

::::::::::::::::::::::::::::::::::::: challenge

## Building a Hypotenuse Function

In Episode 1, you should have worked out an expression for calculating the hypotenuse of a right-angled triangle given the other two sides. Now, create a function to do this, so that you could call:

```python
hypot(3, 4)
```

and it would return the value `5`.

Once you have a function that you think works, try using `math.hypot()` to check your answers.

:::::::::::::::: solution

```python
def hypot(x, y):
    z = ((x ** 2) + (y ** 2)) ** 0.5
    return z

hypot(3, 4)
```

```output
5
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Writing Well-Organised Code

One of the big advantages that Python has as a programming language is that it is usually quite nice to read, unlike many other languages. The fact that indentation is enforced consistently is a big part of this, but there are several more conventions you can use that will help even more. Our suggestions are below, but you are of course free to ignore them. However, you might have local rules on coding style that you will have to adhere to and you should check with colleagues on whether this is the case.

* Always put import statements at the top of your program (after any initial comments). This ensures that when you come back to your program, you will know immediately which modules it is using, and which parts of those modules it needs.
* After the imports, put your function definitions. Again, this means that the functions are defined before you try to use them, and you can see straight away what functions you are using.
* Enter the main body of the program at the bottom of the file.
* Use lots of comments. However obvious the program is, and however well you understand it, this will not be the case if you come back to change it in 2 years' time. If it isn’t you that has to change the program, having the comments there will help even more.

## Reading Data From Files

We have now met a few of Python’s most common data types (there are a lot more and, if you like, you can make your own as well) and you should be happy with the ways we can repeat actions on lists and dictionaries with for loops, as well as take decisions based on our data using if statements. We are now going to introduce a new data type, the Python file object. This is Python’s way of letting us get data from files on the computer. The simplest way to explain it is to get a suitable data file and play with it on the command line. We are going to use a couple of separate files in this worksheet, and we will start by downloading them. They can be found here:

![Intro to Python files on GitHub](https://github.com/sandyjmacdonald/intro-python-course)

Download them all by clicking the green "Code" button, then "Download ZIP". The first file you need is called `seq_lengths.txt`. Make sure that you move the files, once you've unzipped them, into the same folder where you will save the Python programs that you are going to write to process the data. Let's look at the `seq_lengths.txt` file. This is a simple file which contains the lengths of >10,000 DNA sequences produced in a particular experiment, one per line. What we want to do, at least as a first step, is to read these lengths into a list. We need to start by opening the file, so create a new Python program file, and save it in the same folder where the data file is located.

The first thing we have to do is to open the file. The command to do this is `open()` and this returns a file object, which we will call `f`:

```python
f = open("seq_lengths.txt", 'r')
```

`lines` now refers to a list of strings containing each of the lines in the file. Try looking at one or two of them. If you didn’t look at the contents of the files before you opened it with your program, have a look at it now. If you look in Python at `lines[1]` and check the second line in the file you will see some differences. Most obvious is the presence of a "\n" at the end of each line. These are "newline characters" and we need to remember to remove these when we process the data from the file. Although it looks like two characters, it is what is called an escape character, and just a single character but one which we cannot normally see in a string. 

Using `.readlines()` is nice and simple, but has a major drawback. It’s fine when your file is small enough to read all of the lines into memory, but if you are reading a 32Gb SAM file, you are going to run into problems. Here, you want to read one line at a time, and process it. Python files do have a `.readline()` method which will read a single line from the file, but it’s best to just use a for loop. Python has an idea of “iterable” data types which you can put into loops. We have see two of these so far: the list and the dictionary. For a list you get each element in turn, and for a dictionary you get each key in turn. Strings are also iterable and return each character in turn. The point of mentioning this now is that files (or, at least the objects returned by Python’s `open()` function) are also iterable, and Python tries to pass you exactly what we want: one line at a time. So we can start to write a program now to start processing this data file.

Having said that, though, you need to remember that files are not just lists of lines. For a list, we can iterate over the contents with a for loop, and then if we want, we can iterate over the same list again. This is easy for Python to do, because it holds the list in the computer's memory. A file, though, is a bit different. When you are reading a file, you can iterate over the contents, but Python relies on the operating system to get each line at a time for you. Once you get to the end of the file, the operating system does not "rewind" to the start when you want to read it again, it just keeps saying "You're at the end of the file". If you want to read through a file again, the easiest way to do that is to close the file and re-open it.

You could argue that perhaps Python should do this for you when you start a new for loop, but this isn't what you want to do all the time. For example, it's common for data files to contain one or more header lines that describe the data before the data actually start, so a common pattern in programs could look like this:

```python
myfile = open("big_data_file.txt", 'r')
header1 = myfile.readline()
header2 = myfile.readline()
for line in myfile:
	… process data lines …

```

If Python reset the file at the start of the for loop, it would then re-read the two header lines. The take home message here is that if you want to re-read a file, close it and re-open it.

This will be the largest program so far, and what I do when I am embarking on writing a large program is to start with just the basic structure and make sure that works, then add to the program step-by-step and keep running it to make sure it is doing what I expect before it gets too complicated. So to begin:

```python
datafile = open('seq_lengths.txt', 'r')
for line in datafile:
    print(line)
```

OK, so far so good, the program is basically printing the whole file out to the Python Shell window. However, I forgot about the newline characters at the end of the lines. Because the `print()` statement automatically adds a newline to the end of everything it prints, we are getting two at the end each line, which is why the output looks double-spaced. So, the first thing is to fix that by removing the newlines. Strings have a strip method which removes any newlines, spaces or tabs at the start and end of each line, so add the line:

```python
line = line.strip()
```

to the loop before the print statement (at the correct level of indentation) and try the program again. Now the file should look single-spaced. 

An important note about string and integer types: `line = "304"` assigns the _string_ "304" to the variable name "line", whereas `line = 304` assigns the _integer_ 304 to the variable name "line". Both of the bits of data assigned to these variables look similar but behave differently due to their different data types. We can, however, convert one type to another in Python, e.g.:

```python
line = "304"  # 304 is a string here
length = int(line)  # Explicitly convert the string to an integer
```

The variable `length` now contains an integer that we can use as a number in our program. What we want to do here is to store all of the numbers in the file in a single list that we can use later. So, all we need to do is append each value to a list after we have read it from the file and converted it to an integer. But, we don’t have a list to append it to yet…


::::::::::::::::::::::::::::::::::::: challenge

## Reading Sequence Lengths from a File and Storing Them

Start with the code that reads lines from the file and make the following changes:

* Create an empty list (called `data`) somewhere before the start of the `for` loop which reads through the file
* Within the loop, add a line to convert the sequence length string to an integer
* Add another line inside the loop that appends the integer to the `data` list

When the program is run, it should now read through the file and store all of the sequence lengths in a single list.

:::::::::::::::: solution

```python
data = []

datafile = open('seq_lengths.txt', 'r')
for line in datafile:
    line = line.strip()
    length = int(line)
    data.append(length)

print(data)
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Drawing Plots

Now that we have read our data in, we need a way of displaying the data.

One of the main reasons for using Python is the vast array of modules and libraries that are available for you to use in your programs. All of these modules are written by other Python users and shared freely, usually via the Python Package Index ([PyPI](https://pypi.org)) and often maintained in [GitHub](https://github.com). We will talk about some of the main ones later, but for now, we are going to use one called `matplotlib`. Exactly why it is called that doesn’t matter, but what it does is to make it simple for you to draw a wide range of different types of graphs and diagrams. We are going to draw a couple of simple ones in this worksheet and then get a bit more complicated in Worksheet 4.

We need to start by telling Python that we want to use matplotlib, and we do this by putting an `import` statement at the very top of the file to load the module. The version we would suggest is:

```python
import matplotlib.pyplot as plt
```

This loads the plotting parts of matplotlib into a "namespace" called plt. plt is just a name that I chose and you can use something different it you want, but the important thing is that all of the calls to matplotlib functions must subsequently be preceded by plt (or whatever you chose to call it). For example, if we want to create a new figure, we would call:

```python
plt.figure(1)
```

matplotlib is a massive module and contains literally hundreds of possible functions for us to call. We are just going to use three in our program: `plt.figure()`, `plt.hist()` and `plt.show()`. These create a figure, draw a histogram, and display the figure on the screen, respectively.

All you need to do now is to add these to the end of you program, like this:

```pythonplt.figure(1)
plt.hist(data)
plt.show()
```

When you run the program now, it should show you a figure like this:

![An example of a matplotlib histogram](fig/03_matplotlib_histogram.jpg){"An example of a matplotlib histogram"}

::::::::::::::::::::::::::::::::::::: challenge

## Customising Plots

matplotlib is really flexible and you can tweak the figure produced almost any way you would like in order to produce the exact figure that you need by adding extra arguments to the `.hist()` method call. For example:

```python
plt.hist(data, bins=50, color='pink')
```

produces a histogram with 50 pink bars instead of the default of ten blue ones. Try changing these values in your program and see how the figure changes.

If you Google “matplotlib hist”, you should be able to find the full set of possible options and see if you can reproduce this figure:

![Example of matplotlib customised plot](fig/03_matplotlib_stacked_histogram.jpg){"Example of a matplotlib customised plot"}

:::::::::::::::: solution

```python
import matplotlib.pyplot as plt

data = []

datafile = open('seq_lengths.txt', 'r')
for line in datafile:
    line = line.strip()
    length = int(line)
    data.append(length)

plt.figure(1)
plt.hist(data, 
         bins=50, 
         color='green', 
         cumulative=True, 
         orientation='horizontal', 
         histtype='step')
plt.show()
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

