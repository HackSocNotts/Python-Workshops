# Intro to Python
## Session 2

### What will we cover?
In this session, we'll cover the following concepts:

- File Input/Output
- Console Input
- Tuples
- Dictionaries
- List Comprehensions

If you need help at any point, then raise your hand or ask a mentor - they'll be more than happy to help!
Important keywords are in _italics_ - it can be helpful to remember these.

# File Input/Output

We've done a lot of `pure` programming, that is - programming with no side-effects, or external outputs. What if we want to save some data we've created to a file? What if we want to read a file into our program? Thankfully, Python gives us the tools to do so!

To *open* a file (or *create* one if one doesn't exist) we run the function `open`:

```python
myfile = open("/tmp/myfile.txt", "w+")
```

This will open a file, and return an object that allows us to read/write to the object. The second argument specifies what *mode* we want to open the file in, see all of the available modes below:

- "r" - Read - Default value. Opens a file for reading, error if the file does not exist (`FileNotFoundError`).
- "a" - Append - Opens a file for appending, creates the file if it does not exist.
- "w" - Write - Opens a file for writing, creates the file if it does not exist. WILL DELETE ANYTHING ALREADY IN THE FILE!
- "x" - Create - Creates the specified file, returns an error (`FileExistsError`) if the file already exists.
- "w+" - Read and Write - Opens a file for reading and writing. WILL DELETE ANYTHING ALREADY IN THE FILE!
- "a+" - Read and Append - Opens a file for reading and appending.
- Many more combinations of these.

A general `IOError` will be thrown if the file cannot be read/created for any reason.

For now, let's work with `w+` as it clears the file each time we open it, so the file won't keep getting bigger.

To write to the file, we use the `write()` function, and then we `close()` the file after we're done.

```python
myfile.write("This is what I want to write")
myfile.close()
```

If you execute this, and then run the command `cat /tmp/myfile.txt` in the terminal, you should see whatever text you passed into `write()` appear!

Change your code to this and execute it, and take a look at the output. Notice anything?
```python
x = open("/tmp/myfile.txt", "w+")

x.write("Hello")
x.write("Goodbye")

x.close()
```

Hello and Goodbye are printed on the same line! Python doesn't automatically space `write()` calls, so if we want them to have a new line or a space between them we need to put that there explicitly. 

Newlines can be inserted using the `\n` *escape character*. When written to a file or printed to a console, `\n` is turned into a newline.

```python
x = open("/tmp/myfile.txt", "w+")

x.write("Hello\n")
x.write("Goodbye ")
x.write("Friend")
# File should be:
#Hello
#Goodbye Friend
x.close()
```

Running this code multiple times won't change the contents of the file, as the `w` tag means that the file is emptied when opened. If you switch this with the `a` tag, then new `write()` calls append to the file, but you need to make sure the file exists first!

To read from a file, you use the `read()` function!

```python
x = open("readable.txt", "r")

data = x.read()
print(data) #"This is readable text"
x.close()
```

# Console Reading
Although File I/O is important, it's sometimes unnecessary for simple command-line applications. For that, we can input values directly into the console!

The `input()` function waits for input from the user before continuing execution of the program. You can optionally pass it a *prompt* that will be displayed to the user:

```python
print("Hello there!")
userInput = input("What is your favorite number?")
print("Your favorite number is " + userInput)
```

This code as it stands doesn't actually do any number checking, you can type in anything! To fix this, we can use the `string.isnumeric()` function to check if a string only contains numeric characters:

```python
print("Hello there!")
userInput = input("What is your favorite number? ")
if userinput.isnumeric():
    print("Your favorite number is " + userInput)
else:
    print("That wasn't a number!")
```

This is a basic *validation* check.
We can then use the `int()` function to convert our `string` to an `int`, which allows us to use it in mathematical expressions!

```python
print("Hello there!")
userInput = input("What is your favorite number? ")
if userInput.isnumeric():
    print("Your favorite number is " + userInput)
    value = int(userInput) + 5
    print("Adding 5 to that number gives us " + str(value)) # using str() to convert it back to a string!
else:
    print("That wasn't a number!")
```

# Tuples (tuh-ple or too-ple)
If a list is a mutable container of mutable objects, a tuple is an immutable container of immutable objects!

Sounds confusing? This just means that a list can be resized and reordered, and the items within a list can be changed, whereas a tuple has a fixed size, and its contents are constant!

Still confused? Let's get into it. 

```python
tuple1 = (1,3,4,6,9) # We create tuples using () instead of [] like for lists.

firstValue = tuple1[2] # Index the tuple at position 2
print(firstvalue) # Prints "4"

for i in tuple1: # Iterate over the tuple
  print(i) # Prints the numbers 1-5 on separate lines
```

So far it seems pretty similar to a list, right? Well this code won't work:

```python
tuple2 = (1,2,2,4,5)
tuple2[2] = 3 # Will throw an error
```

As stated previously, tuples are immutable, meaning we can't resize them, or change their values. But with all these limitations, why use tuples? 

Tuples allow us to logically group pieces of data together, for easier access and better storage. For example, say you're making a game and you need to store a list of cartesian coordinates (x & y positions on a grid). Tuples allow you to do this very nicely:

```python
coordinates = [(5,4), (2,3), (1,2), (7,2)]
for c in coordinates:
  print("X: " + str(c[0]) + "  Y: " + str(c[1]))
```
Now, each tuple corresponds to a pair of x,y values! Iterating through the list with a for loop will give us that tuple, which we then print the X and Y values of. Much more structured than two separate lists!

Additionally, tuples can be used to _return_ more than one item from a function!

```python
def twoItemFunction(myInput):
  return (myInput, myInput + 1) 
```

The code above simply takes some numeric input N, and returns a tuple of (N, N+1). Obviously this is a simple example, but returning multiple values like this has really powerful implications. 

For example, like mentioned earlier, when working with coordinates it's much nicer to return two coordinates from one function than to need to call two separate functions to get an X and a Y coordinate.

# Dictionaries

Unlike Lists and Tuples, dictionaries create a mapping between a set of *key* objects and a set of *value* objects. They are also mutable just as list are. Let's create a basic one! 

```python
daniel = {
  #Key        #Value
  "name"    : "daniel", 
  "age"     : 21, 
  "role"    : "dev officer", 
  "degree"  : (4, "integrated masters")
}
print(daniel)
```
This dictionary describes me! In order to access an individual element from a tuple, you *index* it like you would an list or tuple, except you use the *key* value as the index!

```python
daniel = {
  #Key        #Value
  "name"    : "daniel", 
  "age"     : 21, 
  "role"    : "dev officer", 
  "degree"  : (4, "integrated masters")
}
print(daniel["name"]) # prints 'daniel'
print(daniel["degree"]) # prints (4, "integrated masters")
```

To add a new key-value part to a dictionary, you *index* the list with the new key, and then assign it a new *value*.

```python
daniel["years programming"] = 6
```

We can also perform checks to see if a key can be found in a dictionary, using the `in` (and optionally `not`) keywords. 

```python
if "years programming" not in daniel:
  daniel["years programming"] = 6
```

Side Note: `in` and `not` can be used in the same way for lists and tuples! `in` is an operator that checks for items being inside *containers* like *lists* and *tuples*, and therefore returns `True` or `False`. This lets us use these as conditions for `if` statements and *loops*.

```python
1 in [1,2,3] # is True
```

# List Comprehensions

List comprehensions provide a concise way to create lists. Using syntax we've already seen before, complicated multi-step list creation can be made really simple! This is difficult to explain, so let's just get into an example.

```python
oldList = [1,2,3,4,5]
newList = []
for i in oldList:
  newList.append(i+1)
```

This code copies data from one list to a new list, while adding 1 to each value. But, as a list comprehension, it looks something like this:

```python
oldList = [1,2,3,4,5]
newList = [i+1 for i in oldList]
print (newList) # [2,3,4,5,6]
```

These two are functionally identical! 

- (i+1) -  The expression that is used for each element of the new list (in our case, 2, 3, 4, etc).
- (for i in oldlist) - Looks very similar to a for loop! This is creating our iterating variable, and which list we want to iterate through!
- [] - The square brackets around the expression signify it is a list comprehension.

This is a really simple example, but it can get more complicated:

```python
newList = [i+1 for i in oldList if i != 3]
print(newList) # [2,3,5,6]
``` 

We can put conditions in there as well!

Here are some more simple examples:
```python
squares = [x**2 for x in range(10)] # List of first 10 square numbers [1,4,9,etc]

listOfWords = ["My", "List", "Of", "Words"]
items = [ word[0] for word in listOfWords ] # List of first letter of each word in the list ["M","L","O","W"]

# We can also iterate through Strings!
string = "My 12345 String"
numbers = [x for x in string if x.isdigit()] # "12345" or ["1","2","3","4","5"] - they are equivalent!
```

This seems pretty powerful, but right now it's essentially turning one list into another. Can we go deeper?

Yes! We can make a list comprehension over 2 lists!

```python
def sum(a,b):
  return a + b

newList = [sum(x,y) for x in [10,20,30] for y in [1,2,3]]

print(newList) # [11, 12, 13, 21, 22, 23, 31, 32, 33]

# This is equivalent to:

newList = []
for x in [10, 20, 30]:
  for y in [1, 2, 3]:
    newList.push(sum(x,y))
```

Here's a bonus list comprehension, see if you can figure out what it does!
```python
mylist = [[1,2,3],[4,5,6],[7,8]]
newlist = [y for x in mylist for y in x]
print(newlist) #???
```
This list comprehension takes a list of lists, and *flattens* them, by removing the inner lists so you are left with a single list of numbers.

You can also put list comprehensions *inside* list comprehensions!

```python
matrix = [[j for j in range(5)] for i in range(5)] 
print(matrix) # [[0,1,2,3,4],[0,1,2,3,4],...]
```
This uses the value of the inner list comprehension to construct the list! This specific example creates a 2-dimensional list (a list within a list), where each sub-list contains the values 0-4.

