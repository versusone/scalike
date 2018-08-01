Scala like List Transformation functions for Python

Scalike (Python3)

Full doc at: www.netnotnut.com/scalike  
Contact scalike@gmx.com  
License: MIT  


Scalike locally wraps List Transformation functions in a way Scala does.

The following Tutorial provides a quick sample for each function.

Finding Help:

$> python
>>> import scalike
>>> help(scalike)
>>> help(scalike.sclist)

To obtain help for a specific function, please use this into Python interpreter:
>>> from scalike import sclist
>>> help(sclist.<funct_name>)
e.g.:
>>> help(sclist.map)

1. Functions Tutorial


Let us open Python interpreter:
>>> from scalike import sclist


Note:
The following functions generally return an sclist.
Each functions has an equivalent (but starting by "_") into the package scalike_gen,
returning an iterable.
Use it if you know you need it !


1.1 MAP Funtions:


- map:
>>> help(sclist.map)
Help on function map in module scalike:

map(*args, **keywords)
      Signature: map(fct)
      map applies the function fct to each item of the list,
      and returns an sclist of fct(item).

      :parameter ignore_none: If true,
      will disgarde Noe value from the list.

      :arg fct : a function, should return something.
      Receive an item as unique argument.
      :returns an sclist.

      ex1: l.map(f1, [1, 2, 3]) returns [f1(1), f1(2), f1(3)]

      ex2:

l = sclist("one", "two", "three", "four")
# Note same as: sclist(("one", "two", "three", "four")) or sclist(["one", "two", "three", "four"]).
>>> l.map(lambda e:e[2])
['e', 'o', 'e', 'u']

- maps:
>>> help(sclist.maps)
Help on function maps in module scalike:

maps(*args, **keywords)
      Signature: maps(fct, *iterables)
      map applies the function fct to each item of the iterables,
      and returns an sclist of fct(item1, item2, itemn, ...).
      Same as map but supports more than one iterable.
      Take as many arguments as there are iterables.

      :arg fct : a function, should return something.
      :returns an sclist.
      Receive as many item args as they are iterables.
      fct must support as many args as they are iterables.

      ex1: l.maps(f1, [1, 2, 3], ['a', 'b', 'c'], [True, False, None]) returns
      Will stop when reach the end of the shortest iterable.

      ex2:

l = sclist(1,2,3)
ll = (4,5,6)
lll = (7,8,9)
>>> l.maps(lambda a, b, c:a + b + c, ll, lll)
[12, 15, 18]

- starmap:
>>> help(sclist.starmap)
Help on function starmap in module scalike:

starmap(*args, **keywords)
      Signature: starmap(fct)
      Similar as maps but use it when this slist values are
      already organized as tuples.
      And fct will take as many args as there is per tuple.
      :arg fct : a function, should return something.
      :returns an sclist.

      ex1: l.starmap(f1, [(1, 2, 3), ('a', 'b', 'c')]) returns sclist([f1(1, 2, 3), f('a', 'b', 'c')])
      Will stop when reached the shorted iterable.

      ex2:

>>> l = sclist((1,2,3), (4,5,6), (7,8,9))
>>> l.starmap(lambda a, b, c:a + b + c)
[6, 15, 24]

- foreach:
>>> help(sclist.foreach)
Help on function foreach in module scalike:

foreach(*args, **keywords)
      Signature: foreach(fct)
      foreach applies the function fct to each item of the list,
      :arg fct : a function, must NOT return anything.

      ex:

>>> l = sclist("one", "two", "three", "four")
>>> l.foreach(lambda e: print(e[2]))
e
o
e
u

- flatmap:
>>> help(sclist.flatmap)
Help on function flatmap in module scalike:

flatmap(*args, **keywords)
      Signature: flatmap(fct)
      flatMap is the same as map, but fct may return a tuple or a list.
      Then each returned list is extended to the resulting list rather than just added.

      :arg fct : a function, must return a tuple or a list.

      :returns a flatten sclist of the resulting values.

      ex:

>>> l = sclist("one", "two", "three", "four")
>>> l.flatmap(lambda e:list(e))
['o', 'n', 'e', 't', 'w', 'o', 't', 'r', 'e', 'e', 'f', 'o', 'u', 'r']

- filter:
>>> help(sclist.filter)
Help on function filter in module scalike:

filter(*args, **keywords)
      Signature: filter(fct)
      filter applies the function fct to each item of the list.
      If fct() is true, this item is added to the returned list.

      :arg fct : a function, must return a boolean: True or False.

      :returns an sclist of the item for which fct() was True.

      ex:

>>> l = sclist("one", "two", "three", "four")
>>> l.filter(lambda e:e.startswith('t'))
['two', 'three']

- dropwhile:
>>> help(sclist.dropwhile)
Help on function dropwhile in module scalike:

dropwhile(*args, **keywords)
      Signature: dropwhile(fct)
      dropwhile drop sclist elements as long as fct(e) is True.
      And starts returning the list elements that left,
      as soon as the predicate becomes False.

      :arg fct : a function, must return a boolean: True or False.
      :returns an sclist of the item soon as fct(e) has been once false.

      ex:

>>> l = sclist("one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve")
>>> l.dropwhile(lambda e:len(e)==3)
['three', 'four', 'five', 'six', 'seven', 'eight', 'nine', 'ten', 'eleven', 'twelve']
>>> l.dropwhile(lambda e:len(e) in (3,4,5))
['eleven', 'twelve']

