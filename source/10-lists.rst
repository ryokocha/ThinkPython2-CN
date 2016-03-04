Lists
列表
=====

This chapter presents one of Python’s most useful built-in types, lists.
You will also learn more about objects and what can happen when you have
more than one name for the same object.
这一章展示了Python中最有用的内置(built-in)类型之一：列表。你还会进一步关于对象(objects)的以及同一个对象有多个名称(name)时会发生什么。

A list is a sequence
一个列表是一个序列
--------------------

Like a string, a **list** is a sequence of values. In a string, the
values are characters; in a list, they can be any type. The values in a
list are called **elements** or sometimes **items**.
类似于字符串，一个**列表**是 一个值的序列。在字符串中，每个值都是字符；在一个列表中，值可以使任何数据类型。一个列表中的值称为**元素**，或者是**项目**。

There are several ways to create a new list; the simplest is to enclose
the elements in square brackets (``[`` and ``]``):
有多种方法可以常见一个新的列表；最简单的方法是用方括号"["和"]"将元素包括起来:

::

    [10, 20, 30, 40]
    ['crunchy frog', 'ram bladder', 'lark vomit']

The first example is a list of four integers. The second is a list of
three strings. The elements of a list don’t have to be the same type.
The following list contains a string, a float, an integer, and (lo!)
another list:
第一个例子是包含4个整数的列表。第二个是一个包含3个字符串的列表。一个列表中的元素不需要是相同的数据类型。下面的列表包含一个字符串，一个浮点数，一个整数和另一个列表:

::

    ['spam', 2.0, 5, [10, 20]]

A list within another list is **nested**.
一个列表在另一个列表中，称为嵌套。

A list that contains no elements is called an empty list; you can create
one with empty brackets, ``[]``.
一个不包含元素的列表称为空列表。你可以用空的方括号``[]``创建一个空列表。

As you might expect, you can assign list values to variables:
正如你可能期望的，你可以将列表的值赋给变量：

::

    >>> cheeses = ['Cheddar', 'Edam', 'Gouda']
    >>> numbers = [42, 123]
    >>> empty = []
    >>> print(cheeses, numbers, empty)
    ['Cheddar', 'Edam', 'Gouda'] [42, 123] []

Lists are mutable
列表是可变的
-----------------

The syntax for accessing the elements of a list is the same as for
accessing the characters of a string—the bracket operator. The
expression inside the brackets specifies the index. Remember that the
indices start at 0:
访问列表中元素的语法和访问字符串中字符的语法相同，都是通过 括号（方括号？）运算符实现的。括号中的表达式指定了 下标（索引位置？）。记住，下标从0开始：

::

    >>> cheeses[0]
    'Cheddar'

Unlike strings, lists are mutable. When the bracket operator appears on
the left side of an assignment, it identifies the element of the list
that will be assigned.
和字符串不同，列表是可以改变的。当括号运算符出现在赋值语句的左边，它就指向了列表中将被赋值的元素。

::

    >>> numbers = [42, 123]
    >>> numbers[1] = 5
    >>> numbers
    [42, 5]

The one-eth element of numbers, which used to be 123, is now 5.
numbers中下标为1的元素，原来是 123，现在是 5.

Figure [fig.liststate] shows the state diagram for cheeses, numbers and
empty:
图 [fig.liststate] 展示了cheeses, number 和 empty 的状态：

.. figure:: figs/liststate.pdf
   :alt: State diagram.

   State diagram.

Lists are represented by boxes with the word “list” outside and the
elements of the list inside. cheeses refers to a list with three
elements indexed 0, 1 and 2. numbers contains two elements; the diagram
shows that the value of the second element has been reassigned from 123
to 5. empty refers to a list with no elements.
列表用外部标有"list"的盒子表示，盒子内部是列表的元素。 cheeses 指向一个有3个元素的列表，3个元素的下标分别是0,1,2。numbers包含两个元素；状态图显示了第二个元素原来是 123，被重新赋值为 5。 empty对应一个没有元素的列表。

List indices work the same way as string indices:
列表下标的工作原理和字符串的相同：

-  Any integer expression can be used as an index.
-  任何整数表达式可以作为下标。

-  If you try to read or write an element that does not exist, you get
   an IndexError.
-  如果你试图读或写一个不存在的元素，你将会得到一个索引错误(IndexError).

-  If an index has a negative value, it counts backward from the end of
   the list.
-  如果下标是负数，它将从列表的末端开始访问列表。

