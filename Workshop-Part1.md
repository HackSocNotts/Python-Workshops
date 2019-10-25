# Intro to Python
## Session 1

### What will we cover?
In this session, we'll cover the following concepts:

- _**"Hello World"**_, or writing your first line of code
- Variables and Types
- Math Operations
- Conditional Programming (IF statements)
- Functions
- Lists
- For & While loops
- String Operations
- Error handling

If you need help at any point, then raise your hand or ask a mentor - they'll be more than happy to help!
Important keywords are in _italics_ - it can be helpful to remember these.

# Getting started with Python
We're not going to be using a local installation of Python, because it's a lot of time and hassle to get set up if not already. So instead we're going to use glitch, which is an online platform for writing code (usually web code, but we're adapting!).
Visit this link, and click 'Remix to Edit' on the right: https://glitch.com/edit/#!/hacksoc-python

You should now be able to access the files on the right and make edits to them. Most of the code will be written in the *`app.py`* file, so open that up.

We're also going to be executing our code from the online terminal. To access the console on Glitch, click *Tools* => *Logs* => *Console*. The console window can be resized as well.

# Hello World, or writing your first line of code

When learning a new programming language, the first line of code you'll write is "Hello World" - a simple program which just prints "Hello World" to the screen.

In Python, such a program might look something like this:

```python
print("Hello World!")
```
Copy this code into your `app.py` file.

To run this, type `python3 app.py` into your terminal.

If you run this program and it works, congratulations! You just ran your very first line of Python code. If not, don't worry - ask a volunteer to help you get set up!

# Variables and types

A _variable_ is a value in your code that you can change. This is useful for storing values that you might need to use later. You can create variables like this:

```python
testing = 3
```

This creates a _variable_ called "testing", and assigns it with a value of 3. You can then use this variable later on in your code, for example if you want to print its value to the screen:

```python
testing = 3
print(testing)
```

Variables in Python have _types_, representing the type of data that is stored in that variable. When you assign a value to a variable, Python deduces the *type* from the data you assign to the variable. This is called _dynamic typing_.

Note: Some languages use *static typing* where the programmer explicitly states the types of variables. Because of this, in python it's possible to accidentally change the type of a variable, so be careful!

Examples of types include:

- Integers (whole numbers) - `int`
- Strings (blocks of text, e.g. `"Hello World"`) - `str`
- Decimal numbers - `float`
- Booleans (`True` or `False`) - `bool`

You don't have to worry about these for now, but knowing about types can be very important in the future, especially when debugging.

# Math operations

In Python, you can perform maths on numbers using _operators_. For example, if you wish to add two numbers together:

```python
mynumber = 2 + 3
print(mynumber)
```

Essentially what you learned in maths class! 
In this case, we have used the `+` operator to add `2` and `3` together. As a result, the variable `mynumber` has a value of 5.

Examples of some operators you can use are:

- Addition - `+`
- Subtraction - `-`
- Multiplication - `*`
- Division - `/`
- Modulus - `%`
    - The modulus operator returns the remainder of a division.
    - For example, `10 % 3` would return 1, because `10` divided by `3` would give you 3 with a remainder of 1.
- Exponents (Powers) - `**`
    - For example, `3 ** 2` would return 9, because 3 to the power of 2 is 9.

These operators respect *Orders of Operation*, and you can use *Brackets* () in your code as well to adjust the order the statement is evaluated:

```python
mynumber = 5 + 2 * 3 # MyNumber is 11
mynumber = (5 + 2) * 3 # MyNumber is 21
```


# Conditional programming (if statements)

There are times where you might want to run a piece of code only under certain conditions. For that, we have the `if` statement.

An `if` statement in Python looks something like this:

```python
myvariable = 3

if myvariable == 3:
    print("My variable is 3")
```

The part after `if` is the _condition_ - this determines whether the code should run. If the condition is `True`, the code runs. If not, it is skipped over.

The `==` is an operator that checks for _equality_ - this compares the values on either side of it, in this case `myvariable` and `3`, and checks if they are the same. If they are, it returns `True`, otherwise it returns `False`.

Examples of other comparisons you can do include:

- Not equal - `!=`
    - This is `True` if the values on either side are **not** the same. False otherwise.
- Less than - `<`
    - This is `True` if the value on the left is **less than** the value on the right. False otherwise.
- Greater than - `>`
    - Same principle as less than, but is `True` if the value on the left is **greater than** the value on the right. False otherwise.
- Less than or equal to - `<=`, greater than or equal to - `>=`
    - These are `True` if the value on the left is **less than** or **equal to** the value on the right, and vice versa for **greater than** or **equal to**.

Tip - If the wide end points towards the larger number, it's true.

For example, you might have some code that looks like this:

```python
myvalue = 4

if myvalue >= 4:
    print("my value is 4 or more")
```

In this case, the code would run, because the condition is true (`myvalue` is greater than or equal to 4). If you were to change it to a smaller number, the code would no longer work.

You can also have multiple conditions in a single if statement, using `and` & `or`:

```python
myvalue = 4

if myvalue >= 4 and myvalue <= 6:
    print("My value is between 4 and 6 inclusive")
```

In this case, the code only runs if both of the conditions are true. If you were to change the number to something not between 4 or 6, the code would no longer run, because one of the conditions is no longer true. 

Additionally, you can chain if statements together, so that if the first if statement has a value of `False`, another statement will be executed instead. This is done using the `elif` keyword.

```python
myvalue = 4

if myvalue == 5:
    print("My value is 5")
elif myvalue == 6:
    print("My value is 6")
```

You can also choose to run a piece of code if no conditions in your if statement are true, using the `else` keyword:

```python
myvalue = 4

if myvalue == 5:
    print("My value is 5")
elif myvalue == 6:
    print("My value is 6")
else:
    print("My value is neither 5 nor 6")
```

In this case, you would see "My value is neither 5 nor 6" on the screen, because the condition is not true. If you were to change `myvalue` to 5, you would see "My value is 5", and changing it to 6 would show you "My value is 6".

# Functions

Functions are blocks of code you can reuse over and over again, to avoid repeating yourself. In fact, you've been using one throughout this worksheet - `print()` is a function!

To create your own function, you _declare_ it like this:

```python
def myfunction():
    print("This is my function!")
```

The `def` keyword tells Python that the code that follows is a function. In this case, our function is called `myfunction`.

You can then _call_ these functions like so:

```python
myfunction()
```

This will run the code inside your function.

You can also _pass_ values to a function, by declaring it like so (these are called _arguments_):

```python
def myfunction(number):
    print("My number is " + str(number))

myfunction(3)
```

Note the "`number`" inside the brackets. This automatically creates a variable, called `number`, for you to use inside that function. You pass in the number by putting it between the brackets when you call the function.

Another commonly used function as seen above is the `str()` function, which allows us to convert a number into to a `string` - allowing us to _concatenate_ or _join_ the number onto the string, which you couldn't do normally as they are different types!

You can also have multiple _arguments_ by separating them with commas, like so:

```python
def myfunction(number1, number2):
    print(number1 + number2)

myfunction(1, 2)
```

Functions can also _return_ a value as its output. You can assign the output to a variable. This is useful if you want to use the result of a function for something else:

```python
def add3numbers(number1, number2, number3):
    result = number1 + number2 + number3
    return result

mynumber = add3numbers(1, 2, 3)
print(mynumber)
```

In this case, the value of `mynumber` is whatever gets returned by `add3numbers()` - in this instance, 6.

# Lists

Lists are a special _type_ in Python - they contain multiple items which you can access individually. You can create a list like this:

```python
fruits = ["apple", "banana", "orange", "pineapple"]
```

This creates a list, called `fruits`, with four items, `"apple"`, `"banana"`, `"orange"` and `"pineapple"`.

You can get the number of items in a list using the `len()` function:

```python
fruits = ["apple", "banana", "orange", "pineapple"]
len(fruits)
```

`len()` returns the number of items in a list, in this case `len()` returns 4.

If you want to add an item to a list, you can use the `append()` _method_ on your list, like so:

```python
fruits.append("tangerine")
print(fruits)
len(fruits)
```

This will add "tangerine" to the end of the list, and show that by printing the new list of five items, as well as printing the number `5`, the new length.

