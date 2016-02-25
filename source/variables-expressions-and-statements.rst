第二章：变量、表达式和语句
=====================================

One of the most powerful features of a programming language is the
ability to manipulate **variables**. A variable is a name that refers to
a value.

编程语言最强大的特性之一，是操作\ **变量**\ 的能力。变量是指向某个值的名称。

赋值语句
---------------------

An **assignment statement** creates a new variable and gives it a value:

\ **赋值语句（assignment statement）**\ 会新建变量，并进行赋值。

::

    >>> message = 'And now for something completely different'
    >>> n = 17
    >>> pi = 3.141592653589793

This example makes three assignments. The first assigns a string to a
new variable named message; the second gives the integer 17 to n; the
third assigns the (approximate) value of :math:`\pi` to pi.

这个例子进行了三次赋值。 第一次将一个字符串赋给一个叫message的新变量；
第二次将整型数17赋给n； 第三次将\ :math:`\pi`\ 的（近似）值赋给pi。

A common way to represent variables on paper is to write the name with
an arrow pointing to its value. This kind of figure is called a **state
diagram** because it shows what state each of the variables is in (think
of it as the variable’s state of mind). Figure [fig.state2] shows the
result of the previous example.

在纸上表示变量的一个常见方法，是写下变量名，然后用箭头指向变量的值。
这种图被称为\ **状态图（state
diagram）**\ ，因为它展示了每个变量所处的状态（可以把其看成是变量的心理状态）。
下图展示了前面例子的结果。

.. figure:: figs/state2.png
   :alt: 状态图。

   状态图。

变量名
--------------

Programmers generally choose names for their variables that are
meaningful—they document what the variable is used for.

程序员通常为变量选择有意义的名字—它们说明了该变量的用途。

Variable names can be as long as you like. They can contain both letters
and numbers, but they can’t begin with a number. It is legal to use
uppercase letters, but it is conventional to use only lower case for
variables names.

变量名可以任意长。它们可以包括字母和数字，但是不能用数字开头。
使用大写字母是合法的，但是根据惯例，变量名只使用小写字母。

The underscore character, ``_``, can appear in a name. It is often used
in names with multiple words, such as ``your_name`` or
``airspeed_of_unladen_swallow``.

下划线字符\ ``_``\ 可以出现在变量名中。
它经常用于有多个单词的变量名，例如\ ``my_name``\ 或者\ ``airspeed_of_unladen_swallow``\ 。

If you give a variable an illegal name, you get a syntax error:

如果你给了变量一个非法的名称，解释器将抛出一个语法错误：

::

    >>> 76trombones = 'big parade'
    SyntaxError: invalid syntax
    >>> more@ = 1000000
    SyntaxError: invalid syntax
    >>> class = 'Advanced Theoretical Zymurgy'
    SyntaxError: invalid syntax

76trombones is illegal because it begins with a number. more@ is illegal
because it contains an illegal character, @. But what’s wrong with
class?

76trombones是非法的，因为它以数字开头。more@是非法的，因为它包含了一个非法字符@。 但是，class错在哪儿了呢?

It turns out that class is one of Python’s **keywords**. The interpreter
uses keywords to recognize the structure of the program, and they cannot
be used as variable names.

原来，class是Python的\ **关键字（keywords）**\ 之一。
解释器使用关键字识别程序的结构，它们不能被用作变量名。

Python 3 has these keywords:

Python 3有以下关键词：

::

    False      class      finally    is         return
    None       continue   for        lambda     try
    True       def        from       nonlocal   while
    and        del        global     not        with
    as         elif       if         or         yield
    assert     else       import     pass
    break      except     in         raise

You don’t have to memorize this list. In most development environments,
keywords are displayed in a different color; if you try to use one as a
variable name, you’ll know.

你没有必要记住上面的关键词。在大部分的开发环境中，会用不同的颜色区别显示关键词；如果你不小心使用关键词作为变量名，你肯定会发现的。

-----------

表达式和语句
--------------------------

An **expression** is a combination of values, variables, and operators.
A value all by itself is considered an expression, and so is a variable,
so the following are all legal expressions:

\ **表达式（expression）**\ 是值、变量和运算符的组合。
值自身被认为是一个表达式，变量也是，因此下面都是合法的表达式：

::

    >>> 42
    42
    >>> n
    17
    >>> n + 25
    42

When you type an expression at the prompt, the interpreter **evaluates**
it, which means that it finds the value of the expression. In this
example, n has the value 17 and n + 25 has the value 42.