- takewhile:
>>> help(sclist.takewhile)
Help on function takewhile in module scalike:

takewhile(*args, **keywords)
      Signature: takewhile(fct)
      takewhile is the opposite of dropwhile.
      takewhile drop sclist elements as long as fct(e) is False.
      And starts returning the list elements that left,
      as soon as the predicate becomes True.

      :arg fct : a function, must return a boolean: True or False.
      :returns an sclist of the item soon as fct(e) has been once false.

      ex:

>>> l = sclist("one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve")
>>> l.takewhile(lambda e:len(e)==3)
['one', 'two']

- mask:
>>> help(sclist.mask)
Help on function mask in module scalike:

mask(*args, **keywords)
      Signature: mask(fct, selectors)
      mask extract the elements which index match the True flag of the selectors.
      :returns an sclist of flagged items.
      ex:
       l = sclist(('a', 'b', 'c', 'd', 'e'))
       l.mask([0, 1, 1, 0]) returns ('b', 'c')

      ex2:

>>> l = sclist("one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve")
>>> l.mask((2,5,7))
['one', 'two', 'three']
>>> l.mask((False,False,True))
['three']
>>> l.mask((False,False,True, 0, 0, 1, False, True, True))
['three', 'six', 'eight', 'nine']

- distinct:

>>> help(sclist.distinct)
Help on function distinct in module scalike:

distinct(*args, **keywords)
      Signature: distinct(omits = None, selects=None, force_filter=False)
      distinct returns a list of the items of this list that only appear once.
      :parameter omits(int) : a list or tuple of indices to omit for the dictinct comparaison.
      If omits is provided selects cannot.
      :parameter selects(int) : a list or tuple of indices to accept for the dictinct comparaison.
      If selects is provided omits cannot.

      If either omits or selects is used:
            This list should be an sclist of iterables.
            Others elements that are not iterable are ignored !

      :return a list of the unique items of the list.

      ex:
l = sclist(1, 1, 1, 2, 2, 2, 2, 3, 4, 4, 4, 4, 5, 6, 6, 6, 6, 6, 7, 7, 7, 7, 8, 9)
>>> l.distinct()
[1, 2, 3, 4, 5, 6, 7, 8, 9]

l = sclist(
(0,1,2,3,4,5,0),
(0,1,2,3,4,0,6),
(0,1,2,3,0,5,6),
(0,1,2,0,4,5,6),
(0,1,2,3,4,5,0),
'a', 'a', 'b',
'b', 'b', 'c',
'abcdefg',
'hellofg',
)

>>> l.distinct()
[(0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 4, 0, 6), (0, 1, 2, 3, 0, 5, 6), (0, 1, 2, 0, 4, 5, 6), 'a', 'b', 'c', 'abcdefg', 'hellofg']
>>>
>>> l.distinct(selects=(0,1,2,3,4), force_filter=True)
[(0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 0, 5, 6), (0, 1, 2, 0, 4, 5, 6), 'abcdefg', 'hellofg']
>>> l.distinct(omits=(5,6), force_filter=True)
[(0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 0, 5, 6), (0, 1, 2, 0, 4, 5, 6), 'a', 'b', 'c', 'abcdefg', 'hellofg']
>>>
>>> l.distinct(selects=(5,6), force_filter=True)
[(0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 4, 0, 6), (0, 1, 2, 0, 4, 5, 6), 'hellofg']
>>> l.distinct(omits=(0,1,2,3,4), force_filter=True)
[(0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 4, 0, 6), (0, 1, 2, 0, 4, 5, 6), 'c', 'hellofg']

- distinct2:
>>> help(sclist.distinct2)
Help on function distinct2 in module scalike:

distinct2(*args, **keywords)
      Signature: distinct2(l)
      distinct2 returns a list of all the items of this list that are not in list l.

      :arg l : an iterable.

      :returns : an sclist.

      ex:

>>> l = sclist('a' ,'b', 'c', 'd')
>>> ll = ('e', 'b', 'd', 'e', 2, 3, 4)

>>> # On itself:
>>> l.distinct2(l)
[]
>>> l.distinct2(ll)
>>> l.distinct2(ll)



1.2 FIND Functions:

- find
>>> help(sclist.find)
Help on function find in module scalike:

find(*args, **keywords)
      Signature: find(fct)
      find applies the function fct to each item of the list.
      If fct() is true, item is returned, otherwise None.
      Just the first valid item is returned.

      :arg fct : a function, must return a boolean: True or False.
      :returns an item for which fct() is True.

      ex:

l=sclist((0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 4, 0, 6), ['a', 'b', 'c', 'd', 'e', 'f', 'g'])
>>> l.find(lambda e:len(e)> 5)
(0, 1, 2, 3, 4, 5, 0)
>>> l.find(lambda e: 5 in e)
(0, 1, 2, 3, 4, 5, 0)

- exist or any
>>> help(sclist.exist)
Help on function exist in module scalike:

exist(*args, **keywords)
      Signature: exist(fct)
      exist applies the function fct to each item of the list.
      If fct() is true, True is returned, otherwise False.
      :arg fct : a function, must return a boolean: True or False.
      :returns if an item satisfies fct() == True, return True.

      ex:

>>> l.exist(lambda e: 5 in e)
True
>>>
>>> l.exist(lambda e: 7 in e)
False

- forall or all:
>>> help(sclist.forall)
Help on function forall in module scalike:

forall(*args, **keywords)
      Signature: forall(fct)
      Same as exists except all item of the list must satisfy: fct() == True,
       otherwise False is returned.
      :arg fct : a function, must return a boolean: True or False.
      :returns if all items satisfies fct() == True, return True.

      ex:

>>> l
[(0, 1, 2, 3, 4, 5, 0), (0, 1, 2, 3, 4, 0, 6), ['a', 'b', 'c', 'd', 'e', 'f', 'g']]
>>> l.forall(lambda e: len(e)>5)
True
>>> l.forall(lambda e: 5 in e)
False



1.3 SORT Functions:

- sortl
>>> help(sclist.sortl)
Help on function sortl in module scalike:

sortl(*args, **keywords)
      Signature: sortl(fct=None, reverse=False)
      Will sort this list using the callable fct to evaluate the value to be sorted.
      ex:
      >>> l
      ['ggg', 'hhh', 'JJJ', 'aaa', 'ccc', 'QQQ', 'ddd']
      >>> l.sortl()
      ['JJJ', 'QQQ', 'aaa', 'ccc', 'ddd', 'ggg', 'hhh']
      or:
      >>> l.sortl(fct=lambda e:e.lower())
      ['aaa', 'ccc', 'ddd', 'ggg', 'hhh', 'JJJ', 'QQQ']

      :returns a sorted sclist.

      ex:

l = sclist('one', 'four', 'three', 'two')
>>> l.sortl(fct=lambda e:str(e[1]))
['one', 'four', 'three', 'two']
>>>
>>> l.sortl(fct=lambda e:str(e[2]))
['one', 'three', 'two', 'four']
>>>
>>> l.sortl(fct=lambda e:str(e[2]), reverse=True)
['four', 'two', 'one', 'three']

- min
>>> help(sclist.min)
Help on function min in module scalike:

min(*args, **keywords)
      Signature: min(fct=None, reverse=False, default=None)
      Will return the shortest value of this list using the callable fct to evaluate the value to be sorted.
      If the list is empty default is returned when provided otherwise a ValueError is raised.
      :returns a sorted sclist.

      ex:

>>> l.min(lambda e: e)
'four'

- max
>>> help(sclist.max)
Help on function max in module scalike:

max(*args, **keywords)
      Signature: max(fct=None, reverse=False, default=None)
      Will return the largest value of this list using the callable fct to evaluate the value to be sorted.
      If the list is empty default is returned when provided otherwise a ValueError is raised.
      :returns a sorted sclist.

      ex:

>>> l.max(lambda e: e)
'two'



1.4. REDUCE Functions:

- reduce:
>>> help(sclist.reduce)
Help on function reduce in module scalike:

reduce(*args, **keywords)
      Signature: reduce(fct)
      reduce, reduce the list to a single value.
      fct is called for each element of the list from left to rigth.
      But instead of receiving only one item, fct receive and .
      e.g.1: list is (a, b, c, d)
      First result = fct(a, b) is called,
      Then result = fct(result, b)
      Then result = fct(result, c) and so on.
      To resume the result is: fct(fct(fct(a, b), c), d).
            Or:
             fct
             / fct d
       / fct c
       /a b

      e.g.2:
      l = [1, 2, 3, 4, 5])
      l.reduce(lambda x, y: x+y) calculates ((((1+2)+3)+4)+5).

      If the list contains only one item, this item is returned.

      :arg fct : function receives 2 argument, item and next item.

      :returns the value of the fct function.

      ex:

>>> l = sclist('a', 'b', 'c', 'd')
>>> l.reduce(lambda a, b: a + b)

- foldleft:
>>> help(sclist.foldleft)
Help on function foldleft in module scalike:

foldleft(*args, **keywords)
      Signature: foldleft(z, fct)
      foldleft applies the function fct to each item of the list.
      foldleft applies in a recursive way, e.g.: the list is (a, b, c):
            First starts by the left side of the list, applying fct to z, a: result = fct(z, a),
            Then going on to the next element of the list, applying fct to result, b: result = fct(result, b),
            and next one ... applying fct to result, c: result = fct(result, c),
            Then keep on going ...
            To resume the result is: fct(fct(fct(z, a), b), c).
            Or:
             fct
             / fct c
       / fct b
       /z a

      :arg z: a predicate any python value.
      :arg fct: a function.

      :returns the result of the function recursively applied to each element of the list from left to righ,
      starting by fct(z, a).

      ex:

>>> l.foldleft('z', lambda a, b: a + b)
'zabcd'
>>>
>>> l.foldleft('', lambda a, b: a + b) # Same as l.reduce()
'abcd'

- foldright:
>>> help(sclist.foldright)
Help on function foldright in module scalike:

foldright(*args, **keywords)
      Signature: foldright(z, fct):
      foldright applies the function fct to each item of the list.
      foldright applies in a recursive way, e.g.: the list is (a, b, c):
            First starts by the right side of the list, applying fct to c, z: result = fct(c, z),
            Then going on to the next previous element of the list, applying fct to result, b: result = fct(b, result),
            and next previous one ... applying fct to result, c: result = fct(c, result),
            Then keep on going ...
            To resume the result is: fct(a, fct(b, fct(c, z))).
            Or:
             fct
             /      a fct
             /       b fct
                   /            c z

      :arg z: a predicate any python value.
      :arg fct: a function.

      :returns the result of the function recursively applied to each element of the list from right to left,
      starting by fct(z, a).

      ex:

>>> l.foldright('z', lambda a, b: a + b)
'dcbaz'



1.5. JOIN Functions:

- union:
>>> help(sclist.union)
Help on function union in module scalike:

union(*args, **keywords)
      Signature: union(l):
      union Merge this list with another list.

      :arg l : an iterable.

      :return the list resulting from the addition of these two list: this + l.

      ex:

>>> l = sclist('a', 'b', 'c', 'd')
>>> ll = (1,2,3,4)
>>> l.union(ll)
['a', 'b', 'c', 'd', 1, 2, 3, 4]

- intersect:
>>> help(sclist.intersect)
Help on function intersect in module scalike:

intersect(*args, **keywords)
      Signature: intersect(l):
      intersect returns a list of all the items this list that are in list l.

      :arg l : an iterable.

      :returns the list resulting from the intersect of these two list this and l.

      ex:

>>> l = sclist("once upon a time in the east !".split())
>>> l
['once', 'upon', 'a', 'time', 'in', 'the', 'east', '!']
>>> ll = "see you next time and call, me once you are in".split()
>>> l.intersect(ll)
['once', 'time', 'in']

- zip:
>>> help(sclist.zip)
Help on function zip in module scalike:

zip(*args, **keywords)
      Signature: zip(l)
      zip returns a list of pairs.
      Each element of la is mapped with the element of the same rank from lb.
      Zipping stops at the shortest list.
      e.g. for:
      la = (a, b, c)
      lb = (x, y, z)
      Results is:
      [(a, x),(b, y),(c, z)]

      :arg l : an iterable.

      :returns a list of la mapped to lb

      ex:

>>> l = sclist('a', 'b', 'c')
>>> ll = sclist(1, 2, 3, 4, 5, 6)
>>> l.zip(ll)
[('a', 1), ('b', 2), ('c', 3)]

- zipl:
>>> help(sclist.zipl)
Help on function zipl in module scalike:

zipl(*args, **keywords)
      Signature: zipl(l)
      zipl returns a list of pairs.
      Each element of la is mapped with the element of the same rank from lb.
      e.g. for:
      la = (a, b, c)
      lb = (x, y, z)
      Results is:
      [(a, x),(b, y),(c, z)]
      Zipping stops at the longuest list, completing by None value.

      :arg l : an iterable, must have the same size than this.

      :returns a list of la mapped to lb

      ex:

>>> l = sclist('a', 'b', 'c')
>>> ll = sclist(1, 2, 3, 4, 5, 6)
>>> l.zipl(ll)
[('a', 1), ('b', 2), ('c', 3), (None, 4), (None, 5), (None, 6)]

- zips:
>>> help(sclist.zips)
Help on function zips in module scalike:

zips(*args, **keywords)
      Signature: zips(*iterables)
      zips returns a list of n-th. e.g.: la, lb, lc, ..., ln-th.
      Each element of la is mapped with the n-th element of the same rank from lb, lc nad ln-th.
      e.g. for:
      la = (a, b, c)
      lb = (x, y, z)
      lc = (1, 2, 3)
      Results is:
      [(a, x, 1),(b, y, 2),(c, z, 3)]

      :arg iterables : one or more lists, must have the same size than this.

      :returns a list of la mapped to lb

      ex:

>>> l = sclist('a', 'b', 'c')
>>> ll = (1, 2, 3, 4, 5, 6)
>>> lll = ('@', '&')
>>> l.zips(ll, lll)
[('a', 1, '@'), ('b', 2, '&')]

- zipls:
>>> help(sclist.zipls)
Help on function zipls in module scalike:

zipls(*args, **keywords)
      Signature: zipls(*iterables)
      zipls returns a list of n-th.
      Each element of la is mapped with the n-th element of the same rank from lb, lc nad ln-th.
      e.g. for:
      la = (a, b, c)
      lb = (x, y, z)
      lc = (1, 2, 3)
      Results is:
      [(a, x, 1),(b, y, 2),(c, z, 3)]
      Zipping stops at the longuest list, completing by None value.

      :arg l : a list, must have the same size than this.

      :returns a list of la mapped to lb

      ex:

>>> l = sclist('a', 'b', 'c')
>>> ll = (1, 2, 3, 4, 5, 6)
>>> lll = ('@', '&')
>>> l.zipls(ll, lll)
[('a', 1, '@'), ('b', 2, '&'), ('c', 3, None), (None, 4, None), (None, 5, None), (None, 6, None)]

- index:
>>> help(sclist.index)
Help on function index in module scalike:

index(*args, **keywords)
      Signature: index()
      index returns a list of pairs.
      Each element this list mapped with its own rank in this list.
      e.g. for:
      l = (a, b, c)
      Results is:
      [(0, a),(1, b),(2, c)]

      :returns a list of la mapped to lb

      ex:

>>> l.index()
[(0, 'a'), (1, 'b'), (2, 'c')]

- indice:
>>> help(sclist.indice)
Help on function indice in module scalike:

indice(*args, **keywords)
      Signature: indice(withString=False)
      This list must be an sclist of iterables.
      Each iterable element of this list receive the element index at first position.
      e.g. for:
      l = [(1, 2, 3), (a, b), (true, false)]
      Results is:
      l = [[0, 1, 2, 3], [1, a, b], [2, true, false]]

      :returns a list

      ex:

>>> l = sclist(('o', 'n', 'e'), ('t', 'w', 'o'), ('t', 'h', 'r', 'e', 'e'))
>>> l.indice()
[[0, 'o', 'n', 'e'], [1, 't', 'w', 'o'], [2, 't', 'h', 'r', 'e', 'e']]

- cartesian:
>>> help(sclist.cartesian)
Help on function cartesian in module scalike:

cartesian(*args, **keywords)
      Signature: cartesian(l)
      cartesian returns a list of pairs.
      cartesian returns a list of the elements of this list: la mapped with the elements of list: lb.
      This list: la is read in its order and each elements of la is mapped with each elements of lb.
      So the resulted list is a product of len(la) * len(lb).
      e.g. for:
      la = (a, b, c, d)
      lb = (x, y, z)
      Results is:
      [(a, x),(a, y),(a, z),
      (b, x),(b, b),(b, z),
      (c, x),(c, y),(c, z),
      (d, x),(d, y),(d, z)]

      :arg l : an iterable.

      :returns the cartesian list of la * lb

      ex:

>>> l = sclist('one', 'two', 'three')
>>> ll = (1, 2)
>>> l.cartesian(ll)
[['one', 1], ['one', 2], ['two', 1], ['two', 2], ['three', 1], ['three', 2]]



1.6 KEYPAIR Functions:

- kvKeys:
>>> help(sclist.kvKeys)
Help on function kvKeys in module scalike:

kvKeys(*args, **keywords)
      Signature: kvKeys()
      This must be an sclist of key/value pairs list (or tuple).
      kvKeys returns a list of the key part of each couple.

      :return an sclist of the keys.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> l.kvKeys()
['a', 'b', 'c']
- kvValues:
>>> help(sclist.kvValues)
Help on function kvValues in module scalike:

kvValues(*args, **keywords)
      Signature: kvValues()
      This must be a list of key/value pairs list (or tuple).
      kvKeys returns a list of the value part of each couple.

      :return an sclist of the values.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> l.kvValues()
[1, 2, 3]

- kvMapKeys:
>>> help(sclist.kvMapKeys)
Help on function kvMapKeys in module scalike:

kvMapKeys(*args, **keywords)
      Signature: kvMapKeys(fct)
      This must be an sclist of key/value pairs list (or tuple).
      map applies the function fct to each key part of each item of the list.
      And returns the new key/value pairs list.

      :arg fct : a function, should return something.

      :returns an sclist.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> l.kvMapKeys(lambda e: e*3)
[['aaa', 1], ['bbb', 2], ['ccc', 3]]

- kvMapValues:
>>> help(sclist.kvMapValues)
Help on function kvMapValues in module scalike:

kvMapValues(*args, **keywords)
      Signature: kvMapValues(fct)
      This must be a list of key/value pairs list (or tuple).
      map applies the function fct to each value part of each item of the list.
      And returns the new key/value pairs list.

      :arg fct : a function, should return something.

      :returns an sclist passed througth the function fct applied to each value part of each pair of the list.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> l.kvMapValues(lambda e: e*3)
[['a', 3], ['b', 6], ['c', 9]]

- kvFilterKeys:
>>> help(sclist.kvFilterKeys)
Help on function kvFilterKeys in module scalike:

kvFilterKeys(*args, **keywords)
      Signature: kvFilterKeys(fct)
      This must be an sclist of key/value pairs list (or tuple).
      filter applies the function fct to each key part of each item of the list.
      And returns the new key/value pairs list.

      :arg fct : a function, should return something.

      :returns the filtered sclist.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> l.kvFilterKeys(lambda e: e<'c')