To access a specific item in a list, you _index_ it, like so:

```python
print(fruits[2]) # Should print 'orange'
```
Some of you may wonder why this prints 'orange' and not 'banana'. That's because computers count from zero! Arrays are *zero indexed* which means the value `0` gets the first item, `1` gets the second item, and so on.

# Loops
Loops are used to run pieces of code repeatedly under certain conditions. Python has two types of loop: the `for` loop and the `while` loop.

A `for` loop allows you to run a piece of code for each item in a list. This is called _iterating_ over a list. You can use the list of fruits from earlier in a for loop, like so:

```python
fruits = ["apple", "banana", "orange", "pineapple"]

for fruit in fruits:
    print(fruit)
```

`fruits` is the name of the existing list you want to _iterate_ over, and `fruit` is a newly created variable (often called an iteration variable) for the "current" item in the list being iterated over. This code would output the following:
```
apple
banana
orange
pineapple
```

If you want to run a piece of code a given number of times, you can do so using the `range()` function:

```python
for i in range(100):
    print(i)
```

The code above prints all positive integers below 100, including 0. This works because the `range(100)` function returns a list of all numbers between 0 and 99 (100 numbers, computers count from zero!).

This is a really useful way of getting code to run a specific number of times. Sometimes the `i` variable (the iteration variable) is not even used!

A `while` loop allows a piece of code to run while a certain condition is true. This is similar to an `if` statement, but instead of running a piece of code if a condition is met, the code is run forever until the condition is no longer met! For example, here is printing all of the numbers from 0 to 100 using a while loop instead of a for loop:

```python
current_number = 0

while current_number < 100:
    print(current_number)
    current_number = current_number + 1
```

The code continues to run while the condition in the `while` statement is true. Because we add one to the number every time, the code will eventually stop running when `current_number` becomes greater than 100.

Be careful - if the condition in your while loop is always true, your code will run infinitely. Don't worry if this happens - if you get stuck in a loop, you can just press `Control-C` on your keyboard to stop your program from running.

Although you can usually write looped code using either `for` loops or `while` loops, one is often more suitable for a task than the other.

For finer control, you can use the keywords `continue` and `break`.

- `continue` - Ends the current iteration of the loop now, and begins the next iteration.
- `break` - Terminates the loop

```python
for i in range(100):
    if (i > 50):
        break
    if i % 2 == 0:
        continue
    print(i)
````

The code above will print the odd numbers between 0 and 50 (`continue` will skip the iterations that are even) and then will `break` the loop once `i` is greater than 50. 
# String operations

There are some operations you can do on strings (text) that might come in useful.

One operation you can do is checking if your string contains certain text - this is called checking for a _substring_ (a string within a string).

In Python, you can do it like this:

```python
mystring = "This is a quick test."

if "quick" in mystring:
    print("Speedy!")
```

We're using the `in` keyword to check if `"quick"` is contained in `mystring` - in this case, it is, so the condition is true and our code can run. You can also use `in` with lists, to check if a list contains an item.

Another operation you can do is combining strings together - this is called _concatenation_. We already saw this earlier when we talked about functions!

In Python, you can do it using the `+` operator on `strings` (unlike numerical values, where `+` will add the values together):

```python
mystring = "Hello " + "World!"
print(mystring)
```

This code will print `Hello World!` to the screen. 

# Error handling
Sometimes, when running our Python code, errors can occur which require our attention. For example, if we try to divide a number by zero:

```python
myvariable = 3 / 0
```

Our code will crash with the following error:

`ZeroDivisionError: division by zero`

We can catch this error using a `try` block:

```python
myvariable = 0
try:
    myvariable = 3 / 0
```

Note that you need to declare any variables you want to create **outside** of the try block, otherwise you can't access them when the block finishes.

This code won't work on its own - each `try` block needs its own corresponding `except` block:

```python
myvariable = 0
try:
    myvariable = 3 / 0
except ZeroDivisionError:
    print("You tried to divide by zero")
```

This catches any `ZeroDivisionError` when one occurs - the code inside the `except` block is run if the code inside the `try` block _throws_ an error.