当你在提示符中输入表达式后，解释器会\ ** 计算（evaluate）**\ 该表达式，即求它的值。在上面的例子中，n的值是17，n + 25的值是42。

A **statement** is a unit of code that has an effect, like creating a
variable or displaying a value.

\ **语句（statement）**\ 是一个会产生影响的代码单元，例如新建一个变量或显示某个值。

::

    >>> n = 17
    >>> print(n)

The first line is an assignment statement that gives a value to n. The
second line is a print statement that displays the value of n.

第一行是一个赋值语句，将某个值赋给了n。第二行是一个打印语句，在屏幕上显示n的值。

When you type a statement, the interpreter **executes** it, which means
that it does whatever the statement says. In general, statements don’t
have values.

当你输入一个语句后，解释器会\ **执行（execute）**\ 这个语句，即按照语句的指令完成操作。一般来说，语句是没有值的。

-------

脚本模式
-----------

So far we have run Python in **interactive mode**, which means that you
interact directly with the interpreter. Interactive mode is a good way
to get started, but if you are working with more than a few lines of
code, it can be clumsy.

到目前为止，我们都是在\ **交互模式（interactive mode）**\ 下运行Python，即直接与解释器进行交互。交互模式对学习入门很有帮助，但是如果你需要编写很多行代码，使用交互模式就不太方便了。

The alternative is to save code in a file called a **script** and then
run the interpreter in **script mode** to execute the script. By
convention, Python scripts have names that end with .py.

另一种方法是将代码保存到一个被称为\ **脚本（script）**\ 的文件里，然后以\ **脚本模式（script mode）**\ 运行解释器并执行脚本。按照约定，Python脚本文件名的后缀是.py。

If you know how to create and run a script on your computer, you are
ready to go. Otherwise I recommend using PythonAnywhere again. I have
posted instructions for running in script mode at
http://tinyurl.com/thinkpython2e.

如果你知道如何在本地电脑新建并运行脚本，那你可以开始编码了。否则的话，我再次建议使用PythonAnywhere。我在 http://tinyurl.com/thinkpython2e 上贴出了如何以脚本模式运行解释器的指南。

Because Python provides both modes, you can test bits of code in
interactive mode before you put them in a script. But there are
differences between interactive mode and script mode that can be
confusing.

由于Python支持两种编码模式，在将代码写入脚本之前，你可以在交互模式下对代码片段进行测试。不过，交互模式和脚本模式之间存在一些差异，可能会让你感到疑惑。

For example, if you are using Python as a calculator, you might type

举个例子，如果你把Python当计算器使用，你可能会输入下面这样的代码：

::

    >>> miles = 26.2
    >>> miles * 1.61
    42.182

The first line assigns a value to miles, but it has no visible effect.
The second line is an expression, so the interpreter evaluates it and
displays the result. It turns out that a marathon is about 42
kilometers.

第一行将一个值赋给miles，但是并没有产生可见的效果。
第二行是一个表达式，因此解释器计算它并将结果显示出来。
结果告诉我们，一段马拉松大概是42公里。

But if you type the same code into a script and run it, you get no
output at all. In script mode an expression, all by itself, has no
visible effect. Python actually evaluates the expression, but it doesn’t
display the value unless you tell it to:

但是如果你将相同的代码键入一个脚本并且运行它，你得不到任何输出。
在脚本模式下，表达式自身不会产生可见的效果。虽然Python实际上计算了表达式，但是如果你不告诉它要显示结果，它是不会那么做的。

::

    miles = 26.2
    print(miles * 1.61)

This behavior can be confusing at first.

此行为开始可能有些令人费解。

A script usually contains a sequence of statements. If there is more
than one statement, the results appear one at a time as the statements
execute.

一个脚本通常包括一系列语句。
如果有多于一条的语句，那么随着语句逐个执行，解释器会逐一显示计算结果。

For example, the script

例如，一下脚本

::

    print(1)
    x = 2
    print(x)

产生的输出结果是

::

    1
    2

The assignment statement produces no output.

赋值语句不产生输出。

To check your understanding, type the following statements in the Python
interpreter and see what they do:

在Python解释器中键入以下的语句，看看他们的结果是否符合你的理解：

::

    5
    x = 5
    x + 1

Now put the same statements in a script and run it. What is the output?
Modify the script by transforming each expression into a print statement
and then run it again.

