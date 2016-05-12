第十七章：类和方法
===================

虽然我们已经在使用部分 Python 面向对象的特性，前两个章节中的程序并不是真正面向对象的，
因为它们没有呈现出程序员自定义类型与对其进行操作的函数（functions）之间的关系。
下一步，我们将会把这些函数转换成明显突出这一关系的方法（methods）。

本章代码可以从\ http://thinkpython2.com/code/Time2.py \ 获取，
练习题的答案位于\ http://thinkpython2.com/code/Point2_soln.py \ 。


面向对象的特性
------------------------

Python 是一门**面向对象的编程语言**，这意味它提供了能够支持面向对象编程的特性。
面向对象编程具有以下特征：

- 程序包含类和方法定义。

- 大部分计算以对象上的操作表示。

- 对象通常代表现实世界的物体，方法对应现实世界中物体交互的方式。

例如，第16章中定义的 ``Time`` 类对应人们用来记录一天中的时间，其中定义的各种函数对应人们使用时间的方式。类似的，第15章中的 ``Point`` 类和 ``Rectangle`` 类对应数学中点和矩形的概念。

到目前为止，我们还没有利用Python提供的支持面向对象编程的特性。这些特性严格来说并不是必须的；大部分提供的是我们已经实现的功能的替代语法。但在很多情况下，这些替代语法更加简洁，更准确地表达了程序的结构。

例如，在 ``Time1.py`` 中，类定义与之后的函数定义之间没有明显的联系。仔细检查之后，才会发现每个函数都至少接受一个 ``Time`` 对象作为参数。

从这个观察中我们发现了\ **方法**\ ；方法是一个与特定的类相关联的函数。我们已经接触了字符串、列表、字典和元组的方法。在这章中，我们将会定义程序员自定义类型的方法。

方法和函数的语义相同，但是有两处句法的不同：

-  方法在一个类定义内部声明，为的是显示地与类进行关联。

-  调用方法的语法和调用函数的语法不同。


In the next few sections, we will take the functions from the previous
two chapters and transform them into methods. This transformation is
purely mechanical; you can do it by following a sequence of steps. If
you are comfortable converting from one form to another, you will be
able to choose the best form for whatever you are doing.


在接下来的几节中，我们会把前面两章中的函数转化为方法。这个转化是纯机械式的；你可以通
过一系列步骤完成。如果你能够轻松地将一种形式转换成另一种形式，就可以选择最适合目前需求的形式。

打印对象
----------------

在第16章中，我们定义了一个名叫 ``Time`` 的类，在\ :ref:`isafter`\ 一节中，你编写了一个叫做 ``print_time`` 的函数：

::

    class Time:
        """Represents the time of day."""

    def print_time(time):
        print('%.2d:%.2d:%.2d' % (time.hour, time.minute, time.second))

想要调用这个函数，你必须把一个 ``Time`` 对象作为一个参数传递给函数。

::

    >>> start = Time()
    >>> start.hour = 9
    >>> start.minute = 45
    >>> start.second = 00
    >>> print_time(start)
    09:45:00

将 ``print_time``` 变成一个方法，我们只需要将函数定义移到类定义里面即可。注意缩进
的变化。

::

    class Time:
        def print_time(time):
            print('%.2d:%.2d:%.2d' % (time.hour, time.minute, time.second))

Now there are two ways to call ``print_time``. The first (and less
common) way is to use function syntax:

现在有两种方法可以调用\ ``print_time``\ 。第一种（也是不常用的）是使用函数的语法：

::

    >>> Time.print_time(start)
    09:45:00

In this use of dot notation, Time is the name of the class, and
``print_time`` is the name of the method. start is passed as a
parameter.

在这个点标记法的用法中，``Time`` 是类的名字，\ ``print_time``\ 是方法的名字。``start`` 是传递的参数。

第二种语法（也更简洁）是使用方法语法：

::

    >>> start.print_time()
    09:45:00

在这个点标记法的用法中，\ ``print_time``\ 是方法的名称，然后 ``start`` 是调用方法的对象
，被称为主语（\ **subject**\ ）。就像一个句子的主语是句子的核心，方法的主语也是方
法作用的主要对象。

在方法中，主语被赋值为第一个参数，所以在这里 ``start`` 被赋值给 ``time`` 上了。

根据约定，方法的第一个参数写作 ``self`` ，所以\ ``print_time``\ 写成这样更常见：

::

    class Time:
        def print_time(self):
            print('%.2d:%.2d:%.2d' % (self.hour, self.minute, self.second))

使用该约定原因在于一种暗喻：

-  在函数调用的语法中，\ ``print_time(start)``\ 表示函数是一个活跃的代理。就像是在
   说“Hi, ``print_time``! 这有一个对象需要你打印”。

-  在面向对象编程中，对象是活跃的代理。一个类似\ ``start.print_time()``\ 的方法
   调用，就像是在说“Hi start! 请打印你自己”。

视角的转换似乎语气更文雅些了，但很难看出其好处。在前面的例子中，的确如此。
但是将职责从函数上面转移到对象上，可以更加容易地写出多样化的函数（或方法），并且代码将更加容易维护和复用。

我们做个练习，将 ``time_to_int`` （见 \ :ref:`prototype`\ ）重写为方法。你或许也想将 ``int_to_time`` 改写为方法，但是那样做并没有什么意义，因为没有调用它的对象。

再举一例
---------------

下面是 ``increment`` （见 \ :ref:`increment`\ ）改写为方法后的代码版本：

::

    # inside class Time:

        def increment(self, seconds):
            seconds += self.time_to_int()
            return int_to_time(seconds)

这个版本假设\ ``time_to_int``\ 已经改成了方法。另外，注意这是一个纯函数，不是修改器。

下面是调用 ``increment`` 的方法：

::

    >>> start.print_time()
    09:45:00
    >>> end = start.increment(1337)
    >>> end.print_time()
    10:07:17

The subject, start, gets assigned to the first parameter, self. The
argument, 1337, gets assigned to the second parameter, seconds.

This mechanism can be confusing, especially if you make an error. For
example, if you invoke increment with two arguments, you get:

::

    >>> end = start.increment(1337, 460)
    TypeError: increment() takes 2 positional arguments but 3 were given

The error message is initially confusing, because there are only two
arguments in parentheses. But the subject is also considered an
argument, so all together that’s three.

By the way, a **positional argument** is an argument that doesn’t have a
parameter name; that is, it is not a keyword argument. In this function
call:

::

    sketch(parrot, cage, dead=True)

parrot and cage are positional, and dead is a keyword argument.

A more complicated example
--------------------------

Rewriting ``is_after`` (from Section [isafter]) is slightly more
complicated because it takes two Time objects as parameters. In this
case it is conventional to name the first parameter self and the second
parameter other:

::

    # inside class Time:

        def is_after(self, other):
            return self.time_to_int() > other.time_to_int()

To use this method, you have to invoke it on one object and pass the
other as an argument:

::

    >>> end.is_after(start)
    True

One nice thing about this syntax is that it almost reads like English:
“end is after start?”

The init method
---------------

The init method (short for “initialization”) is a special method that
gets invoked when an object is instantiated. Its full name is
``__init__`` (two underscore characters, followed by init, and then two
more underscores). An init method for the Time class might look like
this:

::

    # inside class Time:

        def __init__(self, hour=0, minute=0, second=0):
            self.hour = hour
            self.minute = minute
            self.second = second

It is common for the parameters of ``__init__`` to have the same names
as the attributes. The statement

::

            self.hour = hour

stores the value of the parameter hour as an attribute of self.

The parameters are optional, so if you call Time with no arguments, you
get the default values.

::

    >>> time = Time()
    >>> time.print_time()
    00:00:00

If you provide one argument, it overrides hour:

::

    >>> time = Time (9)
    >>> time.print_time()
    09:00:00

If you provide two arguments, they override hour and minute.

::

    >>> time = Time(9, 45)
    >>> time.print_time()
    09:45:00

And if you provide three arguments, they override all three default
values.

As an exercise, write an init method for the Point class that takes x
and y as optional parameters and assigns them to the corresponding
attributes.

The \_\_str\_\_ method
----------------------

``__str__`` is a special method, like ``__init__``, that is supposed to
return a string representation of an object.

For example, here is a str method for Time objects:

::

    # inside class Time:

        def __str__(self):
            return '%.2d:%.2d:%.2d' % (self.hour, self.minute, self.second)

When you print an object, Python invokes the str method:

::

    >>> time = Time(9, 45)
    >>> print(time)
    09:45:00

When I write a new class, I almost always start by writing ``__init__``,
which makes it easier to instantiate objects, and ``__str__``, which is
useful for debugging.

As an exercise, write a str method for the Point class. Create a Point
object and print it.

Operator overloading
--------------------

By defining other special methods, you can specify the behavior of
operators on programmer-defined types. For example, if you define a
method named ``__add__`` for the Time class, you can use the + operator
on Time objects.

Here is what the definition might look like:

::

    # inside class Time:

        def __add__(self, other):
            seconds = self.time_to_int() + other.time_to_int()
            return int_to_time(seconds)

And here is how you could use it:

::

    >>> start = Time(9, 45)
    >>> duration = Time(1, 35)
    >>> print(start + duration)
    11:20:00

When you apply the + operator to Time objects, Python invokes
``__add__``. When you print the result, Python invokes ``__str__``. So
there is a lot happening behind the scenes!

Changing the behavior of an operator so that it works with
programmer-defined types is called **operator overloading**. For every
operator in Python there is a corresponding special method, like
``__add__``. For more details, see
http://docs.python.org/3/reference/datamodel.html#specialnames.

As an exercise, write an add method for the Point class.

Type-based dispatch
-------------------

In the previous section we added two Time objects, but you also might
want to add an integer to a Time object. The following is a version of
``__add__`` that checks the type of other and invokes either
``add_time`` or increment:

::

    # inside class Time:

        def __add__(self, other):
            if isinstance(other, Time):
                return self.add_time(other)
            else:
                return self.increment(other)

        def add_time(self, other):
            seconds = self.time_to_int() + other.time_to_int()
            return int_to_time(seconds)

        def increment(self, seconds):
            seconds += self.time_to_int()
            return int_to_time(seconds)

The built-in function isinstance takes a value and a class object, and
returns True if the value is an instance of the class.

If other is a Time object, ``__add__`` invokes ``add_time``. Otherwise
it assumes that the parameter is a number and invokes increment. This
operation is called a **type-based dispatch** because it dispatches the
computation to different methods based on the type of the arguments.

Here are examples that use the + operator with different types:

::

    >>> start = Time(9, 45)
    >>> duration = Time(1, 35)
    >>> print(start + duration)
    11:20:00
    >>> print(start + 1337)
    10:07:17

Unfortunately, this implementation of addition is not commutative. If
the integer is the first operand, you get

::

    >>> print(1337 + start)
    TypeError: unsupported operand type(s) for +: 'int' and 'instance'

The problem is, instead of asking the Time object to add an integer,
Python is asking an integer to add a Time object, and it doesn’t know
how. But there is a clever solution for this problem: the special method
``__radd__``, which stands for “right-side add”. This method is invoked
when a Time object appears on the right side of the + operator. Here’s
the definition:

::

    # inside class Time:

        def __radd__(self, other):
            return self.__add__(other)

And here’s how it’s used:

::

    >>> print(1337 + start)
    10:07:17

As an exercise, write an add method for Points that works with either a
Point object or a tuple:

-  If the second operand is a Point, the method should return a new
   Point whose :math:`x` coordinate is the sum of the :math:`x`
   coordinates of the operands, and likewise for the :math:`y`
   coordinates.

-  If the second operand is a tuple, the method should add the first
   element of the tuple to the :math:`x` coordinate and the second
   element to the :math:`y` coordinate, and return a new Point with the
   result.

Polymorphism
------------

Type-based dispatch is useful when it is necessary, but (fortunately) it
is not always necessary. Often you can avoid it by writing functions
that work correctly for arguments with different types.

Many of the functions we wrote for strings also work for other sequence
types. For example, in Section [histogram] we used histogram to count
the number of times each letter appears in a word.

::

    def histogram(s):
        d = dict()
        for c in s:
            if c not in d:
                d[c] = 1
            else:
                d[c] = d[c]+1
        return d

This function also works for lists, tuples, and even dictionaries, as
long as the elements of s are hashable, so they can be used as keys in
d.

::

    >>> t = ['spam', 'egg', 'spam', 'spam', 'bacon', 'spam']
    >>> histogram(t)
    {'bacon': 1, 'egg': 1, 'spam': 4}

Functions that work with several types are called **polymorphic**.
Polymorphism can facilitate code reuse. For example, the built-in
function sum, which adds the elements of a sequence, works as long as
the elements of the sequence support addition.

Since Time objects provide an add method, they work with sum:

::

    >>> t1 = Time(7, 43)
    >>> t2 = Time(7, 41)
    >>> t3 = Time(7, 37)
    >>> total = sum([t1, t2, t3])
    >>> print(total)
    23:01:00

In general, if all of the operations inside a function work with a given
type, the function works with that type.

The best kind of polymorphism is the unintentional kind, where you
discover that a function you already wrote can be applied to a type you
never planned for.

Debugging
---------

It is legal to add attributes to objects at any point in the execution
of a program, but if you have objects with the same type that don’t have
the same attributes, it is easy to make mistakes. It is considered a
good idea to initialize all of an object’s attributes in the init
method.

If you are not sure whether an object has a particular attribute, you
can use the built-in function hasattr (see Section [hasattr]).

Another way to access attributes is the built-in function vars, which
takes an object and returns a dictionary that maps from attribute names
(as strings) to their values:

::

    >>> p = Point(3, 4)
    >>> vars(p)
    {'y': 4, 'x': 3}

For purposes of debugging, you might find it useful to keep this
function handy:

::

    def print_attributes(obj):
        for attr in vars(obj):
            print(attr, getattr(obj, attr))

``print_attributes`` traverses the dictionary and prints each attribute
name and its corresponding value.

The built-in function getattr takes an object and an attribute name (as
a string) and returns the attribute’s value.

Interface and implementation
----------------------------

One of the goals of object-oriented design is to make software more
maintainable, which means that you can keep the program working when
other parts of the system change, and modify the program to meet new
requirements.

A design principle that helps achieve that goal is to keep interfaces
separate from implementations. For objects, that means that the methods
a class provides should not depend on how the attributes are
represented.

For example, in this chapter we developed a class that represents a time
of day. Methods provided by this class include ``time_to_int``,
``is_after``, and ``add_time``.

We could implement those methods in several ways. The details of the
implementation depend on how we represent time. In this chapter, the
attributes of a Time object are hour, minute, and second.

As an alternative, we could replace these attributes with a single
integer representing the number of seconds since midnight. This
implementation would make some methods, like ``is_after``, easier to
write, but it makes other methods harder.

After you deploy a new class, you might discover a better
implementation. If other parts of the program are using your class, it
might be time-consuming and error-prone to change the interface.

But if you designed the interface carefully, you can change the
implementation without changing the interface, which means that other
parts of the program don’t have to change.

Glossary
--------

object-oriented language:
    A language that provides features, such as programmer-defined types
    and methods, that facilitate object-oriented programming.

object-oriented programming:
    A style of programming in which data and the operations that
    manipulate it are organized into classes and methods.

method:
    A function that is defined inside a class definition and is invoked
    on instances of that class.

subject:
    The object a method is invoked on.

positional argument:
    An argument that does not include a parameter name, so it is not a
    keyword argument.

operator overloading:
    Changing the behavior of an operator like + so it works with a
    programmer-defined type.

type-based dispatch:
    A programming pattern that checks the type of an operand and invokes
    different functions for different types.

polymorphic:
    Pertaining to a function that can work with more than one type.

information hiding:
    The principle that the interface provided by an object should not
    depend on its implementation, in particular the representation of
    its attributes.

Exercises
---------

Download the code from this chapter from
http://thinkpython2.com/code/Time2.py. Change the attributes of Time to
be a single integer representing seconds since midnight. Then modify the
methods (and the function ``int_to_time``) to work with the new
implementation. You should not have to modify the test code in main.
When you are done, the output should be the same as before. Solution:
http://thinkpython2.com/code/Time2_soln.py.

[kangaroo]

This exercise is a cautionary tale about one of the most common, and
difficult to find, errors in Python. Write a definition for a class
named Kangaroo with the following methods:

#. An ``__init__`` method that initializes an attribute named
   ``pouch_contents`` to an empty list.

#. A method named ``put_in_pouch`` that takes an object of any type and
   adds it to ``pouch_contents``.

#. A ``__str__`` method that returns a string representation of the
   Kangaroo object and the contents of the pouch.

Test your code by creating two Kangaroo objects, assigning them to
variables named kanga and roo, and then adding roo to the contents of
kanga’s pouch.

Download http://thinkpython2.com/code/BadKangaroo.py. It contains a
solution to the previous problem with one big, nasty bug. Find and fix
the bug.

If you get stuck, you can download
http://thinkpython2.com/code/GoodKangaroo.py, which explains the problem
and demonstrates a solution.