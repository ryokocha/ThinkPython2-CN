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

---------

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

---------

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

很快你就会明白二者之间的区别，现在知道这些就足够了。

    译者注：Python核心开发者Brett Cannon详细解释了 `为什么print在Python 3中变成了函数 <http://codingpy.com/article/why-print-became-a-function-in-python-3/>`_。      

---------

算术运算符
--------------------

接下来介绍算术。Python提供了许多代表加法和乘法等运算的特殊符号，叫做 **运算符** （operators）。

After “Hello, World”, the next step is arithmetic. Python provides
**operators**, which are special symbols that represent computations
like addition and multiplication.

运算符 ``+`` 、``-`` 和 ``*`` 分别执行加法、减法和乘法，详见以下示例：

The operators +, -, and \* perform addition, subtraction, and
multiplication, as in the following examples:

::

    >>> 40 + 2
    42
    >>> 43 - 1
    42
    >>> 6 * 7
    42

运算符 / 执行除法运算：

The operator / performs division:

::

    >>> 84 / 2
    42.0

你可能会问，为什么结果是42.0，而不是42。在下节中，我会进行解释。

You might wonder why the result is 42.0 instead of 42. I’ll explain in
the next section.

最后，运算符 ``*`` 执行乘方运算；也就是说，它将某个数字乘以相应的次数：

Finally, the operator \* performs exponentiation; that is, it raises a
number to a power:

::

    >>> 6**2 + 6
    42

某些语言使用 ``^`` 运算符执行乘方运算，但是在Python中，它却属于一种位运算符，叫做XOR。如果你对位运算符不太了解，那么下面的结果会让你感到惊讶：

In some other languages, ``^`` is used for exponentiation, but in Python
it is a bitwise operator called XOR. If you are not familiar with
bitwise operators, the result will surprise you:

::

    >>> 6 ^ 2
    4

我打算在本书中介绍位运算符，但是你可以阅读 `Python官方百科 <http://wiki.python.org/moin/BitwiseOperators>`_ ，了解相关内容。

I won’t cover bitwise operators in this book, but you can read about
them at http://wiki.python.org/moin/BitwiseOperators.

--------

值和类型
----------------

**值（value）** 是程序处理的基本数据之一，比如说一个单词或一个数字。我们目前已经接触到的值有：2，42.0，和 ``'Hello World!'`` 。

A **value** is one of the basic things a program works with, like a
letter or a number. Some values we have seen so far are 2, 42.0, and
``'Hello, World!'``.

这些值又属于不同的 **类型（types）** ：2是一个 **整型数（integer）**，42.0 是一个 **浮点数（floating point number）**，而 ``'Hello, World!'`` 则是一个 **字符串（string）**，之所以这么叫是因为其中的字符被串在了一起（strung together）。

These values belong to different **types**: 2 is an **integer**, 42.0 is
a **floating-point number**, and ``'Hello, World!'`` is a **string**,
so-called because the letters it contains are strung together.

如果你不确定某个值的类型是什么，解释器可以告诉你：

If you are not sure what type a value has, the interpreter can tell you:

::

    >>> type(2)
    <class 'int'>
    >>> type(42.0)
    <class 'float'>
    >>> type('Hello, World!')
    <class 'str'>

“class”一词在上面的结果中，是类别的意思；一个类型就是一个类别的值。

In these results, the word “class” is used in the sense of a category; a
type is a category of values.

不出意料，整型数属于 ``int`` 类型，字符串属于 ``str`` 类型，浮点数属于 ``float`` 类型。

Not surprisingly, integers belong to the type int, strings belong to str
and floating-point numbers belong to float.

那么像 ``'2'`` 和 ``'42.0'`` 这样的值呢？它们看上去像数字，但是又和字符串一样被引号包围？

What about values like ``'2'`` and ``'42.0'``? They look like numbers,
but they are in quotation marks like strings.

::

    >>> type('2')
    <class 'str'>
    >>> type('42.0')
    <class 'str'>

它们其实是字符串。

They’re strings.

当你输入一个大数值的整型数时，你可能会想用逗号进行区分，比如说这样：1,000,000。在Python中，这不是一个合法的 *整型数*，但是确实合法的值。

When you type a large integer, you might be tempted to use commas
between groups of digits, as in 1,000,000. This is not a legal *integer*
in Python, but it is legal:

::

    >>> 1,000,000
    (1, 0, 0)

结果和我们预料的完全不同！Python把1,000,000当作成了一个以逗号区分的整型数序列。在后面的章节中，我们会介绍更多有关这种序列的知识。

That’s not what we expected at all! Python interprets 1,000,000 as a
comma-separated sequence of integers. We’ll learn more about this kind
of sequence later.

