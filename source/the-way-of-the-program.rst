========================
第一章：编程之道
========================

The goal of this book is to teach you to think like a computer scientist. This way of thinking combines some of the best features of mathematics, engineering, and natural science. Like mathematicians, computer scientists use formal languages to denote ideas (specifically computations). Like engineers, they design things, assembling components into systems and evaluating tradeoffs among alternatives. Like scientists, they observe the behavior of complex systems, form hypotheses, and test predictions.

本书的目标是教你像计算机科学家一样思考。这一思考方式集成了数学、工程以及自然科学的一些最好的特点。像数学家一样，计算机科学家使用形式语言表示思想（具体来说是计算）。像工程师一样，计算机科学家设计东西，将零件组成系统，在各种选择之间寻求平衡。像科学家一样，计算机科学家观察复杂系统的行为，形成假设并且对预测进行检验。

The single most important skill for a computer scientist is problem solving. Problem solving means the ability to formulate problems, think creatively about solutions, and express a solution clearly and accurately. As it turns out, the process of learning to program is an excellent opportunity to practice problem-solving skills. That’s why this chapter is called “The Way of the Program”.

对于计算机科学家，最重要的技能是 **解决问题的能力** 。解决问题（problem solving）意味着对问题进行形式化，寻求创新型的解决方案，并且清晰、准确地表达解决方案的能力。事实证明，学习编程的过程是锻炼问题解决能力的一个绝佳机会。这就是为什么本章被称为“编程之道”。

On one level, you will be learning to program, a useful skill by itself. On another level, you will use programming as a means to an end. As we go along, that end will become clearer.

一方面，你将学习如何编程，这本身就是一个有用的技能。另一方面，你将把编程作为实现自己目的的手段。随着学习的深入，你会更清楚自己的目的。

什么是程序？
----------------

A program is a sequence of instructions that specifies how to perform a computation. The computation might be something mathematical, such as solving a system of equations or finding the roots of a polynomial, but it can also be a symbolic computation, such as searching and replacing text in a document or something graphical, like processing an image or playing a video.

**程序** 是一系列说明如何执行计算（computation）的指令。计算可以是数学上的计算，例如寻找公式的解或多项式的根，但它也可以是一个符号计算（symbolic computation），例如在文档中搜索并替换文本或者图片，就像处理图片或播放视频。

The details look different in different languages, but a few basic instructions appear in just about every language:

不同编程语言中，程序的具体细节也不一样，但是有一些基本的指令几乎出现在每种语言当中：

input:
    Get data from the keyboard, a file, the network, or some other device.

*输入（input）：*
    从键盘、文件、网络或者其他设备获取数据。

output:
    Display data on the screen, save it in a file, send it over the network, etc.

*输出（output）：*
    在屏幕上显示数据，将数据保存至文件，通过网络传送数据，等等。

math:
    Perform basic mathematical operations like addition and multiplication.

*数学（math）：*
    执行基本的数学运算，如加法和乘法。

conditional execution:
    Check for certain conditions and run the appropriate code.

*有条件执行（conditional execution）：*
    检查符合某个条件后，执行相应的代码。

repetition:
    Perform some action repeatedly, usually with some variation.

*重复（repetition）：*
    重复执行某个动作，通常会有一些变化。

Believe it or not, that’s pretty much all there is to it. Every program you’ve ever used, no matter how complicated, is made up of instructions that look pretty much like these. So you can think of programming as the process of breaking a large, complex task into smaller and smaller subtasks until the subtasks are simple enough to be performed with one of these basic instructions.

无论你是否相信，这几乎是程序的全部指令了。每个你曾经用过的程序，无论多么复杂，都是由跟这些差不多的指令构成的。因此，你可以认为编程就是将庞大、复杂的任务分解为越来越小的子任务，直到这些子任务简单到可以用这其中的一个基本指令执行。

运行Python
--------------------

One of the challenges of getting started with Python is that you might have to install Python and related software on your computer. If you are familiar with your operat‐ ing system, and especially if you are comfortable with the command-line interface, you will have no trouble installing Python. But for beginners, it can be painful to learn about system administration and programming at the same time.

Python入门的一个障碍，是你可能需要在电脑上安装Python和相关软件。如果你熟悉电脑的操作系统，特别是如果你能熟练使用命令行（command-line interface），安装Python对你来说就不是问题了。但是对于初学者，同时学习系统管理（system administration）和编程这两方面的知识是件痛苦的事。

To avoid that problem, I recommend that you start out running Python in a browser. Later, when you are comfortable with Python, I’ll make suggestions for installing Python on your computer.

为了避免这个问题，我建议你首先在浏览器中运行Python。等你对Python更加了解之后，我会建议你在电脑上安装Python。

There are a number of web pages you can use to run Python. If you already have a favorite, go ahead and use it. Otherwise I recommend PythonAnywhere. I provide detailed instructions for getting started at http://tinyurl.com/thinkpython2e.

