函数
=========

In the context of programming, a **function** is a named sequence of
statements that performs a computation. When you define a function, you
specify the name and the sequence of statements. Later, you can “call”
the function by name.

在编程的语境下，\ **函数（function）**\ 指的是一个有命名的、执行某个计算的语句序列（sequence of statements）。
当你定义一个函数的时候，你需要指定函数的名字和语句序列。
然后，你可以通过这个名字“调用（call）”该函数。

-----

函数调用
--------------

We have already seen one example of a **function call**:

我们已经见过一个\ **函数调用（function call）**\ 的例子。

::

    >>> type(42)
    <class 'int'>

The name of the function is type. The expression in parentheses is
called the **argument** of the function. The result, for this function,
is the type of the argument.

其中，函数的名字是 ``type``。括号中的表达式被称为这个函数的 **实参（argument）**。这个函数执行的结果，就是实参的类型。

It is common to say that a function “takes” an argument and “returns” a
result. The result is also called the **return value**.

人们常说函数“接受”实参，并且“返回”一个结果。
该结果也被称为\ **返回值（return value）**

Python provides functions that convert values from one type to another.
The int function takes any value and converts it to an integer, if it
can, or complains otherwise:

Python提供内建函数，能够将值从一种类型转换为另一种类型。
函数 ``int`` 接受任意值，并在其能做到的情况下，将该任意值转换成一个整数，
否则会报错：

::

    >>> int('32')
    32
    >>> int('Hello')
    ValueError: invalid literal for int(): Hello

int can convert floating-point values to integers, but it doesn’t round
off; it chops off the fraction part:

``int``能将浮点数转换为整数，但是它并不进行舍入，而是截掉了小数部分：

::

    >>> int(3.99999)
    3
    >>> int(-2.3)
    -2

float converts integers and strings to floating-point numbers:

``float``将整数或者字符串转换为浮点数：

::

    >>> float(32)
    32.0
    >>> float('3.14159')
    3.14159

Finally, str converts its argument to a string:

最后，``str``将其实参转换成字符串。

::

    >>> str(32)
    '32'
    >>> str(3.14159)
    '3.14159'

-------

数学函数
--------------

Python has a math module that provides most of the familiar mathematical
functions. A **module** is a file that contains a collection of related
functions.


Python中有一个数学模块（``math``），提供了大部分常用的数学函数。
**模块（module）**\ 是一个包含一批相关函数的文件。

Before we can use the functions in a module, we have to import it with
an **import statement**:

在使用模块之前，我们需要通过 **导入语句（import statement）**导入该模块：、

::

    >>> import math

This statement creates a **module object** named math. If you display
the module object, you get some information about it:


这条语句生成一个名为math的\ **模块对象（module object）**\ 。
如果你打印这个模块对象，你将获得关于它的一些信息：

::

    >>> math
    <module 'math' (built-in)>

The module object contains the functions and variables defined in the
module. To access one of the functions, you have to specify the name of
the module and the name of the function, separated by a dot (also known
as a period). This format is called **dot notation**.

该模块对象包括定义在模块内的函数和变量。
想要访问其中的一个函数，你必须指出该模块的名字以及函数名，
并以点号（也被叫做句号）分割。 这种格式被称作\ **点标记法（dot
notation）**\ 。

::

    >>> ratio = signal_power / noise_power
    >>> decibels = 10 * math.log10(ratio)

    >>> radians = 0.7
    >>> height = math.sin(radians)

The first example uses ``math.log10`` to compute a signal-to-noise ratio
in decibels (assuming that ``signal_power`` and ``noise_power`` are
defined). The math module also provides log, which computes logarithms
base e.

第一个例子使用\ ``math.log10``\ 计算分贝信噪比（假设\ ``signal_power``\ 和\ ``noise_power``\ 已经被定义了）。
math模块也提供了log函数，计算以e为底的对数。

The second example finds the sine of radians. The name of the variable
is a hint that sin and the other trigonometric functions (cos, tan,
etc.) take arguments in radians. To convert from degrees to radians,
divide by 180 and multiply by :math:`\pi`:

第二个例子计算radians的正弦值。
变量名暗示sin函数以及其它三角函数（cos、tan等）接受弧度（radians）实参。
度转换为弧度，将度数除以360，并乘以\ :math:`2 \pi`\ ：

