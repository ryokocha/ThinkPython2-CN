第六章：有返回值的函数
=========================

许多我们前面使用过的 Python 函数都会产生返回值， 如数学函数。
但目前我们所写的函数都是空函数（void）: 它们产生某种效果，像打印一个值或是移动乌龟，但是并没有返回值。
在本章中，你将学习到如何写一个有返回值的函数。

返回值
-------

调用一个有返回值的函数会生成一个返回值， 我们通常将其赋值给某个变量或是作为表达式的一部分。

::

    e = math.exp(1.0)
    height = radius * math.sin(radians)

目前我们所写的函数都是空函数。泛泛地来看，它们没有返回值；更准确地说，它们的返回值是 None 。

本章中， 我们（终于）要开始写有返回值的函数了。
第一个例子是 ``area`` ， 返回给定半径的圆的面积。

::

    def area(radius):
        a = math.pi * radius**2
        return a

之前我们已经见过 ``return`` 语句了，但是在一个有返回值的函数中， ``return`` 语句包含一个表达式。 这条语句的意思是：“马上从该函数返回，并使用接下来的表达式作为返回值”。 此表达式可以是任意复杂的，因此我们可以将该函数写得更简洁些：

::

    def area(radius):
        return math.pi * radius**2

另一方面， 像 a 这样的 **临时变量（temporary
variables）** 能使调试变得更简单。

有时，在条件语句的每一个分支内各有一个返回语句会很有用，。 

::

    def absolute_value(x):
        if x < 0:
            return -x
        else:
            return x

因为这些 ``return`` 语句在不同的条件内，最后只有一个会被执行。

一旦一条返回语句执行，函数则终止，不再执行后续的语句。出现在某条return语句之后的代码，或者在执行流程永远不会到达之处的
代码，被称为\ **死代码（dead code）**\ 。

在一个有返回值的函数中， 最好保证程序执行的每一个流程最终都会碰到一个 ``return`` 语句。例如：

::

    def absolute_value(x):
        if x < 0:
            return -x
        if x > 0:
            return x

这个函数是有问题的。 原因是如果 ``x`` 恰好是 0， 则没有条件为真， 函数将会在未执行任何 ``return`` 语句的情况下终止。 如果函数按照这种执行流程执行完毕，返回值将是 ``None``， 这可不是 0 的绝对值。

::

    >>> absolute_value(0)
    None


顺便说一下，Python提供了一个的内建函数 ``abs`` 用来计算绝对值。

我们来做个练习，写一个比较函数，接受两个值 x 和 y 。
如果 ``x > y``， 则返回 1 ；如果 ``x == y``， 则返回 0 ；如果 ``x < y``，则返回 -1 。


增量式开发
-----------

随着你写的函数越来越大，你在调试上花的时候可能会越来越多。

为了应对越来越复杂的程序，你可能会想尝试一种叫作 **增量式开发（ incremental development )** 的方法。增量式开发的目标，是通过每次只增加和测试少量代码，来避免长时间的调试。

举个例子，假设你想计算两个给定坐标点  :math:`(x_1, y_1)`  和  :math:`(x_2, y_2)` 之间的距离。根据勾股定理（the Pythagorean theorem）
距离是：

.. math:: \mathrm{distance} = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}


第一步要考虑的是在 Python 中，距离函数看起来会是什么样。换句话说，输入（形参）和输出（返回值）是什么？


本例中，输入是可以用 4 个数表示的两个点。返回值是距离， 用浮点数表示。

现在你就可以写出此函数的轮廓了：

::

    def distance(x1, y1, x2, y2):
        return 0.0

显然，此版本不能计算距离；它总是返回 0 。但是在语法上它是正确的，并且能运行，这意味着你可以在使它变得更复杂之前测试它。

用样例实参调用它来进行测试。

::

    >>> distance(1, 2, 4, 6)
    0.0


我选择的这些值，可以使水平距离为 3 ，垂直距离为 4 ；这样结果自然是 5（勾三股四弦五）。
测试一个函数时，知道正确的答案是很有用的。

此时我们已经确认这个函数在语法上是正确的，我们可以开始往函数体中增加代码。
下一步合理的操作，应该是求 :math:`x_2 - x_1` 和 :math:`y_2 - y_1` 这两个差值。
下一个版本在临时变量中存储这些值并打印出来。

::

    def distance(x1, y1, x2, y2):
        dx = x2 - x1
        dy = y2 - y1
        print('dx is', dx)
        print('dy is', dy)
        return 0.0


如果这个函数正常运行，它应该显示 ``dx is 3``  以及 ``dy is 4`` 。
这样的话我们就知道函数获得了正确的实参并且正确执行了第一步计算。
如果不是，也只要检查几行代码。

下一步我们计算 ``dx`` 和 ``dy`` 的平方和。

::

    def distance(x1, y1, x2, y2):
        dx = x2 - x1
        dy = y2 - y1
        dsquared = dx**2 + dy**2
        print('dsquared is: ', dsquared)
        return 0.0

再一次运行程序并检查结果（应该是 25 ）。最后，你可以使用 ``math.sqrt`` 计算并返回结果。

::

    def distance(x1, y1, x2, y2):
        dx = x2 - x1
        dy = y2 - y1
        dsquared = dx**2 + dy**2
        result = math.sqrt(dsquared)
        return result


如果其正确运行的话，你就成功了。否则你可能想在 ``return`` 语句前打印结果检查一下。

该函数的最终版不会在运行时显示任何东西，仅仅返回一个值。
我们之前写的 ``print`` 语句在调试时是很有用的，不过在函数能够正确运行之后，你就该删了它们。
我们称这样的代码为 **脚手架代码（scaffolding)** ， 因为它对程序的构建很有用，但不是最终产品的一部分。


当你刚开始的时候，最好每次只加入一两行代码。
随着经验见长，你会发现自己可以编写、调试更大的代码块了。
无论哪种方式，增量式开发都能节省你大量的调试时间。

这种开发方式的关键是：


#. 从一个能运行的程序开始，并且每次只增加少量改动。无论你何时遇到错误，都能够清楚定位错误的源头。

#. 用临时变量存储中间值，这样你就能显示并检查它们。

#. 一旦程序正确运行，你要删除一些脚手架代码，或者将多条语句组成复合表达式，但是前提是不会影响程序的可读性。


我们来做个练习：运用增量开发方式，写一个叫作 ``hypotenuse`` 的函数，接受直角三角形的两直角边长作为实参，返回该三角形斜边的长度。记录下你开发过程中的每一步。


组合
------

你现在应该已经猜到了，你可以从一个函数内部调用另一个函数。
作为示例，我们接下来写一个函数，接受两个点为参数，分别是圆心和圆周上一点，然后计算圆的面积。

假设圆心坐标存储在变量 ``xc`` 和 ``yc`` 中，圆周上的点的坐标存储在 ``xp`` 和 ``yp`` 中。第一步是计算圆半径，也就是这两个点的距离。我们刚写的`` distance`` 函数就可以计算距离：

::

    radius = distance(xc, yc, xp, yp)

下一步是用得到的半径计算圆面积；我们也刚写了这样的函数：

::

    result = area(radius)

将这些步骤封装在一个函数中，可以得到下面的函数：

::

    def circle_area(xc, yc, xp, yp):
        radius = distance(xc, yc, xp, yp)
        result = area(radius)
        return result

临时变量 ``radius`` 和 ``result`` 对于开发调试很有用的，但是
一旦函数正确运行了，我们可以通过合并函数调用，将程序变得更简洁：

::

    def circle_area(xc, yc, xp, yp):
        return area(distance(xc, yc, xp, yp))


布尔函数
-------------

函数可以返回布尔值（booleans），通常对于隐藏函数内部的复杂测试代码非常方便。
例如：

::

    def is_divisible(x, y):
        if x % y == 0:
            return True
        else:
            return False

通常布尔函数名听起来像是一个疑问句，回答不是 Yes 就是 No， ``is_divisible`` 通过返回 ``True`` 或 ``False`` 来表示 x 是否可以被 y 整除。

请看下面的示例：

::

    >>> is_divisible(6, 4)
    False
    >>> is_divisible(6, 3)
    True

\ ``==``\ 运算符的结果是布尔值，因此我们直接返回它，让代码变得更简洁。

::

    def is_divisible(x, y):
        return x % y == 0

布尔函数通常被用于条件语句中：

::

    if is_divisible(x, y):
        print('x is divisible by y')

很容易写出下面这样的代码：

::

    if is_divisible(x, y) == True:
        print('x is divisible by y')

但这里的比较是多余的。

As an exercise, write a function ``is_between(x, y, z)`` that returns
True if :math:`x \le y \le z` or False otherwise.

我们来做个练习：写一个函数  ``is_between(x, y, z)`` ，如果 :math:`x \le y \le z` 返回 ``True`` 否则返回 ``False``。

再谈递归
----------

我们目前只介绍了 Python 中一个很小的子集，但是当你知道这个子集已经是一个 **完备的** 编程语言，你可能会觉得很有意思。这意味任何能被计算的东西都能用这个语言表达。
有史以来所有程序你都可以仅仅用目前学过的语言特性重写（事实上，你可能还需要一些命令来控制鼠标、磁盘等设备，但仅此而已）。

阿兰·图灵第一个证明了这种说法的正确性，这可是一项非凡的工作。他是首批计算机科学家之一（一些人认为他是数学家，但很多早期的计算机科学家也是出身于数学家）。
相应地，这被称为图灵理论。关于图灵理论更完整（和更准确）的讨论，我推荐Michael Sipser的书 *《Introduction to the Theory of Computation》*。

为了让你明白能用目前学过的工具做什么，我们将计算一些递归定义的数学函数。
递归定义类似循环定义，因为定义中包含一个对已经被定义的事物的引用。
一个纯粹的循环定义并没有什么用：


漩涡状：
	一个用以描述漩涡状物体的形容词。

If you saw that definition in the dictionary, you might be annoyed. On
the other hand, if you looked up the definition of the factorial
function, denoted with the symbol :math:`!`, you might get something
like this:

如果你看到字典里是这样定义的，你大概会生气。
另一方面，如果你查找用 :math:`!` 符号表示的阶乘函数的定义，你可能看到类似下面的内容：

.. math::

   \begin{aligned}
   &&  0! = 1 \\
   &&  n! = n (n-1)!\end{aligned}

该定义指出 0 的阶乘是 1 ，任何其他值 :math:`n` 的阶乘是 :math:`n` 乘以 :math:`n-1` 的阶乘。

所以 :math:`3!` 的阶乘是 3 乘以 :math:`2!` ，它又是 2 乘以 :math:`1!` ， 后者又是 1 乘以  :math:`0!` 。 放到一起， :math:`3!` 等于 3 乘以 2 乘以 1 乘以 1 ，结果是 6 。

如果你可以递归定义某个东西，你就可以写一个 Python 程序计算它。
第一步是决定应该有哪些形参。在此例中 ``factorial``函数很明显接受一个整型数：

::

    def factorial(n):


如果实参刚好是 0 ，我们就返回 1 ：

::

    def factorial(n):
        if n == 0:
            return 1

否则，就到了有意思的部分，我们要进行递归调用来找到 :math:`n-1` 的阶乘然后乘以 :math:`n`: 

::

    def factorial(n):
        if n == 0:
            return 1
        else:
            recurse = factorial(n-1)
            result = n * recurse
            return result

The flow of execution for this program is similar to the flow of
countdown in Section [recursion]. If we call factorial with the value 3:

程序的执行流程和第五章\ :ref:`recursion`\ 一节中的 ``countdown`` 类似。如果我们传入参数的值是 3 ：


由于3不等于0，我们执行第二个分支并计算n-1的阶乘... 

	由于2不等于0，我们执行第二个分支并计算n-1的阶乘... 

		由于1不等于0，我们执行第二个分支并计算n-1的阶乘... 

			由于0等于0，我们执行第一个分支并返回1，不再进行任何递归调用。 

        The return value, 1, is multiplied by :math:`n`, which is 1, and
        the result is returned.

		返回值 1 与 :math:`n` （其为1）相乘，并返回结果。

    The return value, 1, is multiplied by :math:`n`, which is 2, and the
    result is returned.

	返回值（1）被与 :math:`n` （其为2）相乘，并返回结果。

The return value (2) is multiplied by :math:`n`, which is 3, and the
result, 6, becomes the return value of the function call that started
the whole process.

返回值(2)被与 :math:`n` （其为3）相乘，并返回结果6，成为整个过程开始调用的函数的返回值。

Figure [fig.stack3] shows what the stack diagram looks like for this
sequence of function calls.

图 [fig.stack3] 显示了该函数调用序列的栈图看上去是什么样

.. figure:: figs/stack3.pdf
   :alt: Stack diagram.

   Stack diagram.

The return values are shown being passed back up the stack. In each
frame, the return value is the value of result, which is the product of
n and recurse.

图中显示返回值被传回到栈顶。 在每一帧中，返回值就是结果值，即是 n 和 recurse 的乘积。

In the last frame, the local variables recurse and result do not exist,
because the branch that creates them does not run.

最后一帧中，局部变量 recurse 和 result 并不存在， 因为生成它们的分支并没有被执行。

Leap of faith
-------------

信心的飞跃
----------

Following the flow of execution is one way to read programs, but it can
quickly become overwhelming. An alternative is what I call the “leap of
faith”. When you come to a function call, instead of following the flow
of execution, you *assume* that the function works correctly and returns
the right result.

跟踪程序执行流程是理解程序的一种方法，但它可能很快会变得错综复杂。
另一种代替方法我称之为“信心的飞跃”。
当你遇到一个函数调用时，不跟踪执行流程，而是 **假设** 这个函数正确的运行并返回正确的结果。

In fact, you are already practicing this leap of faith when you use
built-in functions. When you call math.cos or math.exp, you don’t
examine the bodies of those functions. You just assume that they work
because the people who wrote the built-in functions were good
programmers.

事实上，当你使用内建函数时，你已经实践过这种方法了。
当你调用 math.cos 或 math.exp 时，你并没有检查那些函数的函数体。
你只是假设了他们能用并且写这些内建函数的都是好程序员。

The same is true when you call one of your own functions. For example,
in Section [boolean], we wrote a function called ``is_divisible`` that
determines whether one number is divisible by another. Once we have
convinced ourselves that this function is correct—by examining the code
and testing—we can use the function without looking at the body again.

当你调用一个自己写的函数时也是一样。
例如，在 [boolean] 小节中，我们写了一个 ``is_divisible`` 函数来检查一个数是否能被另一个数整除。
通过对代码的检查，一旦我们确信这个函数能够正确运行，我们就能不用再查看函数体而直接使用了。

The same is true of recursive programs. When you get to the recursive
call, instead of following the flow of execution, you should assume that
the recursive call works (returns the correct result) and then ask
yourself, “Assuming that I can find the factorial of :math:`n-1`, can I
compute the factorial of :math:`n`?” It is clear that you can, by
multiplying by :math:`n`.

递归程序也是这样。
当你遇到递归调用时， 不用顺着执行流程，你应该假设次递归调用能够正确工作（产生正确的结果）然后问你自己，“假设我可以找到 :math:`n-1` 的阶乘，我可以找到 :math:`n` 的阶乘吗？
很明显你能，只要与 :math:`n` 相乘。

Of course, it’s a bit strange to assume that the function works
correctly when you haven’t finished writing it, but that’s why it’s
called a leap of faith!

当然，当你没写完它的时候，假设函数正确工作有一点儿奇怪， 但这也是为什么这被称作信心的飞跃了！


One more example
----------------

再来一个例子
-------------

After factorial, the most common example of a recursively defined
mathematical function is fibonacci, which has the following definition
(see http://en.wikipedia.org/wiki/Fibonacci_number):

看完了阶层，另一个最普遍的被递归定义的数学函数是 fibonacci ，其定义见 http://en.wikipedia.org/wiki/Fibonacci_number ：

.. math::

   \begin{aligned}
   && \mathrm{fibonacci}(0) = 0 \\
   && \mathrm{fibonacci}(1) = 1 \\
   && \mathrm{fibonacci}(n) = \mathrm{fibonacci}(n-1) + \mathrm{fibonacci}(n-2)\end{aligned}

 Translated into Python, it looks like this:

翻译成 Python 看起来就像这样：

::

    def fibonacci (n):
        if n == 0:
            return 0
        elif  n == 1:
            return 1
        else:
            return fibonacci(n-1) + fibonacci(n-2)

If you try to follow the flow of execution here, even for fairly small
values of :math:`n`, your head explodes. But according to the leap of
faith, if you assume that the two recursive calls work correctly, then
it is clear that you get the right result by adding them together.

这里，如果你试图跟踪执行流程，即使是相当小的 :math:`n` ，也足够你头疼的。但遵循信心的飞跃这条原则，如果你假设这两个递归调用都能正确运行，很明显将他们两个相加就是正确结果。

Checking types
--------------

检查类型
---------

What happens if we call factorial and give it 1.5 as an argument?

如果我们将 1.5 作为参数调用阶乘函数会怎样？

::

    >>> factorial(1.5)
    RuntimeError: Maximum recursion depth exceeded

It looks like an infinite recursion. How can that be? The function has a
base case—when n == 0. But if n is not an integer, we can *miss* the
base case and recurse forever.

看上去像是一个无限循环。但那是如何发生的？ 终止条件是 n == 0 。
但是如果 n 不是一个整数呢？ 终止条件不会满足，递归将永远进行下去。

In the first recursive call, the value of n is 0.5. In the next, it is
-0.5. From there, it gets smaller (more negative), but it will never be
0.

在第一次递归调用中，n 的值是 0.5 。下一次，是 -0.5 。自此它会越来越小，但永远不会是 0 。

We have two choices. We can try to generalize the factorial function to
work with floating-point numbers, or we can make factorial check the
type of its argument. The first option is called the gamma function and
it’s a little beyond the scope of this book. So we’ll go for the second.

我们有两个选择。我们可以试着泛化factorial函数使其能处理浮点数，或者我们可以让factorial检查它的实参的类型。第一个选择被称作gamma函数，它有点儿超过本书的范围了。 所以我们将用第二种方法。

We can use the built-in function isinstance to verify the type of the
argument. While we’re at it, we can also make sure the argument is
positive:

我们可以使用内建函数 isinstance 来验证实参的类型。 同时，我们也可以确保该实参是正数： 

::

    def factorial (n):
        if not isinstance(n, int):
            print('Factorial is only defined for integers.')
            return None
        elif n < 0:
            print('Factorial is not defined for negative integers.')
            return None
        elif n == 0:
            return 1
        else:
            return n * factorial(n-1)

The first base case handles nonintegers; the second handles negative
integers. In both cases, the program prints an error message and returns
None to indicate that something went wrong:

第一个基本条件处理非整数，第二个处理负整数。
在这两个条件中，程序打印一条错误信息并返回None以指明某些东西出错了： 

::

    >>> factorial('fred')
    Factorial is only defined for integers.
    None
    >>> factorial(-2)
    Factorial is not defined for negative integers.
    None

If we get past both checks, we know that :math:`n` is positive or zero,
so we can prove that the recursion terminates.

如果我们通过了这两个检查，那么我们知道 :math:`n` 是一个正数或 0 ， 因此我们可以保证递归终止。


This program demonstrates a pattern sometimes called a **guardian**. The
first two conditionals act as guardians, protecting the code that
follows from values that might cause an error. The guardians make it
possible to prove the correctness of the code.

此程序演示了一个模式，有时称作 **监护人（guardian）模式** 。
前两个条件扮演监护人的角色，避免接下来的代码使用引发错误的值。
监护人使得验证代码的正确性成为可能。


In Section [raise] we will see a more flexible alternative to printing
an error message: raising an exception.

在 [raise] 小结中我们将看到更灵活的方式打印错误信息：抛出异常。

Debugging
---------

调试
-----

Breaking a large program into smaller functions creates natural
checkpoints for debugging. If a function is not working, there are three
possibilities to consider:

将一个大程序分解为较小的函数为调试生成了检查点。
如果一个函数不如预期的运行，有三个可能性需要考虑： 

-  There is something wrong with the arguments the function is getting;
   a precondition is violated.

-  该函数获得的实参有些错误，违反先决条件。

-  There is something wrong with the function; a postcondition is
   violated.

-  该函数有些错误，违反后置条件。

-  There is something wrong with the return value or the way it is being
   used.

-  返回值或者它的使用方法有错误。

To rule out the first possibility, you can add a print statement at the
beginning of the function and display the values of the parameters (and
maybe their types). Or you can write code that checks the preconditions
explicitly.

为了排除第一种可能，你可以在函数的开始增加一条print语句来打印形参的值（也可能是它们的类型）。
或者你可以写代码来检查先决条件。

If the parameters look good, add a print statement before each return
statement and display the return value. If possible, check the result by
hand. Consider calling the function with values that make it easy to
check the result (as in Section [incremental.development]).

如果形参看起来没问题，在每个return语句之前增加一条print语句，来打印返回值。
如果可能，手工检查结果。
考虑用一些容易检查的值来调用该函数（类似在 [incremental.development] 节中）。 

If the function seems to be working, look at the function call to make
sure the return value is being used correctly (or used at all!).

如果该函数看起来正常工作，则检查函数调用确保返回值被正确的使用（或者被用了！）。

Adding print statements at the beginning and end of a function can help
make the flow of execution more visible. For example, here is a version
of factorial with print statements:

在一个函数的开始和结束增加打印语句可以使执行流程更明显。
例如，下面是一个加入打印语句的阶乘函数。

::

    def factorial(n):
        space = ' ' * (4 * n)
        print(space, 'factorial', n)
        if n == 0:
            print(space, 'returning 1')
            return 1
        else:
            recurse = factorial(n-1)
            result = n * recurse
            print(space, 'returning', result)
            return result

space is a string of space characters that controls the indentation of
the output. Here is the result of factorial(4) :

space是一个空格字符的字符串，用来控制输出的缩进。 这是factorial(4)的结果：

::

                     factorial 4
                 factorial 3
             factorial 2
         factorial 1
     factorial 0
     returning 1
         returning 1
             returning 2
                 returning 6
                     returning 24

If you are confused about the flow of execution, this kind of output can
be helpful. It takes some time to develop effective scaffolding, but a
little bit of scaffolding can save a lot of debugging.

如果你对执行流程感到困惑，这种输出可能有用。
开发有效的脚手架代码会花些时间，但是一点点的脚手架代码能够节省调试的时间。

Glossary
--------

术语表
-------

temporary variable（临时变量）:
    A variable used to store an intermediate value in a complex
    calculation.

dead code （死代码）:
    Part of a program that can never run, often because it appears after
    a return statement.

incremental development（增量式开发）:
    A program development plan intended to avoid debugging by adding and
    testing only a small amount of code at a time.

scaffolding（脚手架代码）:
    Code that is used during program development but is not part of the
    final version.

guardian （监护人模式）:
    A programming pattern that uses a conditional statement to check for
    and handle circumstances that might cause an error.

Exercises
---------

练习
-----

Draw a stack diagram for the following program. What does the program
print?

画出下面程序的调用栈图。这个程序的最终输出是什么？

::

    def b(z):
        prod = a(z, z)
        print(z, prod)
        return prod

    def a(x, y):
        x = x + 1
        return x * y

    def c(x, y, z):
        total = x + y + z
        square = b(total)**2
        return square

    x = 1
    y = x + 1
    print(c(x, y+3, x+y))

[ackermann]

The Ackermann function, :math:`A(m, n)`, is defined:

Ackermann 函数 :math:`A(m, n)` 如下定义：

.. math::

   \begin{aligned}
   A(m, n) = \begin{cases}
                 n+1 & \mbox{if } m = 0 \\
           A(m-1, 1) & \mbox{if } m > 0 \mbox{ and } n = 0 \\
   A(m-1, A(m, n-1)) & \mbox{if } m > 0 \mbox{ and } n > 0.
   \end{cases} \end{aligned}

See http://en.wikipedia.org/wiki/Ackermann_function. Write a function
named ack that evaluates the Ackermann function. Use your function to
evaluate ack(3, 4), which should be 125. What happens for larger values
of m and n? Solution: http://thinkpython2.com/code/ackermann.py.

阅读 http://en.wikipedia.org/wiki/Ackermann_function 。
试写一个函数叫做 ack 来计算 Ackermann 函数。
你的程序在计算 ack（3，4）是应该返回 125 。
当输入更大的数会发生什么？
解答：http://thinkpython2.com/code/ackermann.py 。

[palindrome]

A palindrome is a word that is spelled the same backward and forward,
like “noon” and “redivider”. Recursively, a word is a palindrome if the
first and last letters are the same and the middle is a palindrome.

palindrome 是说某个词正着拼反着拼都一样。如 “noon”和“redivider”。
递归地定义为某个词首字母和尾字母相同而中间部分是 palindrome 。

The following are functions that take a string argument and return the
first, last, and middle letters:

下面的函数接受一个字符串参数并返回第一个，最后一个，和中间的字母：

::

    def first(word):
        return word[0]

    def last(word):
        return word[-1]

    def middle(word):
        return word[1:-1]

We’ll see how they work in Chapter [strings].

在章节 [strings] 中我们将看到他们是如何工作的。

#. Type these functions into a file named palindrome.py and test them
   out. What happens if you call middle with a string with two letters?
   One letter? What about the empty string, which is written ``''`` and
   contains no letters?

#. 将它们录入到文件 palindrome.py 中并测试。当你用一个两个字母的字符串调用 middle 时会发生什么？一个字母的呢？空字符串呢？就是这样 ``''`` 的其中不含任何字母的字符串。

#. Write a function called ``is_palindrome`` that takes a string
   argument and returns True if it is a palindrome and False otherwise.
   Remember that you can use the built-in function len to check the
   length of a string.

#. 写一个函数叫 ``is_palindrome`` ，接受一个字符串作为参数。如果是 palindrome 就返回 True 反之 False。 你可以使用内建函数 len 来检查字符串长度。

Solution: http://thinkpython2.com/code/palindrome_soln.py.

解答：http://thinkpython2.com/code/palindrome_soln.py 。

A number, :math:`a`, is a power of :math:`b` if it is divisible by
:math:`b` and :math:`a/b` is a power of :math:`b`. Write a function
called ``is_power`` that takes parameters a and b and returns True if a
is a power of b. Note: you will have to think about the base case.

数 :math:`a` 是  :math:`b` 的幂当它能被  :math:`b` 整除并且 :math:`a/b` 是 :math:`b` 的幂。
写一个函数叫 ``is_power`` 接受两个参数 a 和 b 并且当 a 是 b 的幂时返回 True。注意终止条件。

The greatest common divisor (GCD) of :math:`a` and :math:`b` is the
largest number that divides both of them with no remainder.

 :math:`a` 和 :math:`b` 的最大公约数（GCD）是指能被他俩整除的最大数。


One way to find the GCD of two numbers is based on the observation that
if :math:`r` is the remainder when :math:`a` is divided by :math:`b`,
then :math:`gcd(a,
b) = gcd(b, r)`. As a base case, we can use :math:`gcd(a, 0) = a`.

一种找两个数的GCD的方法基于这样一个原理：如果 :math:`r` 是 :math:`a` 被 :math:`b` 除后的余数，那么  :math:`gcd(a,b) = gcd(b, r)` 。终止条件为 :math:`gcd(a, 0) = a` 。

Write a function called ``gcd`` that takes parameters a and b and
returns their greatest common divisor.

试写一个函数叫 ``gcd`` ，其接受两个参数 a 和 b 并返回最大公约数。

Credit: This exercise is based on an example from Abelson and Sussman’s
*Structure and Interpretation of Computer Programs*.

声明：这份练习基于 Abelson 和 Sussman 的 《Structure and Interpretation of Computer Programs》其中的例子。