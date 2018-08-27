# Objects and values

Before we start with classes we will learn about objects.

What does it mean *object* for programmers.

It's actually easy with Python - every value (it's something you can "store"
into variable) is object.
Some programming languages (e. g. JavaScript, C++, Java) have also
different values than objects. And for example C doesn't have objects at all.
But in Python there is no difference between value and object so
it's little bit difficult to understand. On the other hand you don't have
to know the details.

Basic attribute of objects is that they contain data(information) and *behaviour* -
instructions and/or methods how to work with data.
For example strings contains information (sequence or characters) and
also useful methods as `upper` and `count`.
If strings were not objects Python would have to have a lot more
functions as `str_upper` and `str_count`.
Objects connect data and functionality together.


> [note]
> You will maybe say that for example `len` is function and you will be correct.
> Python is not 100% object oriented languege.
> But function `len` also works on objects which do not have anything in common with strings.


# Classes

Data of each object are specific for concrete object
(e. g. `"abc"` contains different characters than `"def"`)
but functionality - methods - are same for all objects of the same 
type (class). For example string's method `count()` could be
written like that:


```python
def count(string, character):
    sum = 0
    for c in string:
        if c == character:
            sum = sum + 1
    return sum
```

And although different string will return different value
the method itself is same for all strings.

That common behavior is defined by
*type* or *class* of the object. 


> [note]
> In previous versions of Python there was difference between "type"
> and "class" but now they are synonyms.

You can find out type of an object by function `type`:


```pycon
>>> type(0)
<class 'int'>
>>> type(True)
<class 'bool'>
>>> type("abc")
<class 'str'>
>>> with open('file.txt') as f:
...     type(f)
... 
<class '_io.TextIOWrapper'>
```

So `type` returns some classes.
And what is class? It's description how every object of the same type
behaves.

Most of the classes in Python are callable as if they
were functions. This will create an object of the class we called:

```pycon
>>> string_class = type("abc")
>>> string_class(8)
'8'
>>> string_class([1, 2, 3])
'[1, 2, 3]'
```

So it's behaving as function `str`! Isn't it strange?

Now I have to apologize:
[materials for functions](../functions/)
lied a bit. Functions `str`, `int`, `float`, etc. are actually classes.

```pycon
>>> str
<class 'str'>
>>> type('abcdefgh')
<class 'str'>
>>> type('abcdefgh') == str
True
```

But we can call them as if they were functions.
So classes contain not only "description" about how object of the class
will behave but they can also create objects.


## Custom classes

Now we will try to create our own class.

Writing custom class is useful when you want to use more different objects 
with similar behaviour in your program.
For example card game could have Card class,
web application could have User class and
spreadsheet could have Row class.

Now we want to have program about animals.
First of all you have to create Kittie class which can meow:


```python
class Kittie:
    def meow(self):
        print("Meow!")
```

So same as function is defined by `def` keyword, classes are
defined by keyword `class`. Then of course you have to continue with colon
and indentation of class "body".
Similar as `def` creates functions `class` creates class and assigns it to 
name of the class (in our example to `Kittie`).

It's convention that classes are named with the first letter in uppercase so they
are not easily confused with "normal" variables.


> [note]
> Basic classes (`str`, `int`, etc.)
> doesn't have uppercase letter because of historic
> reasons – originally they were really functions.

In the class's body you can define methods which looks like functions.
The difference is that class's methods have `self` as the first argument
which we will explain it later - meowing comes first:

```python
# Creation of the object
kittie = Kittie()

# Calling the method
kittie.meow()
```

In this case you have to be really carefull about uppercase letters:
`Kittie` (with uppercase K) is class - description how kitties behave.
`kittie` (lowercase k) is the object (*instance*) of Kittie class:
variable that represents Kittie.
That object is created by calling the class (same as we
can create string by calling `str()`)

Meow!

## Attributes 

Objects that are created from custom classes have one feature that
classes like `str` don't allow and that's the ability to define class's *attributes* -
information that are stored by the instance of the class.
You can recognise attribute by the period between class instance and the name of its attribute.


