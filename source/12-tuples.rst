Tuples \| 元组
==============

This chapter presents one more built-in type, the tuple, and then shows
how lists, dictionaries, and tuples work together. I also present a
useful feature for variable-length argument lists, the gather and
scatter operators.

One note: there is no consensus on how to pronounce “tuple”. Some people
say “tuh-ple”, which rhymes with “supple”. But in the context of
programming, most people say “too-ple”, which rhymes with “quadruple”.

本章介绍另一个内建的类型 —
元组 [1]_，同时向您展示列表、字典和元组如何结合使用。后面的章节也会展示关于可变长度参数列表的有用功能，以及\ *汇集*\ 和\ *离散*\ 操作。

Tuples are immutable \| 元组的不可变性
--------------------------------------

A tuple is a sequence of values. The values can be any type, and they
are indexed by integers, so in that respect tuples are a lot like lists.
The important difference is that tuples are immutable.

元组是一组\ *值*\ 的序列。 其中的值可以是任意类型， 使用整数索引其位置，
因此元组与列表非常相似。 而重要的不同之处在于元组的不可变性。

Syntactically, a tuple is a comma-separated list of values:

语法上,元组是用逗号隔开的值的列表：

::

    >>> t = 'a', 'b', 'c', 'd', 'e'

Although it is not necessary, it is common to enclose tuples in
parentheses:

尽管不是必须，通常我们在给元组赋值时会用括号把元素封装起来：

::

    >>> t = ('a', 'b', 'c', 'd', 'e')

To create a tuple with a single element, you have to include a final
comma:

使用单一元素建立元组时，需要在结尾使用一个逗号：

::

    >>> t1 = 'a',
    >>> type(t1)
    <class 'tuple'>

A value in parentheses is not a tuple:

括号中仅包含元素（而没有使用逗号结尾）时被赋值的对象不是元组：

::

    >>> t2 = ('a')
    >>> type(t2)
    <class 'str'>

Another way to create a tuple is the built-in function tuple. With no
argument, it creates an empty tuple:

另一个建立元组的方法是使用内建函数tuple。
在没有参数传递时它会产生一个空元组。

::

    >>> t = tuple()
    >>> t
    ()

If the argument is a sequence (string, list or tuple), the result is a
tuple with the elements of the sequence:

如果实参是一个序列（字符串、列表或者元组），结果将是包含序列内元素的一个元组。

::

    >>> t = tuple('lupins')
    >>> t
    ('l', 'u', 'p', 'i', 'n', 's')

Because tuple is the name of a built-in function, you should avoid using
it as a variable name.

因为是内建函数名，所以应该避免将它用于变量名。

Most list operators also work on tuples. The bracket operator indexes an
element:

列表的大多数操作同样也适用于元组。 例如使用方括号索引一个元素：

::

    >>> t = ('a', 'b', 'c', 'd', 'e')
    >>> t[0]
    'a'

And the slice operator selects a range of elements.

切片操作可以选取一个范围内的元素:

::

    >>> t[1:3]
    ('b', 'c')

But if you try to modify one of the elements of the tuple, you get an
error:

但是，如果你试图元组中的一个元素，会得到错误信息：

::

    >>> t[0] = 'A'
    TypeError: object doesn't support item assignment

Because tuples are immutable, you can’t modify the elements. But you can
replace one tuple with another:

因为元组是不可变的，您无法改变其中的元素。
但是您可以使用其他元组替换现有元组：

::

    >>> t = ('A',) + t[1:]
    >>> t
    ('A', 'b', 'c', 'd', 'e')

This statement makes a new tuple and then makes t refer to it.

这个语句产生了一个新元组，并且将它赋给了原先的元组。

The relational operators work with tuples and other sequences; Python
starts by comparing the first element from each sequence. If they are
equal, it goes on to the next elements, and so on, until it finds
elements that differ. Subsequent elements are not considered (even if
they are really big).