[('a', 1), ('b', 2)

- kvFilterValues:
>>> help(sclist.kvFilterValues)
Help on function kvFilterValues in module scalike:

kvFilterValues(*args, **keywords)
      Signature: kvFilterValues(fct)
      This must be an sclist of key/value pairs list (or tuple).
      filter applies the function fct to each value part of each item of the list.
      And returns the new key/value pairs list.

      :arg fct : a function, should return something.

      :returns the filtered sclist.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> l.kvFilterValues(lambda e: e>2)
[('c', 3)]

- kvJoin:
>>> help(sclist.kvJoin)
Help on function kvJoin in module scalike:

kvJoin(*args, **keywords)
      Signature: kvJoin(kv_iterable)
      This must be an sclist of key/value pairs list.
      kv_iterable must be a list of key/value pairs list.
      kvJoin join all the key part of each item this list, with the key part of each item of kv_iterable.
      The values o the two list are wrapped to a list associated to the key.

      Note : if a key appears more than once in one list, it is overwrite by the next key/pair with the same key, within the same list.
       If any your list supports more than one value for one key you should consider to use kvGroupByKey on it first.

      :arg l : a key value pairs list.

      :returns an sclist of key value pairs.

      ex:
      
l = sclist(('a', 1), ('b', 2), ('c', 3))
ll = [('b', 'two'), ('c', 'three'), ('d', 'four')]
>>> l.kvJoin(ll)
[['b', [2, 'two']], ['c', [3, 'three']]]

- kvJoinLeft:
>>> help(sclist.kvJoinLeft)
Help on function kvJoinLeft in module scalike:

kvJoinLeft(*args, **keywords)
      Signature: kvJoinLeft(kv_iterable)
      This must be an sclist of key/value pairs list.
      kv_iterable must be a list of key/value pairs list.
      The same as join, but returns all the key of this list.
      And the value None for the mapped key that do not exists in list kv_iterable.

      Note : if a key appears more than once in one list, it is overwrite by the next key/pair with the same key, within the same list.
       If any your list supports more than one value for one key you should consider to use kvGroupByKey on it first.

      :arg l : a key value pairs list.

      :returns an sclist of key value pairs.

      ex:
      
l = sclist(('a', 1), ('b', 2), ('c', 3))
ll = [('b', 'two'), ('c', 'three'), ('d', 'four')]
>>> l.kvJoinLeft(ll)
[['a', [1, None]], ['b', [2, 'two']], ['c', [3, 'three']]]

- kvJoinrRight:
>>> help(sclist.kvJoinRight)
Help on function kvJoinRight in module scalike:

kvJoinRight(*args, **keywords)
      Signature: kvJoinRight(kv_iterable)
      This must be an sclist of key/value pairs list.
      kv_iterable must be a list of key/value pairs list.
      The same as join, but returns all the key of this list.
      And the value None for the mapped key that do not exists in list kv_iterable.

      Note : if a key appears more than once in one list, it is overwrite by the next key/pair with the same key, within the same list.
       If any your list supports more than one value for one key you should consider to use kvGroupByKey on it first.

      :arg l : a key value pairs list.

      :returns an sclist of key value pairs.

      ex:
      
l = sclist(('a', 1), ('b', 2), ('c', 3))
ll = [('b', 'two'), ('c', 'three'), ('d', 'four')]
>>> l.kvJoinRight(ll)
[['b', ['two', 2]], ['c', ['three', 3]], ['d', ['four', None]]]

- kvSubstract
>>> help(sclist.kvSubstract)
Help on function kvSubstract in module scalike:

kvSubstract(*args, **keywords)
      Signature: kvSubstract(kv_iterable)
      This must be an sclist of key/value pairs list.
      This and kv_iterable must be an list of key/value pairs list.
      kvSubStract returns all the key of this list that do not exist in list kv_iterable.

      Note : if a key appears more than once in one list, it is overwrite by the next key/pair with the same key, within the same list.
       If any your list supports more than one value for one key you should consider to use kvGroupByKey on it first.

      :arg l : a key value pairs list.

      :returns an sclist of a key value pairs.

      ex:
      
>>> l = sclist(('a', 1), ('b', 2), ('c', 3))
>>> ll = sclist(('b', 'two'), ('c', 'three'), ('d', 'four'))
>>> l.kvSubstract(ll)
[['a', 1]]
>>>
>>> ll.kvSubstract(l)
[['d', 'four']]

- kvGroupByKey
>>> help(sclist.kvGroupByKey)
Help on function kvGroupByKey in module scalike:

kvGroupByKey(*args, **keywords)
      Signature: kvGroupByKey()
      This must be an sclist of key/value pairs list (or tuple).
      kvGroupByKey returns all values grouped by key.

      Note : you may use kvGroupByKey when your list supports more than one value for one key.
      before using kvJoin, kvJoinLeft and kvSubstract.

      :returns an sclist of a key value pairs.

      ex:
      
>>> l = sclist(('a', 1), ('c', 33),
('c', 333), ('b', 2), ('c', 3),
('a', 11), ('b', 22), ('c', 3333),
('a', 111)
)

>>> l.kvGroupByKey()
[('a', [1, 11, 111]), ('c', [33, 333, 3, 3333]), ('b', [2, 22])]




2. Cases (Experimental):


Scalike tries to mimic Scala cases !

Finding Help:

$> python
>>> from scalike import cases
>>> help(cases)


1. Case Introduction


We start from there:
$> python
>>> from scalike.cases import *

There are 5 elements entering into play considering using cases for Data dispatching :

    The Case Schema
    The Case Property
    The Switch Operator literally: with Switch() as case replacing the case instruction.
    List filtering, this works on the case instance.
    List Mapping, this works on the Case Property instance


1.1 The Case Schema

1.1.1 Creating a Schema the simplest way :

>>> mySchema = CaseSchema('a', 'b', 'c')

This creates a simple schema with three fields of type String.

The following CaseSchema methods can be used on mySchema :
mySchema.ofields()
str(mySchema) or mySchema.wks()

>>> mySchema.ofields() # ofields means ordered fields
('a', 'b', 'c')
>>> str(mySchema)
{'a': {'*type': 'str', '*required': True}, 'b': {'*type': 'str', '*required': True},
'c': {'*type': 'str', '*required': True}}

As we can see each field is defined by a key-value pair:
<field name>:<type>

Syntax:
<field name>: always a string.
<type>: a wk expression.
A wk expression is a dictionary with a particular format.
Run help(wk) to learn more on wk expression.

There is also 3 more methods:

    addField(*fe)
    reorderFields(*field_names)
    delField(field_name)


1.1.2 Creating a Schema using wk expression :

ex1:

>>> mySchema = CaseSchema(
      'a', # must be an str
      ('b', {'*type': bool}), # must be a bool
      ('c', {'*type': tuple}) # must be a tuple
)


ex2:

>>> mySchema = CaseSchema(
      ('a', {'*type': 'int', '*ge': 3}), # must be an int and greater than 3.
      ('b', {'*date': "%d/%m/%Y"}), # must be a date expedcted format is a string formatted like : '01/11/2016'.
      ('c', {'*ts': '%d/%m/%Y %Hh%Mmn%Ss'}), # Expects a string formatted TimeStamp like this: '01/11/2016 16h40mn3s'.
      ('d', {'*type': 'dict', '*dtype': {'a': {'*type': 'str'}, 'b': {'*type': 'bool'}}}), # must be a dict with keys a,b.
)

>>> str(mySchema)
"{'a': {'*type': 'int', '*ge': 3, '*required': True},
'b': {'*date': '%d/%m/%Y', '*required': True},
'c': {'*ts': '%d/%m/%Y %Hh%Mmn%Ss', '*required': True},
'd': {'*type': 'dict', '*dtype': {'a': {'*type': 'str'},
'b': {'*type': 'bool'}}, '*required': True}}"