The in operator also works on lists.
in 运算符在列表中同样可以使用。
::

    >>> cheeses = ['Cheddar', 'Edam', 'Gouda']
    >>> 'Edam' in cheeses
    True
    >>> 'Brie' in cheeses
    False

Traversing a list
遍历一个列表
-----------------

The most common way to traverse the elements of a list is with a for
loop. The syntax is the same as for strings:
最常用的遍历列表的方式是使用for循环。语法和字符串类似：

::

    for cheese in cheeses:
        print(cheese)

This works well if you only need to read the elements of the list. But
if you want to write or update the elements, you need the indices. A
common way to do that is to combine the built-in functions range and
len:
如果你只需要读取列表中的元素，这种方法已经足够。然而，如果你想要写入或者更新列表中的元素，你需要通过下标访问。一种常用的方法是结合内置函数range和len：

::

    for i in range(len(numbers)):
        numbers[i] = numbers[i] * 2

This loop traverses the list and updates each element. len returns the
number of elements in the list. range returns a list of indices from 0
to :math:`n-1`, where :math:`n` is the length of the list. Each time
through the loop i gets the index of the next element. The assignment
statement in the body uses i to read the old value of the element and to
assign the new value.
这个循环对列表进行遍历并更新每个元素。len返回列表中的元素个数。range返回一个从0到:math:`n-1`下标的列表，其中:math:`n`是列表的长度。每次循环中，i得到下一个元素的下标。循环主体中的赋值语句使用i读取该元素旧值并且赋予其一个新值。

A for loop over an empty list never runs the body:
对一个空列表的for循环将不会执行循环的主体：

::

    for x in []:
        print('This never happens.')

Although a list can contain another list, the nested list still counts
as a single element. The length of this list is four:
尽管一个列表可以包含另一个列表，一个嵌套到另一个列表中的列表本身还是被看作一个单个元素。下面这个列表的长度是4:

::

    ['spam', 1, ['Brie', 'Roquefort', 'Pol le Veq'], [1, 2, 3]]

List operations
列表操作
---------------

The + operator concatenates lists:
+ 运算符连接多个列表:

::

    >>> a = [1, 2, 3]
    >>> b = [4, 5, 6]
    >>> c = a + b
    >>> c
    [1, 2, 3, 4, 5, 6]

The operator repeats a list a given number of times:
运算符*以给定次数的重复一个列表:

::

    >>> [0] * 4
    [0, 0, 0, 0]
    >>> [1, 2, 3] * 3
    [1, 2, 3, 1, 2, 3, 1, 2, 3]

The first example repeats four times. The second example repeats the
list three times.
第一个例子重复4次.第二个例子重复了那个列表3次。

List slices
列表切片
-----------

The slice operator also works on lists:
切片运算符同样对列表适用:

::

    >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
    >>> t[1:3]
    ['b', 'c']
    >>> t[:4]
    ['a', 'b', 'c', 'd']
    >>> t[3:]
    ['d', 'e', 'f']

If you omit the first index, the slice starts at the beginning. If you
omit the second, the slice goes to the end. So if you omit both, the
slice is a copy of the whole list.
如果你忽略了第一个索引，切片将从列表头开始。如果你忽略了第二个，切片将会到列表尾结束。所以如果你两者都忽略，切片就是整个列表的一个拷贝。

::

    >>> t[:]
    ['a', 'b', 'c', 'd', 'e', 'f']

Since lists are mutable, it is often useful to make a copy before
performing operations that modify lists.
由于列表是可变的，通常在对列表进行修改的操作之前做一个列表的拷贝会是很有用的。

A slice operator on the left side of an assignment can update multiple
elements:
赋值语句左边的切片运算符可以更新多个元素:

::

    >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
    >>> t[1:3] = ['x', 'y']
    >>> t
    ['a', 'x', 'y', 'd', 'e', 'f']

List methods
列表方法
------------

Python provides methods that operate on lists. For example, append adds
a new element to the end of a list:
Python为列表提供了一些方法. 例如, append 添加一个新元素到列表的末端:

::

    >>> t = ['a', 'b', 'c']
    >>> t.append('d')
    >>> t
    ['a', 'b', 'c', 'd']

extend takes a list as an argument and appends all of the elements:
extend将一个列表作为参数，并以append方式添加其中的所有元素:

::

    >>> t1 = ['a', 'b', 'c']
    >>> t2 = ['d', 'e']
    >>> t1.extend(t2)
    >>> t1
    ['a', 'b', 'c', 'd', 'e']

This example leaves t2 unmodified.
这个例子中t2没有改动.

sort arranges the elements of the list from low to high:
sort 对列表中的元素从小到大进行排序:

::

    >>> t = ['d', 'c', 'e', 'b', 'a']
    >>> t.sort()
    >>> t
    ['a', 'b', 'c', 'd', 'e']

Most list methods are void; they modify the list and return None. If you
accidentally write t = t.sort(), you will be disappointed with the
result.
大部分列表的方法都是空的；他们对列表进行修改然后返回None。如果你意外的写了t.sort()，你将会对结果失望的。

Map, filter and reduce
映射，筛选和归并
----------------------

To add up all the numbers in a list, you can use a loop like this:
对列表中所有元素求和，你可以这么使用循环:

::

    def add_all(t):
        total = 0
        for x in t:
            total += x
        return total

total is initialized to 0. Each time through the loop, x gets one
element from the list. The += operator provides a short way to update a
variable. This **augmented assignment statement**,
total 被初始化为 0. 每次经过循环, x 从列表中读取一个元素. 运算符+=提供了一个快捷的更新变量的方法。. 这是增量赋值语句,

::

        total += x

is equivalent to
等价于

::

        total = total + x

As the loop runs, total accumulates the sum of the elements; a variable
used this way is sometimes called an **accumulator**.
当循环执行时，totel记录了元素的和; 一个这样的变量有时称为一个**累加器**.

Adding up the elements of a list is such a common operation that Python
provides it as a built-in function, sum:
把一个列表中的元素加起来是一个很常用的操作，所以Python将其设置为一个内建内置函数sum:

::

    >>> t = [1, 2, 3]
    >>> sum(t)
    6

An operation like this that combines a sequence of elements into a
single value is sometimes called **reduce**.
一个像这样的将一系列的元素合并到成一个单一值的操作有时称为**归并**。

Sometimes you want to traverse one list while building another. For
example, the following function takes a list of strings and returns a
new list that contains capitalized strings:
有时在你构建一个列表时需要遍历另一个列表。例如，下面的函数读取一个字符串列表作为参数，返回大写后的新列表：

::

    def capitalize_all(t):
        res = []
        for s in t:
            res.append(s.capitalize())
        return res

res is initialized with an empty list; each time through the loop, we
append the next element. So res is another kind of accumulator.
res 被初始化为一个空的列表; 每次循环我们附加下一个元素，所以res是另一种累加器.

An operation like ``capitalize_all`` is sometimes called a **map**
because it “maps” a function (in this case the method capitalize) onto
each of the elements in a sequence.
类似``capitalize_all``的操作有时被称为**映射(map)**，因为它“映射”一个函数（在本例中是方法capitalize）到序列中的每个元素上。

Another common operation is to select some of the elements from a list
and return a sublist. For example, the following function takes a list
of strings and returns a list that contains only the uppercase strings:
另一个常见的操作是从列表中选择一些元素，并返回一个子列表。举例来说，下面的函数读取一个字符串列表，并返回一个仅包含大写字符串的列表:

::

    def only_upper(t):
        res = []
        for s in t:
            if s.isupper():
                res.append(s)
        return res

isupper is a string method that returns True if the string contains only
upper case letters.
isupper 是一个字符串方法，如果字符串仅含有大写字母，则返回True。

An operation like ``only_upper`` is called a **filter** because it
selects some of the elements and filters out the others.
一个类似``only_upper``的操作称为**筛选**

Most common list operations can be expressed as a combination of map,
filter and reduce.
大部分常用列表操作可以被表示为一个映射、筛选和归并的结合。

Deleting elements
删除元素
-----------------

There are several ways to delete elements from a list. If you know the
index of the element you want, you can use pop:
有多种方法去从列表中删除一个元素。如果你知道元素的下标，你可以使用pop:

::

    >>> t = ['a', 'b', 'c']
    >>> x = t.pop(1)
    >>> t
    ['a', 'c']
    >>> x
    'b'

pop modifies the list and returns the element that was removed. If you
don’t provide an index, it deletes and returns the last element.
pop 修改列表，并返回被移除的元素.如果你不提供下标，它将移除最后一个元素并返回其值。

If you don’t need the removed value, you can use the del operator:
如果你不需要被移除的元素，可以使用del运算符:

::

    >>> t = ['a', 'b', 'c']
    >>> del t[1]
    >>> t
    ['a', 'c']

If you know the element you want to remove (but not the index), you can
use remove:
如果你知道要删除的值，但是不知道其下标，你可以使用remove:

::

    >>> t = ['a', 'b', 'c']
    >>> t.remove('b')
    >>> t
    ['a', 'c']

The return value from remove is None.
remove的返回值是None.

To remove more than one element, you can use del with a slice index:
要移除不止一个元素，你可以结合切片索引使用del:

::

    >>> t = ['a', 'b', 'c', 'd', 'e', 'f']
    >>> del t[1:5]
    >>> t
    ['a', 'f']

As usual, the slice selects all the elements up to but not including the
second index.
同样的，切片选择到第二个下标（不包含第二个下标）中的所有元素

Lists and strings
列表和字符串
-----------------

A string is a sequence of characters and a list is a sequence of values,
but a list of characters is not the same as a string. To convert from a
string to a list of characters, you can use list:
一个字符串是一个字符的序列，一个列表是一个值的序列。但是一个字符的列表不同于字符串。可以使用list讲一个字符串转换为字符的列表:

::

    >>> s = 'spam'
    >>> t = list(s)
    >>> t
    ['s', 'p', 'a', 'm']

Because list is the name of a built-in function, you should avoid using
it as a variable name. I also avoid l because it looks too much like 1.
So that’s why I use t.
由于list是内建函数名，所以你应避免使用它作为一个变量名。我同样避免使用l，因为它看起来很像1，因此我使用t。

The list function breaks a string into individual letters. If you want
to break a string into words, you can use the split method:
list函数将字符串分割成单独的字符。如果你想将一个字符串分割成一些单词，你可以使用split方法:

::

    >>> s = 'pining for the fjords'
    >>> t = s.split()
    >>> t
    ['pining', 'for', 'the', 'fjords']

An optional argument called a **delimiter** specifies which characters
to use as word boundaries. The following example uses a hyphen as a
delimiter:
一个叫做**分隔符**的可选参数指定了什么字符作为单词之间的分界线。下面的例子使用连字符作为分隔符:

::

    >>> s = 'spam-spam-spam'
    >>> delimiter = '-'
    >>> t = s.split(delimiter)
    >>> t
    ['spam', 'spam', 'spam']

join is the inverse of split. It takes a list of strings and
concatenates the elements. join is a string method, so you have to
invoke it on the delimiter and pass the list as a parameter:
join功能和split相反。它将一个字符串列表的元素连接起来。join是一个字符串方法，所以你需要在一个分隔符上调用它，并传入一个列表作为参数:

::

    >>> t = ['pining', 'for', 'the', 'fjords']
    >>> delimiter = ' '
    >>> s = delimiter.join(t)
    >>> s
    'pining for the fjords'

In this case the delimiter is a space character, so join puts a space
between words. To concatenate strings without spaces, you can use the
empty string, ``''``, as a delimiter.
在这个例子中分隔符是一个空格，所以join在单词之间添加一个空格。如果不使用空格连接字符串，你可以使用空字符串``''``作为分割符。

Objects and values
对象和值
------------------

If we run these assignment statements:
如果我们执行以下的赋值语句:

::

    a = 'banana'
    b = 'banana'

We know that a and b both refer to a string, but we don’t know whether
they refer to the *same* string. There are two possible states, shown in
Figure [fig.list1].
我们知道a和b都指向一个字符串，但是我们不知道是否他们指向*同一个*字符串。这里有两种可能的状态，在下图[fig.list1]中表示了出来：

.. figure:: figs/list1.pdf
   :alt: State diagram.

   State diagram.

In one case, a and b refer to two different objects that have the same
value. In the second case, they refer to the same object.
在一种情况中，a和b指向两个有相同值的不同对象。在第二种情况中，它们指向同一个对象。

To check whether two variables refer to the same object, you can use the
is operator.
为了查看是否两个变量指向同一个同一个对象，你可以使用is运算符。

::

    >>> a = 'banana'
    >>> b = 'banana'
    >>> a is b
    True

In this example, Python only created one string object, and both a and b
refer to it. But when you create two lists, you get two objects:
在这个例子中，Python仅生成了一个字符串对象，a和b都指向它。但是当你创建两个列表，你将得到两个对象:

::

    >>> a = [1, 2, 3]
    >>> b = [1, 2, 3]
    >>> a is b
    False

