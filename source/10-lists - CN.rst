列表
=====

这一章展示了Python中最有用的内置(built-in)类型之一：列表。你还会进一步关于对象(objects)的以及同一个对象有多个名称(name)时会发生什么。

列表是一个序列
--------------------

类似于字符串，一个**列表**是 一个值的序列!!!。在字符串中，每个值都是字符；在一个列表中，值可以使任何数据类型。一个列表中的值称为**元素**，或者是**项目**。

有多种方法可以常见一个新的列表；最简单的方法是用方括号"["和"]"将元素包括起来:

::

    [10, 20, 30, 40]
    ['crunchy frog', 'ram bladder', 'lark vomit']

第一个例子是包含4个整数的列表。第二个是一个包含3个字符串的列表。一个列表中的元素不需要是相同的数据类型。下面的列表包含一个字符串，一个浮点数，一个整数和另一个列表:

::

    ['spam', 2.0, 5, [10, 20]]

一个列表在另一个列表中，称为嵌套。

一个不包含元素的列表称为空列表。你可以用空的方括号``[]``创建一个空列表。

正如你可能期望的，你可以将列表的值赋给变量：

::

    >>> cheeses = ['Cheddar', 'Edam', 'Gouda']
    >>> numbers = [42, 123]
    >>> empty = []
    >>> print(cheeses, numbers, empty)
    ['Cheddar', 'Edam', 'Gouda'] [42, 123] []

列表是可变的
-----------------

访问列表中元素的语法和访问字符串中字符的语法相同，都是通过 括号！！！（方括号）运算符实现的。括号中的表达式指定了 下标！！！（索引位置）。记住，下标从0开始：

::

    >>> cheeses[0]
    'Cheddar'

和字符串不同，列表是可以改变的。当括号运算符出现在赋值语句的左边，它就指向了列表中将被赋值的元素。

::

    >>> numbers = [42, 123]
    >>> numbers[1] = 5
    >>> numbers
    [42, 5]

numbers中下标为1的元素，原来是 123，现在是 5.

图 [fig.liststate] 展示了cheeses, number 和 empty 的状态图：

.. figure:: figs/liststate.pdf
   :alt: State diagram.

   状态图.

列表用外部标有"list"的盒子表示，盒子内部是列表的元素。 cheeses 是！！！（对应refers）一个有3个元素的列表，3个元素的下标分别是0,1,2。 numbers包含两个元素；状态图显示了第二个元素原来是 123，被重新赋值为 5。 empty 对应一个没有元素的列表。

列表下标的工作原理和字符串的相同：

-  任何整数表达式可以作为下标。

-  如果你试图读或写一个不存在的元素，你将会得到一个索引错误(IndexError).

-  如果下标是负数，它将从列表的末端开始访问列表。

in 运算符在列表中同样可以使用。

::

    >>> cheeses = ['Cheddar', 'Edam', 'Gouda']
    >>> 'Edam' in cheeses
    True
    >>> 'Brie' in cheeses
    False

遍历一个列表
-----------------

最常用的遍历列表的方式是使用for循环。语法和字符串类似：

::

    for cheese in cheeses:
        print(cheese)

如果你只需要读取列表中的元素，这种方法已经足够。然而，如果你想要写入或者更新列表中的元素，你需要通过下标访问。一种常用的方法是结合内置函数range和len：

::

    for i in range(len(numbers)):
        numbers[i] = numbers[i] * 2

这个循环对列表进行遍历并更新每个元素。len返回列表中的元素个数。range返回一个从0到:math:`n-1`下标的列表，其中:math:`n`是列表的长度。每次循环中，i得到下一个元素的下标。循环主体中的赋值语句使用i读取该元素旧值并且赋予其一个新值。

对一个空列表的for循环将不会执行循环的主体：

::

    for x in []:
        print('This never happens.')

尽管一个列表可以包含另一个列表，一个嵌套到另一个列表中的列表本身还是被看作一个单个元素。下面这个列表的长度是4:

::

    ['spam', 1, ['Brie', 'Roquefort', 'Pol le Veq'], [1, 2, 3]]

列表操作
---------------

+ 运算符连接多个列表:

::

    >>> a = [1, 2, 3]
    >>> b = [4, 5, 6]
    >>> c = a + b
    >>> c
    [1, 2, 3, 4, 5, 6]

