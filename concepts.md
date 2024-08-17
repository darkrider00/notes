![[Pasted image 20240817172909.png]]

The _order of operations_ (also called _precedence_) of Python math operators is similar to that of mathematics. The ** operator is evaluated first; the *, /, //, and % operators are evaluated next, from left to right; and the + and - operators are evaluated last (also from left to right).

![[Pasted image 20240817173024.png]]

>>> str(0)  
'0'  
>>> str(-3.14)  
'-3.14'  
>>> int('42')  
42  
>>> int('-99')  
-99  
>>> int(1.25)  
1  
>>> int(1.99)  
1  
>>> float('3.14')  
3.14  
>>> float(10)  
10.0

![[Pasted image 20240817173404.png]]

Let’s say the user enters the string '4' for myAge. The string '4' is converted to an integer, so you can add one to it. The result is 5. The str() function converts the result back to a string, so you can concatenate it with the second string, 'in a year.', to create the final message. These evaluation steps would look something like the following:

### flow control

![[Pasted image 20240817173446.png]]

![[Pasted image 20240817173538.png]]

### **Elements of Flow Control**

Flow control statements often start with a part called the _condition_ and are always followed by a block of code called the _clause_. Before you learn about Python’s specific flow control statements, I’ll cover what a condition and a block are.

#### **_Conditions_**

The Boolean expressions you’ve seen so far could all be considered conditions, which are the same thing as expressions; _condition_ is just a more specific name in the context of flow control statements. Conditions always evaluate down to a Boolean value, True or False. A flow control statement decides what to do based on whether its condition is True or False, and almost every flow control statement uses a condition.

#### **_Blocks of Code_**

Lines of Python code can be grouped together in _blocks_. You can tell when a block begins and ends from the indentation of the lines of code. There are three rules for blocks.

- Blocks begin when the indentation increases.
- Blocks can contain other blocks.
- Blocks end when the indentation decreases to zero or to a containing block’s indentation.


### If statement :

![[Pasted image 20240817173736.png]]

### else statement :

![[Pasted image 20240817174054.png]]1

### Elif statements :

![[Pasted image 20240817174131.png]]

![[Pasted image 20240817174145.png]]

```python
name = 'Carol'  
age = 3000  
if name == 'Alice':  
    print('Hi, Alice.')  
elif age < 12:  
    print('You are not Alice, kiddo.')  
else:  
    print('You are neither Alice nor a little kid.')
```

![[Pasted image 20240817174214.png]]

![[Pasted image 20240817174220.png]]

#### **_while Loop Statements_**

- The while keyword
- A condition (that is, an expression that evaluates to True or False)
- A colon
- Starting on the next line, an indented block of code (called the while clause)

```python
spam = 0  
if spam < 5:  
    print('Hello, world.')  
    spam = spam + 1

Here is the code with a while statement:

spam = 0  
while spam < 5:  
    print('Hello, world.')  
    spam = spam + 1
```

	![[Pasted image 20240817174422.png]]

![[Pasted image 20240817174457.png]]

##### **An Annoying while Loop**

```python
➊ name = ''  
➋ while name != 'your name':  
       print('Please type your name.')  
    ➌ name = input()  
➍ print('Thank you!')
```
![[Pasted image 20240817174733.png]]

#### **_break Statements_**

```python
➊ while True:  
       print('Please type your name.')  
    ➋ name = input()  
    ➌ if name == 'your name':  
        ➍ break  
➎ print('Thank you!')
```

![[Pasted image 20240817175404.png]]

#### **_continue Statements_**

```
  while True:  
      print('Who are you?')  
      name = input()  
    ➊ if name != 'Joe':  
        ➋ continue  
       print('Hello, Joe. What is the password? (It is a fish.)')  
    ➌ password = input()  
       if password == 'swordfish':  
        ➍ break  
➎ print('Access granted.')

```
![[Pasted image 20240817175440.png]]


**“TRUTHY” AND “FALSEY” VALUES**

Conditions will consider some values in other data types equivalent to True and False. When used in conditions, 0, 0.0, and '' (the empty string) are considered False, while all other values are considered True. For example, look at the following program:

```
name = ''  
➊ while not name:  
    print('Enter your name:')  
    name = input()  
print('How many guests will you have?')  
numOfGuests = int(input())  
➋ if numOfGuests:  
    ➌ print('Be sure to have enough room for all your guests.')  
print('Done')
```

You can view the execution of this program at _[https://autbor.com/howmanyguests/](https://autbor.com/howmanyguests/)_. If the user enters a blank string for name, then the while statement’s condition will be True ➊, and the program continues to ask for a name. If the value for numOfGuests is not 0 ➋, then the condition is considered to be True, and the program will print a reminder for the user ➌.

You could have entered not name != '' instead of not name, and numOfGuests != 0 instead of numOfGuests, but using the truthy and falsey values can make your code easier to read.

#### **_for Loops and the range() Function_**

- The for keyword
- A variable name
- The in keyword
- A call to the range() method with up to three integers passed to it
- A colon
- Starting on the next line, an indented block of code (called the for clause)

![[Pasted image 20240817175525.png]]

### **Importing Modules**

All Python programs can call a basic set of functions called _built-in functions_, including the print(), input(), and len() functions you’ve seen before. Python also comes with a set of modules called the _standard library_. Each module is a Python program that contains a related group of functions that can be embedded in your programs. For example, the math module has mathematics-related functions, the random module has random number-related functions, and so on.

Before you can use the functions in a module, you must import the module with an import statement. In code, an import statement consists of the following:

- The import keyword
- The name of the module
- Optionally, more module names, as long as they are separated by commas

### **Ending a Program Early with the sys.exit() Function**

```python
import sys  
  
while True:  
    print('Type exit to exit.')  
    response = input()  
    if response == 'exit':  
        sys.exit()  
    print('You typed ' + response + '.')
```
### **A Short Program: Guess the Number**

```python
# This is a guess the number game.  
import random  
secretNumber = random.randint(1, 20)  
print('I am thinking of a number between 1 and 20.')  
  
# Ask the player to guess 6 times.  
for guessesTaken in range(1, 7):  
    print('Take a guess.')  
    guess = int(input())  
  
    if guess < secretNumber:  
        print('Your guess is too low.')  
    elif guess > secretNumber:  
        print('Your guess is too high.')  
    else:  
        break    # This condition is the correct guess!  
  
if guess == secretNumber:  
    print('Good job! You guessed my number in ' + str(guessesTaken) + '  
guesses!')  
else:  
    print('Nope. The number I was thinking of was ' + str(secretNumber))
```
# This is a guess the number game.  
import random  
secretNumber = random.randint(1, 20)

First, a comment at the top of the code explains what the program does. Then, the program imports the random module so that it can use the random.randint() function to generate a number for the user to guess. The return value, a random integer between 1 and 20, is stored in the variable secretNumber.

print('I am thinking of a number between 1 and 20.')  
  
# Ask the player to guess 6 times.  
for guessesTaken in range(1, 7):  
    print('Take a guess.')  
    guess = int(input())

The program tells the player that it has come up with a secret number and will give the player six chances to guess it. The code that lets the player enter a guess and checks that guess is in a for loop that will loop at most six times. The first thing that happens in the loop is that the player types in a guess. Since input() returns a string, its return value is passed straight into int(), which translates the string into an integer value. This gets stored in a variable named guess.

    if guess < secretNumber:  
        print('Your guess is too low.')  
    elif guess > secretNumber:  
        print('Your guess is too high.')

These few lines of code check to see whether the guess is less than or greater than the secret number. In either case, a hint is printed to the screen.

    else:  
        break    # This condition is the correct guess!

If the guess is neither higher nor lower than the secret number, then it must be equal to the secret number—in which case, you want the program execution to break out of the for loop.

if guess == secretNumber:  
    print('Good job! You guessed my number in ' + str(guessesTaken) + ' guesses!')  
else:  
    print('Nope. The number I was thinking of was ' + str(secretNumber))


### **A Short Program: Rock, Paper, Scissors**

Let’s use the programming concepts we’ve learned so far to create a simple rock, paper, scissors game. The output will look like this:
Type the following source code into the file editor, and save the file as _rpsGame.py_:

import random, sys  
  
print('ROCK, PAPER, SCISSORS')  
  
### **A Short Program: Rock, Paper, Scissors**

Let’s use the programming concepts we’ve learned so far to create a simple rock, paper, scissors game. The output will look like this:

ROCK, PAPER, SCISSORS  
0 Wins, 0 Losses, 0 Ties  
Enter your move: (r)ock (p)aper (s)cissors or (q)uit  
p  
PAPER versus...  
PAPER  
It is a tie!  
0 Wins, 1 Losses, 1 Ties  
Enter your move: (r)ock (p)aper (s)cissors or (q)uit  
s  
SCISSORS versus...  
PAPER  
You win!  
1 Wins, 1 Losses, 1 Ties  
Enter your move: (r)ock (p)aper (s)cissors or (q)uit  
q

Type the following source code into the file editor, and save the file as _rpsGame.py_:

```python
import random, sys  
  
print('ROCK, PAPER, SCISSORS')  

wins = 0  
losses = 0  
ties = 0  
  
while True: # The main game loop.  
    print('%s Wins, %s Losses, %s Ties' % (wins, losses, ties))  
    while True: # The player input loop.  
        print('Enter your move: (r)ock (p)aper (s)cissors or (q)uit')  
        playerMove = input()  
        if playerMove == 'q':  
            sys.exit() # Quit the program.  
        if playerMove == 'r' or playerMove == 'p' or playerMove == 's':  
            break # Break out of the player input loop.  
        print('Type one of r, p, s, or q.')  
  
    # Display what the player chose:  
    if playerMove == 'r':  
        print('ROCK versus...')  
    elif playerMove == 'p':  
        print('PAPER versus...')  
    elif playerMove == 's':  
        print('SCISSORS versus...')  
  
    # Display what the computer chose:  
    randomNumber = random.randint(1, 3)  
    if randomNumber == 1:  
        computerMove = 'r'  
        print('ROCK')  
    elif randomNumber == 2:  
        computerMove = 'p'  
        print('PAPER')  
    elif randomNumber == 3:  
        computerMove = 's'  
        print('SCISSORS')  
  
    # Display and record the win/loss/tie:  
    if playerMove == computerMove:  
        print('It is a tie!')  
        ties = ties + 1  
    elif playerMove == 'r' and computerMove == 's':  
        print('You win!')  
        wins = wins + 1  
    elif playerMove == 'p' and computerMove == 'r':  
        print('You win!')  
        wins = wins + 1  
    elif playerMove == 's' and computerMove == 'p':  
        print('You win!')  
        wins = wins + 1  
    elif playerMove == 'r' and computerMove == 'p':  
        print('You lose!')  
        losses = losses + 1  
    elif playerMove == 'p' and computerMove == 's':  
        print('You lose!')  
        losses = losses + 1  
    elif playerMove == 's' and computerMove == 'r':  
        print('You lose!')  
        losses = losses + 1
```

```python
import random, sys  
  
print('ROCK, PAPER, SCISSORS')  
  
# These variables keep track of the number of wins, losses, and ties.  
wins = 0  
losses = 0  
ties = 0
```

First, we import the random and sys module so that our program can call the random.randint() and sys.exit() functions. We also set up three variables to keep track of how many wins, losses, and ties the player has had.

```python
while True: # The main game loop.  
    print('%s Wins, %s Losses, %s Ties' % (wins, losses, ties))  
    while True: # The player input loop.  
        print('Enter your move: (r)ock (p)aper (s)cissors or (q)uit')  
        playerMove = input()  
        if playerMove == 'q':  
            sys.exit() # Quit the program.  
        if playerMove == 'r' or playerMove == 'p' or playerMove == 's':  
            break # Break out of the player input loop.  
        print('Type one of r, p, s, or q.')
```
This program uses a while loop inside of another while loop. The first loop is the main game loop, and a single game of rock, paper, scissors is played on each iteration through this loop. The second loop asks for input from the player, and keeps looping until the player has entered an r, p, s, or q for their move. The r, p, and s correspond to rock, paper, and scissors, respectively, while the q means the player intends to quit. In that case, sys.exit() is called and the program exits. If the player has entered r, p, or s, the execution breaks out of the loop. Otherwise, the program reminds the player to enter r, p, s, or q and goes back to the start of the loop.

```
    # Display what the player chose:  
    if playerMove == 'r':  
        print('ROCK versus...')  
    elif playerMove == 'p':  
        print('PAPER versus...')  
    elif playerMove == 's':  
        print('SCISSORS versus...')

The player’s move is displayed on the screen.

    # Display what the computer chose:  
    randomNumber = random.randint(1, 3)  
    if randomNumber == 1:  
        computerMove = 'r'  
        print('ROCK')  
    elif randomNumber == 2:  
        computerMove = 'p'  
        print('PAPER')  
    elif randomNumber == 3:  
        computerMove = 's'  
        print('SCISSORS')
```

Next, the computer’s move is randomly selected. Since random.randint() can only return a random number, the 1, 2, or 3 integer value it returns is stored in a variable named randomNumber. The program stores a 'r', 'p', or 's' string in computerMove based on the integer in randomNumber, as well as displays the computer’s move.

 # Display and record the win/loss/tie:  
    if playerMove == computerMove:  
        print('It is a tie!')  
        ties = ties + 1  
    elif playerMove == 'r' and computerMove == 's':  
        print('You win!')  
        wins = wins + 1  
    elif playerMove == 'p' and computerMove == 'r':  
        print('You win!')  
        wins = wins + 1  
    elif playerMove == 's' and computerMove == 'p':  
        print('You win!')  
        wins = wins + 1  
    elif playerMove == 'r' and computerMove == 'p':  
        print('You lose!')  
        losses = losses + 1  
    elif playerMove == 'p' and computerMove == 's':  
        print('You lose!')  
        losses = losses + 1  
    elif playerMove == 's' and computerMove == 'r':  
        print('You lose!')  
        losses = losses + 1

### functions 

One special thing to note about parameters is that the value stored in a parameter is forgotten when the function returns.

When an expression is used with a return statement, the return value is what this expression evaluates to. For example, the following program defines a function that returns a different string depending on what number it is passed as an argument.

```python
➊ import random  
  
➋ def getAnswer(answerNumber):  
    ➌ if answerNumber == 1:  
           return 'It is certain'  
       elif answerNumber == 2:  
           return 'It is decidedly so'  
       elif answerNumber == 3:  
           return 'Yes'  
       elif answerNumber == 4:  
           return 'Reply hazy try again'  
       elif answerNumber == 5:  
           return 'Ask again later'  
       elif answerNumber == 6:  
           return 'Concentrate and ask again'  
       elif answerNumber == 7:  
           return 'My reply is no'  
       elif answerNumber == 8:  
           return 'Outlook not so good'  
       elif answerNumber == 9:  
           return 'Very doubtful'  
  
➍ r = random.randint(1, 9)  
➎ fortune = getAnswer(r)  
➏ print(fortune)
```

The getAnswer() function is called with r as the argument ➎. The program execution moves to the top of the getAnswer() function ➌, and the value r is stored in a parameter named answerNumber. Then, depending on the value in answerNumber, the function returns one of many possible string values.

In Python, there is a value called None, which represents the absence of a value. The None value is the only value of the NoneType data type.

This value-without-a-value can be helpful when you need to store something that won’t be confused for a real value in a variable. One place where None is used is as the return value of print().

The print() function displays text on the screen, but it doesn’t need to return anything in the same way len() or input() does. But since all function calls need to evaluate to a return value, print() returns None. To see this in action, enter the following into the interactive shell:

```
>>> spam = print('Hello!')  
Hello!  
>>> None == spam  
True

```

Most arguments are identified by their position in the function call. 

For example, random.randint(1, 10) is different from random.randint(10, 1). 
The function call random.randint(1, 10) will return a random integer between 1 and 10 because the first argument is the low end of the range and the second argument is the high end (while random.randint(10, 1) causes an error).

_eyword arguments_ are identified by the keyword put before them in the function call. Keyword arguments are often used for _optional parameters_. For example, the print() function has the optional parameters end and sep to specify what should be printed at the end of its arguments and between its arguments (separating them), respectively.

```
print('Hello', end='')  
print('World')

the output would look like this:

HelloWorld
```

