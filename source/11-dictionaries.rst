Dictionaries
============

字典
============

This chapter presents another built-in type called a dictionary.
Dictionaries are one of Python’s best features; they are the building
blocks of many efficient and elegant algorithms.

本章介绍另一个内建数据类型--字典(dictionary)。
字典是 Python 中最优秀的特性之一；它被运用于构建高效而优雅的算法。

A dictionary is a mapping
-------------------------

字典既映射（mapping)
--------------------

A **dictionary** is like a list, but more general. In a list, the
indices have to be integers; in a dictionary they can be (almost) any
type.

 **字典** 就是更加通用的列表。
在一般列表中，索引必须是整数；但在字典中它们可以是（几乎）任何类型。

A dictionary contains a collection of indices, which are called
**keys**, and a collection of values. Each key is associated with a
single value. The association of a key and a value is called a
**key-value pair** or sometimes an **item**.

一份字典包含了一个索引的集合，被称为 **键（key）** ，和一个值( value )的集合。
一个键对应一个值。
这种一一对应的关联被称为 **键值对（key-value pair)** 或者 **项（item）**。

In mathematical language, a dictionary represents a **mapping** from
keys to values, so you can also say that each key “maps to” a value. As
an example, we’ll build a dictionary that maps from English to Spanish
words, so the keys and the values are all strings.

在数学语言中，字典表示的是从键到值的 **映射**，所以你也可以说每一个键 “映射到” 一个值。

The function dict creates a new dictionary with no items. Because dict
is the name of a built-in function, you should avoid using it as a
variable name.

dict 函数生成了一个不含任何项的新字典。
由于 dict 是内建函数名，你应该避免使用它来命名。

::

    >>> eng2sp = dict()
    >>> eng2sp
    {}

The squiggly-brackets, ``{}``, represent an empty dictionary. To add
items to the dictionary, you can use square brackets:

花括号 ``{}`` 表示一个空字典。要向其中增加项，你可以使用方括号。

::

    >>> eng2sp['one'] = 'uno'

This line creates an item that maps from the key ``'one'`` to the value
``'uno'``. If we print the dictionary again, we see a key-value pair
with a colon between the key and value:

这行代码生成一个键为 ``'one'`` 值为 ``'uno'`` 的项。
如果我们将这个字典打印出来，会看到一个以冒号分隔的键值对。

::

    >>> eng2sp
    {'one': 'uno'}

This output format is also an input format. For example, you can create
a new dictionary with three items:

输出的格式同样也是输入的格式。
例如，你可以像这样创建一个包含三个项的字典。

::

    >>> eng2sp = {'one': 'uno', 'two': 'dos', 'three': 'tres'}

But if you print eng2sp, you might be surprised:

但是，如果你打印eng2sp，你可能很奇怪： 

::

    >>> eng2sp
    {'one': 'uno', 'three': 'tres', 'two': 'dos'}

The order of the key-value pairs might not be the same. If you type the
same example on your computer, you might get a different result. In
general, the order of items in a dictionary is unpredictable.

键-值对的顺序和原来不同。
同样的例子在你的电脑上可能有不同的结果，通常字典中项的顺序是不可预知的。

But that’s not a problem because the elements of a dictionary are never
indexed with integer indices. Instead, you use the keys to look up the
corresponding values:

但这没有关系，因为字典的元素从不会被用整数索引来索引，而是用键来查找对应的值。

::

    >>> eng2sp['two']
    'dos'

The key ``'two'`` always maps to the value ``'dos'`` so the order of the
items doesn’t matter.

键 ``'two'`` 总是映射到值 ``'dos'`` ，因此项的顺序没有关系

If the key isn’t in the dictionary, you get an exception:

如果键不存在字典中，会抛出一个异常。

::

    >>> eng2sp['four']
    KeyError: 'four'

The len function works on dictionaries; it returns the number of
key-value pairs:

len 函数用在字典上会返回键值对的个数。

::

    >>> len(eng2sp)
    3

The in operator works on dictionaries, too; it tells you whether
something appears as a *key* in the dictionary (appearing as a value is
not good enough).

in 用来检验字典中是否存在某个 *键* 。