```python
smokey = Kittie()
smokey.name = 'Smokey'

misty = Kittie()
misty.name = 'Misty'

print(smokey.name)
print(misty.name)
```

In the beginning we said that objects are connecting behaviour with data.
Behaviour is defined in class, data are stored by in attributes.
We can differentiate Kitties for example by their names because of the attributes.

> [note]
> You might notice that by the period after class's object you can get to methods of the class 
> and also to its attributes.
> What will happen if attribute has the same name as method?
> Try it!
>
> ```python
> misty = Kittie()
> misty.meow = 12345
> misty.meow()
> ```

## Parameters `self`

Now we will briefly go back to methods, to be specific we will go back
to parameter `self`.

Each method has access to specific object that it's working on just because of
parameter `self`.
Now when you have named your kitties you can add the name to meowing by the `self` parameter.


```python
class Kittie:
    def meow(self):
        print("{}: Meow!".format(self.name))

smokey = Kittie()
smokey.name = 'Smokey'

misty = Kittie()
misty.name = 'Misty'

smokey.meow()
misty.meow()
```

What just happened? The command `smokey.meow` called *method* which when it's called assigns object
`smokey` as first argument to function `meow`.


> [note]
> This is how *method* is different from *function*:
> method "remembers object it's working on.

And that first argument which contains specific object of just created class is
usually called `self`.
You can of course call it differently but other programmers will not like you :)

Can such method take more that one argument?
It can - in that case`self` will be substituted as the first argument
and the rest of arguments will be taken from how you called the method.
For example:

```python
class Kittie:
    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))

smokey = Kittie()
smokey.name = 'Smokey'
smokey.eat('fish')
```

## Method `__init__`

There is another place where you can pass arguments to the class:
when you are creating new object (calling the class).
You can easily solve the problem that you might see in previous code:
after kittie object is created you have to add name so method
`meow` could work.
Class can be also created by passing parameter when you are calling it:


```python
smokey = Kittie(name='Smokey')
```
Python is using `__init__` (2 underscores, `init`, 2 underscores) for this option.
Those underscores indicate that this method name is somehow special. Method `__init__`
is actually called right when object is being created or in other words - when it's
being initialized (`init` stands for *initialization*).
So you can write it like that:

```python
class Kittie:
    def __init__(self, name):
        self.name = name

    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))

smokey = Kittie('Smokey')
smokey.meow()
```

And now there is no possibility to create kittie without name
so `meow` will work all the times.

Methods with underscores are much more, e. g. `__str__`
method is called when you need the object to be converted into string:


```python
class Kittie:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return '<Kittie named {}>'.format(self.name)

    def meow(self):
        print("{}: Meow!".format(self.name))

    def eat(self, food):
        print("{}: Meow meow! I like {} very much!".format(self.name, food))

smokey = Kittie('Smokey')
print(smokey)
```

## Exercise: Cat

Now when you know how to create kittie class try to make class for cats.

- Cat can meow with `meow` method.
- Cat has 9 lives when it's created (she can't have more than 9 and less than 0 lives). 
- Cat can say if she is alive (has more than 0 lives) with `alive` method.
- Cat can lost live (method `takeoff_life`)
- Cat can be fed with `eat` method that takes exactly 1 argument - specific food (string).
 If the food is `fish` cat will gain one life (if she is not already dead or
 doesn't have maximum lives).

{% filter solution %}
```python
class Cat:
    def __init__(self):         # Init function does not have to take number of lives
        self.lives_number = 9   # as parameter 'cause that number is always the same.

    def meow(self):
        print("Meow, meow, meeeoooow!")

    def alive(self):
        return self.lives_number > 0

    def takeoff_life(self):
        if not self.alive():
            print("You can't kill cat that is already dead, you monster!")
        else:
            self.lives_number -= 1

    def eat(self, food):
        if not self.alive():
            print("It's pointless to give food to dead cat!")
            return
        if food == "fish" and self.lives_number < 9:
            self.lives_number += 1
            print("Cat ate fish and gained 1 life!")
        else:
            print("Cat is eating.")
```
{% endfilter %}

And that's now everythong about classes.
[Next time](../inheritance/) we will learn about inheritance.
And also about doggies :)
