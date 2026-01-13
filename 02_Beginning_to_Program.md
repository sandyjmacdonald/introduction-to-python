---
title: "Beginning to Program"
teaching: 10 # teaching time in minutes
exercises: 2 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is a program and how do you create and run one?
- What is a for loop?
- What is a Python dictionary?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Begin to learn how to build out programs to do specific tasks
- Learn how loops work and why they are useful
- Learn how to format strings
- Learn what dictionaries are and why they are useful

::::::::::::::::::::::::::::::::::::::::::::::::

## First Steps in Programming

So far, it’s been fun playing with commands at the Python prompt, but now we are going to need to start editing programs properly and saving them so that we can change them and re-use parts later. So, on your Spyder menu, click on `File->New file…` and a new tab will open in the Editor pane (the large one occupying the left half of the Spyder window; it will have the title `"untitled0.py"`). This will contain a couple of lines that begin with a # character which will tells Python not to execute the content of the lines (these are called "comments" and are incredibly useful) and some lines between triple-quotes, called a docstring. Underneath these lines, you can start typing you own program.

Start by entering the following code:

```python
shopping = ['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk']

for item in shopping:
    print(item)
```

This is a very simple program, which creates a variable that refers to a list, then prints out each of the items in turn. There are a couple of things to comment on here. Firstly, the `for` statement creates the variable `item` (the variable name can of course be anything that you want), then sets the value of this variable to be each of the elements in the list `shopping` in turn. The line which is indented is then executed for each value assigned to the `item` variable and prints out the value.

To execute the program you first need to save it using the `File->Save as…` menu option. You can save the file anywhere you like on your computer (it helps if you remember where), but it is a good idea (particularly under Windows) to give the file an extension of `.py`. This will mean that the computer will recognise it as a Python program. Once you have saved the file, you can press F5 (or choose `Run->Run` from Spyder’s menu, or press the "play" icon in the menu bar).

Before the program starts running, a dialog box will appear like this:

**INSERT IMAGE HERE**

There are a couple of important points here, which might not be obvious.

Firstly, the "Working Directory" option allows you to choose the folder that the program is running in. For most programs, you will need to set this to be the folder that contains e.g., data files that your program needs to read. For the moment, though, you don't need to worry about it.

The second is a bit more subtle. The "Console" options at the top are important. For the moment, you can leave them set at the default option of "Execute in the current Python or IPython console", and the results of the program will appear in the pane on the bottom right of the window. Later on, we will need to choose "Execute in a dedicated Python console" to allow our programs to open up new windows containing the charts that we will produce in Worksheets 3 and 4.

Returning to our program, and specifically the "for loop". Whenever we want to execute a piece of Python code several times, this is one of the ways we can do it. Python recognises the lines we want to form part of the loop by the level of indentation and it is vital that you maintain consistent indentation throughout your programs. In fact, though, this is one of the things which leads to your programs being more readable and easier to understand, because visually, you can see the structure of the program at a glance by the indentation.

::::::::::::::::::::::::::::::::::::: challenge

## Appending to Lists

1. Change the program above by adding a second list (with a different variable name) to the program, which contains cheese, flour, eggs, spaghetti, sausages and bread.
2. Change the loop so that instead of printing the element, it appends it to first shopping list.
3. Print out the new list.

:::::::::::::::: solution

```python
shopping = ['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk']
extrashopping = ['cheese', 'flour', 'eggs', 'spaghetti', 'sausages', 'bread']

for item in extrashopping:
    shopping.append(item)

print(shopping)
```

```output
['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk', 'cheese', 'flour', 'eggs', 'spaghetti', 'sausages', 'bread']
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Making Decisions

The output from the previous exercise was:

```output
['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk', 'cheese', 'flour', 'eggs', 'spaghetti', 'sausages', 'bread']
```

This looks to me as if it’s worked exactly as I described, but maybe not quite as I intended. We seem to have too many eggs and too much bread. This might not be a problem (and it does illustrate that the same value can be present in a list more than once), but I really just want one copy of each item. What we need to do is check before we add an element that there isn’t a value in there in the first place. Fortunately, Python lets us do this really easily.

For example, if we go back to the IPython Console panel for a minute and try:

```python
shopping = ['eggs', 'cheese', 'milk']

'eggs' in shopping
'frogs' in shopping
'frogs' not in shopping
```

```output
True
False
True
```

We can use this in a new Python statement, which allows us only to execute statements if a particular condition is true. The program could be changed to:

```python
shopping = ['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk']
extrashopping = ['cheese', 'flour', 'eggs', 'spaghetti', 'sausages', 'bread']