So the state diagram looks like Figure [fig.list2].
状态图看起来是如图 [fig.list2]这样的.

.. figure:: figs/list2.pdf
   :alt: State diagram.

   State diagram.

In this case we would say that the two lists are **equivalent**, because
they have the same elements, but not **identical**, because they are not
the same object. If two objects are identical, they are also equivalent,
but if they are equivalent, they are not necessarily identical.
在这个例子中，我们称这两个列表是**相等**的，因为它们有相同的元素。但它们不是**相同**的，因为他们不是同一个对象。如果两个对象是**相同**的，它们也是相等的，但是如果它们是相等的，他们不一定是相同的。

Until now, we have been using “object” and “value” interchangeably, but
it is more precise to say that an object has a value. If you evaluate ,
you get a list object whose value is a sequence of integers. If another
list has the same elements, we say it has the same value, but it is not
the same object.
目前，我们一直交换的使用"对象"和“值”，但是更精确的说是一个对象拥有一个值。如果你运行 （内容缺失？），你会得到一个值为一个整数序列的列表对象。如果另一个列表有同样的元素，我们说它有相同的值，但是它并不是同一个对象。

Aliasing
别名使用
--------

If a refers to an object and you assign b = a, then both variables refer
to the same object:
如果a指向一个对象，然后你赋值b = a，那么两个变量指向同一个对象:

::

    >>> a = [1, 2, 3]
    >>> b = a
    >>> b is a
    True

The state diagram looks like Figure [fig.list3].
状态图如图 [fig.list3]所示.

.. figure:: figs/list3.pdf
   :alt: State diagram.

   State diagram.

The association of a variable with an object is called a **reference**.
In this example, there are two references to the same object.
一个变量和一个对象之间的关联称为**reference**。在这个例子中，有两个对同一个对象的引用。

An object with more than one reference has more than one name, so we say
that the object is **aliased**.
如果一个对象有多于一个引用，我们成这个对象是**有别名的**。

If the aliased object is mutable, changes made with one alias affect the
other:
如果一个有别名的对象是可变的，对其中一个别名的改变对影响到其它的别名：

::

    >>> b[0] = 42
    >>> a
    [42, 2, 3]

Although this behavior can be useful, it is error-prone. In general, it
is safer to avoid aliasing when you are working with mutable objects.
尽管这个行为很有用，但是容易造成错误。通常，对于可改变的对象避免使用别名相对更安全。

For immutable objects like strings, aliasing is not as much of a
problem. In this example:
对于不可改变的对象，使用别名没有什么问题。例如：

::

    a = 'banana'
    b = 'banana'

It almost never makes a difference whether a and b refer to the same
string or not.
使用a或b指向同一个字符串基本上没有任何区别。

List arguments
列表参数
--------------

When you pass a list to a function, the function gets a reference to the
list. If the function modifies the list, the caller sees the change. For
example, ``delete_head`` removes the first element from a list:
当你将一个列表作为参数传给一个函数，函数将得到这个列表的一个引用。如果函数对这个列表参数进行了修改，在原来的列表中会看见变动。例如， ``delete_head``删除列表的第一个元素：

::

    def delete_head(t):
        del t[0]

Here’s how it is used:
它是这么起作用的:

::

    >>> letters = ['a', 'b', 'c']
    >>> delete_head(letters)
    >>> letters
    ['b', 'c']

The parameter t and the variable letters are aliases for the same
object. The stack diagram looks like Figure [fig.stack5].
参数 t 和变量 letters 是同一个对象的别名。栈图如下 [fig.stack5].

.. figure:: figs/stack5.pdf
   :alt: Stack diagram.

   Stack diagram.

Since the list is shared by two frames, I drew it between them.
由于列表被两个帧共享，我把它画在它们中间。

It is important to distinguish between operations that modify lists and
operations that create new lists. For example, the append method
modifies a list, but the + operator creates a new list:
需要注意的是修改列表操作和创建列表操作间的区别，例如， append 方法是修改一个列表，而 + 运算符是创建一个新的列表：

::

    >>> t1 = [1, 2]
    >>> t2 = t1.append(3)
    >>> t1
    [1, 2, 3]
    >>> t2
    None

append modifies the list and returns None.
append修改列表并返回None。

::

    >>> t3 = t1 + [4]
    >>> t1
    [1, 2, 3]
    >>> t3
    [1, 2, 3, 4]
    >>> t1

