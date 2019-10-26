# Intro to Python
## Session 3

### What will we cover?
In this session, we'll put (almost) everything you've learned into making a hangman game!

If you need help at any point, then raise your hand or ask a mentor - they'll be more than happy to help!
Important keywords are in _italics_ - it can be helpful to remember these.

# Getting Started
First things first, lets get the core of the *game loop* working. We could break this into separate .py files, but for simplicity's sake we'll keep it all in one file. There are also so many ways of doing this, the way shown here is only one way of implementing this game.

Let's take the users name, shall we?

In an empty file (either create a new .py file, or delete the one you were using), enter the following code:


```python
name = input("What is your name?\n")
print("Hello " + name + "\n")
```
This will allow the user to enter their name. We will use this to prompt the user later. Below this, type the following code:

```python
while True:
  print("hello!")
```

This loop will print `"hello"` forever, or until you hit Ctrl-C and stop the program. We want our hangman game to run forever until the user stops it.

What's the most important thing for a game of hangman? A word! Above the `while True` loop, create a function called `pickWord()`, and have it simply return the string `"python"` for now:

```python
def pickWord():
  return "python"

while True:
  word = pickWord()
  print(word)
```

We now have a word for our hangman game! Lets set up the game state so we can actually play the game. We need: 
- a 'blanked out' list, the same size as the word and which will be populated by our correct guesses.
- a list of all the letters in the alphabet, so we can tell what letters the player can still guess.
- a life counter

We can do the blanked out string and the list of all letters using list comprehensions:

```python
while True:
  word = pickWord()
  blankedWord = ["*" for character in word]
  availableGuesses = [str(chr(i)) for i in range(97, 123)]
  life = 10
```

# Inputting Letters

The next thing to do is allow the user to start inputting letters. Just below this code, create another `while True` loop which will contain our 'guessing' logic. Indentation is important!

```python
# Our 'game' loop
while True:
  word = pickWord()
  blankedWord = ["*" for character in word]
  availableGuesses = [str(chr(i)) for i in range(97, 123)]
  life = 10

  # Our 'guessing' loop
  while True:
    print("Current Word: " + "".join(blankedWord))
    print("Letters Remaining: " + "".join(availableGuesses))
    print("Lives Remaining: " + str(life))
    guess = input("Please guess a letter, " + name + "\n")
```

But what if the user doesn't enter a letter, or enters 2 letters, or nothing? We need to check for all of these, and reset the loop in that case:

```python
    if len(guess) != 1 or not guess.isalpha():
      print("Please enter a valid letter!\n")
      continue
```

Also, what if the player has guessed that letter already?

```python
    if guess not in availableGuesses:
      print("You have already guessed this letter!\n")
      continue
```

Right now, our code should look something like this:

```python
name = input("What is your name?\n")
print("Hello " + name + "\n")

def pickWord():
  return "python"

# Our 'game' loop
while True:
  word = pickWord()
  blankedWord = ["*" for character in word]
  availableGuesses = [str(chr(i)) for i in range(97, 123)]
  life = 10

  # Our 'guessing' loop
  while True:
    print("Current Word: " + "".join(blankedWord))
    print("Letters Remaining: " + "".join(availableGuesses))
    print("Lives Remaining: " + str(life))
    guess = input("Please guess a letter, " + name + "\n")

    if len(guess) != 1 or not guess.isalpha():
      print("Please enter a valid letter!\n")
      continue

    if guess not in availableGuesses:
      print("You have already guessed this letter!\n")
      continue
```

# Calculating Successful Guesses

If the code gets to this point, we know that it's a valid guess, so we can remove the guess from the `availableGuesses` list. What we now need to determine is if it was a 'successful' guess.

The check for that, is to see if the `guess` is in the actual word:

```python
    availableGuesses.remove(guess)
    if guess in word:
      print("Yes! " + guess + " is in the word!")
    else:
      print("Sorry, " + guess + " is not in the word...")
```

Now, in order to actually progress the game, we need to update our game state variables! First, let's remove this letter from our available guesses:

```python
    if guess in word:
      print("Yes! " + guess + " is in the word!\n")
    else:
      print("Sorry, " + guess + " is not in the word...\n")
```

Now, we need to update the blanked word to fill in the `*`s with the actual guessed character. We can do that with a for loop. Put this underneath `print("Yes! " + guess + " is in the word!\n")`
```python
      for i in range(len(word)): # for i from 0 to (wordlength - 1)
        if word[i] == guess:
          blankedWord[i] = guess   
```

Again, this isn't the simplest way to do this, you can almost certainly do this in a list comprehension, but for simplicity's sake let's leave it at that.

Now, we can actually check to see if we won, by checking `blankedWord` and seeing if there are any `*`s left!

```python
      if "*" not in blankedWord:
        print("You won!")    
        answer = input("Would you like to go again? (y/n): ")
        if (answer.lower() in ["no", "n"]):
          print("Goodbye")
          exit(0)
        else
          print("Let's play again!\n")
          break
```

This should be what our code looks like now:

```python
name = input("What is your name?\n")
print("Hello " + name + "\n")

def pickWord():
  return "python"

# Our 'game' loop
while True:
  word = pickWord()
  blankedWord = ["*" for character in word]
  availableGuesses = [str(chr(i)) for i in range(97, 123)]
  life = 10

  # Our 'guessing' loop
  while True:
    print("Current Word: " + "".join(blankedWord))
    print("Letters Remaining: " + "".join(availableGuesses))
    print("Lives Remaining: " + str(life))
    guess = input("Please guess a letter, " + name + "\n")

    # If not entered one character, or it isn't an alphabet character, retry.
    if len(guess) != 1 or not guess.isalpha():
      print("Please enter a valid letter!\n")
      continue

    # If not an available guess, retry
    if guess not in availableGuesses:
      print("You have already guessed this letter!\n")
      continue

    # We know that it's a successful guess, so remove from the list
    availableGuesses.remove(guess)

    # If the guess is in the word, process and check if won.
    if guess in word:
      print("Yes! " + guess + " is in the word!\n")

      # replace * in blankedWord with correct value
      for i in range(len(word)): # for i from 0 to (wordlength - 1)
        if word[i] == guess:
          blankedWord[i] = guess   

      # If there are no *, the word has been guessed.
      if "*" not in blankedWord:
        print("You won!")    

        # Ask for game restart
        answer = input("Would you like to go again? (y/n): ")
        if (answer.lower() in ["no", "n"]):
          print("Goodbye")
          exit(0)
        else:
          print("Let's play again!\n")
          break

    else:
      print("Sorry, " + guess + " is not in the word...\n")
```

# Incorrect guesses

Now to handle incorrect guesses. First we remove one from your life, and then we check to see if you're out of lives:

```python
    else:
      print("Sorry, " + guess + " is not in the word...\n")
      life = life -1 # Remove one from life

      # If out of lives, ask for game restart.
      if life <= 0:
        print("Game Over!")
        answer = input("Would you like to go again? (y/n): ")
        if (answer.lower() in ["no", "n"]):
          print("Goodbye")
          exit(0)
        else:
          print("Let's play again!\n")
          break
```

# File I/O

Finally, we should probably get a bunch of new words in there no?
On the left in Glitch, click `New File`, call it `words.txt` or similar and then click `Add File`. Open that file, and on separate lines, write as many words as you want! Make sure there are no spaces or punctuation, only words on separate lines.

Once you've done that, go back to the .js file, and go to the very top. We need to pick a word randomly from the list in the file, and we'll use a function from the *standard library module* called `random`.

```python
import random

file = open("words.txt", "r")
words = file.read().splitlines()
file.close()

name = input("What is your name?\n")
print("Hello " + name + "\n")

def pickWord():
  return random.choice(words)
```

# Finally:

Here is the code as it stands now:

```python
import random

file = open("words.txt", "r")
words = file.read().splitlines()
file.close()

name = input("What is your name?\n")
print("Hello " + name + "\n")

def pickWord():
  return random.choice(words)

# Our 'game' loop
while True:
  word = pickWord()
  blankedWord = ["*" for character in word]
  availableGuesses = [str(chr(i)) for i in range(97, 123)]
  life = 10

  # Our 'guessing' loop
  while True:
    print("Current Word: " + "".join(blankedWord))
    print("Letters Remaining: " + "".join(availableGuesses))
    print("Lives Remaining: " + str(life))
    guess = input("Please guess a letter, " + name + "\n")

    # If not entered one character, or it isn't an alphabet character, retry.
    if len(guess) != 1 or not guess.isalpha():
      print("Please enter a valid letter!\n")
      continue

    # If not an available guess, retry
    if guess not in availableGuesses:
      print("You have already guessed this letter!\n")
      continue

    # We know that it's a successful guess, so remove from the list
    availableGuesses.remove(guess)

    # If the guess is in the word, process and check if won.
    if guess in word:
      print("Yes! " + guess + " is in the word!\n")

      # replace * in blankedWord with correct value
      for i in range(len(word)): # for i from 0 to (wordlength - 1)
        if word[i] == guess:
          blankedWord[i] = guess   

      # If there are no *, the word has been guessed.
      if "*" not in blankedWord:
        print("You won!")    

        # Ask for game restart
        answer = input("Would you like to go again? (y/n): ")
        if (answer.lower() in ["no", "n"]):
          print("Goodbye")
          exit(0)
        else:
          print("Let's play again!\n")
          break

    else:
      print("Sorry, " + guess + " is not in the word...\n")
      life = life -1 # Remove one from life

      # If out of lives, ask for game restart.
      if life <= 0:
        print("Game Over!")
        answer = input("Would you like to go again? (y/n): ")
        if (answer.lower() in ["no", "n"]):
          print("Goodbye")
          exit(0)
        else:
          print("Let's play again!\n")
          break
```

# Possible Improvements
- Replace state variables with a dictionary.
  - state = {"life": 10, "blankedWord" : *etc*}
- Split into multiple files.
- Some repeated code (do you want to try again?)
  - Split into function?
- random.choice() can pick the same option multiple times, maybe assign a weight so it doesn't pick the same words over again?
  - Tuples
- *Maybe a command line representation of actual hangman*?

# Most important tip of all
- Don't be afraid if you don't know what something is!
- This was not all-encompassing, python is a *big* language.

If you come across a piece of syntax that you don't understand, google it! The internet is an amazing resource for programmers, don't expect to memorise everything you've learned today!