for item in extrashopping:
    if item not in shopping:
        shopping.append(item)

print(shopping)
```

```output
['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk', 'cheese', 'spaghetti', 'sausages']
```

Much better. A couple of points to notice with the indentation. The `if` statement is indented with respect to the `for` statement, so it will be executed every time the loop executes. The `append` method call is indented with respect to the `if` statement, and so it will only be executed if the condition in the `if` statement (i.e., `item not in shopping`) is `True`. Finally, the last print statement is at the very start of the line; this means it will only execute once all iterations of the loop are done.

::::::::::::::::::::::::::::::::::::: challenge

## Additional Logic

Change the program above to print out a message when a duplicate item is found. To do this, you could add another `if` statement to see if the item is in the list. 

Alternatively, you can add an `else:` clause to the existing if statement. This will be executed when the condition in the `if` statement is `False`.

:::::::::::::::: solution

```python
shopping = ['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk']
extrashopping = ['cheese', 'flour', 'eggs', 'spaghetti', 'sausages', 'bread']

for item in extrashopping:
    if item not in shopping:
        shopping.append(item)
    else:
        print(item, 'is already in the shopping list')

print(shopping)
```

```output
flour is already in the shopping list
eggs is already in the shopping list
bread is already in the shopping list

['bread', 'potatoes', 'eggs', 'flour', 'rubber duck', 'pizza', 'milk', 'cheese', 'spaghetti', 'sausages']
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Counting Loops

Looping over elements of a list is great, but there are other circumstances where you just want to do something a set number of times. Most programming languages have a `for` statement which does exactly this, but as we have seen above, Python’s `for` statement goes through a list and returns each value in that list. Fortunately, Python has a function which generates the numbers for us to use in a `for` loop. Go to the Python shell and type:

```python
list(range(10))
```

```output
[0,1,2,3,4,5,6,7,8,9]
```

So, a loop like this:

```python
for i in range(10):
    print(i)
```

would print out the numbers 0 to 9, one to a line. The `range()` function can provide most lists of numbers that you would need.

::::::::::::::::::::::::::::::::::::: challenge

## Experimenting with the `range()` Function

Explore what you can do with the `range()` function. It can take just one number as we did above, or two as a starting and ending value, or even three which are a start, end, and step value. Try all three versions of the range command, and then work out how to get the list: `[4, 11, 18, 25]`.

:::::::::::::::: solution

```python
list(range(26))
list(range(4,26))
list(range(4,26,7))
```

```output
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25]
[4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25]
[4, 11, 18, 25]
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Direct and Indirect Loops

So, `range()` gets us a list we can use to count any number that we want, but why does it stop short of the limit we give it?  Why does `range(n)` mean 0 to n-1 instead of 1 to n?  Well, try out the following two pieces of code:

```python
for item in shopping:
    print(item)
```

```python
for i in range(len(shopping)):
    print(shopping[i])
```

They should be exactly the same: `range()` behaves as it does so that you can use it to index lists (and other sequence data types).

The first is an example of a direct loop, in which you pull out the items one by one directly from the list. The second is an indirect list, where you step through the indices and use them to get the required elements from the list.

Which one is better?  Generally, the direct method is slightly clearer and a bit more _Pythonic_. However, there are circumstances where an indirect loop is a bit clearer. If you have two lists of the same size, you might need to print out the corresponding elements of the two lists (although there might be better ways to do this, as well). In this case, you can use `range()` with the size of one of the lists, and then use the index to get the elements of both lists.

::::::::::::::::::::::::::::::::::::: challenge

## Iterating Over Lists with Ranges

Start with your shopping list and create a new list with the amounts you need to buy of each item. So for example:

```python
shopping = ['bicycle pump', 'sofa', 'yellow paint']
amounts = [1, 7, 9]
```

then write a loop to step through and print the item and the amount on the same line.

:::::::::::::::: solution

```python
for i in range(len(shopping)):
    print(shopping[i], amounts[i])
```

```output
bicycle pump 1
sofa 7
yellow paint 9
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Enumerating Lists

That all works fine, but it’s not generally considered to be a very Pythonic way of doing things. Why? Because you are introducing a new list (with the `range()` function), that you use to step through two other pre-existing lists. It’s not a huge problem, and if you are happy using this kind of approach, then feel free to use it. However, Python provides you with another possibility, which is the `enumerate()` function. Enumerate again lets you step through a list, but rather than returning just the elements of the list, with each element it also gives you the index of that element in the list. You can then use that index to e.g., look up values in other lists. So the solution to the above exercise could look like this:

```python
shopping = ['bicycle pump', 'sofa', 'yellow paint']
amounts = [1, 7, 9]

for i, item in enumerate(shopping):
    print(item, amounts[i])
```

This looks a bit odd the first time you see it, so it’s worth looking at a couple of things just to clarify what is happening. The first thing to try is look at what `enumerate()` does:

```python
list(enumerate(shopping))
```

```output
[(0, 'bicycle pump'), (1, 'sofa'), (2, 'yellow paint')]
```

This is a list of pairs of values in parentheses (these are tuples, of which more in a moment…). The `for` loop goes through each of these tuples in turn, and “unpacks” them into the two variables: `i` and `item`. Unpacking is something that tends to happen a lot in Python programs, usually because it makes the code more readable. It most commonly occurs in `for` loops, but you can do it anywhere where you need to split a list (or tuple) into a number of variables, for example:

```python
number, type = (0, 'bicycle pump')
```

## String Formatting

When you print out pairs of values, like in the exercise above, the output is a bit boring. It’s just a name and a number on a line. It could be a bit prettier, or at least more nicely formatted. You can put a few extra strings in there to make it clearer like this:

```python
print("I need to buy", amounts[i], shopping[i])
```

```output
I need to buy 7 sofa
```

This is fine, but it is difficult to control the formatting, particularly when you are mixing numbers and strings. Most programming languages have some function or facility for creating formatted strings and Python is no exception. In Python’s case, you start with a string into which you wish to insert the values of your variables, with the characters `{}` at the point where you want the value to appear. You then call that string's `.format()` method, with the variables you want to insert in the brackets.

```python
s = "I need to buy {:d} {:s}".format(7, 'snakes')
print(s)
```

```output
I need to buy 7 snakes
```

Don’t we all?  In the format string, the `:d` indicates that you are expecting to put an integer in that position (d stands for “decimal” i.e., it puts the base-10 representation of the number at that point - you can use `:h` and `:o` for hexadecimal or octal respectively if you need to). The `:s` indicates a string is required, but if the value you give is not a string, Python usually knows how to convert it into one. You can modify these in different ways, for example `:03d` would take your number and make sure that it is at least three digits long, filling with zeros if necessary. So `7` would appear in the formatted string as `007`. The full list of different formats and modifiers is on the Cheat Sheet.

This is actually just one way of formatting strings in Python, each of which has its own strengths and weaknesses, and which one you choose might depends on exactly what your program is trying to do. The latest version of string formatting, only added in Python version 3.6, are so-called “f-strings”. These look similar to the above, but you can put the name of a variable in the braces to use the value of that variable in the string.

```python
print(f"I need to buy {amounts[i]} {shopping[i]}”)
```

```output
I need to buy 7 sofa
```

As with the `.format()` method, you can specify the required data type and formatting options for each variable using the same `:03d` style syntax.

::::::::::::::::::::::::::::::::::::: challenge

## Iterating Over Lists with Formatted Strings

Change your program to print out a formatted string for each of the items in your shopping list along with the amount you need to buy of that item.

:::::::::::::::: solution

```python
shopping = ['bicycle pump', 'sofa', 'yellow paint']
amounts = [1, 7, 9]

for i, item in enumerate(shopping):
    print(f"I need to buy {amounts[i]} {item}")
```

```output
I need to buy 1 bicycle pump
I need to buy 7 sofa
I need to buy 9 yellow paint
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Looking Up Data

Keeping data in parallel lists like this is fine if you are really, really careful and you don’t need to change the lists that much. Otherwise, it is prone to errors. One way of getting round this is to use a new data type called a dictionary. Dictionaries are sort of like lists, but instead of holding just a single value, they hold a key-value pair, so when you are looking up a value in the dictionary you supply the key and the dictionary returns the value, rather than just using an index. For example:

```python
student_numbers = { "Bioscience Technology": 16, 
                    "Computational Biology": 12,
                    "Post-Genomic Biology": 20,
                    "Ecology and Environmental Management": 3,
                    "Maths in the Living Environment": 0
                    }