::

    >>> degrees = 45
    >>> radians = degrees / 180.0 * math.pi
    >>> math.sin(radians)
    0.707106781187

The expression math.pi gets the variable pi from the math module. Its
value is a floating-point approximation of :math:`\pi`, accurate to
about 15 digits.

表达式math.pi从math模块中获得变量pi。
该变量的值是\ :math:`\pi`\ 的一个浮点数近似值，精确到大约15位数。

If you know trigonometry, you can check the previous result by comparing
it to the square root of two divided by two:

如果你懂几何学（trigonometry），你可以将之前的结果和二分之根号二进行比较，检查是否正确：

::

    >>> math.sqrt(2) / 2.0
    0.707106781187

--------

组合
-----------

So far, we have looked at the elements of a program—variables,
expressions, and statements—in isolation, without talking about how to
combine them.

目前为止，我们已经分别介绍了程序的基本元素——变量、表达式和语句，但是还没有讨论如何组合它们。

One of the most useful features of programming languages is their
ability to take small building blocks and **compose** them. For example,
the argument of a function can be any kind of expression, including
arithmetic operators:

编程语言的最有用特征之一，是能够将小块构建材料\ **组合（compose）**\ 在一起。
例如，函数的实参可以是任意类型的表达式，包含算术运算符：

::

    x = math.sin(degrees / 360.0 * 2 * math.pi)

And even function calls:

甚至是函数调用：

::

    x = math.exp(math.log(x+1))

Almost anywhere you can put a value, you can put an arbitrary
expression, with one exception: the left side of an assignment statement
has to be a variable name. Any other expression on the left side is a
syntax error (we will see exceptions to this rule later).

几乎任何你可以放值的地方，你都可以放表达式，只有一个例外：
赋值语句的左侧必须是一个变量名。左侧放其他任何表达式都会产生语法错误
（后面我们会讲到这个规则的例外）。

::

    >>> minutes = hours * 60                 # right
    >>> hours * 60 = minutes                 # wrong!
    SyntaxError: can't assign to operator

-------

增加新函数
--------------------

So far, we have only been using the functions that come with Python, but
it is also possible to add new functions. A **function definition**
specifies the name of a new function and the sequence of statements that
run when the function is called.

目前为止，我们只了使用Python自带的函数， 但是增加新函数也是可能的。
一个\ **函数定义（function definition）**\ 指定了新函数的名
以及当函数被调用时执行的语句序列。

下面是一个示例：

::

    def print_lyrics():
        print("I'm a lumberjack, and I'm okay.")
        print("I sleep all night and I work all day.")

def is a keyword that indicates that this is a function definition. The
name of the function is ``print_lyrics``. The rules for function names
are the same as for variable names: letters, numbers and underscore are
legal, but the first character can’t be a number. You can’t use a
keyword as the name of a function, and you should avoid having a
variable and a function with the same name.

def是一个关键字，其指明这是一个函数定义。
这个函数的名字是\ ``print_lyrics``\ 。
函数的命名规则和变量名相同：字母、数字以及一些标点符号是合法的，
但是第一个字符不能是数字。不能使用关键字作为函数名，并应该避免
变量和函数同名。

The empty parentheses after the name indicate that this function doesn’t
take any arguments.

函数名后面的空括号表明该函数不接受任何实参。

The first line of the function definition is called the **header**; the
rest is called the **body**. The header has to end with a colon and the
body has to be indented. By convention, indentation is always four
spaces. The body can contain any number of statements.

函数定义的第一行被称作\ **函数头（header）**\ ；
其余部分被称作\ **函数体（body）**\ 。
函数体必须以冒号结尾，而且必须缩进。
按照惯例，缩进经常是4个空格。 函数体能包含任意条数的语句。

The strings in the print statements are enclosed in double quotes.
Single quotes and double quotes do the same thing; most people use
single quotes except in cases like this where a single quote (which is
also an apostrophe) appears in the string.

打印语句中的字符串被括在双引号中。单引号和双引号的作用相同；大多数人使用单引号，上述代码中的情况除外，即单引号（同时也是撇号）出现在字符串中。