现在将同样的语句写入一个脚本中并执行它。输出结果是什么？
修改脚本，将每个表达式变成打印语句，再次运行它。

-------

运算的顺序
-------------------

When an expression contains more than one operator, the order of
evaluation depends on the **order of operations**. For mathematical
operators, Python follows mathematical convention. The acronym
**PEMDAS** is a useful way to remember the rules:

当一个表达式中有多于一个运算符时，计算的顺序由\ **优先级规则（rules of
precedence）**\ 决定。 对于算数运算符，Python遵循数学里的惯例。 缩写\ **PEMDAS**\ 有助于记住这一规则：

-  **P**\ arentheses have the highest precedence and can be used to
   force an expression to evaluate in the order you want. Since
   expressions in parentheses are evaluated first, 2 \* (3-1) is 4, and
   (1+1)\*\*(5-2) is 8. You can also use parentheses to make an
   expression easier to read, as in (minute \* 100) / 60, even if it
   doesn’t change the result.

-  括号（\ **P**\ arentheses）具有最高的优先级，并且可以被用于强制表达式按你希望的顺序计算。
   既然在括号中的表达式首先被计算，那么2 \*
   (3-1)的结果是4，(1+1)\*\*(5-2)的结果是8。
   你也可以用括号提高表达式的可读性，如写成(minute \* 100) /
   60，即使这样并不改变运算的结果。

-  **E**\ xponentiation has the next highest precedence, so 1 + 2\*\*3
   is 9, not 27, and 2 \* 3\*\*2 is 18, not 36.

-  指数运算（\ **E**\ xponentiation）具有次高的优先级，因此1 + 2\*\*3的结果是9而非27，
   2 \* 3\*\*2的结果是18而非36。

-  **M**\ ultiplication and **D**\ ivision have higher precedence than
   **A**\ ddition and **S**\ ubtraction. So 2\*3-1 is 5, not 4, and
   6+4/2 is 8, not 5.

-  乘法（\ **M**\ ultiplication）和除法（\ **D**\ ivision）有相同的优先级，
   比加法（\ **A**\ ddition）和减法（\ **S**\ ubtraction）高，加法和减法也具有相同的优先级。
   因此2\*3-1是5而非4，6+4/2是8而非5。

-  Operators with the same precedence are evaluated from left to right
   (except exponentiation). So in the expression degrees / 2 \* pi, the
   division happens first and the result is multiplied by pi. To divide
   by :math:`2 \pi`, you can use parentheses or write degrees / 2 / pi.

-  具有相同优先级的运算符按照从左到右的顺序进行计算（除了指数运算）。
   因此表达式degrees / 2 \* pi中，除法先运算，然后结果被乘以pi。
   为了被\ :math:`2 \pi`\ 除，你可以使用括号，或者写成degrees / 2 / pi。
   
I don’t work very hard to remember the precedence of operators. If I
can’t tell by looking at the expression, I use parentheses to make it
obvious.

我不会费力去记住这些运算符的优先级规则。如果看完表达式后分不出优先级，我会使用括号使计算顺序变得更明显。

-------

字符串运算
-----------------

In general, you can’t perform mathematical operations on strings, even
if the strings look like numbers, so the following are illegal:

一般来讲，你不能对字符串执行数学运算，即使字符串看起来很像数字，
因此下面这些表达式是非法的：

::

    '2'-'1'    'eggs'/'easy'    'third'*'a charm'

But there are two exceptions, + and .

但有两个例外，+ 和 \*。

The + operator performs **string concatenation**, which means it joins
the strings by linking them end-to-end. For example:

+ 运算符可用于 **字符串连接**，也就是将字符串首尾相连起来。例如：

::

    >>> first = 'throat'
    >>> second = 'warbler'
    >>> first + second
    throatwarbler

The operator also works on strings; it performs repetition. For example,
``'Spam'*3`` is ``'SpamSpamSpam'``. If one of the values is a string,
the other has to be an integer.

\* 运算符也可应用于字符串；它执行重复运算。
例如，\ ``'Spam'*3``\ 的结果是\ ``'SpamSpamSpam'``\ 。
如果其中一个运算数是字符串，则另外一个必须是整型数。

This use of + and makes sense by analogy with addition and
multiplication. Just as 4\*3 is equivalent to 4+4+4, we expect
``'Spam'*3`` to be the same as ``'Spam'+'Spam'+'Spam'``, and it is. On
the other hand, there is a significant way in which string concatenation
and repetition are different from integer addition and multiplication.
Can you think of a property that addition has that string concatenation
does not?

