---
title: Writing Functions
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain and identify the difference between function definition and function call.
- Write a function that takes a small, fixed number of arguments and produces a single result.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I create my own functions?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Break programs down into functions to make them easier to understand.

- Human beings can only keep a few items in working memory at a time.
- Understand larger/more complicated ideas by understanding and combining pieces.
  - Components in a machine.
  - Lemmas when proving theorems.
- Functions serve the same purpose in programs.
  - *Encapsulate* complexity so that we can treat it as a single "thing".
- Also enables *re-use*.
  - Write one time, use many times.

## Define a function using `def` with a name, parameters, and a block of code.

- Begin the definition of a new function with `def`.
- Followed by the name of the function.
  - Must obey the same rules as variable names.
- Then *parameters* in parentheses.
  - Empty parentheses if the function doesn't take any inputs.
  - We will discuss this in detail in a moment.
- Then a colon.
- Then an indented block of code.

```python
def print_greeting():
    print('Hello!')
```

## Defining a function does not run it.

- Defining a function does not run it.
  - Like assigning a value to a variable.
- Must call the function to execute the code it contains.
- The commands for the function are read and stored after the `def` block, but not actually executed until the function is called later on.
  - Imagine getting a recipe card and keeping it in your kitchen.  You can cook it anytime, but you haven't completed any of the steps until you start that cooking process.
  - This means that Python won't complain about problems until you call the function.  More specifically, just because the definition of a function runs without error doesn't mean that there won't be errors when it executes later.

```python
print_greeting()
```

```output
Hello!
```

## Arguments in call are matched to parameters in definition.

- Functions are most useful when they can operate on different data.
- Specify *parameters* when defining a function.
  - These become variables when the function is executed.
  - Are assigned the arguments in the call (i.e., the values passed to the function).

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

- Via [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705):
  `()` contains the ingredients for the function
  while the body contains the recipe.

## Functions may return a result to their caller using `return`.

- Use `return ...` to give a value back to the caller.
- May occur anywhere in the function.
- But functions are easier to understand if `return` occurs:
  - At the start to handle special cases.
  - At the very end, with a final result.

```python
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
```

```python
a = average([1, 3, 4])
print('average of actual values:', a)
```

```output
2.6666666666666665
```

```python
print('average of empty list:', average([]))
```

```output
None
```

- Remember: [every function returns something](04-built-in.md).
- A function that doesn't explicitly `return` a value automatically returns `None`.

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

```output
1871/3/19
result of call is: None
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Definition and Use

What does the following program print?

```python
def report(pressure):
    print('pressure is', pressure)

report(22.5)
```

:::::::::::::::  solution

## Solution

```output
pressure is 22.5
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Order of Operations

The example above:

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

printed:

```output
1871/3/19
result of call is: None
```

Explain why the two lines of output appeared in the order they did.

:::::::::::::::  solution

## Solution

Each line of Python code is executed in order, regardless of whether that line calls
out to a function, which may call out to other functions, or a
variable assignment. In this case, the second line call to `print` will not execute until
the result of `print_date` is complete in the first line.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulation

Fill in the blanks to create a function that takes a single filename as an argument,
loads the data in the file named by the argument,
and returns the minimum value in that data.

```python
import pandas

def min_in_data(____):
    data = ____
    return ____
```

:::::::::::::::  solution

## Solution

```python
import pandas

def min_in_data(filename):
    data = pandas.read_csv(filename)
    return data.min()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Find the First

Fill in the blanks to create a function that takes a list of numbers as an argument
and returns the first negative value in the list.
What does your function do if the list is empty?

```python
def first_negative(values):
    for v in ____:
        if ____:
            return ____
```

:::::::::::::::  solution

## Solution

```python
def first_negative(values):
    for v in values:
        if v < 0:
            return v
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Calling by Name