::

    >>> 'one' in eng2sp
    True
    >>> 'uno' in eng2sp
    False

To see whether something appears as a value in a dictionary, you can use
the method values, which returns a collection of values, and then use
the in operator:

想要知道字典中是否存在某个值，你可以使用 values 方法，它返回值的集合，然后你可以使用 in 操作符来验证。

::

    >>> vals = eng2sp.values()
    >>> 'uno' in vals
    True

The in operator uses different algorithms for lists and dictionaries.
For lists, it searches the elements of the list in order, as in
Section [find]. As the list gets longer, the search time gets longer in
direct proportion.

in 操作符对列表和字典采用不同的算法。
对于列表，如 [find] 小结提到的，它按顺序依次查找目标。
随着列表的增长，搜索时间成正比增长。

For dictionaries, Python uses an algorithm called a **hashtable** that
has a remarkable property: the in operator takes about the same amount
of time no matter how many items are in the dictionary. I explain how
that’s possible in Section [hashtable], but the explanation might not
make sense until you’ve read a few more chapters.

对于字典，Python使用一种叫做 **哈希表（hashtable）** 的算法， 其具有非凡的性质：无论字典中有多少项，in运算符几乎花费相同的时间。

Dictionary as a collection of counters
--------------------------------------

字典作为计数器集合
-------------------

Suppose you are given a string and you want to count how many times each
letter appears. There are several ways you could do it:

假设给你一个字符串，你想计算每个字母出现的次数。
有多种方法可以使用：

#. You could create 26 variables, one for each letter of the alphabet.
   Then you could traverse the string and, for each character, increment
   the corresponding counter, probably using a chained conditional.

#. 你可以生成26个变量，每个对应一个字母表中的字母。然后你可以遍历字符串，对于 每个字符，递增相应的计数器，可能使用链式条件。


#. You could create a list with 26 elements. Then you could convert each
   character to a number (using the built-in function ord), use the
   number as an index into the list, and increment the appropriate
   counter.

#. 你可以生成具有26个元素的列表。然后你可以将每个字符传化为一个数字（使用内建函数ord），使用这些数字作为列表的索引，并递增适当的计数器。 

#. You could create a dictionary with characters as keys and counters as
   the corresponding values. The first time you see a character, you
   would add an item to the dictionary. After that you would increment
   the value of an existing item.

#. 你可以生成一个字典，将字符作为键，计数器作为相应的值。 第一次看到一个字母， 你应该向字典中增加一项。 这之后，你应该递增一个已有项的值。

Each of these options performs the same computation, but each of them
implements that computation in a different way.

每个方法都是为了做同一件事，但是各自的实现方法不同。

An **implementation** is a way of performing a computation; some
implementations are better than others. For example, an advantage of the
dictionary implementation is that we don’t have to know ahead of time
which letters appear in the string and we only have to make room for the
letters that do appear.

**实现** 是指执行某种计算的方法；诸多实现各有优劣。
例如，使用字典的实现其优势是我们不需要事先知道字符串中有几种字符，当出现时只要分配空间就好了。

Here is what the code might look like:

代码可能是这样：

::

    def histogram(s):
        d = dict()
        for c in s:
            if c not in d:
                d[c] = 1
            else:
                d[c] += 1
        return d

The name of the function is histogram, which is a statistical term for a
collection of counters (or frequencies).

函数名 histogram(直方图) 是一个统计术语，指计数器（或是频率）的集合。

The first line of the function creates an empty dictionary. The for loop
traverses the string. Each time through the loop, if the character c is
not in the dictionary, we create a new item with key c and the initial
value 1 (since we have seen this letter once). If c is already in the
dictionary we increment d[c].

函数的第一行生成一个字典。for循环遍历该字符串。 每次循环，如果字符c不在字典中， 我们用键c和初始值1生成一个新项 （由于我们见到了一次该字母）。 如果c已经在字 典中了，那么我们递增d[c]。 

Here’s how it works:

下面是运行结果：

::

    >>> h = histogram('brontosaurus')
    >>> h
    {'a': 1, 'b': 1, 'o': 2, 'n': 1, 's': 2, 'r': 2, 'u': 2, 't': 1}