All quotation marks (single and double) must be “straight quotes”,
usually located next to Enter on the keyboard. “Curly quotes”, like the
ones in this sentence, are not legal in Python.

所有引号（单引号和双引号）必须是“直引号（straight quotes）”，它们通常位于键盘Enter键旁边。“弯引号（curly quotes）”则是这个句子中所使用的引号，它在Python语言中是不合法的。

If you type a function definition in interactive mode, the interpreter
prints dots (...) to let you know that the definition isn’t complete:

如果你在交互模式中键入函数定义，解释器会打印三个句点（\ *...*\ ），
让你知道定义并没有结束。

::

    >>> def print_lyrics():
    ...     print("I'm a lumberjack, and I'm okay.")
    ...     print("I sleep all night and I work all day.")
    ...

To end the function, you have to enter an empty line.

为了完成函数定义，你必须输入一个空行。

Defining a function creates a **function object**, which has type
``function``:

定义一个函数会创建一个 **函数对象（function object）**，其类型是 ``function``：

::

    >>> print(print_lyrics)
    <function print_lyrics at 0xb7e99e9c>
    >>> type(print_lyrics)
    <class 'function'>

The syntax for calling the new function is the same as for built-in
functions:

调用新函数的语法，和调用内建函数的语法相同：

::

    >>> print_lyrics()
    I'm a lumberjack, and I'm okay.
    I sleep all night and I work all day.

Once you have defined a function, you can use it inside another
function. For example, to repeat the previous refrain, we could write a
function called ``repeat_lyrics

一旦你定义了一个函数，你就可以在另一个函数内部使用它。
例如，为了重复之前的叠句（refrain），我们可以写一个名叫\ ``repeat_lyrics``\ 的函数：

::

    def repeat_lyrics():
        print_lyrics()
        print_lyrics()

And then call ``repeat_lyrics``:

然后调用\ ``repeat_lyrics``\ ：

::

    >>> repeat_lyrics()
    I'm a lumberjack, and I'm okay.
    I sleep all night and I work all day.
    I'm a lumberjack, and I'm okay.
    I sleep all night and I work all day.

But that’s not really how the song goes.

不过，这首歌的歌词实际上不是这样的。

------

定义和使用
--------------------

Pulling together the code fragments from the previous section, the whole
program looks like this:

将上一节的多个代码段组合在一起，整个程序看起来是这样的：

::

    def print_lyrics():
        print("I'm a lumberjack, and I'm okay.")
        print("I sleep all night and I work all day.")

    def repeat_lyrics():
        print_lyrics()
        print_lyrics()

    repeat_lyrics()

This program contains two function definitions: ``print_lyrics`` and
``repeat_lyrics``. Function definitions get executed just like other
statements, but the effect is to create function objects. The statements
inside the function do not run until the function is called, and the
function definition generates no output.

该程序包含两个函数定义：\ ``print_lyrics``\ 和\ ``repeat_lyrics``\ 。
函数定义和其它语句一样，都会被执行，但是其作用是创建函数对象。
函数内部的语句在函数被调用之前，是不会执行的，而且函数定义没有任何输出。

As you might expect, you have to create a function before you can run
it. In other words, the function definition has to run before the
function gets called.

你可能猜到了，在运行函数之前，你必须先创建这个函数。换句话说，函数定义必须在其第一次被调用之前执行。

As an exercise, move the last line of this program to the top, so the
function call appears before the definitions. Run the program and see
what error message you get.

我们做个小练习，将该程序的最后一行移到顶部，使得函数调用出现在函数定义之前。运行程序，看看会得到怎样的错误信息。

Now move the function call back to the bottom and move the definition of
``print_lyrics`` after the definition of ``repeat_lyrics``. What happens
when you run this program?

现在将函数调用移回底部，然后将\ ``print_lyrics``\ 的定义移到\ ``repeat_lyrics``\ 的定义之后。这次运行这一程序时会发生什么？

-----


执行流程
-----------------

To ensure that a function is defined before its first use, you have to
know the order statements run in, which is called the **flow of
execution**.

为了保证函数第一次使用之前被定义，你必须要知道语句被执行的顺序，
这也被称作\ **执行流程（flow of execution）**\ 。

