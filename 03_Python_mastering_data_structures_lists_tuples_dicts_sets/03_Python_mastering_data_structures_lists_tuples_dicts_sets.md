
[![Open In
Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pmRaul/DA-Python/blob/main/03_Python_mastering_data_structures_lists_tuples_dicts_sets/03_Python_mastering_data_structures_lists_tuples_dicts_sets.ipynb)



# Python Data Structures 📊🐍



In this post, we\'ll explore the different data structures available in
`Python` that we can leverage for our projects. Libraries like `Numpy`
or `Pandas`, which we will talk about later, are designed to extend
these data structures for more advanced data analysis tasks. The
structures we\'ll cover include `tuples`, `lists`, `dicts`, and `sets`.



## Tuples 📦



A `tuple` is an `immutable` object with a fixed length. This means that
once created, a `tuple` cannot be modified, making it a great choice for
encapsulating data that shouldn\'t change. To define a `tuple`, simply
create a sequence of values separated by commas within parentheses.


 
``` python
t = (1, 2, 3)
t
```

 {.output .execute_result execution_count="1"}
    (1, 2, 3)




You can access the different values in a `tuple` using their index in
the sequence.


 
``` python
t[0]
```

 {.output .execute_result execution_count="3"}
    1




> ⚠️ Remember: in `Python`, the first index is always `0`, and the last
> one is the length of the object minus 1. Trying to access an index
> outside this range will result in an error.


 
``` python
t[len(t)-1]
```

 {.output .execute_result execution_count="6"}
    3




Since a `tuple` is an `immutable` object, you cannot change any of its
values once it\'s created.


 
``` python
t[0] = 4
```

 {.output .error ename="TypeError" evalue="'tuple' object does not support item assignment"}




You can apply certain operators to a `tuple`. For instance, the `+`
operator allows you to concatenate multiple tuples, and the `*` operator
repeats a tuple a specified number of times.


 
``` python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

t1 + t2
```

 {.output .execute_result execution_count="9"}
    (1, 2, 3, 4, 5, 6)



 
``` python
t1*3
```

 {.output .execute_result execution_count="10"}
    (1, 2, 3, 1, 2, 3, 1, 2, 3)




You can unpack a `tuple`\'s values into individual variables using the
`=` operator.


 
``` python
a, b, c = t1
b
```

 {.output .execute_result execution_count="13"}
    2




This is commonly used when extracting values returned by a `function`,
which we\'ll discuss in a future post.

In a `tuple`, you can include values of different types.


 
``` python
t = (1, "hello", True)
t
```

 {.output .execute_result execution_count="15"}
    (1, 'hello', True)




You can also iterate over the values in a `tuple` like this:


 
``` python
for item in t:
    print(item)
```

 {.output .stream .stdout}
    1
    hello
    True




## Lists 📃



A `list` is similar to a `tuple`, but it is `mutable`, which means you
can modify its length and content. You define a `list` by placing a
sequence of values separated by commas between square brackets.


 
``` python
l = [1, 2, 3]
l
```

 {.output .execute_result execution_count="31"}
    [1, 2, 3]




You can use `list` methods to add or remove elements.


 
``` python
l.append(4)
l
```

 {.output .execute_result execution_count="32"}
    [1, 2, 3, 4]



 
``` python
l.insert(2, 2.5)
l
```

 {.output .execute_result execution_count="33"}
    [1, 2, 2.5, 3, 4]



 
``` python
l.pop(2)
```

 {.output .execute_result execution_count="34"}
    2.5




You can also remove an element by its value.


 
``` python
l.remove(3)
l
```

 {.output .execute_result execution_count="36"}
    [1, 2, 4]




You can check if a `list` contains a specific element.


 
``` python
3 in l
```

 {.output .execute_result execution_count="37"}
    False




Like `tuples`, you can use operators to concatenate or repeat `lists`.


 
``` python
l1 = [1, 2, 3]
l2 = ["hello", "world"]

l1 + l2
```

 {.output .execute_result execution_count="40"}
    [1, 2, 3, 'hello', 'world']



 
``` python
l1*3
```

 {.output .execute_result execution_count="41"}
    [1, 2, 3, 1, 2, 3, 1, 2, 3]




You can access a specific element by its index.


 
``` python
l = [1, 2, 3, 4]
l[0]
```

 {.output .execute_result execution_count="44"}
    1




You can also slice a `list` to retrieve a subset of elements.


 
``` python
l[1:3]
```

 {.output .execute_result execution_count="46"}
    [2, 3]




You can use negative indices to access elements relative to the end of
the `list`.


 
``` python
l[-1]
```

 {.output .execute_result execution_count="50"}
    4




You can reverse a `list` by using slicing.


 
``` python
l[::-1]
```

 {.output .execute_result execution_count="55"}
    [4, 3, 2, 1]




### Sequential Functions 🔄



In `Python`, there are several functions that allow you to iterate over
sequences.


 
``` python
for i, v in enumerate(l):
    print(i, v)
```

 {.output .stream .stdout}
    0 1
    1 2
    2 3
    3 4



 
``` python
for v1, v2 in zip(l1, l2):
    print(v1, v2)
```

 {.output .stream .stdout}
    1 hello
    2 world



 
``` python
for v in reversed(l):
    print(v)
```

 {.output .stream .stdout}
    4
    3
    2
    1




## Dicts 📋



`dict` is one of the most important data structures in `Python`. Also
known as `hash map`, it consists of key-value pairs, where both the
`key` and the `value` are `Python` objects. You define a `dict` using a
sequence of key-value pairs within curly braces.


 
``` python
d = {'a': 1, 'b': 2, 'c': 3}
d
```

 {.output .execute_result execution_count="60"}
    {'a': 1, 'b': 2, 'c': 3}




You can add new values by specifying a new `key` and `value`.


 
``` python
d['d'] = 4
d
```

 {.output .execute_result execution_count="61"}
    {'a': 1, 'b': 2, 'c': 3, 'd': 4}




You can check if a `dict` contains a specific key.


 
``` python
'a' in d
```

 {.output .execute_result execution_count="62"}
    True




You can delete entries in a `dict` using the `del` keyword.


 
``` python
del d['d']
d
```

 {.output .execute_result execution_count="64"}
    {'a': 1, 'b': 2, 'c': 3}




You can get a list of all the `keys` or `values` in a `dict`.


 
``` python
d.keys()
```

 {.output .execute_result execution_count="65"}
    dict_keys(['a', 'b', 'c'])



 
``` python
d.values()
```

 {.output .execute_result execution_count="66"}
    dict_values([1, 2, 3])




You can merge two `dicts` using the `update` method.


 
``` python
d2 = {'d': 4, 'e': 5}
d.update(d2)
d
```

 {.output .execute_result execution_count="68"}
    {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}




It is very common in `Python` to create `dicts` from `lists`.


 
``` python
d = {}
keys = ['a', 'b', 'c']
values = [1, 2, 3]
for k, v in zip(keys, values):
    d[k] = v
d
```

 {.output .execute_result execution_count="69"}
    {'a': 1, 'b': 2, 'c': 3}




## Sets 🛠️



A `set` is an unordered collection of unique `objects`, similar to a
`dict`, but it only contains keys, not values. You create a `set` by
placing a sequence of values separated by commas within curly braces.


 
``` python
s = {1, 2, 3}
s
```

 {.output .execute_result execution_count="70"}
    {1, 2, 3}




You have several `methods` at your disposal to work with `sets`.


 
``` python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

a.union(b)
```

 {.output .execute_result execution_count="72"}
    {1, 2, 3, 4, 5, 6}



 
``` python
a.intersection(b)
```

 {.output .execute_result execution_count="73"}
    {3, 4}



 
``` python
{1, 2}.issubset(a)
```

 {.output .execute_result execution_count="75"}
    True




## List Comprehension ✨



`List comprehension` is one of the most useful features in `Python`, as
it provides a quick and concise way to create a new list from another
one, while filtering or transforming elements.


 
``` python
l = [1, 2, 3, 4, 5]
l2 = [2*i for i in l]
l2
```

 {.output .execute_result execution_count="78"}
    [2, 4, 6, 8, 10]




You can use equivalent expressions with other data structures, such as
`dicts`.


 
``` python
l1 = ['a', 'b', 'c']
l2 = [1, 2, 3]
d = {k: v for k, v in zip(l1, l2) if v <= 2}
d
```

 {.output .execute_result execution_count="81"}
    {'a': 1, 'b': 2}




## Summary 📝



In this post, we covered the data structures that `Python` offers and
the most useful functions when working with them. We can use `tuples`,
`lists`, `dicts`, and `sets` to group `Python` objects into structures
with their own entity and functionality. Data analysis libraries like
`Numpy` and `Pandas` extend these structures and functionalities for
more complex tasks.



## Exercises 🛠️📚



### Task 1: Manipulate a List 📃🔄

**Instructions:**

1.  Create a list `l = [10, 20, 30, 40]`
2.  Append the value `50` to the list.
3.  Insert the value `25` at index 2.
4.  Remove the value `40` from the list.


<details>
  <summary>🔍 Reveal Solution</summary>
  
```python
l = [10, 20, 30, 40]
l.append(50)
l.insert(2, 25)
l.remove(40)
l
```

</details>




### Task 2: Work with Dicts 📋✨

**Instructions:**

1.  Create a dictionary `d = {'a': 1, 'b': 2}`
2.  Add the key-value pair `'c': 3`
3.  Delete the key `'b'`


<details>
  <summary>🔍 Reveal Solution</summary>

```python
d = {'a': 1, 'b': 2}
d['c'] = 3
del d['b']
d
```

</details>




### Task 3: Explore Sets 🛠️💡

**Instructions:**

1.  Create two sets `a = {1, 2, 3}` and `b = {3, 4, 5}`
2.  Find the union and intersection of both sets.


<details>
  <summary>🔍 Reveal Solution</summary>

```python
a = {1, 2, 3}
b = {3, 4, 5}
a.union(b)
a.intersection(b)
```

</details>


