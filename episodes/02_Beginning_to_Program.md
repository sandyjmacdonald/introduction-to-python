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

## Direct and Indirect Loops

## Enumerating Lists

## String Formatting

## Looking Up Data

## Summary