Execution always begins at the first statement of the program.
Statements are run one at a time, in order from top to bottom.

执行流程总是开始于程序的第一条语句。自顶向下，每次执行一条语句。

Function definitions do not alter the flow of execution of the program,
but remember that statements inside the function don’t run until the
function is called.

函数定义不改变程序执行的流程，但是请记住，函数内部的语句直到该函数被调用时才执行。

A function call is like a detour in the flow of execution. Instead of
going to the next statement, the flow jumps to the body of the function,
runs the statements there, and then comes back to pick up where it left
off.

函数调用像是在执行流程上绕了一个弯路。
执行流程没有进入下一条语句，而是跳入函数体，执行那里的语句，然后回到它离开的位置。

That sounds simple enough, until you remember that one function can call
another. While in the middle of one function, the program might have to
run the statements in another function. Then, while running that new
function, the program might have to run yet another function!

听起来足够简单，至少在你想起一个函数可以调用另一个函数之前。
当在一个函数执行到中间的时候，程序可能必须执行另一个函数里的语句。
然后当执行那个新函数的时候，程序可能又得执行另外一个函数！

Fortunately, Python is good at keeping track of where it is, so each
time a function completes, the program picks up where it left off in the
function that called it. When it gets to the end of the program, it
terminates.

幸运的是，Python善于记录程序执行流程的位置，因此每次一个函数完成时，
程序会回到调用它的那个函数原来执行的位置。当到达程序结尾时，执行流程终止。

In summary, when you read a program, you don’t always want to read from
top to bottom. Sometimes it makes more sense if you follow the flow of
execution.

总之，你在阅读一个程序时，没有必要总是从顶至下读。有时候，跟着执行流程阅读反而更加合理。

------

形参和实参
------------------------

Some of the functions we have seen require arguments. For example, when
you call math.sin you pass a number as an argument. Some functions take
more than one argument: math.pow takes two, the base and the exponent.

我们之前接触的一些函数需要实参。例如，当你调用math.sin时，你传递一个数字作为实参。
有些函数要求一个以上的实参：math.pow 接受两个，底数和指数。

Inside the function, the arguments are assigned to variables called
**parameters**. Here is a definition for a function that takes an
argument:

在函数内部，实参被赋给称作\ **形参（parameters）**\ 的变量。
下面是一个函数的定义，其接受一个实参：

::

    def print_twice(bruce):
        print(bruce)
        print(bruce)

This function assigns the argument to a parameter named bruce. When the
function is called, it prints the value of the parameter (whatever it
is) twice.

此函数将实参赋给名为bruce的形参。当函数被调用的时候，它打印形参（无论它是什么）的值两次。

This function works with any value that can be printed.

该函数对任意能被打印的值都有效。

::

    >>> print_twice('Spam')
    Spam
    Spam
    >>> print_twice(42)
    42
    42
    >>> print_twice(math.pi)
    3.14159265359
    3.14159265359

The same rules of composition that apply to built-in functions also
apply to programmer-defined functions, so we can use any kind of
expression as an argument for ``print_twice``:

组合规则不仅适用于内建函数，而且也适用于开发者自定义的函数，因此我们可以使用任意类型的表达式作为\ ``print_twice``\ 的实参：

::

    >>> print_twice('Spam '*4)
    Spam Spam Spam Spam
    Spam Spam Spam Spam
    >>> print_twice(math.cos(math.pi))
    -1.0
    -1.0

The argument is evaluated before the function is called, so in the
examples the expressions ``'Spam '*4`` and math.cos(math.pi) are only
evaluated once.

实参在函数被调用之前被计算，因此在这些例子中，
表达式\ ``'Spam '*4``\ 和math.cos(math.pi)都只被计算了一次。

You can also use a variable as an argument:

你也可以用变量作为实参：

::

    >>> michael = 'Eric, the half a bee.'
    >>> print_twice(michael)
    Eric, the half a bee.
    Eric, the half a bee.

The name of the variable we pass as an argument (michael) has nothing to
do with the name of the parameter (bruce). It doesn’t matter what the
value was called back home (in the caller); here in ``print_twice``, we
call everybody bruce.

我们传递的实参名（michael）与形参的名字（bruce）没有任何关系。
这个值在传入函数之前叫什么都没有关系；只要进了\ ``print_twice``\ ，我们将所有人都叫作bruce。