运算符*以给定次数的重复一个列表:

::

    >>> [0] * 4
    [0, 0, 0, 0]
    >>> [1, 2, 3] * 3
    [1, 2, 3, 1, 2, 3, 1, 2, 3]

第一个例子重复4次.第二个例子重复了那个列表3次。

列表切片
-----------

切片运算符同样对列表适用:

::

    >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
    >>> t[1:3]
    ['b', 'c']
    >>> t[:4]
    ['a', 'b', 'c', 'd']
    >>> t[3:]
    ['d', 'e', 'f']

如果你忽略了第一个索引，切片将从列表头开始。如果你忽略了第二个，切片将会到列表尾结束。所以如果你两者都忽略，切片就是整个列表的一个拷贝。

::

    >>> t[:]
    ['a', 'b', 'c', 'd', 'e', 'f']

由于列表是可变的，通常在对列表进行修改的操作之前做一个列表的拷贝会是很有用的。
Since lists are mutable, it is often useful to make a copy before
performing operations that modify lists.

赋值语句左边的切片运算符可以更新多个元素:

::

    >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
    >>> t[1:3] = ['x', 'y']
    >>> t
    ['a', 'x', 'y', 'd', 'e', 'f']

列表方法
------------

Python为列表提供了一些方法. 例如, append 添加一个新元素到列表的末端:

::

    >>> t = ['a', 'b', 'c']
    >>> t.append('d')
    >>> t
    ['a', 'b', 'c', 'd']

extend将一个列表作为参数，并以append方式添加其中的所有元素:

::

    >>> t1 = ['a', 'b', 'c']
    >>> t2 = ['d', 'e']
    >>> t1.extend(t2)
    >>> t1
    ['a', 'b', 'c', 'd', 'e']

这个例子中t2没有改动.

sort 对列表中的元素从小到大进行排序:

::

    >>> t = ['d', 'c', 'e', 'b', 'a']
    >>> t.sort()
    >>> t
    ['a', 'b', 'c', 'd', 'e']

大部分列表的方法都是空的；他们对列表进行修改然后返回None。如果你意外的写了t.sort()，你将会对结果失望的。

映射，筛选和归并
----------------------

对列表中所有元素求和，你可以这么使用循环:

::

    def add_all(t):
        total = 0
        for x in t:
            total += x
        return total

total 被初始化为 0. 每次经过循环, x 从列表中读取一个元素. 运算符+=提供了一个快捷的更新变量的方法。. 这是增量赋值语句,

::

        total += x

等价于

::

        total = total + x

当循环执行时，totel记录了元素的和; 一个这样的变量有时称为一个**累加器**.

把一个列表中的元素加起来是一个很常用的操作，所以Python将其设置为一个内建！！！（内置）函数sum:

::

    >>> t = [1, 2, 3]
    >>> sum(t)
    6

一个像这样的将一系列的元素合并到成一个单一值的操作有时称为**归并**。

有时在你构建一个列表时需要遍历另一个列表。例如，下面的函数读取一个字符串列表作为参数，返回大写后的新列表：

::

    def capitalize_all(t):
        res = []
        for s in t:
            res.append(s.capitalize())
        return res

res 被初始化为一个空的列表; 每次循环我们附加下一个元素，所以res是另一种累加器.

类似``capitalize_all``的操作有时被称为**映射(map)**，因为它“映射”一个函数（在本例中是方法capitalize）到序列中的每个元素上。

另一个常见的操作是从列表中选择一些元素，并返回一个子列表。举例来说，下面的函数读取一个字符串列表，并返回一个仅包含大写字符串的列表:

::

    def only_upper(t):
        res = []
        for s in t:
            if s.isupper():
                res.append(s)
        return res

isupper 是一个字符串方法，如果字符串仅含有大写字母，则返回True。

一个类似``only_upper``的操作称为**筛选**，因为它选出一部份元素，而滤掉其它元素。

大部分常用列表操作可以被表示为一个映射、筛选和归并的结合。

删除元素
-----------------

有多种方法去从列表中删除一个元素。如果你知道元素的下标，你可以使用pop:

::

    >>> t = ['a', 'b', 'c']
    >>> x = t.pop(1)
    >>> t
    ['a', 'c']
    >>> x
    'b'

pop 修改列表，并返回被移除的元素. 如果你不提供下标，它将移除最后一个元素并返回其值。