The + operator creates a new list and leaves the original list
unchanged.
运算符 + 创建了一个新列表，而不改变原始的列表。

This difference is important when you write functions that are supposed
to modify lists. For example, this function *does not* delete the head
of a list:
如果你要编写一个修改列表的函数，这一点就很重要。例如，这个函数*不会*删除列表的第一个元素：

::

    def bad_delete_head(t):
        t = t[1:]              # WRONG!

The slice operator creates a new list and the assignment makes t refer
to it, but that doesn’t affect the caller.
切片操作创建了一个新列表，然后这个表达式让 t 指向了它，但是并不会影响原来被调用的列表。

::

    >>> t4 = [1, 2, 3]
    >>> bad_delete_head(t4)
    >>> t4
    [1, 2, 3]

At the beginning of ``bad_delete_head``, t and t4 refer to the same
list. At the end, t refers to a new list, but t4 still refers to the
original, unmodified list.
在 ``bad_delete_head``的开始，t和t4指向同一个列表。在结束时，t指向一个新列表，但是t4仍然指向原来的没有被改动列表。

An alternative is to write a function that creates and returns a new
list. For example, tail returns all but the first element of a list:
一个替代的写法是写一个函数来创建并返回一个新的列表。例如，tail返回列表中除了第一个之外的所有元素：

::

    def tail(t):
        return t[1:]

This function leaves the original list unmodified. Here’s how it is
used:
这个函数不会修改原来的列表。这里展示了它是怎么使用的：

::

    >>> letters = ['a', 'b', 'c']
    >>> rest = tail(letters)
    >>> rest
    ['b', 'c']

Debugging
调试
---------

Careless use of lists (and other mutable objects) can lead to long hours
of debugging. Here are some common pitfalls and ways to avoid them:
粗心的使用列表（以及其他可改变的对象）会导致长时间的调试。下面给出一些常见的陷阱以及避免它们的方法：

#. Most list methods modify the argument and return None. This is the
   opposite of the string methods, which return a new string and leave
   the original alone.
#. 大多数的列表的方法对参数进行修改，然后返回None。这和字符串的方法相反。字符串的方法会保留原始的字符串并返回一个新的字符串。

   If you are used to writing string code like this:
   如果你习惯这样写字符串代码：

   ::

       word = word.strip()

   It is tempting to write list code like this:
   那么你很可能会写出下面的代码：

   ::

       t = t.sort()           # WRONG!

   Because sort returns None, the next operation you perform with t is
   likely to fail.
   因为sort返回None，所以你的下一个对t执行的操作很可能会失败。

   Before using list methods and operators, you should read the
   documentation carefully and then test them in interactive mode.
   在使用list方法和操作符之前，你应该仔细的阅读文档然后在交互模式下测试。

#. Pick an idiom and stick with it.
#. 养成自己的代码风格.

   Part of the problem with lists is that there are too many ways to do
   things. For example, to remove an element from a list, you can use
   pop, remove, del, or even a slice assignment.
   列表的一个问题就是有太多途径去做同样的事情。例如，要删除列表中的一个元素，你可以使用pop，remove，del甚至切片赋值。

   To add an element, you can use the append method or the + operator.
   Assuming that t is a list and x is a list element, these are correct:
   要添加一个元素，你可以使用append方法或者+运算符。假设t是一个列表，x是一个列表元素，以下是正确的：

   ::

       t.append(x)
       t = t + [x]
       t += [x]

   And these are wrong:
   而这些是错误的：

   ::

       t.append([x])          # WRONG!
       t = t.append(x)        # WRONG!
       t + [x]                # WRONG!
       t = t + x              # WRONG!

   Try out each of these examples in interactive mode to make sure you
   understand what they do. Notice that only the last one causes a
   runtime error; the other three are legal, but they do the wrong
   thing.
   在交互模式下测试每一个例子，保证你明白它们做了什么。注意只有最后一个会导致运行时错误，其他的都是合乎规范的的，但做了错误的事情。

#. Make copies to avoid aliasing.
#. 通过创建拷贝来避免别名.

   If you want to use a method like sort that modifies the argument, but
   you need to keep the original list as well, you can make a copy.
   如果你要使用类似 sort 的方法来修改参数，但同时有要保留原列表，你可以创建一个拷贝。

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
   在这个例子中你还可以使用内建函数 sorted，它将返回一个新的已排序的列表，原列表将保持不变。

   ::

       >>> t2 = sorted(t)
       >>> t
       [3, 1, 2]
       >>> t2
       [1, 2, 3]