--------

形式语言和自然语言
----------------------------

**自然语言（natural language）** 是人们交流所使用的语言，例如英语、西班牙语和法语。它们不是人为设计出来的（尽管有人试图这样做）；而是自然演变而来。

**Natural languages** are the languages people speak, such as English,
Spanish, and French. They were not designed by people (although people
try to impose some order on them); they evolved naturally.

**形式语言（formal languages）**\ 是人类为了特殊用途而设计出来的。例如，数学家使用的记号（notation）就是形式语言，特别擅长表示数字和符号之间的关系。化学家使用形式语言表示分子的化学结构。 最重要的是：

**Formal languages** are languages that are designed by people for
specific applications. For example, the notation that mathematicians use
is a formal language that is particularly good at denoting relationships
among numbers and symbols. Chemists use a formal language to represent
the chemical structure of molecules. And most importantly:

    **编程语言是被设计用于表达计算的形式语言。**

    **Programming languages are formal languages that have been designed
    to express computations.**

形式语言通常拥有严格的 **语法** 规则，规定了详细的语句结构。例如，\ :math:`3 + 3 = 6`\ 是语法正确的数学表达式，而\ :math:`3 + = 3 \$ 6`\ 则不是；:math:`H_2O`\ 是语法正确的化学式，而\ :math:`_2Zz`\ 则不是。

Formal languages tend to have strict **syntax** rules that govern the
structure of statements. For example, in mathematics the statement
:math:`3 + 3 = 6` has correct syntax, but :math:`3 + = 3 \$ 6` does not.
In chemistry :math:`H_2O` is a syntactically correct formula, but
:math:`_2Zz` is not.

语法规则有两种类型，分别涉及\ **记号（tokens）**\ 和结构。记号是语言的基本元素，例如单词、数字和化学元素。
:math:`3 + = 3 \$ 6`\ 这个式子的问题之一，就是 $ 在数学中不是一个合法的记号
（至少据我所知）。类似的，:math:`_2Zz` 也不合法，因为没有一个元素的简写是 :math:`Zz`。

Syntax rules come in two flavors, pertaining to **tokens** and
structure. Tokens are the basic elements of the language, such as words,
numbers, and chemical elements. One of the problems with
:math:`3 += 3 \$ 6` is that :math:` \$ ` is not a legal token in
mathematics (at least as far as I know). Similarly, :math:`_2Zz` is not
legal because there is no element with the abbreviation :math:`Zz`.

第二种语法规则与标记的组合方式有关。\ :math:`3 + = 3`\ 这个方程是非法的，因为即使\ :math:`+`\ 和\ :math:`=`\ 都是合法的记号，但是你却不能把它们俩紧挨在一起。类似的，在化学式中，下标位于元素之后，而不是之前。

The second type of syntax rule pertains to the way tokens are combined.
The equation :math:`3 += 3` is illegal because even though :math:`+` and
:math:`=` are legal tokens, you can’t have one right after the other.
Similarly, in a chemical formula the subscript comes after the element
name, not before.

“This is @ well-structured Engli$h sentence with invalid t\*kens in it.
This sentence all valid tokens has, but invalid structure with.”

    译者注：上面两句英文都是不符合语法的，一个包含非法标记，另一个句子结构不和语法。

当你读一个用英语写的句子或者用形式语言写的语句时，你都必须要理清各自的结构（尽管在阅读自然语言时，你是下意识地进行的）。这个过程被称为 **解析（parsing）**。

When you read a sentence in English or a statement in a formal language,
you have to figure out the structure (although in a natural language you
do this subconsciously). This process is called **parsing**.

虽然形式语言和自然语言有很多共同点——标记、结构和语法，它们也有一些不同：

Although formal and natural languages have many features in
common—tokens, structure, and syntax—there are some differences:

*歧义性*：
    自然语言充满歧义，人们使用上下文线索以及其它信息处理这些歧义。形式语言被设计成几乎或者完全没有歧义，这意味着不管上下文是什么，任何语句都只有一个意义。

ambiguity:
    Natural languages are full of ambiguity, which people deal with by
    using contextual clues and other information. Formal languages are
    designed to be nearly or completely unambiguous, which means that
    any statement has exactly one meaning, regardless of context.

*冗余性*：
    为了弥补歧义性并减少误解，自然语言使用很多冗余。结果，自然语言经常很冗长。形式语言则冗余较少，更简洁。

redundancy:
    In order to make up for ambiguity and reduce misunderstandings,
    natural languages employ lots of redundancy. As a result, they are
    often verbose. Formal languages are less redundant and more concise.