What does this short program print?

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(day=1, month=2, year=2003)
```

1. When have you seen a function call like this before?
2. When and why is it useful to call functions this way?
  {: .python}

:::::::::::::::  solution

## Solution

The program prints:

```output
2003/2/1
```

It is useful to call a function with named arguments to ensure that the
values of each argument are assigned to the intended argument in the
function. This allows the order of arguments to be specified independently
of how they are defined in the function itself.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulate of If/Print Block

The code below will run on a label-printer for chicken eggs.  A digital scale will report a chicken egg mass (in grams) to the computer and then the computer will print a label.

Please re-write the code so that the if-block is folded into a function.

```python
 import random
 for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass=70+20.0*(2.0*random.random()-1.0)

    print(mass)
   
    #egg sizing machinery prints a label
    if(mass>=85):
       print("jumbo")
    elif(mass>=70):
       print("large")
    elif(mass<70 and mass>=55):
       print("medium")
    else:
       print("small")
```

The simplified program  follows.  What function definition will make it functional?

```python
 # revised version
 import random
 for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass=70+20.0*(2.0*random.random()-1.0)

    print(mass,print_egg_label(mass))    

```

1. Create a function definition for `print_egg_label()` that will work with the revised program above.  Note, the function's return value will be significant. Sample output might be `71.23 large`.
2. A dirty egg might have a mass of more than 90 grams, and a spoiled or broken egg will probably have a mass that's less than 50 grams.  Modify your `print_egg_label()` function to account for these error conditions. Sample output could be `25 too light, probably spoiled`.

:::::::::::::::  solution

## Solution

```python
def print_egg_label(mass):
  if(mass>=90):
     print(mass, "dirty")
  elif(mass>=85):
     print(mass, "jumbo")
  elif(mass>=70):
     print(mass, "large")
  elif(mass<70 and mass>=55):
     print(mass, "medium")
  else:
     print(mass, "too light, probably spoiled")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulating Data Analysis

Assume that the following code has been executed:

```python
import pandas

df = pandas.read_csv('gapminder_gdp_asia.csv', index_col=0)
japan = df.ix['Japan']
```

1. Complete the statements below to obtain the average GDP for Japan
  across the years reported for the 1980s.

```python
year = 1983
gdp_decade = 'gdpPercap_' + str(year // ____)
avg = (japan.ix[gdp_decade + ___] + japan.ix[gdp_decade + ___]) / 2
```

2. Abstract the code above into a single function.

```python
def avg_gdp_in_decade(country, continent, year):
    df = pd.read_csv('gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
    ____
    ____
    ____
    return avg
```

3. How would you generalize this function
  if you did not know beforehand which specific years occurred as columns in the data?
  For instance, what if we also had data from years ending in 1 and 9 for each decade?
  (Hint: use the columns to filter out the ones that correspond to the decade,
  instead of enumerating them in the code.)

:::::::::::::::  solution

## Solution

1. 
```python
year = 1983
gdp_decade = 'gdpPercap_' + str(year // 10)
avg = (japan.ix[gdp_decade + '2'] + japan.ix[gdp_decade + '7']) / 2
```

2. 
```python
def avg_gdp_in_decade(country, continent, year):
    df = pd.read_csv('gapminder_gdp_' + continent + '.csv', index_col=0)
    c = df.ix[country]
    gdp_decade = 'gdpPercap_' + str(year // 10)
    avg = (c.ix[gdp_decade + '2'] + c.ix[gdp_decade + '7'])/2
    return avg
```

3. We need to loop over the reported years
  to obtain the average for the relevant ones in the data.

```python
def avg_gdp_in_decade(country, continent, year):
    df = pd.read_csv('gapminder_gdp_' + continent + '.csv', index_col=0)
    c = df.ix[country] 
    gdp_decade = 'gdpPercap_' + str(year // 10)
    total = 0.0
    num_years = 0
    for yr_header in c.index: # c's index contains reported years
        if yr_header.startswith(gdp_decade):
            total = total + c.ix[yr_header]
            num_years = num_years + 1
    return total/num_years
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Break programs down into functions to make them easier to understand.
- Define a function using `def` with a name, parameters, and a block of code.
- Defining a function does not run it.
- Arguments in call are matched to parameters in definition.
- Functions may return a result to their caller using `return`.

::::::::::::::::::::::::::::::::::::::::::::::::::