The histogram indicates that the letters ``'a'`` and ``'b'`` appear
once; ``'o'`` appears twice, and so on.

histogram 直方图函数表明字母 ``'a'`` 和 ``'b'`` 出现了一次，  ``'o'`` 出现了两次，等等。

Dictionaries have a method called get that takes a key and a default
value. If the key appears in the dictionary, get returns the
corresponding value; otherwise it returns the default value. For
example:

字典类有一个 get 方法，接受一个键和一个默认值作为参数，如果字典中存在该键，则返回对应值，否则返回传入的默认值。

::

    >>> h = histogram('a')
    >>> h
    {'a': 1}
    >>> h.get('a', 0)
    1
    >>> h.get('b', 0)
    0

As an exercise, use get to write histogram more concisely. You should be
able to eliminate the if statement.

练习：试简化 histogram 函数，你应该考虑消除 if 语句。

Looping and dictionaries
------------------------

循环和字典
------------

If you use a dictionary in a for statement, it traverses the keys of the
dictionary. For example, ``print_hist`` prints each key and the
corresponding value:

在 for 循环中使用字典会遍历其所有的键。
下例 ``print_hist`` 会打印所有键与对应的值：

::

    def print_hist(h):
        for c in h:
            print(c, h[c])

Here’s what the output looks like:

输出类似：

::

    >>> h = histogram('parrot')
    >>> print_hist(h)
    a 1
    p 1
    r 2
    t 1
    o 1

Again, the keys are in no particular order. To traverse the keys in
sorted order, you can use the built-in function sorted:

再唠叨一下，字典中的键是无序的。
如果要以确定的顺序便利字典，你可以使用内建方法 sorted：

::

    >>> for key in sorted(h):
    ...     print(key, h[key])
    a 1
    o 1
    p 1
    r 2
    t 1

Reverse lookup
--------------

逆向查找
---------

Given a dictionary d and a key k, it is easy to find the corresponding
value v = d[k]. This operation is called a **lookup**.

给出一个字典d以及一个键t，很容易找到相应的值v = d[k]。
该运算被称作 **查找（lookup）** 。

But what if you have v and you want to find k? You have two problems:
first, there might be more than one key that maps to the value v.
Depending on the application, you might be able to pick one, or you
might have to make a list that contains all of them. Second, there is no
simple syntax to do a **reverse lookup**; you have to search.

但是如果你想通过 v 找到 k 呢？
有两个问题：
第一，可能有不止一个的键其映射到值v。
你可能可以找到唯一一个，不然就得用个 list 把多个键包起来。
第二，没有简单的语法可以完成 **逆向查找（reverse lookup）**；你必须搜索。

Here is a function that takes a value and returns the first key that
maps to that value:

下面这个函数接受一个值并返回映射到该值的第一个键：

::

    def reverse_lookup(d, v):
        for k in d:
            if d[k] == v:
                return k
        raise LookupError()

This function is yet another example of the search pattern, but it uses
a feature we haven’t seen before, raise. The **raise statement** causes
an exception; in this case it causes a LookupError, which is a built-in
exception used to indicate that a lookup operation failed.

该函数是搜索模式的另一个例子，但是它使用了一个我们之前没有见过的特性，raise。 
**raise 语句** 能触发异常，这里它触发了 ValueError，这是一个内建异常用以表示查找操作失败。

If we get to the end of the loop, that means v doesn’t appear in the
dictionary as a value, so we raise an exception.

如果我们到达循环结尾，这意味着 v在字典中不作为值存在， 所以我们触发一个异常。 

Here is an example of a successful reverse lookup:

这有一个成功逆向查找的例子：

::

    >>> h = histogram('parrot')
    >>> key = reverse_lookup(h, 2)
    >>> key
    'r'

And an unsuccessful one:

和一个失败的：

::

    >>> key = reverse_lookup(h, 3)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
      File "<stdin>", line 5, in reverse_lookup
    LookupError

The effect when you raise an exception is the same as when Python raises
one: it prints a traceback and an error message.