*字面性*：
    自然语言充满成语和隐喻。如果我说“The penny dropped”，可能根本没有便士、也没什么东西掉下来（这个成语的意思是，经过一段时间的困惑后终于理解某事）。形式语言的含义，与它们字面的意思完全一致。

literalness:
    Natural languages are full of idiom and metaphor. If I say, “The
    penny dropped”, there is probably no penny and nothing dropping
    (this idiom means that someone understood something after a period
    of confusion). Formal languages mean exactly what they say.

由于我们都是说着自然语言长大的，我们有时候很难适应形式语言。形式语言与自然语言之间的不同，类似诗歌与散文之间的差异，而且更加明显：

Because we all grow up speaking natural languages, it is sometimes hard
to adjust to formal languages. The difference between formal and natural
language is like the difference between poetry and prose, but more so:

*诗歌*：
    单词的含义和声音都有作用，
    整首诗作为一个整理，会对人产生影响，或是引发情感上的共鸣。
    歧义不但常见，而且经常是故意为之。

Poetry:
    Words are used for their sounds as well as for their meaning, and
    the whole poem together creates an effect or emotional response.
    Ambiguity is not only common but often deliberate.

*散文*：
    单词表面的含义更重要，句子结构背后的寓意更深。
    散文比诗歌更适合分析，但仍然经常有歧义。

Prose:
    The literal meaning of words is more important, and the structure
    contributes more meaning. Prose is more amenable to analysis than
    poetry but still often ambiguous.

*程序*：
    计算机程序的含义是无歧义、无引申义的，
    通过分析程序的标记和结构，即可完全理解。

Programs:
    The meaning of a computer program is unambiguous and literal, and
    can be understood entirely by analysis of the tokens and structure.

形式语言的信息密度要高于自然语言，因此阅读的时间会更长。另外，形式语言的结构也很重要，所以从上往下、从左往右阅读，并不总是最好的策略。相反，你得学会在脑海里分析一个程序，识别不同的标记并理解其结构。最后，注重细节。拼写和标点方面的小错误在自然语言中无伤大雅，但是在形式语言中却会产生很大的影响。

Formal languages are more dense than natural languages, so it takes
longer to read them. Also, the structure is important, so it is not
always best to read from top to bottom, left to right. Instead, learn to
parse the program in your head, identifying the tokens and interpreting
the structure. Finally, the details matter. Small errors in spelling and
punctuation, which you can get away with in natural languages, can make
a big difference in a formal language.

--------

调试
---------

Programmers make mistakes. For whimsical reasons, programming errors are
called **bugs** and the process of tracking them down is called
**debugging**.

程序员都会犯错。由于比较奇怪的原因，编程错误被称为 **故障（译者注：英文为bug，一般指虫子）**，追踪错误的过程被称为 **调试（debugging）**。

Programming, and especially debugging, sometimes brings out strong
emotions. If you are struggling with a difficult bug, you might feel
angry, despondent, or embarrassed.

编程，尤其是调试，有时会让人动情绪。如果你有个很难的bug解决不了，你可能会感到愤怒、忧郁抑或是丢人。

There is evidence that people naturally respond to computers as if they
were people. When they work well, we think of them as teammates, and
when they are obstinate or rude, we respond to them the same way we
respond to rude, obstinate people (Reeves and Nass, *The Media Equation:
How People Treat Computers, Television, and New Media Like Real People
and Places*).

有证据表明，人们很自然地把计算机当人来对待。当计算机表现好的时候，我们认为它们是队友，而当它们固执或无礼的时候，我们也会像对待固执或无礼人的一样对待它们（Reeves and Nass, *The Media Equation:
How People Treat Computers, Television, and New Media Like Real People
and Places*）。

Preparing for these reactions might help you deal with them. One
approach is to think of the computer as an employee with certain
strengths, like speed and precision, and particular weaknesses, like
lack of empathy and inability to grasp the big picture.

对这些反应做好准备有助于你对付它们。
一种方法是将计算机看做是一个雇员，拥有特定的长处，
例如速度和精度，也有些特别的缺点，像缺乏沟通以及不善于把握大局。

Your job is to be a good manager: find ways to take advantage of the
strengths and mitigate the weaknesses. And find ways to use your
emotions to engage with the problem, without letting your reactions
interfere with your ability to work effectively.

你的工作是当一个好的管理者：找到充分利用优点、摒弃弱点的方法。
并且找到使用你的情感来解决问题的方法，
而不是让你的情绪干扰你有效工作的能力。

Learning to debug can be frustrating, but it is a valuable skill that is
useful for many activities beyond programming. At the end of each
chapter there is a section, like this one, with my suggestions for
debugging. I hope they help!

