# Intro to Python
## Session 2

### What will we cover?
In this session, we'll cover the following concepts:

- File Input/Output
- Tuples
- Dictionaries
- List Comprehensions
- Classes

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

# Tuples
