# Dictionaries

Another basic data type which we will instroduce is
*dictionary*, abbr. `dict`.

Similar to lists dictionaries contains values inside.
Opposite to lists where all elements are in specific order, there are two types
of elements in dictionaries: *key* and *value*. There exists
exactly one value to every key (I don't want to confuse you right at the beginning
but so you know - empty list can be also value to the key).

You can use dictionary when you have some data each can be somehow named but you want 
to work with them as one variable.

There is a dictionary with 3 keys and each one of them has value:

```pycon
>>> me = {'name': 'Marketa', 'city': 'Prague', 'numbers': [20, 8]}
```

{# XXX - Only visible on Python 3.5 and below. How to teach this?
When you print the dictionary you will probably find out
that keys with values are in different order.
Dictionaries doesn't have order of elements they are just 
assigning values to the keys.
#}

You can get values from the dictionary similar was as
from lists but instead of index you have to use the key. 

```pycon
>>> me['name']
'Marketa'
```

If you would want to work with non-existent key Python won't like it:

```pycon
>>> me['age']
Traceback (most recent call last):
  File "<stdin>", line 1, in &lt;module&gt;
KeyError: 'age'
```

You can also change values with keys.

```pycon
>>> me['numbers'] = [3, 7, 42]
>>> me
{'name': 'Marketa', 'city': 'Prague', 'numbers': [20, 8, 42]}
```

... or add:

```pycon
>>> me['language'] = 'Python'
>>> me
{'name': 'Marketa', 'city': 'Prague', 'numbers': [20, 8, 42], 'language': 'Python'}
```

... or delete wit `del` command (also same as lists):

```pycon
>>> del me['numbers']
>>> me
{'name': 'Marketa', 'city': 'Prague', 'language': 'Python'}
```

## Lookup table

Another use of dictionaries than data clustering is
so-called *lookup table*.
There are values of same type.

This is useful for example with phone book.
For every name there is one phone number.
Or other example is dictionary with words translations.


```python
phones = {
    'Mary': '153 85283',
    'Theresa': '237 26505',
    'Paul': '385 11223',
    'Michael': '491 88047',
}

colours = {
    'pear': 'green',
    'apple': 'red',
    'melon': 'green',
    'plum': 'purple',
    'radish': 'red',
    'cabbage': 'green',
    'carrot': 'orange',
}
```

## Iteration

Když dáš slovník do cyklu `for`, dostaneš klíče:

```pycon
>>> popisy_funkci = {'len': 'délka', 'str': 'řetězec', 'dict': 'slovník'}
>>> for klic in popisy_funkci:
...     print(klic)
str
dict
len
```

Pokud chceš hodnoty, stačí použít metodu `values`:

```pycon
>>> for hodnota in popisy_funkci.values():
...     print(hodnota)
řetězec
slovník
délka
```

Většinou ale potřebuješ jak klíče tak hodnoty.
K tomu mají slovníky metodu `items`,
která bude v cyklu `for` dávat dvojice:

```pycon
>>> for klic, hodnota in popisy_funkci.items():
...     print('{}: {}'.format(klic, hodnota))
str: řetězec
dict: slovník
len: délka
```

> [note]
> Existuje i metoda `keys()`, která vrací klíče.
>
> To, co `keys()`, `values()` a `items()` vrací, jsou speciální objekty,
> které kromě použití ve `for` umožňují další
> operace: například pracovat s klíči jako s množinou.
> V [dokumentaci](https://docs.python.org/3.0/library/stdtypes.html#dictionary-view-objects)
> Pythonu je to všechno popsáno.

V průběhu takového `for` cyklu nesmíš
do slovníku přidávat záznamy, ani záznamy odebírat:

```python
>>> for klic in popisy_funkci:
...     del popisy_funkci[klic]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: dictionary changed size during iteration
```

Hodnoty u už existujících klíčů ale měnit můžeš.


## Jak udělat slovník

Slovník se dá vytvořit dvěma způsoby.
První, pomocí {složených závorek}, jsme už viděl{{gnd('i', 'y', both='i')}};
další využívají funkci `dict`.
Ta, ve stylu `str`, `int` či `list`, převede cokoli, co jde, na slovník.

Slovník je ovšem dost specifická struktura –
čísla nebo typické seznamy na něj převádět nejdou.
Můžeme ale na slovník převést *jiný slovník*.
Nový slovník žije svým vlastním životem;
následné změny se promítnou jen do něj.

```python
barvy_po_tydnu = dict(barvy)
for klic in barvy_po_tydnu:
    barvy_po_tydnu[klic] = 'černo-hnědo-' + barvy_po_tydnu[klic]
print(barvy['jablko'])
print(barvy_po_tydnu['jablko'])
```

Druhá věc, která jde převést na slovník, je
*sekvence dvojic* klíč/hodnota:

```python
data = [(1, 'jedna'), (2, 'dva'), (3, 'tři')]
nazvy_cisel = dict(data)
```

A to je vše, co se na slovník dá převést.

Jako bonus umí funkce `dict` ještě
brát pojmenované argumenty.
Každé jméno argumentu převede na řetězec,
použije ho jako klíč, a přiřadí danou hodnotu:

```python
popisy_funkci = dict(len='délka', str='řetězec', dict='slovník')
print(popisy_funkci['len'])
```

> [note]
> Pozor na to, že v tomhle případě musí být klíče
> pythonní „jména“ – musí být použitelné jako jména proměnných.
> Například takhle nejde zadat jako klíč řetězec
> `"def"` nebo `"propan-butan"`.

Pojmenované argumenty jde kombinovat s ostatními
způsoby vytvoření `dict`.


## A to je zatím ke slovníkům vše

Chceš-li mít všechny triky, které  slovníky umí,
pěkně pohromadě, můžeš si stáhnout
[Slovníkový tahák](https://pyvec.github.io/cheatsheets/dicts/dicts-cs.pdf).

Kompletní popis slovníků najdeš
v [dokumentaci](https://docs.python.org/3.0/library/stdtypes.html#mapping-types-dict)
Pythonu.