+和\*的使用类比加法和乘法也讲得通。 就像由于4\*3与4+4+4等价，
我们就猜测\ ``'Spam'*3``\ 和\ ``'Spam'+'Spam'+'Spam'``\ 等价，而事实上的确如此。
另一方面，字符串连接和重复与整数的加法和乘法截然不同。
你能想出来一个加法具有而字符串连接不具有的性质么？

-------

注释
--------

As programs get bigger and more complicated, they get more difficult to
read. Formal languages are dense, and it is often difficult to look at a
piece of code and figure out what it is doing, or why.

随着程序变得越来越大，越来越复杂，它们变得越来越难读。
形式语言是稠密的，读一段代码并说出其做什么或者为什么这样通常很难。

For this reason, it is a good idea to add notes to your programs to
explain in natural language what the program is doing. These notes are
called **comments**, and they start with the ``#`` symbol:

因此，在你的程序中用自然语言做笔记，解释程序做什么通常是比较好的办法。
这些标注被称为\ **注释（comments）**\ ，以\ ``#``\ 符号开始。

::

    # compute the percentage of the hour that has elapsed
    percentage = (minute * 100) / 60

In this case, the comment appears on a line by itself. You can also put
comments at the end of a line:

此例中，注释独立一行。你也可以将注释放在行尾：

::

    percentage = (minute * 100) / 60     # percentage of an hour

Everything from the # to the end of the line is ignored—it has no effect
on the execution of the program.

从#开始到行尾的所有东西都被忽略了—其对程序执行没有影响。

Comments are most useful when they document non-obvious features of the
code. It is reasonable to assume that the reader can figure out *what*
the code does; it is more useful to explain *why*.

在注释中记录代码不明显的特征，是最有帮助的。
假设读者能够读懂代码做了\ *什么*\ 是合理的；
但是解释代码\ *为什么*\ 这么做则更有用。

This comment is redundant with the code and useless:

下面这个注释只是重复了代码，没有什么用：

::

    v = 5     # 将5赋值给v

This comment contains useful information that is not in the code:

下面的注释包括了代码中没有的有用信息：

::

    v = 5     # 加速度，单位：米/秒

Good variable names can reduce the need for comments, but long names can
make complex expressions hard to read, so there is a tradeoff.

好的变量名能够减少对注释的需求，但是长变量名使得表达式很难读，
因此这里有个平衡问题。

----

调试
---------

Three kinds of errors can occur in a program: syntax errors, runtime
errors, and semantic errors. It is useful to distinguish between them in
order to track them down more quickly.

程序中会出现下面三种错误：语法错误（syntax error）、运行时错误(runtime error)和语义错误(semantic error)。我们如果能够分辨出三者区别，有助于在快速追踪这些错误。

Syntax error:
    “Syntax” refers to the structure of a program and the rules about
    that structure. For example, parentheses have to come in matching
    pairs, so (1 + 2) is legal, but 8) is a **syntax error**.

    If there is a syntax error anywhere in your program, Python displays
    an error message and quits, and you will not be able to run the
    program. During the first few weeks of your programming career, you
    might spend a lot of time tracking down syntax errors. As you gain
    experience, you will make fewer errors and find them faster.

语法错误：
    语法指的是程序的结构及其背后的规则。例如，括号必须要成对出现，所以(1 + 2)是合法的，但是8)则是一个 **语法错误**。

    如果你的程序中存在一个语法错误，Python会显示一条错误信息，然后退出运行。你无法顺利运行程序。在你编程生涯的头几周里，你可能会花大量时间追踪语法错误。随着你的经验不断积累，犯的语法错误会越来越少，发现错误的速度也会更快。

Runtime error:
    The second type of error is a runtime error, so called because the
    error does not appear until after the program has started running.
    These errors are also called **exceptions** because they usually
    indicate that something exceptional (and bad) has happened.

    Runtime errors are rare in the simple programs you will see in the
    first few chapters, so it might be a while before you encounter one.

运行时错误：
    第二种错误类型是运行时错误，这么称呼是因为这类错误只有在程序开始运行后才会出现。这类错误也被称为 **异常（exception）**，因为它们通常说明发生了某些特别的（而且不好的）事情。

    在前几章提供的简单程序中，你很少会碰到运行时错误，所以你可能需要一段时间才会接触到这种错误。