关系型操作也适用于元组和其他序列；Python
会首先比较序列中的第一个元素，如果它们相同就会去比较下一组元素，以此往复，直至比值不同。
其后的元素（即便是差异很大）也不会再参与比较。

::

    >>> (0, 1, 2) < (0, 3, 4)
    True
    >>> (0, 1, 2000000) < (0, 3, 4)
    True

Tuple assignment \| 元组赋值
----------------------------

It is often useful to swap the values of two variables. With
conventional assignments, you have to use a temporary variable. For
example, to swap a and b:

两个变量互换值的操作通常很有用。 传统的，你需要使用一个临时变量。
例如为了交换和：

::

    >>> temp = a
    >>> a = b
    >>> b = temp

This solution is cumbersome; **tuple assignment** is more elegant:

这个方法很繁琐；通过\ **元组赋值**\ 的来实现更为优雅:

::

    >>> a, b = b, a

The left side is a tuple of variables; the right side is a tuple of
expressions. Each value is assigned to its respective variable. All the
expressions on the right side are evaluated before any of the
assignments.

等号左侧是变量构成的元组；右侧是元组赋值的表达式。
每个值都被赋给了对应的要互换的变量。
变量被重新赋值前，右侧的表达式会被优先运行。

The number of variables on the left and the number of values on the
right have to be the same:

使用元组赋值，左右的变量数必须相同：

::

    >>> a, b = 1, 2, 3
    ValueError: too many values to unpack

More generally, the right side can be any kind of sequence (string, list
or tuple). For example, to split an email address into a user name and a
domain, you could write:

一般说来，元组赋值的右侧表达式可以是任意类型（字符串、列表或者元组）的序列。
例如， 将一个电子邮箱地址分成用户名和域名， 你可以：

::

    >>> addr = 'monty@python.org'
    >>> uname, domain = addr.split('@')

The return value from split is a list with two elements; the first
element is assigned to uname, the second to domain.

函数返回的对象是一个包含两个元素的列表；第一个元素被赋给了的变量，第二个被赋给了。

::

    >>> uname
    'monty'
    >>> domain
    'python.org'

Tuples as return values \| 元组作为返回值
-----------------------------------------

Strictly speaking, a function can only return one value, but if the
value is a tuple, the effect is the same as returning multiple values.
For example, if you want to divide two integers and compute the quotient
and remainder, it is inefficient to compute x/y and then x%y. It is
better to compute them both at the same time.

严格地说，一个函数只能返回一个值，但是如果以元组作为这个返回值，其效果等同于返回多个值。
例如，你想对两个整数做除法，计算出商和余数，依次计算出\ ``x/y}和\lstinline``\ x

The built-in function divmod takes two arguments and returns a tuple of
two values, the quotient and remainder. You can store the result as a
tuple:

内建函数\ ` <https://docs.python.org/3/library/functions.html#divmod>`__\ 接受两个参数，返回包含两个值的元组
— 输入参数做除法的商和余数。 您可以使用元组来存储返回值:

::

    >>> t = divmod(7, 3)
    >>> t
    (2, 1)

Or use tuple assignment to store the elements separately:

或者使用元组赋值分别存储它们：

::

    >>> quot, rem = divmod(7, 3)
    >>> quot
    2
    >>> rem
    1

Here is an example of a function that returns a tuple:

下面是另一个返回元组作为结果的函数例子：

::

    def min_max(t):
        return min(t), max(t)

max and min are built-in functions that find the largest and smallest
elements of a sequence. ``min_max`` computes both and returns a tuple of
two values.

和
是用于找出一组元素序列中最大值和最小值的内建函数，函数同时计算出它们并组装成元组返回结果。

Variable-length argument tuples \| 可变长度参数元组
---------------------------------------------------

Functions can take a variable number of arguments. A parameter name that
begins with **gathers** arguments into a tuple. For example, printall
takes any number of arguments and prints them:

函数可以同时接受多个参数。 以 **** 开头的定义参数可以将输入的参数
*汇集*\ 到一个元组中。 例如 可以接受任意数量的参数，并且打印出来:

::

    def printall(*args):
        print(args)

The gather parameter can have any name you like, but args is
conventional. Here’s how the function works:

汇集的形参可以使用任意名字， 传统上使用. 以下显示了这个函数的调用效果：

::

    >>> printall(1, 2.0, '3')
    (1, 2.0, '3')

The complement of gather is **scatter**. If you have a sequence of
values and you want to pass it to a function as multiple arguments, you
can use the operator. For example, divmod takes exactly two arguments;
it doesn’t work with a tuple:

*离散*\ **scatter**\ 是汇集的补充。 如果你有一个值的序列，并且希望
将其作为多个参数传递给一个函数，你可以使用运算符\*。 例如，
需要接受两个实参；一个元组则无法作为参数传递进去：

::

    >>> t = (7, 3)
    >>> divmod(t)
    TypeError: divmod expected 2 arguments, got 1

But if you scatter the tuple, it works:

但是如果您将这个元组打散，它就可以被传递进函数：

::

    >>> divmod(*t)
    (2, 1)

Many of the built-in functions use variable-length argument tuples. For
example, max and min can take any number of arguments:

多数内建函数使用可变长度参数元组。 例如， 和 可以取任意数量的参数。

::

    >>> max(1, 2, 3)
    3

But sum does not.

但是求和操作并不如此：

::

    >>> sum(1, 2, 3)
    TypeError: sum expected at most 2 arguments, got 3

As an exercise, write a function called sumall that takes any number of
arguments and returns their sum.

您可以尝试写一个叫做
的函数作为练习，使它能够接受任何数量的传参并返回它们的和。

Lists and tuples \| 列表和元组
------------------------------

zip is a built-in function that takes two or more sequences and returns
a list of tuples where each tuple contains one element from each
sequence. The name of the function refers to a zipper, which joins and
interleaves two rows of teeth.

是一个内建函数，用于将两个或多个序列组装成包含元组的列表返回出来，每个元组包含了各个序列中相对位置的一个元素。这个函数的起名来源于名词拉链(zipper),形象的显示年对应两列对应位置的牙齿组合起来。

This example zips a string and a list:

下面例子显示了组合字符串和列表操作：

::

    >>> s = 'abc'
    >>> t = [0, 1, 2]
    >>> zip(s, t)
    <zip object at 0x7f7d0a9e7c48>

The result is a **zip object** that knows how to iterate through the
pairs. The most common use of zip is in a for loop:

输出的结果是一个可以通过每个内在的元组对进行迭代的 对象。
函数最常见用法就是基于循环的迭代遍历:

::

    >>> for pair in zip(s, t):
    ...     print(pair)
    ...
    ('a', 0)
    ('b', 1)
    ('c', 2)

A zip object is a kind of **iterator**, which is any object that
iterates through a sequence. Iterators are similar to lists in some
ways, but unlike lists, you can’t use an index to select an element from
an iterator.

` <https://docs.python.org/3/library/functions.html#zip>`__\ 对象是一个友善的\ **迭代器**\ ，后者是指任何一种能够按照某个序列迭代的对象。
迭代器在某些方面与列表非常相似，
不同之处在于你无法通过索引来选择迭代器中的某个元素。

If you want to use list operators and methods, you can use a zip object
to make a list:

如果你想对zip对象使用列表的操作和方法，你可以通过zip对象创造一个列表：

::

    >>> list(zip(s, t))
    [('a', 0), ('b', 1), ('c', 2)]

The result is a list of tuples; in this example, each tuple contains a
character from the string and the corresponding element from the list.

结果就是产生了一个包含若干元组的列表；在这个例子中，每个元组又包含了字符串中的一个字符和列表
中对应的一个元素。

If the sequences are not the same length, the result has the length of
the shorter one.

如果用于创建的序列长度不一，返回的对象的长度以最短序列的长度为准。