student_numbers["Bioscience Technology"]
```

```output
16
```

The data is enclosed in curly brackets and is a comma-separated list of key-value pairs. The key and value are separated by a colon. The key can be any immutable type (so, mainly strings, numbers or tuples). Notice I have split the assignment statement to create the dictionary over several lines. Python normally expects a command to be on a single line, but sometimes it can work out when a statement is not finished, for example, when you haven’t closed a set of brackets. Python will continue to prompt for input until you close the bracket properly before trying to execute the command.

Dictionaries themselves are a mutable datatype, so the values associated with a key can be changed:

```python
student_numbers["Bioscience Technology"] += 1
```

and if you try to assign a value to a key that doesn’t exist, Python creates the entry for you automatically. 

```python
student_numbers["Gardening"] = 10
```

Of course, getting rid of entries in the dictionary is easy as well:

```python
del student_numbers["Maths in the Living Environment"]
```

If we know the keys in the dictionary we can look up the values. If we want to loop over the values in the dictionary, we could create a list of the keys and loop over that, but that’s no better than keeping the keys and values in separate lists. Instead, Python can create a list of the keys for you when you need it.

```python
student_numbers.keys()
```

We can now put this into a `for` loop, with or without sorting it first. If we are not bothered about the order (and Python doesn’t make any promises about the order the keys will be supplied in, they will be the order that is most efficient for Python to store and look up the keys. It almost certainly won’t be either the order the keys were added to the dictionary or alphabetical order), then we can just just loop directly over the dictionary:

```python
for item in student_numbers:
    print(item, student_numbers[item])
```

That should work as expected.  Notice here there is a blank line at the end of the loop. This is only required when you are executing loops interactively and it’s just so that Python knows you have got to the end of the block (or suite) of code that you want to be inside the loop.

As well as getting the keys, you could also get the values as a list using `.values()`. Slightly more efficient is to get the key-value pairs in one step using:

```python
student_numbers.items()
```

```output
[('Gardening', 10), ('Computational Biology', 10), ('Post-Genomic 
Biology', 20), ('Bioscience Technology', 16), ('Ecology and 
Environmental Management', 3)]
```

Have a **careful** look at this output. The square brackets show that this is a list of things. But each item in that list is in fact two pieces of data in round brackets. When you do have several items in (round) brackets (parentheses) like this, it is actually a new data type which is a variant of a list, called a tuple.

The main difference between a list and a tuple is that tuples are immutable. Once it is defined, it cannot be changed again, you can’t add items to it or change what is in a particular place in the tuple. They can be useful in a lot of circumstances, particularly where you need to be strict about the contents of a list. 

One example is when you are dealing with coordinates, where you need to be sure that your coordinate sets are of a particular size. However, there is nothing you can do with a tuple that you can’t do with a list. There are two ways we can use this in a `for` loop. Firstly, we can use a variable which will contain the tuple and unpack it in the body of the loop:

```python
for data in student_numbers.items():
    print(data[0], data[1])
```

or you can unpack the data directly in the `for` statement:

```python
for course, students in student_numbers.items():
    print(course, students)
```

If you are putting the data into a formatted string, you will need to put the data into a tuple to use the interpolation operator, so you can exploit the fact that Python gives it to you in a tuple directly:

```python
for data in student_numbers.items():
    print("Course '%s' has %d students" % data)
```

This is our first example of a compound data structure (in this case, a list of tuples). The ability to construct arbitrarily complex data structures like this easily is one of the most powerful features of Python and one we will explore more in the next worksheet.

::::::::::::::::::::::::::::::::::::: challenge

## Iterating Over Dictionaries

We are nearly finished shopping now and all we need to do is change the program so that the amounts and items are stored in a dictionary and print out the items and amounts by looping over the dictionary.

Do it twice, once looping over the the dictionary to get the keys (or use the keys) and once by getting the key-value pairs directly from the dictionary.

:::::::::::::::: solution

```python
shopping = {'bicycle pump': 1,
            'sofa': 7,
            'yellow paint': 9
            }

for item in shopping:
    print(f"I need to buy {shopping[item]} {item}")

for item, amount in shopping.items():
    print(f"I need to buy {amount} {item}")
```

```output
I need to buy 1 bicycle pump
I need to buy 7 sofa
I need to buy 9 yellow paint

I need to buy 1 bicycle pump
I need to buy 7 sofa
I need to buy 9 yellow paint
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Summary

- `for` loops can be used to repeat a block of code for each item in a list.
- `range()` can be used to create a list of numbers,  so you can execute the statements within the loop a given number of times. Specifically, `range()` returns a "generator object" which will return the numbers to you one by one. This saves memory space when the range of numbers you need to use is large, but if you actually need a list, calling `list(range(<number>))` will get all the numbers for you.
- `if:` `elif:` `else:` statements can be used to choose one of a number of optional blocks of code depending on the conditions in the `if` and `elif` clauses.
- String interpolation allows you to insert values into a string, enabling sophisticated formatting.
- Tuples are a new data type which are like fixed lists, which can’t be changed once they are created.
- Dictionaries are another data type which stores key-value pairs.
- The `.keys()`, `.values()` and `.items()` methods are used to get lists of the contents of a dictionary.