如果你不需要被移除的元素，可以使用del运算符:

::

    >>> t = ['a', 'b', 'c']
    >>> del t[1]
    >>> t
    ['a', 'c']

如果你知道要删除的值，但是不知道其下标，你可以使用remove:

::

    >>> t = ['a', 'b', 'c']
    >>> t.remove('b')
    >>> t
    ['a', 'c']

remove的返回值是None.

要移除不止一个元素，你可以结合切片索引使用del:

::

    >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
    >>> del t[1:5]
    >>> t
    ['a', 'f']

同样的，切片选择到第二个下标（不包含第二个下标）中的所有元素
As usual, the slice selects all the elements up to but not including the
second index.

Lists and strings
-----------------

A string is a sequence of characters and a list is a sequence of values,
but a list of characters is not the same as a string. To convert from a
string to a list of characters, you can use list:

::

    >>> s = 'spam'
    >>> t = list(s)
    >>> t
    ['s', 'p', 'a', 'm']

Because list is the name of a built-in function, you should avoid using
it as a variable name. I also avoid l because it looks too much like 1.
So that’s why I use t.

The list function breaks a string into individual letters. If you want
to break a string into words, you can use the split method:

::

    >>> s = 'pining for the fjords'
    >>> t = s.split()
    >>> t
    ['pining', 'for', 'the', 'fjords']

An optional argument called a **delimiter** specifies which characters
to use as word boundaries. The following example uses a hyphen as a
delimiter:

::

    >>> s = 'spam-spam-spam'
    >>> delimiter = '-'
    >>> t = s.split(delimiter)
    >>> t
    ['spam', 'spam', 'spam']

join is the inverse of split. It takes a list of strings and
concatenates the elements. join is a string method, so you have to
invoke it on the delimiter and pass the list as a parameter:

::

    >>> t = ['pining', 'for', 'the', 'fjords']
    >>> delimiter = ' '
    >>> s = delimiter.join(t)
    >>> s
    'pining for the fjords'

In this case the delimiter is a space character, so join puts a space
between words. To concatenate strings without spaces, you can use the
empty string, ``''``, as a delimiter.

Objects and values
------------------

If we run these assignment statements:

::

    a = 'banana'
    b = 'banana'

We know that a and b both refer to a string, but we don’t know whether
they refer to the *same* string. There are two possible states, shown in
Figure [fig.list1].

.. figure:: figs/list1.pdf
   :alt: State diagram.

   State diagram.

In one case, a and b refer to two different objects that have the same
value. In the second case, they refer to the same object.

To check whether two variables refer to the same object, you can use the
is operator.

::

    >>> a = 'banana'
    >>> b = 'banana'
    >>> a is b
    True

In this example, Python only created one string object, and both a and b
refer to it. But when you create two lists, you get two objects:

::

    >>> a = [1, 2, 3]
    >>> b = [1, 2, 3]
    >>> a is b
    False

So the state diagram looks like Figure [fig.list2].

.. figure:: figs/list2.pdf
   :alt: State diagram.

   State diagram.

In this case we would say that the two lists are **equivalent**, because
they have the same elements, but not **identical**, because they are not
the same object. If two objects are identical, they are also equivalent,
but if they are equivalent, they are not necessarily identical.

Until now, we have been using “object” and “value” interchangeably, but
it is more precise to say that an object has a value. If you evaluate ,
you get a list object whose value is a sequence of integers. If another
list has the same elements, we say it has the same value, but it is not
the same object.

Aliasing
--------

If a refers to an object and you assign b = a, then both variables refer
to the same object:

::

    >>> a = [1, 2, 3]
    >>> b = a
    >>> b is a
    True

The state diagram looks like Figure [fig.list3].

.. figure:: figs/list3.pdf
   :alt: State diagram.

   State diagram.

The association of a variable with an object is called a **reference**.
In this example, there are two references to the same object.

An object with more than one reference has more than one name, so we say
that the object is **aliased**.

If the aliased object is mutable, changes made with one alias affect the
other:

::

    >>> b[0] = 42
    >>> a
    [42, 2, 3]

Although this behavior can be useful, it is error-prone. In general, it
is safer to avoid aliasing when you are working with mutable objects.

For immutable objects like strings, aliasing is not as much of a
problem. In this example:

::

    a = 'banana'
    b = 'banana'

It almost never makes a difference whether a and b refer to the same
string or not.

List arguments
--------------

When you pass a list to a function, the function gets a reference to the
list. If the function modifies the list, the caller sees the change. For
example, ``delete_head`` removes the first element from a list:

::

    def delete_head(t):
        del t[0]

Here’s how it is used:

::

    >>> letters = ['a', 'b', 'c']
    >>> delete_head(letters)
    >>> letters
    ['b', 'c']

The parameter t and the variable letters are aliases for the same
object. The stack diagram looks like Figure [fig.stack5].

.. figure:: figs/stack5.pdf
   :alt: Stack diagram.

   Stack diagram.

Since the list is shared by two frames, I drew it between them.

It is important to distinguish between operations that modify lists and
operations that create new lists. For example, the append method
modifies a list, but the + operator creates a new list:

::

    >>> t1 = [1, 2]
    >>> t2 = t1.append(3)
    >>> t1
    [1, 2, 3]
    >>> t2
    None

append modifies the list and returns None.

::

    >>> t3 = t1 + [4]
    >>> t1
    [1, 2, 3]
    >>> t3
    [1, 2, 3, 4]
    >>> t1

The + operator creates a new list and leaves the original list
unchanged.

This difference is important when you write functions that are supposed
to modify lists. For example, this function *does not* delete the head
of a list:

::

    def bad_delete_head(t):
        t = t[1:]              # WRONG!

The slice operator creates a new list and the assignment makes t refer
to it, but that doesn’t affect the caller.

::

    >>> t4 = [1, 2, 3]
    >>> bad_delete_head(t4)
    >>> t4
    [1, 2, 3]

At the beginning of ``bad_delete_head``, t and t4 refer to the same
list. At the end, t refers to a new list, but t4 still refers to the
original, unmodified list.

An alternative is to write a function that creates and returns a new
list. For example, tail returns all but the first element of a list:

::

    def tail(t):
        return t[1:]

This function leaves the original list unmodified. Here’s how it is
used:

::

    >>> letters = ['a', 'b', 'c']
    >>> rest = tail(letters)
    >>> rest
    ['b', 'c']

Debugging
---------

Careless use of lists (and other mutable objects) can lead to long hours
of debugging. Here are some common pitfalls and ways to avoid them:

#. Most list methods modify the argument and return None. This is the
   opposite of the string methods, which return a new string and leave
   the original alone.

   If you are used to writing string code like this:

   ::

       word = word.strip()

   It is tempting to write list code like this:

   ::

       t = t.sort()           # WRONG!

   Because sort returns None, the next operation you perform with t is
   likely to fail.

   Before using list methods and operators, you should read the
   documentation carefully and then test them in interactive mode.

#. Pick an idiom and stick with it.

   Part of the problem with lists is that there are too many ways to do
   things. For example, to remove an element from a list, you can use
   pop, remove, del, or even a slice assignment.

   To add an element, you can use the append method or the + operator.
   Assuming that t is a list and x is a list element, these are correct:

   ::

       t.append(x)
       t = t + [x]
       t += [x]

   And these are wrong:

   ::

       t.append([x])          # WRONG!
       t = t.append(x)        # WRONG!
       t + [x]                # WRONG!
       t = t + x              # WRONG!

   Try out each of these examples in interactive mode to make sure you
   understand what they do. Notice that only the last one causes a
   runtime error; the other three are legal, but they do the wrong
   thing.

#. Make copies to avoid aliasing.

   If you want to use a method like sort that modifies the argument, but
   you need to keep the original list as well, you can make a copy.

   ::

       >>> t = [3, 1, 2]
       >>> t2 = t[:]
       >>> t2.sort()
       >>> t
       [3, 1, 2]
       >>> t2
       [1, 2, 3]

   In this example you could also use the built-in function sorted,
   which returns a new, sorted list and leaves the original alone.

   ::

       >>> t2 = sorted(t)
       >>> t
       [3, 1, 2]
       >>> t2
       [1, 2, 3]

Glossary
--------

list:
    A sequence of values.

element:
    One of the values in a list (or other sequence), also called items.

nested list:
    A list that is an element of another list.

accumulator:
    A variable used in a loop to add up or accumulate a result.

augmented assignment:
    A statement that updates the value of a variable using an operator
    like ``+=``.