Glossary
术语
--------

list:
    A sequence of values.
列表:
    一个值的序列。

element:
    One of the values in a list (or other sequence), also called items.
元素:
    列表（或序列）中的一个值，也称为项目。

nested list:
    A list that is an element of another list.
嵌套列表:
    一个作为另一个列表的元素的列表。

accumulator:
    A variable used in a loop to add up or accumulate a result.
累加器:
    循环中用于相加或累积出一个结果的变量。

augmented assignment:
    A statement that updates the value of a variable using an operator
    like ``+=``.
增量赋值:
    一个使用类似``+=``操作符来更新一个变量的值的语句。

reduce:
    A processing pattern that traverses a sequence and accumulates the
    elements into a single result.
归并:
    遍历序列，将所有元素求和为一个值的处理模式。

map:
    A processing pattern that traverses a sequence and performs an
    operation on each element.
映射:
    遍历序列，对每个元素执行操作的处理模式。

filter:
    A processing pattern that traverses a list and selects the elements
    that satisfy some criterion.
筛选:
    遍历序列，选出满足一定标准的元素的处理模式。

object:
    Something a variable can refer to. An object has a type and a value.
对象:
    变量可以指向的东西。一个对象有其数据类型和值。

equivalent:
    Having the same value.
相等:
    有相同的值。

identical:
    Being the same object (which implies equivalence).
相同:
    是同一个对象（隐含着相等）。

reference:
    The association between a variable and its value.
引用:
    一个变量和它的值之间的关联。

aliasing:
    A circumstance where two or more variables refer to the same object.
别名使用:
    一种两个或者两个以上变量指向同一个对象的情况。

delimiter:
    A character or string used to indicate where a string should be
    split.
分隔符:
    一个用于指示字符串分割位置的字符或者字符串。

Exercises
练习
---------

You can download solutions to these exercises from
http://thinkpython2.com/code/list_exercises.py.
你可以从http://thinkpython2.com/code/list_exercises.py下载这些联系的解答。

Write a function called ``nested_sum`` that takes a list of lists of
integers and adds up the elements from all of the nested lists. For
example:
写一个叫做``nested_sum``的函数，这个函数读取一个由一些整数列表构成的列表，并将所有的嵌套列表中的元素相加。例如：

::

    >>> t = [[1, 2], [3], [4, 5, 6]]
    >>> nested_sum(t)
    21

[cumulative]

Write a function called cumsum that takes a list of numbers and returns
the cumulative sum; that is, a new list where the :math:`i`\ th element
is the sum of the first :math:`i+1` elements from the original list. For
example:
写一个叫做cumsum的函数，读取一个数值列表并返回累加和，即一个新列表，其中第:math:`i`\个元素是元列表中前:math:`i+1`个元素的和。例如：

::

    >>> t = [1, 2, 3]
    >>> cumsum(t)
    [1, 3, 6]

Write a function called ``middle`` that takes a list and returns a new
list that contains all but the first and last elements. For example:
写一个叫做``middle``的函数，读取一个列表，并返回一个除了第一个和最后一个元素的列表。例如：

::

    >>> t = [1, 2, 3, 4]
    >>> middle(t)
    [2, 3]

Write a function called ``chop`` that takes a list, modifies it by
removing the first and last elements, and returns None. For example:
写一个叫做``chop``的函数，读取一个列表，移除第一个和最后一个列表，并返回None。例如：

::

    >>> t = [1, 2, 3, 4]
    >>> chop(t)
    >>> t
    [2, 3]

Write a function called ``is_sorted`` that takes a list as a parameter
and returns True if the list is sorted in ascending order and False
otherwise. For example:
写一个叫做``is_sorted``的函数，读取一个列表，如果列表是递增排列的则返回True，否则返回False。例如：

::

    >>> is_sorted([1, 2, 2])
    True
    >>> is_sorted(['b', 'a'])
    False

[anagram]

Two words are anagrams if you can rearrange the letters from one to
spell the other. Write a function called ``is_anagram`` that takes two
strings and returns True if they are anagrams.
如果可以通过重拍一个单词中字幕的顺序得到另外一个，那么称这两个单词是变位词。写一个叫做``is_anagram``的函数，读取两个字符串，如果它们是变位词则返回True。

[duplicate]