网络上有许多网页可以让你运行Python。如果你已经有最喜欢的网站，那就打开网页运行Python吧。如果没有，我推荐PythonAnywhere。我在 http://tinyurl.com/thinkpython2e 给出了详细的使用指南。

There are two versions of Python, called Python 2 and Python 3. They are very simi‐ lar, so if you learn one, it is easy to switch to the other. In fact, there are only a few differences you will encounter as a beginner. This book is written for Python 3, but I include some notes about Python 2.

目前Python有两个版本，分别是Python 2和Python 3。二者十分相似，因此如果你学过某个版本，可以很容易地切换到另一个版本。事实上，作为初学者，你只会接触到很少数的不同之处。本书采用的是Python 3，但是我会加入一些关于Python 2的说明。

The Python interpreter is a program that reads and executes Python code. Depend‐ ing on your environment, you might start the interpreter by clicking on an icon, or by typing python on a command line. When it starts, you should see output like this:

Python的 **解释器** 是一个读取并执行Python代码的程序。根据你的电脑环境不同，你可以通过双击图标，或者在命令行输入`python`的方式来启动解释器。解释器启动后，你应该看到类似下面的输出：

::

    Python 3.4.0 (default, Jun 19 2015, 14:20:21)
    [GCC 4.8.2] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

The first three lines contain information about the interpreter and the operating sys‐ tem it’s running on, so it might be different for you. But you should check that the version number, which is 3.4.0 in this example, begins with 3, which indicates that you are running Python 3. If it begins with 2, you are running (you guessed it) Python 2.

前三行中包含了关于解释器及其运行的操作系统的信息，因此你看到的内容可能不一样。但是你应该检查下版本号是否以3开头，上面示例中的版本号是3.4.0。如果以3开头，那说明你正在运行Python 3。如果以2开头，那说明你正在运行（你猜对了）Python 2。

The last line is a prompt that indicates that the interpreter is ready for you to enter code. If you type a line of code and hit Enter, the interpreter displays the result:

最后一行是一个提示符（prompt），表明你可以在解释器中输入代码了。如果你输入一行代码然后按回车（Enter），解释器就会显示结果： 

::

    >>> 1 + 1
    2

Now you’re ready to get started. From here on, I assume that you know how to start the Python interpreter and run code.

现在你已经做好了开始学习的准备。接下来，我将默认你已经知道如何启动Python解释器和执行代码。

第一个程序
----------------

Traditionally, the first program you write in a new language is called “Hello, World!” because all it does is display the words “Hello, World!” In Python, it looks like this:

根据传统，你用一门新语言写的第一个程序叫做“Hello, World!”，因为它的功能只不过是显示单词“Hello, World!”。在Python中，它看起来是这样： 

::

    >>> print('Hello, World!')

This is an example of a print statement, although it doesn’t actually print anything on paper. It displays a result on the screen. In this case, the result is the words

    Hello, World!

这是一个 ``print`` 函数的示例，尽管它并不会真的在纸上打印。它将结果显示在屏幕上。在此例中，结果是单词： 

::

    Hello, World!

The quotation marks in the program mark the beginning and end of the text to be displayed; they don’t appear in the result.

程序中的单引号标记了被打印文本的首尾；它们不会出现在结果中。

The parentheses indicate that print is a function. We’ll get to functions in Chapter 3. In Python 2, the print statement is slightly different; it is not a function, so it doesn’t use parentheses.

括号说明 ``print`` 是一个函数。我们将在第三章介绍函数。在Python 2中， print是一个语句；不是函数，所以不需要使用括号。

::

    >>> print 'Hello, World!'

This distinction will make more sense soon, but that’s enough to get started.

很快你就会明白二者之间的区别，现在你知道这些就足够了。

    译者注：Python核心开发者Brett Cannon详细解释了为什么print在Python 3中变成了函数。 http://codingpy.com/article/why-print-became-a-function-in-python-3/     

算术运算符
--------------------

After “Hello, World”, the next step is arithmetic. Python provides
**operators**, which are special symbols that represent computations
like addition and multiplication.



The operators +, -, and * perform addition, subtraction, and
multiplication, as in the following examples:

::

    >>> 40 + 2
    42
    >>> 43 - 1
    42
    >>> 6 * 7
    42

The operator / performs division:

::

    >>> 84 / 2
    42.0

You might wonder why the result is 42.0 instead of 42. I’ll explain in
the next section.

Finally, the operator \* performs exponentiation; that is, it raises a
number to a power:

::

    >>> 6**2 + 6
    42

In some other languages, ``^`` is used for exponentiation, but in Python
it is a bitwise operator called XOR. If you are not familiar with
bitwise operators, the result will surprise you:

::

    >>> 6 ^ 2
    4

I won’t cover bitwise operators in this book, but you can read about
them at http://wiki.python.org/moin/BitwiseOperators.