reduce:
    A processing pattern that traverses a sequence and accumulates the
    elements into a single result.

map:
    A processing pattern that traverses a sequence and performs an
    operation on each element.

filter:
    A processing pattern that traverses a list and selects the elements
    that satisfy some criterion.

object:
    Something a variable can refer to. An object has a type and a value.

equivalent:
    Having the same value.

identical:
    Being the same object (which implies equivalence).

reference:
    The association between a variable and its value.

aliasing:
    A circumstance where two or more variables refer to the same object.

delimiter:
    A character or string used to indicate where a string should be
    split.

Exercises
---------

You can download solutions to these exercises from
http://thinkpython2.com/code/list_exercises.py.

Write a function called ``nested_sum`` that takes a list of lists of
integers and adds up the elements from all of the nested lists. For
example:

::

    >>> t = [[1, 2], [3], [4, 5, 6]]
    >>> nested_sum(t)
    21

[cumulative]

Write a function called cumsum that takes a list of numbers and returns
the cumulative sum; that is, a new list where the :math:`i`\ th element
is the sum of the first :math:`i+1` elements from the original list. For
example:

::

    >>> t = [1, 2, 3]
    >>> cumsum(t)
    [1, 3, 6]

Write a function called ``middle`` that takes a list and returns a new
list that contains all but the first and last elements. For example:

::

    >>> t = [1, 2, 3, 4]
    >>> middle(t)
    [2, 3]

Write a function called ``chop`` that takes a list, modifies it by
removing the first and last elements, and returns None. For example:

::

    >>> t = [1, 2, 3, 4]
    >>> chop(t)
    >>> t
    [2, 3]

Write a function called ``is_sorted`` that takes a list as a parameter
and returns True if the list is sorted in ascending order and False
otherwise. For example:

::

    >>> is_sorted([1, 2, 2])
    True
    >>> is_sorted(['b', 'a'])
    False

[anagram]

Two words are anagrams if you can rearrange the letters from one to
spell the other. Write a function called ``is_anagram`` that takes two
strings and returns True if they are anagrams.

[duplicate]

Write a function called ``has_duplicates`` that takes a list and returns
True if there is any element that appears more than once. It should not
modify the original list.

This exercise pertains to the so-called Birthday Paradox, which you can
read about at http://en.wikipedia.org/wiki/Birthday_paradox.

If there are 23 students in your class, what are the chances that two of
you have the same birthday? You can estimate this probability by
generating random samples of 23 birthdays and checking for matches.
Hint: you can generate random birthdays with the randint function in the
random module.

You can download my solution from
http://thinkpython2.com/code/birthday.py.

Write a function that reads the file words.txt and builds a list with
one element per word. Write two versions of this function, one using the
append method and the other using the idiom t = t + [x]. Which one takes
longer to run? Why?

Solution: http://thinkpython2.com/code/wordlist.py.

[wordlist1] [bisection]

To check whether a word is in the word list, you could use the in
operator, but it would be slow because it searches through the words in
order.

Because the words are in alphabetical order, we can speed things up with
a bisection search (also known as binary search), which is similar to
what you do when you look a word up in the dictionary. You start in the
middle and check to see whether the word you are looking for comes
before the word in the middle of the list. If so, you search the first
half of the list the same way. Otherwise you search the second half.

Either way, you cut the remaining search space in half. If the word list
has 113,809 words, it will take about 17 steps to find the word or
conclude that it’s not there.

Write a function called ``in_bisect`` that takes a sorted list and a
target value and returns the index of the value in the list if it’s
there, or None if it’s not.

Or you could read the documentation of the bisect module and use that!
Solution: http://thinkpython2.com/code/inlist.py.

Two words are a “reverse pair” if each is the reverse of the other.
Write a program that finds all the reverse pairs in the word list.
Solution: http://thinkpython2.com/code/reverse_pair.py.

Two words “interlock” if taking alternating letters from each forms a
new word. For example, “shoe” and “cold” interlock to form “schooled”.
Solution: http://thinkpython2.com/code/interlock.py. Credit: This
exercise is inspired by an example at http://puzzlers.org.

#. Write a program that finds all pairs of words that interlock. Hint:
   don’t enumerate all pairs!

#. Can you find any words that are three-way interlocked; that is, every
   third letter forms a word, starting from the first, second or third?