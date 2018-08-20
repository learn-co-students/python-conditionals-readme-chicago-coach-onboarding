
# Conditionals

## Introduction

We have been learning about different ways to use Python to interact with and manipulate data. However, we havent yet had a way to dynamically manipulate data or perform actions. For example, if a restaurant is too expensive we may want to choose a different one. If it's too cold outside, we should find something to do inside. These are just simple examples of decisions we might want our code to make as well. In this lab, we will introduce conditionals that allow us to do just that. We can use some pieces of data to inform decisions and choose one operation over any number of others.

## Learning Objectives

* Understand how an `if` statement can change the execution flow of our code when certain conditions are met
* Understand how the `if` keyword works with the `else` keyword in Python
* See how to select certain data by combining `if` statements in `for` loops 

## If Statement and Execution Flow

So far in Python, all of our lines of code run one after the other. So in the code below, `vacation_days` is initially assigned to `0`, then it is reassigned by incrementing by one, and again reassigned by incrementing again by one, which brings the `vacation_days` to a total of `2`.


```python
vacation_days = 0
vacation_days += 1
vacation_days += 1
vacation_days
```




    2



> The `+=` is used to increment. The statement `vacation_days += 1` can be thought of as `vacation_days = vacation_days + 1`. On line 2, `vacation_days` is `0`. Then we reassign `vacation_days` to equal the current value of `vacation_days`, which is `0`, plus `1`. Again we increment vacation_days on line 3, which would now equate to `1 + 1`, and finally we output the new value of `vacation_days`, `2`.


Contrast this with code that contains an `if` statement. Code that is part of an `if` block runs only when the conditional argument following the `if` evaluates to `True`. So it is not necessarily the case that every line of code runs.


```python
vacation_days = 1
if False:
    # code does not run as conditional argument False
    vacation_days += 1
    print("we incremented vacation days")
if True:
    print("we did NOT increment vacation days")
    
```

    we did NOT increment vacation days



```python
vacation_days
```




    1



Above we can see that since the condition following the `if` equals `False`, the code directly underneath is not run.  So, `vacation_days` stays assigned to the number 1.  

> **Note:** A *block* is any piece of code that grouped together.

With conditionals, we indicate that something is part of the *block* by indenting. So the line `vacation_days += 1` is indented to ensure that it is run as a part of the conditional argument above. To end the block we simply stop indenting.


```python
vacation_days = 1
if False: 
    # if block begins
    vacation_days += 1
# if block ends
vacation_days += 2
vacation_days
```




    3



So in the above cell, the last two lines are run because they are **not** part of the `if` block.

And, as you may have guessed, when the conditional argument is `True`, the code in the conditional block **does** run.  


```python
vacation_days = 1
if True:
    # code in if block runs, as True
    vacation_days += 1
vacation_days
```




    2



## Truthiness

![truthiness](truthiness.png "Truthiness")

So far our conditionals have depended on whether something evaluates exactly to `True` or `False`.  But conditionals don't force us to be so precise. Conditionals also consider some values `True` if they are `truthy` and `False` if they are `falsy`.  Take a look at the following:


```python
vacation_days = 1
if vacation_days:
    # this is run
    vacation_days += 1
vacation_days
```




    2



Even through `vacation_days` did not equal `True` above, it still ran the code in the `if` block because the value for `vacation_days` was `1`, which is considered `truthy`.

However, `0` is **not** considered truthy.  


```python
vacation_days = 0
if vacation_days:
    # this is not run
    vacation_days += 1
vacation_days
```




    0



Since `0` is **not** `truthy`, it is considered `falsy`. We can see that the `if` block was not run and `vacation_days` was not incremented, almost as if `vacation_days` evaluated to `False`. 

So what is truthy and what is falsy in Python?  Zero is falsy, and `None` is falsy.  Also falsy are values like empty lists and strings (e.g. `''`, `[]`) Let's take a look at that. 


```python
greeting = ''
if greeting:
    greeting += 'Hello'
else:
    greeting += 'Goodbye'
greeting
```




    'Goodbye'



If we are ever curious about the whether something is truthy or falsy in Python, we can just ask with the `bool` function.


```python
bool(0) # False
```




    False




```python
bool(1) # True
```




    True




```python
bool('')
```




    False




```python
bool([])
```




    False



## Using Data to Make Decisions

Our code in conditional arguments becomes more interesting when we use conditional arguments that are less direct than just `True` or `False`.

Let's say you have a management system that allows employees to put in their vacation days and the system has a way of auto tagging vacations as disruptive, average, or minimal based on the number of days being taken off. This helps to give immediate feedback for you so that you can make sure to plan deadlines and staff projects  appropriately. So, we'll use conditional statements that use the number of days taken off as the input to figure out if the vacation is disruptive, normal, or minimal. 

Let's start out with just creating logic that creates a tag for disruptive vacations or vacations longer than 5 days off of work. All other vacations can be tagged as average.


```python
number_of_days = 7
if number_of_days > 5:
    print("#disruptive")
else:
    print("#average")
```

    #disruptive


Great, now what if we want to tag vacations that are under 3 days off as minimally disruptive? Well, we don't want to create a new if block entirely. If we do, then our else statement will always run and we'll get `#average` and `#minimal`, which is not what we want. 

So, Python provides us with another conditional statement that is in between if and else, `elif`. This is basically saying, okay if the first `if` statement doesnt pass, check the next `if` statement until you hit an `else` or the block ends. 


```python
number_of_days = 2
if number_of_days > 5:
    print("#disruptive")
elif number_of_days < 3:
    print("#minimal")
else:
    print("#average")
```

    #minimal



```python
number_of_days = 3
if number_of_days > 5:
    print("#disruptive")
elif number_of_days < 3:
    print("#minimal")
else:
    print("#average")
```

    #average


We can see how powerful this kind of code can be to creating a dynamic and efficient programs and to makings decisions. Now, there is no need for anyone to manually rank each employee's vacations and we have a system that flags vacations that might need some special planning by management in order to keep work running smoothly.

### Conditionals in Loops

Finally, we can use conditionals in loops.  This is great at filtering out certain elements and selecting just what we need.  Let's see this.


```python
greetings = ['hello', 'bonjour', 'hola', 'hallo', 'ciao', 'ola', 'namaste', 'salam']

selected = []

for greeting in greetings:
    if greeting.startswith('h'):
        selected.append(greeting) 

print(selected)
```

    ['hello', 'hola', 'hallo']


The above `for` loop uses a conditional to move through the list of words one by one and check if the word starts with `h`. **If** it does, it adds that word to the `selected` list. Then we print that list of selected words to see which words were copied from the greetings list. 

We can see that our loop and conditional statement were sucessfull and only added in the greetings that started with `'h'`. So by using the `for` loop combined with an `if` statement we can choose elements of a list based on specific criteria.

### Summary

In this lesson, we saw how conditionals allow us to make decisions with our code by only executing code under the `if` statement when the conditional argument is `True` or truthy.  We then saw how we can use the `else` statement to only run code when the conditional argument is `False` or falsy, and as we know, code that is not in a conditional block is still run as normal.  

We examined what is truthy or falsy, and saw that None, 0, empty strings and lists are falsy. If we are unsure, we can use the `bool` function to see a the boolean value of a piece of data. Finally, we saw how by using `if` in a `for` loop we can return a subset of a collection that meets a criteria.