你触发的异常和 Python 触发的产生效果一样，都打印一条回溯和错误信息。

The raise statement can take a detailed error message as an optional
argument. For example:

raise 语句接受一个详细的错误信息作为可选的实参。 例如：

::

    >>> raise LookupError('value does not appear in the dictionary')
    Traceback (most recent call last):
      File "<stdin>", line 1, in ?
    LookupError: value does not appear in the dictionary

A reverse lookup is much slower than a forward lookup; if you have to do
it often, or if the dictionary gets big, the performance of your program
will suffer.

逆向查找比正向查找慢得多；
如果你频繁执行这个操作或是字典很大，程序性能会变得很差。

Dictionaries and lists
----------------------

字典和列表
----------

Lists can appear as values in a dictionary. For example, if you are
given a dictionary that maps from letters to frequencies, you might want
to invert it; that is, create a dictionary that maps from frequencies to
letters. Since there might be several letters with the same frequency,
each value in the inverted dictionary should be a list of letters.

在字典中，列表可以作为值出现。
例如，如果你有一个从字母映射到频率的字典， 而你想倒转它；也就是生成一个从频率映射到字母的字典。
应为可能有些字母具有相同的频率，所以在倒转字典中的每个值应该是一个字母组成的列表。

Here is a function that inverts a dictionary:

下面是一个倒转字典的函数：

::

    def invert_dict(d):
        inverse = dict()
        for key in d:
            val = d[key]
            if val not in inverse:
                inverse[val] = [key]
            else:
                inverse[val].append(key)
        return inverse

Each time through the loop, key gets a key from d and val gets the
corresponding value. If val is not in inverse, that means we haven’t
seen it before, so we create a new item and initialize it with a
**singleton** (a list that contains a single element). Otherwise we have
seen this value before, so we append the corresponding key to the list.

每次循环，key从 d 获得一个键和相应的值 val 。
如果 val 不在 inverse 中，意味着我们之前没有见过它， 因此我们生成一个新项并用一个 **单元素集合（singleton）** （包括唯一元素 的列表） 初始化它。


Here is an example:

下面是一个例子：

::

    >>> hist = histogram('parrot')
    >>> hist
    {'a': 1, 'p': 1, 'r': 2, 't': 1, 'o': 1}
    >>> inverse = invert_dict(hist)
    >>> inverse
    {1: ['a', 'p', 't', 'o'], 2: ['r']}

.. figure:: figs/dict1.pdf
   :alt: State diagram.

   State diagram.

Figure [fig.dict1] is a state diagram showing hist and inverse. A
dictionary is represented as a box with the type dict above it and the
key-value pairs inside. If the values are integers, floats or strings, I
draw them inside the box, but I usually draw lists outside the box, just
to keep the diagram simple.

状态图 [fig.dict1] 显示了 hist 和 inverse。
用上标 dict 类型的盒子表示一个字典，其中是键值对。
如果值是整数，浮点数或是字符串我就画在里面，为了简洁通常将列表画在盒子外。

Lists can be values in a dictionary, as this example shows, but they
cannot be keys. Here’s what happens if you try:

如本例所示，列表可以作为字典中的值，但是不能是键。
下面演示了这样做的结果：

::

    >>> t = [1, 2, 3]
    >>> d = dict()
    >>> d[t] = 'oops'
    Traceback (most recent call last):
      File "<stdin>", line 1, in ?
    TypeError: list objects are unhashable

I mentioned earlier that a dictionary is implemented using a hashtable
and that means that the keys have to be **hashable**.

我之前提过，字典使用哈希表实现，这意味着键必须是 **可哈希的（hashable）** 。

A **hash** is a function that takes a value (of any kind) and returns an
integer. Dictionaries use these integers, called hash values, to store
and look up key-value pairs.

**哈希（hash）** 函数接受一个值（任何类型）并返回一个整数。
字典使用这些整数，被称作哈希值，来存储和查找键-值对。 

This system works fine if the keys are immutable. But if the keys are
mutable, like lists, bad things happen. For example, when you create a
key-value pair, Python hashes the key and stores it in the corresponding
location. If you modify the key and then hash it again, it would go to a
different location. In that case you might have two entries for the same
key, or you might not be able to find a key. Either way, the dictionary
wouldn’t work correctly.