::

    >>> list(zip('Anne', 'Elk'))
    [('A', 'E'), ('n', 'l'), ('n', 'k')]

You can use tuple assignment in a for loop to traverse a list of tuples:

您可以通过元组赋值在循环中遍历包含元组的列表：

::

    t = [('a', 0), ('b', 1), ('c', 2)]
    for letter, number in t:
        print(number, letter)

Each time through the loop, Python selects the next tuple in the list
and assigns the elements to letter and number. The output of this loop
is:

循环中的每次执行， Python 会选择列表中的下一个元组，并将其内容赋给 和
。因此循环打印的输出会是这样：

::

    0 a
    1 b
    2 c

If you combine zip, for and tuple assignment, you get a useful idiom for
traversing two (or more) sequences at the same time. For example,
``has_match`` takes two sequences, t1 and t2, and returns True if there
is an index i such that t1[i] == t2[i]:

如果将、和元组赋值结合起来使用，您会得出一个有用的惯用方法用于
同时遍历两个（甚至多个）序列。 如下例，
接受两个序列，和，并返回一个真值如果存在满足判别式的索引：

::

    def has_match(t1, t2):
        for x, y in zip(t1, t2):
            if x == y:
                return True
        return False

If you need to traverse the elements of a sequence and their indices,
you can use the built-in function enumerate:

如果需要遍历一个序列的元素以及它们的索引号，您可以使用内建函数：

::

    for index, element in enumerate('abc'):
        print(index, element)

The result from enumerate is an enumerate object, which iterates a
sequence of pairs; each pair contains an index (starting from 0) and an
element from the given sequence. In this example, the output is

的返回结果是一个枚举对象(enumerate
object)，它可基于一个包含若干个\ *对*\ 的序列进行迭代，每个对包含了（从0开始计数）的索引号和对应的元素。在刚才的例子中，对应的输出结果会和上次一样：

::

    0 a
    1 b
    2 c

Again.

Dictionaries and tuples \| 字典和元组
-------------------------------------

Dictionaries have a method called items that returns a sequence of
tuples, where each tuple is a key-value pair.

字典对象有一个内建方法叫做\ ` <https://docs.python.org/3/library/stdtypes.html?highlight=items#dict.items>`__\ ，
它返回一个以元组形式存放的键-值对的序列。

::

    >>> d = {'a':0, 'b':1, 'c':2}
    >>> t = d.items()
    >>> t
    dict_items([('c', 2), ('a', 0), ('b', 1)])

The result is a ``dict_items`` object, which is an iterator that
iterates the key-value pairs. You can use it in a for loop like this:

其结果是一个对象，其实质是一个可以通过键-值对迭代的迭代器。
您可以在循环中像这样使用它:

::

    >>> for key, value in d.items():
    ...     print(key, value)
    ...
    c 2
    a 0
    b 1

As you should expect from a dictionary, the items are in no particular
order.

和字典对象相似，内部的项是无序存放的。

Going in the other direction, you can use a list of tuples to initialize
a new dictionary:

另一方面，您可以使用元组的列表初始化一个新的字典：

::

    >>> t = [('a', 0), ('c', 2), ('b', 1)]
    >>> d = dict(t)
    >>> d
    {'a': 0, 'c': 2, 'b': 1}

Combining dict with zip yields a concise way to create a dictionary:

和的结合使用产生了一个简洁的字典生成法:

::

    >>> d = dict(zip('abc', range(3)))
    >>> d
    {'a': 0, 'c': 2, 'b': 1}

The dictionary method update also takes a list of tuples and adds them,
as key-value pairs, to an existing dictionary.

字典的方法也接受元组的列表，并作为键-值对把它们加入到该字典中去。

It is common to use tuples as keys in dictionaries (primarily because
you can’t use lists). For example, a telephone directory might map from
last-name, first-name pairs to telephone numbers. Assuming that we have
defined last, first and number, we could write:

更加常用的方法是在字典中使用元组作为键（因为列表做不了键）。例如，一个电话簿希望基于用户的姓（）、名（）对来映射号码（），假设我们已经定义了
, 和 三个变量，我们可以这样实现映射：

::

    directory[last, first] = number

The expression in brackets is a tuple. We could use tuple assignment to
traverse this dictionary.

方括号中的表达式是一个元组。 为我们可以通过元组赋值来遍历这个字典：

::

    for last, first in directory:
        print(first, last, directory[last,first])

This loop traverses the keys in directory, which are tuples. It assigns
the elements of each tuple to last and first, then prints the name and
corresponding telephone number.

该循环遍历中的键，它们其实是元组。 它将元组的元素赋给和，
然后打印出姓名和对应的电话号码。

There are two ways to represent tuples in a state diagram. The more
detailed version shows the indices and elements just as they appear in a
list. For example, the tuple ``('Cleese', 'John')`` would appear as in
Figure [fig.tuple1].

用两个状态图来表述这些元组。细致的说，索引号和对应元素就像列表一样存放在元组中。例如，元组可像图 [fig.tuple1]一样存放。

.. figure:: ../source/figs/tuple1.pdf
   :alt: State diagram.

   State diagram.

But in a larger diagram you might want to leave out the details. For
example, a diagram of the telephone directory might appear as in
Figure [fig.dict2].

在大图中，我们忽略这些细节。 该电话簿的结构图可能像图 [fig.dict2]一样。

.. figure:: ../source/figs/dict2.pdf
   :alt: State diagram.

   State diagram.

Here the tuples are shown using Python syntax as a graphical shorthand.
The telephone number in the diagram is the complaints line for the BBC,
so please don’t call it.

因此，Python风格的元组用法可用这两幅图来描述。
此图中的电话号码是BBC的投诉热线，请不要拨打它。

Sequences of sequences \| 序列嵌套
----------------------------------

I have focused on lists of tuples, but almost all of the examples in
this chapter also work with lists of lists, tuples of tuples, and tuples
of lists. To avoid enumerating the possible combinations, it is
sometimes easier to talk about sequences of sequences.

我们已经谈过了包含元组的列表，事实上，本章大多数例子也适用于列表嵌套列表、元组嵌套元组，以及元组嵌套列表。
为了避免一一穷举这类可能的嵌套组合，我们简称为序列嵌套。

In many contexts, the different kinds of sequences (strings, lists and
tuples) can be used interchangeably. So how should you choose one over
the others?

在很多情况下，不同类型的序列（字符串、列表、元组）可以互换使用。
因此，我们如何选用合适的嵌套对象呢？

To start with the obvious, strings are more limited than other sequences
because the elements have to be characters. They are also immutable. If
you need the ability to change the characters in a string (as opposed to
creating a new string), you might want to use a list of characters
instead.

首先，显而易见的是字符串的使用范围比其他序列更为有限，因为它的所有元素都是字符，且字符串不可变。如果你希望能够改变字符在字符串中的位置，使用列表嵌套字符比较合适。

Lists are more common than tuples, mostly because they are mutable. But
there are a few cases where you might prefer tuples:

列表比元组更常见，这源于它们可变性的易用。
但是有些情况下我们不得不更青睐元组：

#. In some contexts, like a return statement, it is syntactically
   simpler to create a tuple than a list.

#. If you want to use a sequence as a dictionary key, you have to use an
   immutable type like a tuple or string.

#. If you are passing a sequence as an argument to a function, using
   tuples reduces the potential for unexpected behavior due to aliasing.

#. 在一些情况下（例如语句），从句式上生成一个元组比列表要简单。

#. 如果你想使用一个序列作为字典的键，那么你必须使用元组或字符串这样的不可变类型。

#. 如果你向函数传入一个序列作为参数，那么使用元组以降低由于别名而产生的意外行为的可能性。

Because tuples are immutable, they don’t provide methods like sort and
reverse, which modify existing lists. But Python provides the built-in
function sorted, which takes any sequence and returns a new list with
the same elements in sorted order, and reversed, which takes a sequence
and returns an iterator that traverses the list in reverse order.