Write a function called ``has_duplicates`` that takes a list and returns
True if there is any element that appears more than once. It should not
modify the original list.
写一个叫做``has_duplicates``的函数，读取一个列表，如果一个元素在列表中出现了不止一次则返回True。这个函数不能改变原列表。

This exercise pertains to the so-called Birthday Paradox, which you can
read about at http://en.wikipedia.org/wiki/Birthday_paradox.
这个练习是关于一个叫做生日悖论的问题。你可以在http://en.wikipedia.org/wiki/Birthday_paradox中了解更多相关的内容。

If there are 23 students in your class, what are the chances that two of
you have the same birthday? You can estimate this probability by
generating random samples of 23 birthdays and checking for matches.
Hint: you can generate random birthdays with the randint function in the
random module.
如果你的班级上有 23 个学生， 2 个学生生日相同的概率是多少？你可以通过随即产生
23 个生日并检查匹配来估计概率。提示：你可以使用 random 模块中的 randint 函
数来生成随即生日。

You can download my solution from
http://thinkpython2.com/code/birthday.py.
你可以从http://thinkpython2.com/code/birthday.py.下载我的解答。

Write a function that reads the file words.txt and builds a list with
one element per word. Write two versions of this function, one using the
append method and the other using the idiom t = t + [x]. Which one takes
longer to run? Why?
编写函数，读取文件 words.txt，建立一个列表，每个单词为一个元素。编写两个版本函数，一个使用 append 方法，另一个使用 t = t + [x]。那个版本运行得慢？为什么？

Solution: http://thinkpython2.com/code/wordlist.py.
解答: http://thinkpython2.com/code/wordlist.py.

[wordlist1] [bisection]

To check whether a word is in the word list, you could use the in
operator, but it would be slow because it searches through the words in
order.
检查一个单词是否在单词表中，你可以使用 in 运算符，但这很慢，因为它按顺序查找单词。

Because the words are in alphabetical order, we can speed things up with
a bisection search (also known as binary search), which is similar to
what you do when you look a word up in the dictionary. You start in the
middle and check to see whether the word you are looking for comes
before the word in the middle of the list. If so, you search the first
half of the list the same way. Otherwise you search the second half.
由于单词是按照字母顺序排序的，我们可以使用两分法（也称二进制搜索）来加快速度，类似你在字典中查找单词的方法。你从中间开始，如果你要找的单词在中间的单词之前，你查找前半部分，否则你查找后半部分。

Either way, you cut the remaining search space in half. If the word list
has 113,809 words, it will take about 17 steps to find the word or
conclude that it’s not there.
每次查找，你将搜索范围减小一半。如果单词表有 113,809 个单词，你只需要 17步来找到这个单词，或着知道单词不存在。

Write a function called ``in_bisect`` that takes a sorted list and a
target value and returns the index of the value in the list if it’s
there, or None if it’s not.
写一个叫做``in_bisect``，参数为一个已排序的列表和一个目标值，返回该值在列表中的位置，如果不存在则返回 None。

Or you could read the documentation of the bisect module and use that!
或者你可以阅读bisect模块的文档并使用它！
Solution: http://thinkpython2.com/code/inlist.py.
解答: http://thinkpython2.com/code/inlist.py.

Two words are a “reverse pair” if each is the reverse of the other.
Write a program that finds all the reverse pairs in the word list.
两个单词被称为是“反转词对”，如果一个是另一个的反转。编写函数，找出单词表中所有的反转词对。
Solution: http://thinkpython2.com/code/reverse_pair.py.
解答: http://thinkpython2.com/code/reverse_pair.py.

Two words “interlock” if taking alternating letters from each forms a
new word. For example, “shoe” and “cold” interlock to form “schooled”.
两个单词被称为是“连锁词”，如果交替的从两个单词中取出字符将组成一个新的单词。例如，“ shoe”和“ cold”连锁后成为“ schooled”。
Solution: http://thinkpython2.com/code/interlock.py. Credit: This
exercise is inspired by an example at http://puzzlers.org.
解答: http://thinkpython2.com/code/interlock.py. 致谢: 这个练习的灵感由这个网站中的一个例子而来：http://puzzlers.org.

#. Write a program that finds all pairs of words that interlock. Hint:
   don’t enumerate all pairs!
#. 编写程序，找出所有的连锁词。提示：不要列举所有的单词对。

#. Can you find any words that are three-way interlocked; that is, every
   third letter forms a word, starting from the first, second or third?
#. 你能够找到三重连锁的单词吗？即每个字母依次从 3 个单词得到。