如果键是不可变的，那么此系统可以很好地工作。
但是如果键是可变的，如列表，那么糟糕事就发生了。
例如，当你生成一个键-值对的时候，Python哈希键并将其存储在相应的位置。
如果你改变键然后再次哈希它，它将到另一个位置。
在那种情况下，对于相同的键，你可能有两个入口， 或者你可能无法找到一个键。
无论如何，字典都不会正确的工作。

That’s why keys have to be hashable, and why mutable types like lists
aren’t. The simplest way to get around this limitation is to use tuples,
which we will see in the next chapter.

这就是为什么键必须是可哈希的，以及为什么如列表这种可变类型不能作为键。
绕过这种限制最简单的方法是使用元组， 我们将在下一章中介绍。


Since dictionaries are mutable, they can’t be used as keys, but they
*can* be used as values.

因为字典是可变的，因此它们不能作为键，但是可以用作值。

Memos
-----

备忘录
------

If you played with the fibonacci function from
Section [one.more.example], you might have noticed that the bigger the
argument you provide, the longer the function takes to run. Furthermore,
the run time increases quickly.

如果你在 [one.more.example] 小节中接触过 fibonacci 函数了，你可能注意到输入的参数越大，函数运行就需要越多时间。
而且运行时间增长得非常快。

To understand why, consider Figure [fig.fibonacci], which shows the
**call graph** for fibonacci with n=4:

要理解其原因，思考图 [fig.fibonacci] ，其展示了当 n=4 时 fibonacci 的 **调用图（call graph）** 。

.. figure:: figs/fibonacci.pdf
   :alt: Call graph.

   Call graph.

A call graph shows a set of function frames, with lines connecting each
frame to the frames of the functions it calls. At the top of the graph,
fibonacci with n=4 calls fibonacci with n=3 and n=2. In turn, fibonacci
with n=3 calls fibonacci with n=2 and n=1. And so on.

调用图展示了函数框的集合，每个框到其调用函数的框用线相连。
在图的顶端，n=4的fibonacci调用n=3和n=2的fibonacci。
接着，n=3的fibonacci调用n=2和n=1的fibonacci，等等。 

Count how many times fibonacci(0) and fibonacci(1) are called. This is
an inefficient solution to the problem, and it gets worse as the
argument gets bigger.

数数 fibonacci(0) 和 fibonacci(1) 总共被调用了几次。
对该问题，这不是一个高效的解，并且随着实参的变大会变得更糟。

One solution is to keep track of values that have already been computed
by storing them in a dictionary. A previously computed value that is
stored for later use is called a **memo**. Here is a “memoized” version
of fibonacci:

一个解决办法是保存已经计算过的值，将它们存在一个字典中。
存储之前计算过的值以便今后使用，它被称作 **备忘录（memo）** 。
这是使用备忘录的fibonacci的实现： 

::

    known = {0:0, 1:1}

    def fibonacci(n):
        if n in known:
            return known[n]

        res = fibonacci(n-1) + fibonacci(n-2)
        known[n] = res
        return res

known is a dictionary that keeps track of the Fibonacci numbers we
already know. It starts with two items: 0 maps to 0 and 1 maps to 1.

known是一个字典，其记录我们已经计算过的 fibonacci 数。
它从两项开始：0映射到0，1映射到1。

Whenever fibonacci is called, it checks known. If the result is already
there, it can return immediately. Otherwise it has to compute the new
value, add it to the dictionary, and return it.

当 fibonacci 被调用时，它先检查known。 如果结果存在，则立即返回。 否则，它必须计算新的值，将其加入字典，并返回它。

If you run this version of fibonacci and compare it with the original,
you will find that it is much faster.

将两个版本的 fibonacci 函数比比看，你就知道它有多快了。

Global variables
----------------

全局变量
---------

In the previous example, known is created outside the function, so it
belongs to the special frame called ``__main__``. Variables in
``__main__`` are sometimes called **global** because they can be
accessed from any function. Unlike local variables, which disappear when
their function ends, global variables persist from one function call to
the next.