正由于元组的不可变性，元组没有类似于列表中的 （\ *排序*\ ） 和
（\ *逆序*\ ）这样的方法。 然而 Python 提供了内建函数
，用于对任意序列排序并输出相同元素的列表，以及
，用于对序列逆向排序并生成一个可以遍历的迭代器。

Debugging \| 调试
-----------------

Lists, dictionaries and tuples are examples of **data structures**; in
this chapter we are starting to see compound data structures, like lists
of tuples, or dictionaries that contain tuples as keys and lists as
values. Compound data structures are useful, but they are prone to what
I call **shape errors**; that is, errors caused when a data structure
has the wrong type, size, or structure. For example, if you are
expecting a list with one integer and I give you a plain old integer
(not in a list), it won’t work.

列表、字典和元组都是\ *数据结构* （\ **data
structures**\ ）的实例；本章中我们开始接触到复合数据结构（\ **compound
data
structures**\ ），如：列表嵌套元组，又如使用元组作为键而列表作为值的字典。复合数据结构非常实用，然而使用时容易出现所谓的\ *形状错误*\ （\ **shape
errors**\ ），也就是说由于数据结构的类型、大小或结构问题而引发的错误。例如，当你希望使用封装整数的列表时却用成了没被列表包含的一串整数。

To help debug these kinds of errors, I have written a module called
structshape that provides a function, also called structshape, that
takes any kind of data structure as an argument and returns a string
that summarizes its shape. You can download it from
http://thinkpython2.com/code/structshape.py

