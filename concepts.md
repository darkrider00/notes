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