-------

变量和形参都是局部的
----------------------------------

When you create a variable inside a function, it is **local**, which
means that it only exists inside the function. For example:

当你在函数里面创建一个变量时，这个变量是\ **局部的（local）**\ ，
也就是说它只在函数内部存在。例如：

::

    def cat_twice(part1, part2):
        cat = part1 + part2
        print_twice(cat)

This function takes two arguments, concatenates them, and prints the
result twice. Here is an example that uses it:

此函数接受两个实参，级联它们并打印结果两次。 下面是这个函数的一个用例：

::

    >>> line1 = 'Bing tiddle '
    >>> line2 = 'tiddle bang.'
    >>> cat_twice(line1, line2)
    Bing tiddle tiddle bang.
    Bing tiddle tiddle bang.

When ``cat_twice`` terminates, the variable cat is destroyed. If we try
to print it, we get an exception:

当\ ``cat_twice``\ 结束时，变量cat被销毁了。
如果我们试图打印它，我们将获得一个异常：

::

    >>> print(cat)
    NameError: name 'cat' is not defined

Parameters are also local. For example, outside ``print_twice``, there
is no such thing as bruce.

形参也都是局部的。例如，在\ ``print_twice``\ 函数外面， 没有bruce这个变量。

----

栈图
--------------

To keep track of which variables can be used where, it is sometimes
useful to draw a **stack diagram**. Like state diagrams, stack diagrams
show the value of each variable, but they also show the function each
variable belongs to.

有时，画一个\ **栈图（stack diagram）**\ 可以帮助你跟踪哪个变量能在哪儿用。
像状态图一样，栈图展示每个变量的值，但是它们也展示了每个变量所属的函数。

Each function is represented by a **frame**. A frame is a box with the
name of a function beside it and the parameters and variables of the
function inside it. The stack diagram for the previous example is shown
in Figure [fig.stack].

每个函数用一个\ **框架（frame）**\ 表示。
一个框架是一个盒子，函数名写在旁边，形参以及函数内部的变量写在里面。
前面例子的栈图如下图所示。

.. figure:: figs/stack.png
   :alt: 栈图。

   栈图。

The frames are arranged in a stack that indicates which function called
which, and so on. In this example, ``print_twice`` was called by
``cat_twice``, and ``cat_twice`` was called by ``__main__``, which is a
special name for the topmost frame. When you create a variable outside
of any function, it belongs to ``__main__``.

这些框架排列成栈的形式，其中说明了哪个函数调用了哪个函数等信息。
在此例中，\ ``print_twice``\ 被\ ``cat_twice``\ 调用，
``cat_twice``\ 又被\ ``__main__``\ 调用，\ ``__main__``\ 是一个表示最上层框架的特殊名字。
当你在所有函数之外创建一个变量时，它就属于\ ``__main__``\ 。

Each parameter refers to the same value as its corresponding argument.
So, part1 has the same value as line1, part2 has the same value as
line2, and bruce has the same value as cat.

每个形参都指向其对应实参的值。
因此part1和line1的值相同，part2和line2的值相同， bruce和cat的值相同。

If an error occurs during a function call, Python prints the name of the
function, the name of the function that called it, and the name of the
function that called *that*, all the way back to ``__main__``.

如果函数调用时发生错误，Python会打印此函数的名字以及调用它的函数的名字，
以及调用 *后面这个函数* 的函数的名字，一直到\ ``__main__``\ 为止。

For example, if you try to access cat from within ``print_twice``, you
get a NameError:

例如，如果你试图在\ ``print_twice``\ 里面访问cat，
你将获得一个NameError：

::

    Traceback (innermost last):
      File "test.py", line 13, in __main__
        cat_twice(line1, line2)
      File "test.py", line 5, in cat_twice
        print_twice(cat)
      File "test.py", line 9, in print_twice
        print(cat)
    NameError: name 'cat' is not defined

This list of functions is called a **traceback**. It tells you what
program file the error occurred in, and what line, and what functions
were executing at the time. It also shows the line of code that caused
the error.