1.1.3 Creating a Schema from an empty constructor :

>>> mySchema = CaseSchema()
>>> mySchema.addField('a')
>>> mySchema.addField('b', {'*type': 'int'}, '*value': 123)
>>> mySchema.addField('c', {'*type': 'bool', '*value': False})

>>> str(mySchema)
"{'a': {'*type': 'str', '*required': True}, 'b': {'*type': 'int', '*value': 123, '*required': True}, 'c': {'*type': 'bool', '*value':alse, '*required': True}}"


1.2 Creating a Case Property

A case property is made from a call on a schema.
The arguments are a list (or tuple, actually an iterable) and a format string to match the list item to the schema's fields.

1.2.1 With no format string:

>>> myCaseProperty = mySchema(['a1', 2, True])
>>> str(myCaseProperty)
"{'a': 'a1', 'b': 2, 'c': True}"

This creates an instance of CaseProperty and will match:
• 'a1'	to myCaseProperty.a
• 2	to myCaseProperty.b
• True	to myCaseProperty.c

1.2.1 With an Anonymous format string:

>>> myCaseProperty = mySchema(['a1', 2, True], '%', '%', '%')
>>> str(myCaseProperty)
"{'a': 'a1', 'b': 2, 'c': True}"

Matches the same than before.

1.2.2 With Nominative format strings:

>>> myCaseProperty = mySchema(['a1', 2, True], '%a', '%b', '%c')
>>> str(myCaseProperty)
"{'a': 'a1', 'b': 2, 'c': True}"

1.2.3 With Wild format strings:

    o : ignore this field
    ooo: Ignore anything from the begining or the end.

# ooo: ignores the end of the list and start from the begining. >>> myCaseProperty = mySchema(['a1', 2, True], '%a', ooo)
>>> str(myCaseProperty)
"{'a': 'a1', 'b': 123, 'c': False}"

Only matches 'a1' to myCaseProperty.a and the other fields take their default value.

>>> myCaseProperty = mySchema(['a1', 2, True], '%a', '%b', ooo)
>>> str(myCaseProperty)
"{'a': 'a1', 'b': 2, 'c': False}"
>>> # Same as: >>> myCaseProperty = mySchema(['a1', 2, True], '%', '%', ooo)
>>> str(myCaseProperty)
"{'a': 'a1', 'b': 2, 'c': False}"

Only matches:
• 'a1'	to myCaseProperty.a
• 2	to myCaseProperty.b
And the last field c take its default value

Some CaseProperty usefull methods are:

myCaseProperty.fields()
myCaseProperty.ofields()
myCaseProperty.wks()
myCaseProperty.setField(name, value):
myCaseProperty.getField(name)

1.3 The Switch Operator literally: with Switch() as case
We see this in the next example.

1.4 List filtering, this works on the case instance.
We see this in the next example.

1.5 List Mapping, this works on the Case Property instance
We see this in the next example.



2. Cases use Cases


Sample analysing huge files (Gigas long) :


2.1 First look

Sample Datasource: For our case study we'll use an Apache server log for SSL analysis as Data Source.
This file sizes multiple Gigas octets.

We open Python interpreter:

$>python
>>> from scalike.case import *
>>> fd = open(apache.log)
>>> lines = fd.readlines()
>>> fd.close()

_ First 2 lines are:
lines = [
'192.123.234.012 - - "[29/Aug/2017:02:00:46 +0200]" "POST /my/uri HTTP/1.1" 200 624 "Apache CXF 3.0.4" "TLSv1.2" "AES128-SHA256" "BACKEND_SERVER1" "193.108.111.231" "www.my.site.com" "text/xml; charset=UTF-8" "-"',
'192.123.234.013 - - "[29/Aug/2017:02:00:46 +0200]" "POST /my/uri HTTP/1.1" 200 624 "Apache CXF 3.0.4" "TLSv1.2" "AES128-SHA256" "BACKEND_SERVER1" "193.108.111.231" "www.my.site.com" "text/xml; charset=UTF-8" "-"'
]

An arbitrary shlex on it guives :