为了方面调试这类错误，笔者编写了一个叫做 的模块， 它提供了一个名为
的函数，用于接受并分析数据结构对象作，并返回描述它形状的文字信息。你可以在\ `此处 <http://thinkpython2.com/code/structshape.py>`__\ 下载到它(\ http://thinkpython2.com/code/structshape.py)。

Here’s the result for a simple list:

这里是它分析简单列表的结果展示：

::

    >>> from structshape import structshape
    >>> t = [1, 2, 3]
    >>> structshape(t)
    'list of 3 int'

A fancier program might write “list of 3 int\ *s*”, but it was easier
not to deal with plurals. Here’s a list of lists:

更完美的程序应该显示 “list of 3
int\ *s*”，但是忽略英文复数使程序简单的多。我们再看一个列表嵌套的例子：

::

    >>> t2 = [[1,2], [3,4], [5,6]]
    >>> structshape(t2)
    'list of 3 list of 2 int'

If the elements of the list are not the same type, structshape groups
them, in order, by type:

如果列表内嵌套的元素不是相同类型， 会按类型的组将它们归并:

::

    >>> t3 = [1, 2, 3, 4.0, '5', '6', [7], [8], 9]
    >>> structshape(t3)
    'list of (3 int, float, 2 str, 2 list of int, int)'

Here’s a list of tuples:

以下是一个元组的例子：

::

    >>> s = 'abc'
    >>> lt = list(zip(t, s))
    >>> structshape(lt)
    'list of 3 tuple of (int, str)'

And here’s a dictionary with 3 items that map integers to strings.

下面，一个包含3个映射整数到字符串的键值对的字典被分析：

::

    >>> d = dict(lt)
    >>> structshape(d)
    'dict of 3 int->str'

If you are having trouble keeping track of your data structures,
structshape can help.

因此如果你对使用的数据结构有疑惑，可以使用来帮助解析。

Glossary \| 术语表
------------------

tuple:
    An immutable sequence of elements.

元组：
    一组不可变的元素的序列。

tuple assignment:
    An assignment with a sequence on the right side and a tuple of
    variables on the left. The right side is evaluated and then its
    elements are assigned to the variables on the left.

元组赋值：
    一种通过赋值方式，通过等号右侧的序列向等号左侧的一组变量的元组进行赋值。右侧许两种的每个元素会被计算，然后赋给左侧元组中对应的变量。

gather:
    The operation of assembling a variable-length argument tuple.

汇集：
    组装可变长度变量元组的一种操作。

scatter:
    The operation of treating a sequence as a list of arguments.

分散：
    将一个序列变换成一个参数列表的操作。

zip object:
    The result of calling a built-in function zip; an object that
    iterates through a sequence of tuples.

zip 对象：
    使用内建函数所返回的结果， 它是一个可通过元组序列逐个迭代的对象。

iterator:
    An object that can iterate through a sequence, but which does not
    provide list operators and methods.

迭代器：
    :
    一种可以通过一个序列逐个迭代的对象，但是它并不提供列表的某些操作和方法。

data structure:
    A collection of related values, often organized in lists,
    dictionaries, tuples, etc.

数据结构：
    一个有相关关联的数据的集合，通常使用列表、字典和元组等综合构成。

shape error:
    An error caused because a value has the wrong shape; that is, the
    wrong type or size.

形状错误：
    由于数据结构的类型、大小或结构问题而引发的错误。

Exercises \| 练习
-----------------

Write a function called ``most_frequent`` that takes a string and prints
the letters in decreasing order of frequency. Find text samples from
several different languages and see how letter frequency varies between
languages. Compare your results with the tables at
http://en.wikipedia.org/wiki/Letter_frequencies. Solution:
http://thinkpython2.com/code/most_frequent.py.

写一个名为\ **\ 的函数，它接受字符串并按字母降序打印出字符出现频率。
找一些不同语言的文本样本来试试看不同语言文本间区别。
将你的结果和维基百科上\ `字母频率 <http://en.wikipedia.org/wiki/Letter_frequencies>`__\ 表相比较。

`参考答案 <http://thinkpython2.com/code/most_frequent.py>`__

[anagrams]

More anagrams!

#. Write a program that reads a word list from a file (see
   Section [wordlist]) and prints all the sets of words that are
   anagrams.

   Here is an example of what the output might look like:

   ::

       ['deltas', 'desalt', 'lasted', 'salted', 'slated', 'staled']
       ['retainers', 'ternaries']
       ['generating', 'greatening']
       ['resmelts', 'smelters', 'termless']

   Hint: you might want to build a dictionary that maps from a
   collection of letters to a list of words that can be spelled with
   those letters. The question is, how can you represent the collection
   of letters in a way that can be used as a key?

#. Modify the previous program so that it prints the longest list of
   anagrams first, followed by the second longest, and so on.

#. In Scrabble a “bingo” is when you play all seven tiles in your rack,
   along with a letter on the board, to form an eight-letter word. What
   collection of 8 letters forms the most possible bingos? Hint: there
   are seven.

   Solution: http://thinkpython2.com/code/anagram_sets.py.

   易位构词游戏
   (`anagrams <https://zh.wikipedia.org/wiki/%E6%98%93%E4%BD%8D%E6%9E%84%E8%AF%8D%E6%B8%B8%E6%88%8F>`__)！

#. 编写一个程序使之能从文件以列表形式读入单词 （参考章节 [wordlist]）
   并且打印出所有符合异位构词的组合。

   下面是一个输出异位构词的样例：

   ::

       ['deltas', 'desalt', 'lasted', 'salted', 'slated', 'staled']
       ['retainers', 'ternaries']
       ['generating', 'greatening']
       ['resmelts', 'smelters', 'termless']

   提示：也许你可以建立一个字典用于映射一个字符集合到一个该集合可异位构词的词汇集合。

#. 改写前面的程序，使之首先打印包含异位构词数量最多的词汇列表，第二多次之，依次按异位构词数量排列。

#. `Scrabble <https://en.wikipedia.org/wiki/Scrabble>`__
   `游戏 <https://zh.wikipedia.org/wiki/Scrabble>`__ 中， “bingo” ...

   `参考答案 <http://thinkpython2.com/code/anagram_sets.py>`__

Two words form a “metathesis pair” if you can transform one into the
other by swapping two letters; for example, “converse” and “conserve”.
Write a program that finds all of the metathesis pairs in the
dictionary. Hint: don’t test all pairs of words, and don’t test all
possible swaps. Solution: http://thinkpython2.com/code/metathesis.py.
Credit: This exercise is inspired by an example at http://puzzlers.org.

如果两个单词中的某一单词可以通过调换两个字母变为另一个，这两个单词就构成了“metatheisi
pair”；比如“converse”和“conserve”。
写一个程序来找出给定字典里所有的“metatheisi
pair”。提示：不用测试所有的单词组合，也不用测试所有的字母调换组合。

`参考答案 <http://thinkpython2.com/code/metathesis.py>`__

这个练习受\ http://puzzlers.org\ 的案例启发而成。

Here’s another Car Talk Puzzler
(http://www.cartalk.com/content/puzzlers):

    What is the longest English word, that remains a valid English word,
    as you remove its letters one at a time?

    Now, letters can be removed from either end, or the middle, but you
    can’t rearrange any of the letters. Every time you drop a letter,
    you wind up with another English word. If you do that, you’re
    eventually going to wind up with one letter and that too is going to
    be an English word—one that’s found in the dictionary. I want to
    know what’s the longest word and how many letters does it have?

    I’m going to give you a little modest example: Sprite. Ok? You start
    off with sprite, you take a letter off, one from the interior of the
    word, take the r away, and we’re left with the word spite, then we
    take the e off the end, we’re left with spit, we take the s off,
    we’re left with pit, it, and I.

另一个猜谜题 `car talk
puzzler <http://www.cartalk.com/content/puzzlers>`__ ：

    世界上哪个最长的英文单词，当你每一次从中删掉一个字母以后，剩下的字符仍然能构成一个单词？

    被删掉的字母可以位于首尾或是中间，但不允许重新去排列剩下的字母，这样你得到一个新单词。这样一直下去最终你只剩一个字母，并且它也是一个单词
    —
    一个你可以在字典里查到的单词。我们想找到最初的这个单词可以最长可以多长，有多少个字母构成？

    我先给出一个短小的例子：“Sprite”，从 sprite 起，我们可以拿掉中间的
    ‘r’ 从而获得单词 spite，拿去字母 ‘e’ 得到 spit，再去掉 ‘s’ 剩下
    pit， it，最后 I。

Write a program to find all words that can be reduced in this way, and
then find the longest one.

This exercise is a little more challenging than most, so here are some
suggestions:

#. You might want to write a function that takes a word and computes a
   list of all the words that can be formed by removing one letter.
   These are the “children” of the word.

#. Recursively, a word is reducible if any of its children are
   reducible. As a base case, you can consider the empty string
   reducible.

#. The wordlist I provided, words.txt, doesn’t contain single letter
   words. So you might want to add “I”, “a”, and the empty string.

#. To improve the performance of your program, you might want to memoize
   the words that are known to be reducible.

Solution: http://thinkpython2.com/code/reducible.py.

写一个程序按照这种规则找到所有可以缩词的单词，然后看看其中哪个词最长。

以下是对这个稍具挑战的练习的一些建议：

#. 可能你需要写一个函数将输入单词的所有“子词”（即拿掉一个字母后所有可能的新词）以列表形式输出。

#. 递归的看，如果一个可被缩词的单词是另一个单词的子词，那另一个单词也可被缩。
   我们可从空字符串开始考虑。

#. 我们提供的词汇表并未包含诸如 ‘I’、 ‘a’
   这样的单个字母词汇，因此你可能需要加上它们。

#. 为了提高你程序的性能， 你可能需要暂存好已被发现的可被缩词的词汇。

`参考答案 <http://thinkpython2.com/code/reducible.py>`__

.. [1]
   值得注意的是，“tuple”并没有统一的发音，有些人读“tuh-ple”，音律类似于“supple”；而有人读“too-ple”音律类似于“quadruple”。