这个函数列表被称作\ **回溯（traceback）**\ 。
它告诉你发生错误的程序文件，错误在哪一行，以及当时在执行哪个函数。
它还会显示引起错误的那一行代码。

The order of the functions in the traceback is the same as the order of
the frames in the stack diagram. The function that is currently running
is at the bottom.

回溯中的函数顺序，与栈图中的函数顺序一致。出错时正在运行的那个函数则位于回溯信息的底部。

------

有返回值函数和无返回值函数
-------------------------------------

Some of the functions we have used, such as the math functions, return
results; for lack of a better name, I call them **fruitful functions**.
Other functions, like ``print_twice``, perform an action but don’t
return a value. They are called **void functions**.

有一些我们之前用过的函数，例如数学函数，会返回结果；
由于没有更好的名字，我姑且叫它们\ **有返回值函数（fruitful functions）**\ 。
其它的函数，像\ ``print_twice``\ ，执行一个动作但是不返回任何值。
它们被称为\ **无返回值函数（void functions）**\ 。

When you call a fruitful function, you almost always want to do
something with the result; for example, you might assign it to a
variable or use it as part of an expression:

当你调用一个有返回值函数时，你几乎总是想用返回的结果做些事情；
例如你可能将它赋值给一个变量，或者把它用在表达式里。

::

    x = math.cos(radians)
    golden = (math.sqrt(5) + 1) / 2

When you call a function in interactive mode, Python displays the
result:

当你在交互模式下调用一个函数的时候，Python解释器会马上显示结果：

::

    >>> math.sqrt(5)
    2.2360679774997898

But in a script, if you call a fruitful function all by itself, the
return value is lost forever!

但是在脚本中，如果你单单调用一个有返回值函数， 返回值就永远丢失了！

::

    math.sqrt(5)

This script computes the square root of 5, but since it doesn’t store or
display the result, it is not very useful.

该脚本计算5的平方根，但是既然它没保存或者显示这个结果，
这个脚本就没多大用处。

Void functions might display something on the screen or have some other
effect, but they don’t have a return value. If you assign the result to
a variable, you get a special value called None.

无返回值函数可能在屏幕上显示一些东西或者产生其它的影响，
但是它们没有返回值。如果你试图将这个结果赋给一个变量，
你得到的则是一个被称作None的特殊值。

::

    >>> result = print_twice('Bing')
    Bing
    Bing
    >>> print(result)
    None

The value None is not the same as the string ``'None'``. It is a special
value that has its own type:

None这个值和字符串\ ``'None'``\ 不同。这是一个自己有独立类型的特殊值：

::

    >>> print(type(None))
    <class 'NoneType'>

The functions we have written so far are all void. We will start writing
fruitful functions in a few chapters.

目前为止我们写的函数都是无返回值函数。
我们将在几章之后开始写有返回值函数。

-----

为什么用函数？
--------------

It may not be clear why it is worth the trouble to divide a program into
functions. There are several reasons:

-  Creating a new function gives you an opportunity to name a group of
   statements, which makes your program easier to read and debug.

-  Functions can make a program smaller by eliminating repetitive code.
   Later, if you make a change, you only have to make it in one place.

-  Dividing a long program into functions allows you to debug the parts
   one at a time and then assemble them into a working whole.

-  Well-designed functions are often useful for many programs. Once you
   write and debug one, you can reuse it.

Debugging
---------

One of the most important skills you will acquire is debugging. Although
it can be frustrating, debugging is one of the most intellectually rich,
challenging, and interesting parts of programming.

In some ways debugging is like detective work. You are confronted with
clues and you have to infer the processes and events that led to the
results you see.

Debugging is also like an experimental science. Once you have an idea
about what is going wrong, you modify your program and try again. If
your hypothesis was correct, you can predict the result of the
modification, and you take a step closer to a working program. If your
hypothesis was wrong, you have to come up with a new one. As Sherlock
Holmes pointed out, “When you have eliminated the impossible, whatever
remains, however improbable, must be the truth.” (A. Conan Doyle, *The
Sign of Four*)

For some people, programming and debugging are the same thing. That is,
programming is the process of gradually debugging a program until it
does what you want. The idea is that you should start with a working
program and make small modifications, debugging them as you go.