学习调试可能很令人泄气，
但是它对于许多编程之外的活动也是一个非常有价值的技能。
在每一章的结尾，我都会花一节内容介绍一些调试建议，比如说这一节。希望能帮到你！

-------

词汇表
--------

*解决问题*：
    将问题形式化、寻找并表达解决方案的过程。

problem solving:
    The process of formulating a problem, finding a solution, and
    expressing it.

*高级语言（high-level language）*：
    像Python这样被设计成人类容易阅读和编写的编程语言。

high-level language:
    A programming language like Python that is designed to be easy for
    humans to read and write.

*低级语言(low-level language)*：
    被设计成计算机容易运行的编程语言；也被称为“机器语言”或“汇编语言（assembly language）”。
    
low-level language:
    A programming language that is designed to be easy for a computer to
    run; also called “machine language” or “assembly language”.

*可移植性*：
    程序能够在多种计算机上运行的特性。

portability:
    A property of a program that can run on more than one kind of
    computer.

*解释器*：
    读取另一个程序并执行该程序的程序。

interpreter:
    A program that reads another program and executes it

*提示符*：
    解释器所显示的字符，表明已准备好接受用户的输入。

prompt:
    Characters displayed by the interpreter to indicate that it is ready
    to take input from the user.

*程序*：
    说明一个计算的一组指令。

program:
    A set of instructions that specifies a computation.

*打印语句*：
    使Python解释器在屏幕上显示某个值的指令。

print statement:
    An instruction that causes the Python interpreter to display a value
    on the screen.

*运算符*：
    代表类似加法、乘法或者字符串连接（string concatenation）等简单计算的特殊符号。

operator:
    A special symbol that represents a simple computation like addition,
    multiplication, or string concatenation.

*值*：
    程序所处理数据的基本元素之一，例如数字或字符串。

value:
    One of the basic units of data, like a number or string, that a
    program manipulates.

*类型*：
    值的类别。我们目前接触的类型有整型数（类型为 ``int``）、浮点数（类型为 ``float`` ）和字符串（类型为 ``str`` ）

type:
    A category of values. The types we have seen so far are integers
    (type int), floating-point numbers (type float), and strings (type
    str).

*整型数*：
    代表整数的类型。

integer:
    A type that represents whole numbers.

*浮点数*：
    代表一个有小数点的数字的类型。

floating-point:
    A type that represents numbers with fractional parts.

*字符串*：
    代表一系列字符的类型。

string:
    A type that represents sequences of characters.

*自然语言*：
    任意一种人们日常使用的、自然演变而来的语言。

natural language:
    Any one of the languages that people speak that evolved naturally.

*形式语言*：
    任意一种人类为了某种目的而设计的语言，例如用来表示数学概念或者电脑程序；所有的编程语言都是形式语言。

formal language:
    Any one of the languages that people have designed for specific
    purposes, such as representing mathematical ideas or computer
    programs; all programming languages are formal languages.

*记号*：
    程序语法结构中的基本元素之一，与自然语言中的单词类似。

token:
    One of the basic elements of the syntactic structure of a program,
    analogous to a word in a natural language.

*语法*：
    规定了程序结构的规则。

syntax:
    The rules that govern the structure of a program.

*解析*：
    阅读程序，并分析其语法结构的过程

parse:
    To examine a program and analyze the syntactic structure.

*故障*：
    程序中的错误。

bug:
    An error in a program.

*调试*：
    寻找并解决错误的过程。
    
debugging:
    The process of finding and correcting bugs.

------

练习题
---------

It is a good idea to read this book in front of a computer so you can
try out the examples as you go.

Whenever you are experimenting with a new feature, you should try to
make mistakes. For example, in the “Hello, world!” program, what happens
if you leave out one of the quotation marks? What if you leave out both?
What if you spell print wrong?

This kind of experiment helps you remember what you read; it also helps
when you are programming, because you get to know what the error
messages mean. It is better to make mistakes now and on purpose than
later and accidentally.

#. In a print statement, what happens if you leave out one of the
   parentheses, or both?

#. If you are trying to print a string, what happens if you leave out
   one of the quotation marks, or both?

#. You can use a minus sign to make a negative number like -2. What
   happens if you put a plus sign before a number? What about 2++2?

#. In math notation, leading zeros are ok, as in 02. What happens if you
   try this in Python?

#. What happens if you have two values with no operator between them?

Start the Python interpreter and use it as a calculator.

#. How many seconds are there in 42 minutes 42 seconds?

#. How many miles are there in 10 kilometers? Hint: there are 1.61
   kilometers in a mile.

#. If you run a 10 kilometer race in 42 minutes 42 seconds, what is your
   average pace (time per mile in minutes and seconds)? What is your
   average speed in miles per hour?