Semantic error:
    The third type of error is “semantic”, which means related to
    meaning. If there is a semantic error in your program, it will run
    without generating error messages, but it will not do the right
    thing. It will do something else. Specifically, it will do what you
    told it to do.

    Identifying semantic errors can be tricky because it requires you to
    work backward by looking at the output of the program and trying to
    figure out what it is doing.

    第三类错误是“语义”错误，即与程序的意思的有关。如果你的程序中有语义错误，程序在运行时不会产生错误信息，但是不会返回正确的结果。它会返回另外的结果。严格来说，它是按照你的指令在运行。

    识别语义错误可能是棘手的，因为这需要你反过来思考，通过观察程序的输出来搞清楚它在做什么。

----

词汇表
--------

变量：
    变量是指向某个值的名称。

variable:
    A name that refers to a value.

赋值语句：
    将某个值赋给变量的语句。

assignment:
    A statement that assigns a value to a variable.

状态图：
    变量及其所指的值的图形表示。

state diagram:
    A graphical representation of a set of variables and the values they
    refer to.

关键词：
    关键词是用于解析程序的；你不能将像if、def和while这样的关键词作为变量名。

keyword:
    A reserved word that is used to parse a program; you cannot use
    keywords like if, def, and while as variable names.

运算数（operand）：
    运算符所操作的值之一。

operand:
    One of the values on which an operator operates.

表达式：
    变量、运算符和值的组合，代表一个单一的结果。

expression:
    A combination of variables, operators, and values that represents a
    single result.

计算（evaluate）：
    通过执行运算以简化表达式，从而得出一个单一的值。

evaluate:
    To simplify an expression by performing the operations in order to
    yield a single value.

语句：
    代表一个命令或行为的一段代码。目前为止我们接触的语句有赋值语句和打印语句。

statement:
    A section of code that represents a command or action. So far, the
    statements we have seen are assignments and print statements.

执行：
    运行一个语句，并按照语句的指令操作。

execute:
    To run a statement and do what it says.

交互式模式：
    通过在提示符中输入代码，使用Python解释器的一种方式。

interactive mode:
    A way of using the Python interpreter by typing code at the prompt.

脚本模式：
    使用Python解释器从脚本中读取代码，并运行脚本的方式。

script mode:
    A way of using the Python interpreter to read code from a script and
    run it.

脚本：
    保存在文件中的程序。

script:
    A program stored in a file.

运算顺序：
    有关多个运算符和运算数时计算顺序的规则。

order of operations:
    Rules governing the order in which expressions involving multiple
    operators and operands are evaluated.

连接：
    将两个运算数首尾相连。

concatenate:
    To join two operands end-to-end.

注释：
    程序中提供给其他程序员（任何阅读源代码的人）阅读的信息，对程序的执行没有影响。

comment:
    Information in a program that is meant for other programmers (or
    anyone reading the source code) and has no effect on the execution
    of the program.

语法错误：
    使得程序无法进行解析（因此无法进行解释）的错误。

syntax error:
    An error in a program that makes it impossible to parse (and
    therefore impossible to interpret).

异常：
    只有在程序运行时才发现的错误。

exception:
    An error that is detected while the program is running.

语义：
    程序的意思。

semantics:
    The meaning of a program.

语义错误：
    使得程序偏离程序员原本目的的错误。

semantic error:
    An error in a program that makes it do something other than what the
    programmer intended.

----

练习题
---------

Repeating my advice from the previous chapter, whenever you learn a new
feature, you should try it out in interactive mode and make errors on
purpose to see what goes wrong.

-  We’ve seen that n = 42 is legal. What about 42 = n?

-  How about x = y = 1?

-  In some languages every statement ends with a semi-colon, ;. What
   happens if you put a semi-colon at the end of a Python statement?

-  What if you put a period at the end of a statement?

-  In math notation you can multiply :math:`x` and :math:`y` like this:
   :math:`x y`. What happens if you try that in Python?

Practice using the Python interpreter as a calculator:

#. The volume of a sphere with radius :math:`r` is
   :math:`\frac{4}{3} \pi r^3`. What is the volume of a sphere with
   radius 5?

#. Suppose the cover price of a book is $24.95, but bookstores get a 40%
   discount. Shipping costs $3 for the first copy and 75 cents for each
   additional copy. What is the total wholesale cost for 60 copies?

#. If I leave my house at 6:52 am and run 1 mile at an easy pace (8:15
   per mile), then 3 miles at tempo (7:12 per mile) and 1 mile at easy
   pace again, what time do I get home for breakfast?