For example, Linux is an operating system that contains millions of
lines of code, but it started out as a simple program Linus Torvalds
used to explore the Intel 80386 chip. According to Larry Greenfield,
“One of Linus’s earlier projects was a program that would switch between
printing AAAA and BBBB. This later evolved to Linux.” (*The Linux Users’
Guide* Beta Version 1).

Glossary
--------

function:
    A named sequence of statements that performs some useful operation.
    Functions may or may not take arguments and may or may not produce a
    result.

function definition:
    A statement that creates a new function, specifying its name,
    parameters, and the statements it contains.

function object:
    A value created by a function definition. The name of the function
    is a variable that refers to a function object.

header:
    The first line of a function definition.

body:
    The sequence of statements inside a function definition.

parameter:
    A name used inside a function to refer to the value passed as an
    argument.

function call:
    A statement that runs a function. It consists of the function name
    followed by an argument list in parentheses.

argument:
    A value provided to a function when the function is called. This
    value is assigned to the corresponding parameter in the function.

local variable:
    A variable defined inside a function. A local variable can only be
    used inside its function.

return value:
    The result of a function. If a function call is used as an
    expression, the return value is the value of the expression.

fruitful function:
    A function that returns a value.

void function:
    A function that always returns None.

None:
    A special value returned by void functions.

module:
    A file that contains a collection of related functions and other
    definitions.

import statement:
    A statement that reads a module file and creates a module object.

module object:
    A value created by an import statement that provides access to the
    values defined in a module.

dot notation:
    The syntax for calling a function in another module by specifying
    the module name followed by a dot (period) and the function name.

composition:
    Using an expression as part of a larger expression, or a statement
    as part of a larger statement.

flow of execution:
    The order statements run in.

stack diagram:
    A graphical representation of a stack of functions, their variables,
    and the values they refer to.

frame:
    A box in a stack diagram that represents a function call. It
    contains the local variables and parameters of the function.

traceback:
    A list of the functions that are executing, printed when an
    exception occurs.

Exercises
---------

Write a function named ``right_justify`` that takes a string named s as
a parameter and prints the string with enough leading spaces so that the
last letter of the string is in column 70 of the display.

::

    >>> right_justify('monty')
                                                                     monty

Hint: Use string concatenation and repetition. Also, Python provides a
built-in function called len that returns the length of a string, so the
value of ``len('monty')`` is 5.

A function object is a value you can assign to a variable or pass as an
argument. For example, ``do_twice`` is a function that takes a function
object as an argument and calls it twice:

::

    def do_twice(f):
        f()
        f()

Here’s an example that uses ``do_twice`` to call a function named
``print_spam`` twice.

::

    def print_spam():
        print('spam')

    do_twice(print_spam)

#. Type this example into a script and test it.

#. Modify ``do_twice`` so that it takes two arguments, a function object
   and a value, and calls the function twice, passing the value as an
   argument.

#. Copy the definition of ``print_twice`` from earlier in this chapter
   to your script.

#. Use the modified version of ``do_twice`` to call ``print_twice``
   twice, passing ``'spam'`` as an argument.

#. Define a new function called ``do_four`` that takes a function object
   and a value and calls the function four times, passing the value as a
   parameter. There should be only two statements in the body of this
   function, not four.

Solution: http://thinkpython2.com/code/do_four.py.

Note: This exercise should be done using only the statements and other
features we have learned so far.

#. Write a function that draws a grid like the following:

   ::

       + - - - - + - - - - +
       |         |         |
       |         |         |
       |         |         |
       |         |         |
       + - - - - + - - - - +
       |         |         |
       |         |         |
       |         |         |
       |         |         |
       + - - - - + - - - - +

   Hint: to print more than one value on a line, you can print a
   comma-separated sequence of values:

   ::

       print('+', '-')

   By default, print advances to the next line, but you can override
   that behavior and put a space at the end, like this:

   ::

       print('+', end=' ')
       print('-')

   The output of these statements is ``'+ -'``.

   A print statement with no argument ends the current line and goes to
   the next line.

#. Write a function that draws a similar grid with four rows and four
   columns.

Solution: http://thinkpython2.com/code/grid.py. Credit: This exercise is
based on an exercise in Oualline, *Practical C Programming, Third
Edition*, O’Reilly Media, 1997.