在前面的例子中，known 在函数的外面被生成， 因此它属于被称作 ``__main__`` 的特殊的域。 
因为 ``__main__`` 中的变量可以被任何函数访问它们也被称作 **全局变量（global）** 。
和函数结束时它们就会消失的局部变量不同， 全局变量从一个函数调用到另一个调用一直都存在。

It is common to use global variables for **flags**; that is, boolean
variables that indicate (“flag”) whether a condition is true. For
example, some programs use a flag named verbose to control the level of
detail in the output:

全局变量普遍用作 **标记（flag）**； 也就是指示（标记）一个条件是否为真的布尔变量。
例如，一些程序使用一个被称作verbose的标记来控制输出的信息等级：

::

    verbose = True

    def example1():
        if verbose:
            print('Running example1')

If you try to reassign a global variable, you might be surprised. The
following example is supposed to keep track of whether the function has
been called:

如果你试图对一个全局变量重新赋值，结果可能出乎意料。
下面的例子本应该能够记录是否该函数已经被调用过了： 

::

    been_called = False

    def example2():
        been_called = True         # WRONG

But if you run it you will see that the value of ``been_called`` doesn’t
change. The problem is that example2 creates a new local variable named
``been_called``. The local variable goes away when the function ends,
and has no effect on the global variable.

但是如果你运行它你会发现 ``been_called`` 的值并未发生改变。
问题在于 example2 生成一个新的被称作 ``been_called`` 的局部变量。
当函数结束的时候，该局部变量也消失了，并且对全局变量没有影响。


To reassign a global variable inside a function you have to **declare**
the global variable before you use it:

要在函数内对全局变量重新赋值，你必须在使用之前 **声明(declare)** 该全局变量。

::

    been_called = False

    def example2():
        global been_called 
        been_called = True

The **global statement** tells the interpreter something like, “In this
function, when I say ``been_called``, I mean the global variable; don’t
create a local one.”

**global 语句** 告诉编译器，“在这个函数里当我说 ``been_called`` 时我指的是那个全局变量，别生成局部变量”。

Here’s an example that tries to update a global variable:

这是一个试图更新全局变量的例子： 

::

    count = 0

    def example3():
        count = count + 1          # WRONG

If you run it you get:

一旦运行你会发现：

::

    UnboundLocalError: local variable 'count' referenced before assignment

Python assumes that count is local, and under that assumption you are
reading it before writing it. The solution, again, is to declare count
global.

Python假设count是局部的，在这个假设下你是在未写入任何东西前就试图读取。
解决方法还是声明 count 是全局的。

::

    def example3():
        global count
        count += 1

If a global variable refers to a mutable value, you can modify the value
without declaring the variable:

如果全局变量是可变的，你可以不加声明地修改它：

::

    known = {0:0, 1:1}

    def example4():
        known[2] = 1

So you can add, remove and replace elements of a global list or
dictionary, but if you want to reassign the variable, you have to
declare it:

因此你可以增加、删除和替代全局列表或者字典的元素，但是如果你想对变量重新赋值，你必须声明它： 

::

    def example5():
        global known
        known = dict()

Global variables can be useful, but if you have a lot of them, and you
modify them frequently, they can make programs hard to debug.

全局变量有时是很有用的，但如果你的程序中有很多全局变量，而且修改频繁，这样的程序在调试时会很麻烦。

Debugging
---------

调试
------

As you work with bigger datasets it can become unwieldy to debug by
printing and checking the output by hand. Here are some suggestions for
debugging large datasets:

当你操作较大的数据集时，通过打印并手工检查数据来调试很不方便。 
下面是对于调试大数据集合的一些建议：

Scale down the input:
    If possible, reduce the size of the dataset. For example if the
    program reads a text file, start with just the first 10 lines, or
    with the smallest example you can find. You can either edit the
    files themselves, or (better) modify the program so it reads only
    the first n lines.

    If there is an error, you can reduce n to the smallest value that
    manifests the error, and then increase it gradually as you find and
    correct errors.

缩小输入：
	如果可能，减小数据集合的大小。
	例如如果程序读入一个文本文件，从前10行开始或是你找到的更小的样例。
	你可以选择编辑读入的文件或是（最好）修改程序使它只读入开始的 n 行。

Check summaries and types:
    Instead of printing and checking the entire dataset, consider
    printing summaries of the data: for example, the number of items in
    a dictionary or the total of a list of numbers.

    A common cause of runtime errors is a value that is not the right
    type. For debugging this kind of error, it is often enough to print
    the type of a value.

检查摘要和类型：
	不用打印并检查全部数据集合，而是考虑打印数据的摘要： 例如 字典中项的数目或者数字列表的总和。 

	通常的运行时错误原因是一个值的类型不正确。 为了调试此类错误，打印值的类型通 常就足够了。

Write self-checks:
    Sometimes you can write code to check for errors automatically. For
    example, if you are computing the average of a list of numbers, you
    could check that the result is not greater than the largest element
    in the list or less than the smallest. This is called a “sanity
    check” because it detects results that are “insane”.

    Another kind of check compares the results of two different
    computations to see if they are consistent. This is called a
    “consistency check”.

编写自检代码：
	有时你可以写代码来自动检查错误。 例如，如果你正在计算数字列表的 平均数， 你可以检查其结果不用大于列表中最大的元素或者不小于最小的。 这被称 作“合理性检查”，因为它探测出“不合理的”结果。
	
	另一类检查比较两个不同计算的结果来看一下它们是否一致。这被称作“一致性检查”。 

Format the output:
    Formatting debugging output can make it easier to spot an error. We
    saw an example in Section [factdebug]. The pprint module provides a
    pprint function that displays built-in types in a more
    human-readable format (pprint stands for “pretty print”).

格式化输出：
	格式化调试输出能够更容易定位一个错误。 [factdebug] 节中我们看到一个例子。pprint模块提供了一个pprint函数，其以更可读的格式显示内建类型（pprint 代表 “pretty print”）。

Again, time you spend building scaffolding can reduce the time you spend
debugging.

在唠叨一次，你花在建立脚手架上的时间能减少你花在调试上的时间。

Glossary
--------

术语表
-------

mapping（映射）:
    A relationship in which each element of one set corresponds to an
    element of another set.

dictionary（字典）:
    A mapping from keys to their corresponding values.

key-value pair（键值对）:
    The representation of the mapping from a key to a value.

item（项）:
    In a dictionary, another name for a key-value pair.

key（键）:
    An object that appears in a dictionary as the first part of a
    key-value pair.

value（值）:
    An object that appears in a dictionary as the second part of a
    key-value pair. This is more specific than our previous use of the
    word “value”.

implementation（实现）:
    A way of performing a computation.

hashtable（哈希表）:
    The algorithm used to implement Python dictionaries.

hash function（哈希函数）:
    A function used by a hashtable to compute the location for a key.

hashable（可哈希的）:
    A type that has a hash function. Immutable types like integers,
    floats and strings are hashable; mutable types like lists and
    dictionaries are not.

lookup（查找）:
    A dictionary operation that takes a key and finds the corresponding
    value.

reverse lookup（逆向查找）:
    A dictionary operation that takes a value and finds one or more keys
    that map to it.

raise statement（raise 语句）:
    A statement that (deliberately) raises an exception.

singleton（单元素集合）:
    A list (or other sequence) with a single element.

call graph（调用图）:
    A diagram that shows every frame created during the execution of a
    program, with an arrow from each caller to each callee.

memo（备忘录）:
    A computed value stored to avoid unnecessary future computation.

global variable（全局变量）:
    A variable defined outside a function. Global variables can be
    accessed from any function.

global statement（global 语句）:
    A statement that declares a variable name global.

flag（标记）:
    A boolean variable used to indicate whether a condition is true.

declaration（声明）:
    A statement like global that tells the interpreter something about a
    variable.

Exercises
---------

练习
------

[wordlist2]

单词表2

Write a function that reads the words in words.txt and stores them as
keys in a dictionary. It doesn’t matter what the values are. Then you
can use the in operator as a fast way to check whether a string is in
the dictionary.

试写一函数读入words.txt中的单词并存储为字典中的键。值无所谓。之后你可以使用 in 操作符检查一个字符串是否在字典中。

If you did Exercise [wordlist1], you can compare the speed of this
implementation with the list in operator and the bisection search.

如果你完成过 单词表1，你可以比较一下 in 操作符和bisection search的速度。

[setdefault]

Read the documentation of the dictionary method setdefault and use it to
write a more concise version of ``invert_dict``. Solution:
http://thinkpython2.com/code/invert_dict.py.

阅读字典方法 setdefault 的文档并写一个更简洁的 ``invert_dict`` 。
解：http://thinkpython2.com/code/invert_dict.py.

Memoize the Ackermann function from Exercise [ackermann] and see if
memoization makes it possible to evaluate the function with bigger
arguments. Hint: no. Solution:
http://thinkpython2.com/code/ackermann_memo.py.

回忆练习 [ackermann] 中的Ackermann函数尝试使用备忘录让它可以解决更大的参数。没有提示！
解：http://thinkpython2.com/code/ackermann_memo.py.

If you did Exercise [duplicate], you already have a function named
``has_duplicates`` that takes a list as a parameter and returns True if
there is any object that appears more than once in the list.

如果你做了练习 [duplicate]，你已经有个函数叫 ``has_duplicates`` ，其接受一个列表作为参数，如果其中有某个对象在列表中出现不止一次就返回True。

Use a dictionary to write a faster, simpler version of
``has_duplicates``. Solution:
http://thinkpython2.com/code/has_duplicates.py.

用字典写个更快更简单的版本。
解：http://thinkpython2.com/code/has_duplicates.py.

[exrotatepairs]

Two words are “rotate pairs” if you can rotate one of them and get the
other (see ``rotate_word`` in Exercise [exrotate]).

两个单词如果反转其中一个就会得到另一个被称作“反转对”。（看练习 [exrotate] 中的反转词）

Write a program that reads a wordlist and finds all the rotate pairs.
Solution: http://thinkpython2.com/code/rotate_pairs.py.

试写一程序读入单词表并找到所有反转对。
解：http://thinkpython2.com/code/rotate_pairs.py.

Here’s another Puzzler from *Car Talk*

这里是取自 *Car Talk* 的另一个题。

(http://www.cartalk.com/content/puzzlers):

    This was sent in by a fellow named Dan O’Leary. He came upon a
    common one-syllable, five-letter word recently that has the
    following unique property. When you remove the first letter, the
    remaining letters form a homophone of the original word, that is a
    word that sounds exactly the same. Replace the first letter, that
    is, put it back and remove the second letter and the result is yet
    another homophone of the original word. And the question is, what’s
    the word?

    Now I’m going to give you an example that doesn’t work. Let’s look
    at the five-letter word, ‘wrack.’ W-R-A-C-K, you know like to ‘wrack
    with pain.’ If I remove the first letter, I am left with a
    four-letter word, ’R-A-C-K.’ As in, ‘Holy cow, did you see the rack
    on that buck! It must have been a nine-pointer!’ It’s a perfect
    homophone. If you put the ‘w’ back, and remove the ‘r,’ instead,
    you’re left with the word, ‘wack,’ which is a real word, it’s just
    not a homophone of the other two words.

    But there is, however, at least one word that Dan and we know of,
    which will yield two homophones if you remove either of the first
    two letters to make two, new four-letter words. The question is,
    what’s the word?

You can use the dictionary from Exercise [wordlist2] to check whether a
string is in the word list.

你可以使用练习 [wordlist2] 中的字典检查某字符串是否出现在单词表中。

To check whether two words are homophones, you can use the CMU
Pronouncing Dictionary. You can download it from
http://www.speech.cs.cmu.edu/cgi-bin/cmudict or from
http://thinkpython2.com/code/c06d and you can also download
http://thinkpython2.com/code/pronounce.py, which provides a function
named ``read_dictionary`` that reads the pronouncing dictionary and
returns a Python dictionary that maps from each word to a string that
describes its primary pronunciation.

Write a program that lists all the words that solve the Puzzler.
Solution: http://thinkpython2.com/code/homophone.py.