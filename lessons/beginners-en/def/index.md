# Functions
In the previous [lesson]({{ lesson_url('beginners/functions') }}) 
we were working with functions that were written by someone else - they are
already built-in in Python.


```python
from math import pi

print(pi)
```

Today we will learn how to code our own functions
because we might need some tasks to run repeatedly. 

It's not that difficult.


```python
def  find_perimeter( width ,  height ): 
    "Returns the rectangle's perimeter of the given sides" 
    return  2 * (width  +  height)

print ( find_perimeter(4 ,  2))

```

How does that work?

Function is *defined* with command `def` and right after that
you have to write name of the function brackets (which may contain 
*arguments*) and then, of course, colon (we have already said that when there
is a colon everything that belongs to in our case now the function
must be intended). That intended code is called *body of a function* and it
contains commands that the function performs. There can be more commands 
including `if`, `loop`, etc.
The body can start with *documentation comment* which describes what
the function is doing.

A function can return some value with `return` command.


```python
def  print_score(name, score): 
    print (name, 'score is', score) 
    if score > 1000:
        print('World record!') 
    elif score > 100: 
        print('Perfect!') 
    elif score > 10: 
        print('Passable.') 
    elif score > 1: 
        print('At least something') 
    else: 
        print('Maybe next time')

print_score('Your', 256) 
print_score('Denis', 5)

```

When you are calling a function the arguments you write in the brackets
will be assign to the variables that specified function also has in
brackets.
So when you will call our new function with print_score('Your', 256)
you can imagine that it's doing following:


```python
name = 'Your'
score = 256

print (name, 'score is', score) 
if score > 1000:
    ... #etc.
        
```
## Return

The `return` command *terminates* the function and returns the value 
out of the function. You can use in only in functions.

So it behaves like `break` which terminates cycles.


```python
def yes_or_no(question):
    "Returns True or False, depending on the user's answers."
    while True:
        answer = input(question)
        if answer == 'yes':
            return True
        elif answer == 'no':
            return False
        else:
            print('What do you want!! Just  type "Yes" or "No".')

if yes_or_no('Do you want to play the game?'):
    print('OK but you have to program it first')
else:
    print('That is sad' )

```

> [note]
> Same as `if` and `break` `return` is also *command*, not a function
> So there doesn't have to be brackets after it.

Try to write a function that returns the area of the ellipse with given 
dimentions.
the formula is <var>A</var> = π<var>a</var><var>b</var>,
where <var>a</var> and <var>b</var> sre axes length.

Then call the function and print the result.

{% filter solution %}
```python
from  math  import  pi

def ellipse(a, b): 
    return pi * a * b
    
print('The area with 3 cm and 5 cm axes length is', ellipse(3, 5),'cm2')

```
{% endfilter %}


### Return or print?

The last program could be also written like that:

```python
from math import pi

def ellipse(a, b): 
    print('The area is', pi * a * b) #Caution, 'print' instead of 'return'!
    
ellipse(3, 5)

```

The program works this way, too. But it loses one of the main advantages
that functions have - when you want to use the value differently than to `print`.

You can use function that returns any result in the different calculations:


```python
def elliptical_cylinder(a, b, hight):
    return ellipse(a, b) * hight

print(elliptical_cylinder(3, 5, 3))
```

... but if ellipse function would just print the result we wouldn't be
able to calculate the area of elliptical cylinder this way.

Another reason why is `return` better than `print` is that one function
could be used in many different situations.
We wouldn't be able to use function with `print` any reasonable way when we 
don't care about knowing the result.
For example in some graphic games, web applications or to 
control a robot.

It is similar with input: if I would use function with `input` I could use
it only if there will be user with keyboard present.
That's why it's always better to pass arguments to a function and
have `input` outside of it:

```python
from  math  import  pi

def ellipse(a, b): 
    """This will return only the result - the ellipse's area with a and b axes"""
    #there is only the calculation
    return pi * a * b
    
#print and input are "outside"
x = input('Enter length of 1st axe: ')
y = input('Enter length of 1st axe: ')
print('The are is', ellipse(x, y))
```

There are of course exceptions: a function that directly generates 
a text can be written with `print`, also a function that processes text information.
But when the function counts something it's better to not have
`print` and `input` inside it.


## None

When the function does not end with `return`
the value that it is returning is automatically `None`.

It's a value that is already "inside" Python (same as `True` and `False`).
It's literally "none, nothing".

```python
def nothing():
    "This function isn't doing anything."

print(nothing())
```


## Local variables

Congratulations! You can now define your own functions!
Now we have to explain what are local and global variables.

A function can use variables from "outside":

```python
pi = 3.1415926

def circle_area(radius):
    return pi * radius ** 2

print(circle_area(100))
```

But every variable and argument that is defined within the function body are
*brand new* and they have nothing in common with "outside" code.

Variables that are defined inside a function body are *local variables*
because they works only locally inside the function.
So this won't work how you would think:


```python
x = 0

def set_x(value):
    x = value  # Přiřazení do lokální proměnné!

set_x(40)
print(x)
```

Variables that are not local are *global variables* -
they exist within the whole program. (But in function that defines
variable with the same name this variable would have has value that exist within
the function).

Now let's show example.
Before you will run next program
try to think how it will behave.
Than run it and if it did something different than
you thought try to explain why.
There is a catch :)

```python
from math import pi
area = 0
a = 30

def ellipse_area(a, b):
    area = pi * a * b  #Assign to 'area`
    a = a + 3  #Assign to 'a`
    return area

print(ellipse_area(a, 20))
print(area)
print(a)
```

Now try to answer:

* Is variable `pi` local or global?
* Is variable `area` local or global?
* Is variable `a` local or global?
* Is variable `b` local or global?


{% filter solution %}
* `pi` is global - it's not defined within the function and it's
accessible in the whole program.
* `area` - there are two variables of that name - one is global
ant the other one is local for function `ellipse_area`.
* `a` - there are also two variables. And there was that catch.
Writing `a = a + 3` has no point. There will be bigger number assign to
variable `a` but the function ends right after that and this `a` will no 
longer be available.
* `b` is only local - it's an argument for `ellipse_area` function.

{% endfilter %}

If it seems confusing and complicated just avoid naming variables (and
function's arguments) within a function same as those outside