>>> record = shlex.split(lines[0])
['192.123.234.012', '-', '-', '[29/Aug/2017:02:00:46 +0200]', 'POST /my/uri HTTP/1.1',
'200', '624', 'Apache CXF 3.0.4', 'TLSv1.2', 'AES128-SHA256', 'BACKEND_SERVER1',
'193.108.111.231', 'www.my.site.com', 'text/xml; charset=UTF-8', '-']
>>> len(line)
15



2.2 Making the case schema

_ First sample line is:
line = '
192.123.234.012 - - "[29/Aug/2017:02:00:46 +0200]" "POST /my/uri HTTP/1.1" 200 624 "Apache CXF 3.0.4" "TLSv1.2" "AES128-SHA256" "BACKEND_SERVER1" "193.108.111.231" "www.my.site.com" "text/xml; charset=UTF-8" "-"
'

_ An arbitrary shlex on it guives :
>>> line = shlex.split(line.strip())
['192.123.234.012', '-', '-', '[29/Aug/2017:02:00:46 +0200]', 'POST /my/uri HTTP/1.1', '200', '624', 'Apache CXF 3.0.4', 'TLSv1.2',
'AES128-SHA256', 'BACKEND_SERVER1', '193.108.111.231', 'www.my.site.com', 'text/xml; charset=UTF-8', '-']
>>> len(line)
15


2.3 Field dispatch:

Lines	Sample	Fields
0 to 2	'192.123.234.012', '-', '-'	Ignore
3	'[29/Aug/2017:02:00:46 +0200]'	ts (TimeStamp
4	'POST /my/uri HTTP/1.1',	Ignore
5	'200	rcode (response code)/td>
6 to 7	'624', 'Apache CXF 3.0.4',	Ignore
8	'TLSv1.2',	protocol
9	'AES128-SHA256',	cipher
10	'BACKEND_SERVER1',	Ignore
11	'193.108.111.231',	ip
12 to 14	'www.my.site.com', 'text/xml; charset=UTF-8', '-'	Ignore

Once we have created our schema, our case Property would be:
cp = sslCaseSchema(line, o,o,o, '%ts', o, '%rcode', o,o, '%protocol', '%cipher', o, '%ip', ooo)

In next chapter we'll see how to create our shema !


ARRET ICI !! 2.4 Complexe Types formatting:

TimeStamp Formatting:
_ Testing our split lambda function:
>>> '[29/Aug/2017:02:00:46 +0200]'.split()[0][1:]
'29/Aug/2017:02:00:46'
Our function will be: lambda e: e.split()[0][1:]

Testing *ts in wk:
>>> p = wk.WKS()
>>> p.ts = {'*ts': '%d/%b/%Y:%H:%M:%S'}
>>> wk.check(p, {'ts': '29/Aug/2017:02:00:46'})
>>> p.ts
datetime.datetime(2017, 8, 29, 2, 0, 46) # ok:
# We could check this also:
>>> p = wk.WKS()
>>> p.ts = {'*ts': '%d/%b/%Y:%H:%M:%S', '*withConvert':lambda e:e.split()[0][1:], '*type': 'str'}
>>> wk.check(p, {'ts': '[29/Aug/2017:02:00:46 +0200]'})
>>> p.ts
datetime.datetime(2017, 8, 29, 2, 0, 46) # ok


=> So we are sure that our Case constructor will gracefully support a wk on the TimeStamp.


2.5 Building the CaseSchema instance
sslCaseSchema = CaseSchema(('ts', {'*ts': '%d/%b/%Y:%H:%M:%S', '*withConvert':lambda e:e.split()[0][1:], '*type': 'str'}), ('rcode', {'*type': int, '*withEval': True}), 'protocol', 'cipher', 'ip')


2.6 Complete source:

import shlex, datetime
from scalike import *
lines = sclist('
192.123.234.012 - - "[29/Aug/2017:02:00:46 +0200]" "POST /my/uri HTTP/1.1" 200 624 "Apache CXF 3.0.4" "TLSv1.2" "AES128-SHA256" "BACKEND_SERVER1" "193.108.111.231" "www.my.site.com" "text/xml; charset=UTF-8" "-"
')

sslCaseSchema = CaseSchema(('ts', {'*ts': '%d/%b/%Y:%H:%M:%S', '*withConvert':lambda e:e.split()[0][1:], '*type': 'str'}), ('rcode', {'*type': int, '*withEval': True}), 'protocol', 'cipher', 'ip')
def f(e):
   e = shlex.split(e) # must be an Iterable
   with Switch(e) as case:
      # Use do_raise=True first time you run f(e) ==>
      if not case(o,o,o, '[*', o, {'*type': 'int', '*withEval': True}, ooo):return None
      # Creating our ssl record:
      cp = sslCaseSchema(e, o,o,o, '%ts', o, '%rcode', o,o, '%protocol', '%cipher', o, '%ip', ooo)
      myts = datetime.datetime(2015, 2, 28, 1, 1, 1)
      if cp.ts < myts: return None
      if (cp.protocol.startswith('SSL') or cs.protocol.startswith('RC4')):return None

return cs

# ignore_none and force_ignore allow map to acte as a filter for None value returned by fct.
l = lines.map(f, ignore_none=True, force_ignore=True)

# e.g.2:
l.map(lambda e: e.fields())



3. Analysing Huge fies using Paralline:


4. Trace:
