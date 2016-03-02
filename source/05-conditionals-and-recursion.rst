Conditionals and recursion 条件和递归
========================================

The main topic of this chapter is the if statement, which executes
different code depending on the state of the program. But first I want
to introduce two new operators: floor division and modulus.

这章的中心话题是能够根据程序的状态执行不同命令的if语句。但是首先我想介绍两个新的运算符 : 地板除运算符和求余运算符。

Floor division and modulus　地板除运算符和求余运算符
-----------------------------------------------------------------

The **floor division** operator, ``//``, divides two numbers and rounds
down to an integer. For example, suppose the run time of a movie is 105
minutes. You might want to know how long that is in hours. Conventional
division returns a floating-point number:

**地板除运算符(floor division operator)**\, ``//``, 先做除法然后将结果保留到整数。比如，如果一部电影有 105 分钟，你可能想知道这代表着多少小时，传统的除法操作会返回一个浮点数:

::

    >>> minutes = 105
    >>> minutes / 60
    1.75

But we don’t normally write hours with decimal points. Floor division
returns the integer number of hours, dropping the fraction part:

但是，用小时做单位的时候，我们通常并不写出小数部分。地板除丢弃除法运算结果的小数部分返回整数个小时:

::

    >>> minutes = 105
    >>> hours = minutes // 60
    >>> hours
    1

To get the remainder, you could subtract off one hour in minutes:

如果你希望得到余数，你可以从除数中减去一个小时也就是60分钟:

::

    >>> remainder = minutes - hours * 60
    >>> remainder
    45

An alternative is to use the **modulus operator**, ``%``, which divides
two numbers and returns the remainder.

另一个运算符就是 **求余运算符(modulus operator)**\ 对整数进行运算，
返回第一个运算数除以第二个所得的余数。

::

    >>> remainder = minutes % 60
    >>> remainder
    45

The modulus operator is more useful than it seems. For example, you can
check whether one number is divisible by another—if x % y is zero, then
x is divisible by y.

求余运算符比它看起更加有用。比如，你可以查看一个是否可以被另一个数整除——如果　x % y　是 0，那么 x 能被 y　整除。

Also, you can extract the right-most digit or digits from a number. For
example, x % 10 yields the right-most digit of x (in base 10). Similarly
x % 100 yields the last two digits.

此外，你也能获得一个数的最右一位或者各位的数字。 例如x %
10产生x的最右一位数字（十进制中）。 相似的，x % 100产生最后两位数字。

If you are using Python 2, division works differently. The division
operator, ``/``, performs floor division if both operands are integers,
and floating-point division if either operand is a float.

如果你正在使用　Python 2, 那么除法就会和前面的介绍有点不同。除法运算符， ``/``　在被除数和除数都是整数的时候进行地板除，但是当被除数和除数中任意一个是浮点数的时候进行浮点数除法。(译者注:在 Python3 版本中无论任何类型都会保持小数部分)

Boolean expressions 布尔表达式
--------------------------------------

A **boolean expression** is an expression that is either true or false.
The following examples use the operator ==, which compares two operands
and produces True if they are equal and False otherwise:

**布尔表达式（boolean expression）**\ 的结果为真或者假。
下面的例子使用==运算符，它比较两个运算数，
如果它们相等，则产生True，否则产生False。

::

    >>> 5 == 5
    True
    >>> 5 == 6
    False

True and False are special values that belong to the type bool; they are
not strings:

True和False是属于bool类型的特殊的值， 它们不是字符串。

::

    >>> type(True)
    <class 'bool'>
    >>> type(False)
    <class 'bool'>

The == operator is one of the **relational operators**; the others are:

==运算符是\ **关系运算符（relational operators）**\ 之一， 其它的是：

::

          x != y               # x is not equal to y
          x > y                # x is greater than y
          x < y                # x is less than y
          x >= y               # x is greater than or equal to y
          x <= y               # x is less than or equal to y

Although these operations are probably familiar to you, the Python
symbols are different from the mathematical symbols. A common error is
to use a single equal sign (=) instead of a double equal sign (==).
Remember that = is an assignment operator and == is a relational
operator. There is no such thing as =< or =>.

虽然这些运算符对你来说可能很熟悉，但是Python的符号与数学符号不相同。
一个通常的错误是使用单独一个等号（=）而不是双等号（==）。
记住，=是赋值运算符，==是关系运算符。 没有类似=<或=>的东西。

Logical operators　逻辑运算符
----------------------------------

There are three **logical operators**: and, or, and not. The semantics
(meaning) of these operators is similar to their meaning in English. For
example, x > 0 and x < 10 is true only if x is greater than 0 *and* less
than 10.

有三个\ **逻辑运算符（logical operators）**\ ：and、or和not。
这些运算符的含义和它们的英语意思相似。例如如果x大于0并且小于10，则只在　x > 0
而且 x < 10　时为真。


n%2 == 0 or n%3 == 0 is true if *either or both* of the conditions is
true, that is, if the number is divisible by 2 *or* 3.

只要有一个条件为真，也就是数字n能被2或者3整除， 则n%2 == 0 or n%3 ==
0为真。

Finally, the not operator negates a boolean expression, so not (x > y)
is true if x > y is false, that is, if x is less than or equal to y.

最后，not对一个布尔表达式取反， 因此，如果x >
y为假，也就是说x小于或等于y， 则not (x > y)为真。

Strictly speaking, the operands of the logical operators should be
boolean expressions, but Python is not very strict. Any nonzero number
is interpreted as True:

严格来讲，布尔运算符的运算数应该是布尔表达式，
但是Python并不严格。任何非0的数字都被解释成“真”。


::

    >>> 42 and True
    True

This flexibility can be useful, but there are some subtleties to it that
might be confusing. You might want to avoid it (unless you know what you
are doing).

这种灵活性很有用，但有一些细节可能容易令人困惑。你可能需要避免它（除非你知道你正在做什么）。

Conditional execution　有条件的执行
------------------------------------------

In order to write useful programs, we almost always need the ability to
check conditions and change the behavior of the program accordingly.
**Conditional statements** give us this ability. The simplest form is
the if statement:

为了写出有用的程序，我们几乎总是需要检测条件并相应的改变程序行为的能力。
**条件语句（Conditional statements）**\ 给予我们这一能力。
最简单的形式是if语句：

::

    if x > 0:
        print('x is positive')

The boolean expression after if is called the **condition**. If it is
true, the indented statement runs. If not, nothing happens.

if之后的布尔表达式被称作\ **条件（condition）**\ 。
如果它为真，则缩进的语句会被执行。 如果不是，则什么也不会发生。

if statements have the same structure as function definitions: a header
followed by an indented body. Statements like this are called **compound
statements**.

if语句和函数定义有相同的结构：一个语句头跟着一个缩进的语句体。
类似的语句被称作\ **复合语句（compound statements）**\ 。

There is no limit on the number of statements that can appear in the
body, but there has to be at least one. Occasionally, it is useful to
have a body with no statements (usually as a place keeper for code you
haven’t written yet). In that case, you can use the pass statement,
which does nothing.

语句体中可出现的语句数目没有限制，但是至少得有一个。
偶尔，一条语句都没有的语句体也是有用的（通常是为你还没写的代码占一个位子）。
这种情况下，你可以使用pass语句，它什么也不做。

::

    if x < 0:
        pass          # TODO: need to handle negative values!

Alternative execution　二选一执行
------------------------------------------

A second form of the if statement is “alternative execution”, in which
there are two possibilities and the condition determines which one runs.
The syntax looks like this:


if语句的第二种形式是\ **二选一执行（alternative execution）**\ ，
此时有两个可能的选择，由条件决定执行哪一个。 语法看起来是这样：

::

    if x % 2 == 0:
        print('x is even')
    else:
        print('x is odd')

If the remainder when x is divided by 2 is 0, then we know that x is
even, and the program displays an appropriate message. If the condition
is false, the second set of statements runs. Since the condition must be
true or false, exactly one of the alternatives will run. The
alternatives are called **branches**, because they are branches in the
flow of execution.

如果x除以2的余数是0，那么我们知道x是偶数，
并且程序对这一效果显示一个信息。 如果条件为假，执行第二段语句。
既然条件要么为真要么为假，两个选择之一必被执行。
这些选择被称作\ **分支（branches）**\ ，因为它们是执行流程的分支。

Chained conditionals 链式条件
----------------------------------------

Sometimes there are more than two possibilities and we need more than
two branches. One way to express a computation like that is a **chained
conditional**:

有时有超过两个可能的情况，于是我们需要多于两个的分支。
表示像这样的计算的方法之一是\ **链式条件（chained conditional）**\ ：

::

    if x < y:
        print('x is less than y')
    elif x > y:
        print('x is greater than y')
    else:
        print('x and y are equal')

elif is an abbreviation of “else if”. Again, exactly one branch will
run. There is no limit on the number of elif statements. If there is an
else clause, it has to be at the end, but there doesn’t have to be one.

elif是“else if”的缩写。同样地，必有一个分支被执行。
elif语句的数目没有限制。如果有一个else从句，
它必须是在最后，但并不是必须要有一个。

::

    if choice == 'a':
        draw_a()
    elif choice == 'b':
        draw_b()
    elif choice == 'c':
        draw_c()

Each condition is checked in order. If the first is false, the next is
checked, and so on. If one of them is true, the corresponding branch
runs and the statement ends. Even if more than one condition is true,
only the first true branch runs.

按顺序检测逐个条件，如果第一个为假，检测下一个，以此类推。
如果它们中有一个为真，相应的分支被执行，并且语句结束。
即便有不止一个条件为真，也只执行第一个为真的分支。

Nested conditionals 嵌套条件
--------------------------------------

One conditional can also be nested within another. We could have written
the example in the previous section like this:

一个条件可以嵌到另一个里面。我们可以这样写前一节的例子：

::

    if x == y:
        print('x and y are equal')
    else:
        if x < y:
            print('x is less than y')
        else:
            print('x is greater than y')

The outer conditional contains two branches. The first branch contains a
simple statement. The second branch contains another if statement, which
has two branches of its own. Those two branches are both simple
statements, although they could have been conditional statements as
well.

外面的条件包括两个分支。第一个分支包括一条简单的语句。
第二个分支又包括一个if语句，它有自己的两个分支。
那两个分支都是简单的语句，当然它们也可以是条件语句。

Although the indentation of the statements makes the structure apparent,
**nested conditionals** become difficult to read very quickly. It is a
good idea to avoid them when you can.

虽然语句的缩进使得结构很明显，但是\ **嵌套条件（nested conditionals）**
仍然很难快速地阅读。一般来讲，当你可以的时候，避免使用嵌套条件是个好办法。

Logical operators often provide a way to simplify nested conditional
statements. For example, we can rewrite the following code using a
single conditional:

逻辑运算符经常提供一个化简嵌套条件语句的方法。
例如，我们可以用一个单一条件重写下面的代码：

::

    if 0 < x:
        if x < 10:
            print('x is a positive single-digit number.')

The print statement runs only if we make it past both conditionals, so
we can get the same effect with the and operator:

只有我们通过了两个条件检测的时候，print语句才被执行，
因此我们可以用and运算符得到相同的效果：

::

    if 0 < x and x < 10:
        print('x is a positive single-digit number.')

For this kind of condition, Python provides a more concise option:

但是对于这样的条件，Python 提供了一种更加简洁的选择。

::

    if 0 < x < 10:
        print('x is a positive single-digit number.')

Recursion　递归
------------------

It is legal for one function to call another; it is also legal for a
function to call itself. It may not be obvious why that is a good thing,
but it turns out to be one of the most magical things a program can do.
For example, look at the following function:

一个函数调用另一个是合法的，一个函数调用它自己也是合法的。
这样的好处可能并不是那么显然，但它实际上成为了程序能做到的最神奇的事情之一。
例如，看一下这个程序：

::

    def countdown(n):
        if n <= 0:
            print('Blastoff!')
        else:
            print(n)
            countdown(n-1)

If n is 0 or negative, it outputs the word, “Blastoff!” Otherwise, it
outputs n and then calls a function named countdown—itself—passing n-1
as an argument.

如果n是0或负数，它输出单词“Blastoff!”。
否则，它输出n然后调用一个名为countdown的函数—它自己— 传递n-1作为实参。

What happens if we call this function like this?

如果我们像这样调用该函数会发生什么呢？

::

    >>> countdown(3)

The execution of countdown begins with n=3, and since n is greater than
0, it outputs the value 3, and then calls itself...

countdown开始以n=3执行，既然n大于0， 它输出值3，然后调用它自己...

    The execution of countdown begins with n=2, and since n is greater
    than 0, it outputs the value 2, and then calls itself...

    countdown开始以n=2执行，既然n大于0， 它输出值2，然后调用它自己...

        The execution of countdown begins with n=1, and since n is
        greater than 0, it outputs the value 1, and then calls itself...

        countdown开始以n=1执行，既然n大于0，
        它输出值1，然后调用它自己...

            The execution of countdown begins with n=0, and since n is
            not greater than 0, it outputs the word, “Blastoff!” and
            then returns.

            countdown开始以n=0执行，既然n不大于0，
            它输出单词“Blastoff!”，然后返回。

        The countdown that got n=1 returns.

        获得n=1的countdown返回。

    The countdown that got n=2 returns.

    获得n=2的countdown返回。

The countdown that got n=3 returns.

获得n=3的countdown返回。

And then you’re back in ``__main__``. So, the total output looks like
this:

然后你回到\ ``__main__``\ 中。因此整个输出类似于：

::

    3
    2
    1
    Blastoff!

A function that calls itself is **recursive**; the process of executing
it is called **recursion**.

一个调用它自己的函数是\ **递归的（recursive）**\ ，
这个过程被称作\ **递归（recursion）**\ 。


As another example, we can write a function that prints a string n
times.

再举一例，我们可以写一个函数，其打印一个字符串n次。

::

    def print_n(s, n):
        if n <= 0:
            return
        print(s)
        print_n(s, n-1)

If n <= 0 the **return statement** exits the function. The flow of
execution immediately returns to the caller, and the remaining lines of
the function don’t run.

如果n <= 0，return语句退出函数。
执行流程马上返回到调用者，函数剩余的行不会被执行。

The rest of the function is similar to countdown: it displays s and then
calls itself to display s :math:`n-1` additional times. So the number of
lines of output is 1 + (n - 1), which adds up to n.

函数的其余部分和countdown相似： 如果n比0大，它显示s并调用它自己，再显示s
:math:`n-1`\ 次。 因此，输出的行数是1 + (n - 1)，加起来是n。

For simple examples like this, it is probably easier to use a for loop.
But we will see examples later that are hard to write with a for loop
and easy to write with recursion, so it is good to start early.

对于像这样简单的例子，使用for循环可能更容易。
但是我们后面将看到一些用for循环很难写，用递归却很容易的例子，
所以早点儿开始使用递归有好处。


Stack diagrams for recursive functions 递归函数栈图
---------------------------------------------------

In Section [stackdiagram], we used a stack diagram to represent the
state of a program during a function call. The same kind of diagram can
help interpret a recursive function.

在[stackdiagram]节中，我们用栈图表示函数调用期间程序的状态。
同样的图能帮我们理解一个递归函数。

Every time a function gets called, Python creates a frame to contain the
function’s local variables and parameters. For a recursive function,
there might be more than one frame on the stack at the same time.

每当一个函数被调用时，Python生成一个新的函数框架，
其包括函数的局部变量和形参。
对于一个递归函数，在栈上可能同时有多个框架。

Figure [fig.stack2] shows a stack diagram for countdown called with n =
3.

图[fig.stack2]展示了一个以n = 3调用countdown的栈图。

.. figure:: figs/stack2.png
   :alt: Stack diagram.

   Stack diagram.

As usual, the top of the stack is the frame for ``__main__``. It is
empty because we did not create any variables in ``__main__`` or pass
any arguments to it.

通常，栈顶是\ ``__main__``\ 框架。
因为我们在\ ``__main__``\ 中没有创建任何变量也没有传递任何实参给它，
所以它是空的。

The four countdown frames have different values for the parameter n. The
bottom of the stack, where n=0, is called the **base case**. It does not
make a recursive call, so there are no more frames.

对于形参n，四个countdown框架有不同的值。
n=0的栈底，被称作\ **基础情形（base case）**\ 。
它不再进行递归调用了，所以没有更多的框架了。

As an exercise, draw a stack diagram for ``print_n`` called with
``s = 'Hello'`` and n=2. Then write a function called ``do_n`` that
takes a function object and a number, n, as arguments, and that calls
the given function n times.

作为一个练习，请你画一个以\ ``s = 'Hello'``\ 和n=2调用\ ``print_n``\ 的栈图。
写一个名为\ ``do_n``\ 的函数，接受一个函数对象和一个数n作为实参，
能够调用指定的函数n次。

Infinite recursion　无限递归
------------------------------------

If a recursion never reaches a base case, it goes on making recursive
calls forever, and the program never terminates. This is known as
**infinite recursion**, and it is generally not a good idea. Here is a
minimal program with an infinite recursion:

如果一个递归永不会到达基础情形，它将永远进行递归调用，
并且程序永远不会终止。这被称作\ **无限递归（infinite recursion）**\ ，
通常这不是一个好主意。这是最小的具有无限递归的程序：

::

    def recurse():
        recurse()

In most programming environments, a program with infinite recursion does
not really run forever. Python reports an error message when the maximum
recursion depth is reached:

在大多数编程环境里，一个具有无限递归的程序并非永远不会终止。
当达到最大递归深度时，Python报告一个错误信息：

::

      File "<stdin>", line 2, in recurse
      File "<stdin>", line 2, in recurse
      File "<stdin>", line 2, in recurse
                      .   
                      .
                      .
      File "<stdin>", line 2, in recurse
    RuntimeError: Maximum recursion depth exceeded

This traceback is a little bigger than the one we saw in the previous
chapter. When the error occurs, there are 1000 recurse frames on the
stack!

此回溯比我们在前面章节看到的大一点。
当错误出现的时候，在栈上有1000个递归框架！

If you write encounter an infinite recursion by accident, review your
function to confirm that there is a base case that does not make a
recursive call. And if there is a base case, check whether you are
guaranteed to reach it.

如果你遇到了无限递归的错误，检查你的函数确认基础情形（base case）没有继续调用递归。
同时如果确实有正确的基础情形（base case），请检查基础情形（base case）是不是能够被调用。

Keyboard input　键盘输入
----------------------------

The programs we have written so far accept no input from the user. They
just do the same thing every time.

到目前为止我们所写的程序都不接受来自用户的输入，从这个意义上讲有点儿粗鲁。
每次它们都只是做相同的事情。

Python provides a built-in function called ``input`` that stops the program
and waits for the user to type something. When the user presses Return
or Enter, the program resumes and ``input`` returns what the user typed
as a string. In Python 2, the same function is called ``raw_input``.

Python 提供了一个内建函数``input``从键盘获得用户输入。当此函数被调用时,它会暂停程序同时等待用户输入。
当用户按下回车键(Return or Enter)，程序恢复执行并且\ ``input``\ 以字符串形式返回用户键入的内容。
Python 2提供了一个叫做\ ``raw_input``\ 的相似功能函数，

::

    >>> text = input()
    What are you waiting for?
    >>> text
    What are you waiting for?

Before getting input from the user, it is a good idea to print a prompt
telling the user what to type. ``input`` can take a prompt as an
argument:

在从用户那儿获得输入之前，打印一个提示告诉用户输入什么是个好办法。
\``input``\ 可以把提示语作为实参。

::

    >>> name = input('What...is your name?\n')
    What...is your name?
    Arthur, King of the Britons!
    >>> name
    Arthur, King of the Britons!

The sequence ``\n`` at the end of the prompt represents a **newline**,
which is a special character that causes a line break. That’s why the
user’s input appears below the prompt.

提示的最后这一段\ ``\n``\ 表示一个\ **新行（newline）**\ ，
它是一个特别的字符，会造成换行。
这也是用户的输入出现在提示符下面的原因。

If you expect the user to type an integer, you can try to convert the
return value to int:

如果你期望用户键入一个整数，那么你可以试着将返回值转化为int：

::

    >>> prompt = 'What...is the airspeed velocity of an unladen swallow?\n'
    >>> speed = input(prompt)
    What...is the airspeed velocity of an unladen swallow?
    42
    >>> int(speed)
    42

But if the user types something other than a string of digits, you get
an error:

但是，如果用户键入不是数字构成的字符串，会获得一个错误：

::

    >>> speed = input(prompt)
    What...is the airspeed velocity of an unladen swallow?
    What do you mean, an African or a European swallow?
    >>> int(speed)
    ValueError: invalid literal for int() with base 10

We will see how to handle this kind of error later.

我们后面将会看到处理这类错误的方法。

Debugging　调试
------------------

When a syntax or runtime error occurs, the error message contains a lot
of information, but it can be overwhelming. The most useful parts are
usually:

当出现语法错误和运行时错误的时候， Python　提供的错误信息包含了很多的信息，但是这些错误信息可能太多了。通常，最有用的部分是：

-  What kind of error it was, and

-  错误是哪类，以及

-  Where it occurred.

-  它发生在哪儿。

Syntax errors are usually easy to find, but there are a few gotchas.
Whitespace errors can be tricky because spaces and tabs are invisible
and we are used to ignoring them.

语法错误通常很容易被找到，但也有一些需要想想。
空白分隔符错误很棘手，因为空格和制表符是不可见的而且我们习惯于忽略它们。

::

    >>> x = 5
    >>>  y = 6
      File "<stdin>", line 1
        y = 6
        ^
    IndentationError: unexpected indent

In this example, the problem is that the second line is indented by one
space. But the error message points to y, which is misleading. In
general, error messages indicate where the problem was discovered, but
the actual error might be earlier in the code, sometimes on a previous
line.

在这个例子中，问题在于第二行缩进了一个空格。
但是错误信息指向y，这是个误导。 通常，错误信息指向发现错误的地方，
但是实际的错误可能发生在代码中的更早前的地方， 有时在前一行。

The same is true of runtime errors. Suppose you are trying to compute a
signal-to-noise ratio in decibels. The formula is
:math:`SNR_{db} = 10 \log_{10} (P_{signal} / P_{noise})`. In Python, you
might write something like this:

运行时错误也同样。假设你正试图给计算机键入一个分贝信噪比。
公式是\ :math:`SNR_{db} = 10 \log_{10} (P_{signal} / P_{noise})`\ 。
在Python中，你可能如此写：

::

    import math
    signal_power = 9
    noise_power = 10
    ratio = signal_power // noise_power
    decibels = 10 * math.log10(ratio)
    print(decibels)

When you run this program, you get an exception:

但是，当你运行它的时候， 你将获得一个错误信息。

::

    Traceback (most recent call last):
      File "snr.py", line 5, in ?
        decibels = 10 * math.log10(ratio)
    ValueError: math domain error

The error message indicates line 5, but there is nothing wrong with that
line. To find the real error, it might be useful to print the value of
ratio, which turns out to be 0. The problem is in line 4, which uses
floor division instead of floating-point division.

该错误信息指向第5行，但是那一行没什么错误。
为了找到真正的错误，打印ratio也许会有用，它实际上是0。
问题是在第4行，使用了地板除而不是浮点数除法。

You should take the time to read error messages carefully, but don’t
assume that everything they say is correct.

你应该花些时间仔细阅读错误信息，但是不要轻易地认为错误信息的提示都是准确的。

Glossary　词汇表
----------------

floor division:
    An operator, denoted //, that divides two numbers and rounds down
    (toward zero) to an integer.
    
地板除:
    一个操作符,用 // 表示，表示对两个数做除法同时向0取整

modulus operator:
    An operator, denoted with a percent sign (%), that works on integers
    and returns the remainder when one number is divided by another.
    
求余运算符:
    一个运算符,用百分号 % 表示，返回两个整除相除的余数

boolean expression:
    An expression whose value is either True or False.

布尔表达式:
    一段代码声明，只有 True（真）和 False（假）两个取值。

relational operator:
    One of the operators that compares its operands: ==, !=, >, <, >=,
    and <=.
    
关系运算符:
    关系运算符确定下列关系： 等于(==), 不等于(!=)，大于(>)，小于(<)，大于等于(>=)，小于等于(<=)
    

logical operator:
    One of the operators that combines boolean expressions: and, or, and
    not.

逻辑运算符:
    逻辑运算符链接布尔表达式,包括 : 与(and),或(or),与非(and or,译者注，类似 C 语言中的 \ ``bool ? a : b``\ 表达式)

conditional statement:
    A statement that controls the flow of execution depending on some
    condition.

条件语句:
   一段代码语句，根据条件决定程序的执行流

condition:
    The boolean expression in a conditional statement that determines
    which branch runs.

条件:
    决定那个分支会被执行的布尔表达式

compound statement:
    A statement that consists of a header and a body. The header ends
    with a colon (:). The body is indented relative to the header.

合成语句:
    由头和主体组成的代码语句。头以 : 结尾，主体依照头相应决定决定

branch:
    One of the alternative sequences of statements in a conditional
    statement.

分支:
    条件语句中的一个部分

chained conditional:
    A conditional statement with a series of alternative branches.

链式条件:
    由一系列替代分支组成的条件

nested conditional:
    A conditional statement that appears in one of the branches of
    another conditional statement.

嵌套条件:
    出现在其他条件语句中的条件语句

return statement:
    A statement that causes a function to end immediately and return to
    the caller.

返回语句：
　　　 结束函数执行并且将结果返回给调用者的语句

recursion:
    The process of calling the function that is currently executing.

递归:
    调用正在执行的函数本身的过程

base case:
    A conditional branch in a recursive function that does not make a
    recursive call.

基本条件:
    在递归函数中，不进行递归调用的条件分支
    
infinite recursion:
    A recursion that doesn’t have a base case, or never reaches it.
    Eventually, an infinite recursion causes a runtime error.

无限递归:
    没有基本条件或者不能执行基本条件的递归函数。最终无限递归会导致执行时错误。

Exercises　练习题
------------------

习题 5-1
^^^^^^^^^^

The time module provides a function, also named time, that returns the
current Greenwich Mean Time in “the epoch”, which is an arbitrary time
used as a reference point. On UNIX systems, the epoch is 1 January 1970.

time模块提供了一个可以返回当前格林威治时间的函数，名字也是time。但是这个函数使用纪元(the epoch)以来的秒数为单位，
纪元是一个明确定义的时间参考点，在 Unix 系统中，纪元是1970年1月1号。

::

    >>> import time
    >>> time.time()
    1437746094.5735958

Write a script that reads the current time and converts it to a time of
day in hours, minutes, and seconds, plus the number of days since the
epoch.

请写一个脚本读取当前时间并且转换为用时分秒已经自从纪元以来的天数表示的日期。

习题 5-2
^^^^^^^^^^

Fermat’s Last Theorem says that there are no positive integers
:math:`a`, :math:`b`, and :math:`c` such that

费马最后定理的内容是，没有任何整数\ :math:`a`\ ，\ :math:`b`\ ，\ :math:`c`\ 能够使

.. math:: a^n + b^n = c^n

for any values of :math:`n` greater than 2.

对于任何大于2的\ :math:`n`\ 成立。

#. Write a function named ``check_fermat`` that takes four parameters—a,
   b, c and n—and checks to see if Fermat’s theorem holds. If :math:`n`
   is greater than 2 and
   
   写一个名为\ ``check_fermat``\ 的函数，其接受四个形参—a，b，c以及n
   —然后检查费马最后定理是否成立。 如果\ :math:`n`\ 大于2且等式

   .. math:: a^n + b^n = c^n

   the program should print, “Holy smokes, Fermat was wrong!” Otherwise
   the program should print, “No, that doesn’t work.”
   
   成立，程序会输出“Holy smokes, Fermat was wrong!”。 否则程序输出“No,
   that doesn’t work.”。

#. Write a function that prompts the user to input values for a, b, c
   and n, converts them to integers, and uses ``check_fermat`` to check
   whether they violate Fermat’s theorem.
   
   写一个函数提示用户输入a，b，c以及n的值，将它们转换成整数，
   然后使用\ ``check_fermat``\ 检查他们是否会违反费马最后定理。
   
习题 5-3
^^^^^^^^^^

If you are given three sticks, you may or may not be able to arrange
them in a triangle. For example, if one of the sticks is 12 inches long
and the other two are one inch long, it is clear that you will not be
able to get the short sticks to meet in the middle. For any three
lengths, there is a simple test to see if it is possible to form a
triangle:

如果你有三根棍子，你有可能将它们组成三角形，也可能不行。
比如，如果一根棍子是12英寸长，其它两根都是1英寸长，显然
你不可能让两根短的在中间接合。对于任意三个长度，有一个简单的测试
它们能否组成三角形的办法：

    If any of the three lengths is greater than the sum of the other
    two, then you cannot form a triangle. Otherwise, you can. (If the
    sum of two lengths equals the third, they form what is called a
    “degenerate” triangle.)

    如果三个长度中的任意一个超过了其它二者之和，你就不能组成三角形。否则你就可以
    组成三角形。（如果两个长度之和等于第三个，它们就组成所谓“退化的”三角形。）

#. Write a function named ``is_triangle`` that takes three integers as
   arguments, and that prints either “Yes” or “No,” depending on whether
   you can or cannot form a triangle from sticks with the given lengths.

   写一个名为\ ``is_triangle``\ 的函数，其接受三个整数作为形参，
   能够根据给定的三个长度的棍子能否构成三角形来打印“Yes”或“No”。

#. Write a function that prompts the user to input three stick lengths,
   converts them to integers, and uses ``is_triangle`` to check whether
   sticks with the given lengths can form a triangle.

   写一个函数，提示用户输入三根棍子的长度，将它们转换成整数，然后使用
   ``is_triangle``\ 检查给定长度的棍子能否构成三角形。

习题 5-4
^^^^^^^^^^

What is the output of the following program? Draw a stack diagram that
shows the state of the program when it prints the result.

下面程序的输出是什么？画出展示程序每次打印输出时候的栈图。

::

    def recurse(n, s):
        if n == 0:
            print(s)
        else:
            recurse(n-1, n+s)

    recurse(3, 0)

#. What would happen if you called this function like this: recurse(-1,
   0)?
   
   如果你使用 recurse(-1,0) 这样的方式调用函数会有什么结果？

#. Write a docstring that explains everything someone would need to know
   in order to use this function (and nothing else).
   
   请写一个说明注释来解释需要使用这个函数的人需要知道全部知识(不要添加其他信息)

习题 5-５
^^^^^^^^^^

The following exercises use TurtleWorld from Chapter [turtlechap]:

后面的习题要用到第[turtlechap]章中的TurtleWorld：

Read the following function and see if you can figure out what it does.
Then run it (see the examples in Chapter [turtlechap]).

阅读如下的函数，看看你能否看懂它是做什么的。然后运行它（见第[turtlechap]章的例子）。

::

    def draw(t, length, n):
        if n == 0:
            return
        angle = 50
        fd(t, length*n)
        lt(t, angle)
        draw(t, length, n-1)
        rt(t, 2*angle)
        draw(t, length, n-1)
        lt(t, angle)
        bk(t, length*n)

习题 5-６
^^^^^^^^^^

.. figure:: figs/koch.png
   :alt: A Koch curve.

   A Koch curve.
   
   Koch曲线。

The Koch curve is a fractal that looks something like Figure [fig.koch].
To draw a Koch curve with length :math:`x`, all you have to do is

Koch曲线是一个看起来类似图[fig.koch]的分形。想要画一个长度为\ :math:`x`\ 的Koch曲线，
你只需要

#. Draw a Koch curve with length :math:`x/3`.

   画一个长度为\ :math:`x/3`\ 的Koch曲线。

#. Turn left 60 degrees.

   左转60度。

#. Draw a Koch curve with length :math:`x/3`.

   画一个长度为\ :math:`x/3`\ 的Koch曲线。

#. Turn right 120 degrees.

   右转60度。

#. Draw a Koch curve with length :math:`x/3`.

   画一个长度为\ :math:`x/3`\ 的Koch曲线。

#. Turn left 60 degrees.

   左转60度。

#. Draw a Koch curve with length :math:`x/3`.

   画一个长度为\ :math:`x/3`\ 的Koch曲线。

The exception is if :math:`x` is less than 3: in that case, you can just
draw a straight line with length :math:`x`.

例外情况是\ :math:`x`\ 小于3的情形：此时，你可以仅仅
画一道长度为\ :math:`x`\ 的直线。

#. Write a function called koch that takes a turtle and a length as
   parameters, and that uses the turtle to draw a Koch curve with the
   given length.

   写一个名为koch的函数，接受一个海龟和一个长度作为形参，然后
   使用海龟画一条给定长度的Koch曲线。

#. Write a function called snowflake that draws three Koch curves to
   make the outline of a snowflake.

   写一个名为snowflake的函数，其能够画出三条Koch曲线，以构成雪花的轮廓。

   Solution: http://thinkpython.com/code/koch.py.

   解答在：\ http://thinkpython.com/code/koch.py\ 。

#. The Koch curve can be generalized in several ways. See
   http://en.wikipedia.org/wiki/Koch_snowflake for examples and
   implement your favorite.

   Koch曲线能够以多种方式被泛化，
   见\ http://en.wikipedia.org/wiki/Koch_snowflake\ 的例子，并实现你最喜欢的一个。
