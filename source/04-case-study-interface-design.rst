案例学习：接口设计
============================

This chapter presents a case study that demonstrates a process for
designing functions that work together.

本章分享一个案例学习，演示如何设计出相互配合协作的函数的过程。

It introduces the turtle module, which allows you to create images using
turtle graphics. The turtle module is included in most Python
installations, but if you are running Python using PythonAnywhere, you
won’t be able to run the turtle examples (at least you couldn’t when I
wrote this).

本章将会介绍 ``turtle`` 模块，可以让你使用海龟图形生成图片。大部分的Python安装环境下都内置了这个模块，但是如果你是在PythonAnywhere上运行Python的，你将无法运行本章中的代码示例（至少在我写下这章时是做不到的）。

If you have already installed Python on your computer, you should be
able to run the examples. Otherwise, now is a good time to install. I
have posted instructions at http://tinyurl.com/thinkpython2e.

如果你已经在自己的电脑上安装了Python，那么不会有问题。否则，建议你现在安装。我在 http://tinyurl.com/thinkpython2e 这个页面上发布了相关指南。

Code examples from this chapter are available from
http://thinkpython2.com/code/polygon.py.

本章的示例代码可以从\ http://thinkpython2.com/code/polygon.py\ 获得。

turtle模块
-----------------

To check whether you have the turtle module, open the Python interpreter
and type

打开Python解释器，输入以下代码，检查你是否安装了turltle模块：

::

    >>> import turtle
    >>> bob = turtle.Turtle()

When you run this code, it should create a new window with small arrow
that represents the turtle. Close the window.

运行上面的代码后，应该会新建一个窗口，中间有一个小箭头，代表的就是海龟。现在关闭窗口。

Create a file named mypolygon.py and type in the following code:

新建一个名叫  ``mypolygon.py`` 的文件，输入以下代码：

::

    import turtle
    bob = turtle.Turtle()
    print(bob)
    turtle.mainloop()

The turtle module (with a lowercase ’t’) provides a function called
Turtle (with an uppercase ’T’) that creates a Turtle object, which we
assign to a variable named bob. Printing bob displays something like:

turtle模块（t为小写）提供了一个叫作 ``Turtle`` 的函数（T为大写），这个函数会创建一个Turtle对象，我们将其赋值给名为 ``bob``的变量。打印bob的话，会输出下面这样的结果：

::

    <turtle.Turtle object at 0xb7bfbf4c>

This means that bob refers to an object with type Turtle as defined in
module turtle.

这意味着，bob指向一个类型为Turtle的对象，这个类型是由turtle模块定义的。

``mainloop`` tells the window to wait for the user to do something,
although in this case there’s not much for the user to do except close
the window.

``mainloop`` 告诉窗口等待用户操作，尽管在这个例子中用户除了关闭窗口之外，并没有其他可做的事情。

Once you create a Turtle, you can call a **method** to move it around
the window. A method is similar to a function, but it uses slightly
different syntax. For example, to move the turtle forward:

创建了一个Turtle对象之后，你可以调用 **方法（method）**来在窗口中移动该对象。方法与函数类似，但是其语法略有不同。例如，要让turtle向前走：

::

    bob.fd(100)

The method, fd, is associated with the turtle object we’re calling bob.
Calling a method is like making a request: you are asking bob to move
forward.

方法fd与我们称之为bob的对象是相关联的。调用方法就像提出一个请求：你在请求bob往前走。

The argument of fd is a distance in pixels, so the actual size depends
on your display.

fd方法的实参是像素距离，所以实际行动的距离取决于你的屏幕大小。

Other methods you can call on a Turtle are bk to move backward, lt for
left turn, and rt right turn. The argument for lt and rt is an angle in
degrees.

对于一个Turtle，你能调用的其他方法还包括：让它向后走的bk，向左转的lt，向右转的rt。lt和rt这两个方法接受的实参是角度。

Also, each Turtle is holding a pen, which is either down or up; if the
pen is down, the Turtle leaves a trail when it moves. The methods pu and
pd stand for “pen up” and “pen down”.

另外，每个Turtle都握着一支笔，不是落笔就是抬笔；如果落笔了，Turtle就会在移动时留下痕迹。pu和pd这两个方法分别代表“抬笔（pen up）”和“落笔（pen down）”。

To draw a right angle, add these lines to the program (after creating
bob and before calling ``mainloop``):

::

    bob.fd(100)
    bob.lt(90)
    bob.fd(100)

When you run this program, you should see bob move east and then north,
leaving two line segments behind.

当你运行此程序时，你应该会看到bob先朝东移动，然后向北移动，在身后留下两条线段。

Now modify the program to draw a square. Don’t go on until you’ve got it
working!

现在修改程序，画一个正方形。在没有成功之前，不要继续往下读。

---

简单的重复
-----------------

Chances are you wrote something like this:

很有可能你刚才写了像下面这样的一个程序：

::

    bob.fd(100)
    bob.lt(90)

    bob.fd(100)
    bob.lt(90)

    bob.fd(100)
    bob.lt(90)

    bob.fd(100)

We can do the same thing more concisely with a for statement. Add this
example to mypolygon.py and run it again:

我们可以利用for语句，以更简洁的代码来做相同的事情。
将下面的示例代码加入mypolygon.py，并重新运行：

::

    for i in range(4):
        print('Hello!')

You should see something like this:

你会看到如下输出：

::

    Hello!
    Hello!
    Hello!
    Hello!

This is the simplest use of the for statement; we will see more later.
But that should be enough to let you rewrite your square-drawing
program. Don’t go on until you do.

这是for语句最简单的用法；后面我们会介绍更多的用法。
但是这对于让你重写你的画正方形程序已经足够了。 如果没有完成，请不要往下读。

Here is a for statement that draws a square:

这是一个画正方形的for语句：

::

    for i in range(4):
        bob.fd(100)
        bob.lt(90)

The syntax of a for statement is similar to a function definition. It
has a header that ends with a colon and an indented body. The body can
contain any number of statements.

for语句的语法和函数定义类似。
它有一个以冒号结尾的语句头（header）以及一个缩进的语句体（body）。
语句体可以包含任意条语句。

A for statement is also called a **loop** because the flow of execution
runs through the body and then loops back to the top. In this case, it
runs the body four times.

for语句有时被称为\ **循环（loop）**\ ，因为执行流程会贯穿整个语句体，然后再循环回顶部。
在此例中，它将运行语句体四次。

This version is actually a little different from the previous
square-drawing code because it makes another turn after drawing the last
side of the square. The extra turn takes more time, but it simplifies
the code if we do the same thing every time through the loop. This
version also has the effect of leaving the turtle back in the starting
position, facing in the starting direction.

这个版本和前面画正方形的代码有所不同，因为它在画完正方形最后一条边后，
又多转了一下。这个额外的转动多花了些时间，
但是如果我们每次都通过循环做相同的事情，反而是简化了代码。
这个版本最终让海龟放回了初始位置，朝向也与出发时一致。

练习
---------

The following is a series of exercises using TurtleWorld. They are meant
to be fun, but they have a point, too. While you are working on them,
think about what the point is.

下面是学习使用Turtle的一系列练习。
它们是为了好玩而设计的，但是它们也有想表达的东西。
当你做这些练习的时候，想一想它们想告诉你的是什么。

The following sections have solutions to the exercises, so don’t look
until you have finished (or at least tried).

后面几节是这些练习的答案，因此如果你没完成（或者至少试过），不要看答案。

#. Write a function called square that takes a parameter named t, which
   is a turtle. It should use the turtle to draw a square.

   写一个名为square的函数，接受一个名为t的形参，t是一个海龟。
   这个函数应该用这只海龟画一个正方形。

   Write a function call that passes bob as an argument to square, and
   then run the program again.

   写一个函数调用，将bob作为实参传给square，然后再重新运行程序。


#. Add another parameter, named length, to square. Modify the body so
   length of the sides is length, and then modify the function call to
   provide a second argument. Run the program again. Test your program
   with a range of values for length.

   给square增加另一个名为length的形参。
   修改函数体，使得正方形边的长度是length，然后修改函数调用，提供第二个实参。
   重新运行程序。用一系列length值测试你的程序。

#. Make a copy of square and change the name to polygon. Add another
   parameter named n and modify the body so it draws an n-sided regular
   polygon. Hint: The exterior angles of an n-sided regular polygon are
   :math:`360/n` degrees.

   复制square，并将函数改名为polygon。
   增加另外一个名为n的形参并修改函数体，让它画一个正n边形（n-sided regular polygon）。
   提示：正n边形的外角是\ :math:`360/n`\ 度。

#. Write a function called circle that takes a turtle, t, and radius, r,
   as parameters and that draws an approximate circle by calling polygon
   with an appropriate length and number of sides. Test your function
   with a range of values of r.

   写一个名为circle的函数，它接受一个海龟t和半径r作为形参，
   然后通过以合适的边长和边数调用polygon，画一个近似圆形。
   用一系列r值测试你的函数。

   Hint: figure out the circumference of the circle and make sure that
   length \* n = circumference.

   提示：算出圆的周长并确保length \* n = circumference。

#. Make a more general version of circle called arc that takes an
   additional parameter angle, which determines what fraction of a
   circle to draw. angle is in units of degrees, so when angle=360, arc
   should draw a complete circle.

   完成一个更一般化（general）的circle函数，称作arc，其接受一个额外的参数angle，
   确定画多大部分的圆。angle的单位是度，因此当angle=360时， arc
   应该画一个整圆。

---

封装
-------------

The first exercise asks you to put your square-drawing code into a
function definition and then call the function, passing the turtle as a
parameter. Here is a solution:

第一个练习要求你将画正方形的代码放到函数定义中,然后调用该函数，
将海龟作为形参传递给它。下面是一个解法：

::

    def square(t):
        for i in range(4):
            t.fd(100)
            t.lt(90)

    square(bob)

The innermost statements, fd and lt are indented twice to show that they
are inside the for loop, which is inside the function definition. The
next line, square(bob), is flush with the left margin, which indicates
the end of both the for loop and the function definition.

最内部的语句，fd和lt被缩进两次，以显示它们处在for循环内，
而该循环又在函数定义内。下一行square(bob)和左边界（left margin）对齐，
表示for循环和函数定义结束。

Inside the function, t refers to the same turtle bob, so t.lt(90) has
the same effect as bob.lt(90). In that case, why not call the parameter
bob? The idea is that t can be any turtle, not just bob, so you could
create a second turtle and pass it as an argument to square:

在函数内部，t指的是同一只海龟bob， 所以t.lt(90)和bob.lt(90)的效果相同。
那么为什么不将形参命名为bob呢？ 因为t可以是任何海龟而不仅仅是bob，
也就是说你可以创建第二只海龟，并且将它作为实参传递给square：

::

    alice = Turtle()
    square(alice)

Wrapping a piece of code up in a function is called **encapsulation**.
One of the benefits of encapsulation is that it attaches a name to the
code, which serves as a kind of documentation. Another advantage is that
if you re-use the code, it is more concise to call a function twice than
to copy and paste the body!

将一部分代码包装在函数里被称作 **encapsulation（封装）**\ 。
封装的好处之一，是它为这些代码赋予一个名字，
这充当了某种文档说明。另一个好处是，如果你重复使用这些代码，
调用函数两次比拷贝粘贴函数体要更加简洁！

---

泛化
--------------

The next step is to add a length parameter to square. Here is a
solution:

下一个练习是给square增加一个length形参。下面是一个解法：

::

    def square(t, length):
        for i in range(4):
            t.fd(length)
            t.lt(90)

    square(bob, 100)

Adding a parameter to a function is called **generalization** because it
makes the function more general: in the previous version, the square is
always the same size; in this version it can be any size.

为函数增加一个形参被称作\ **泛化（generalization）**\ ，
因为这使得函数更通用：在前面的版本中，
正方形的边长总是一样的；此版本中它可以是任意大小。

The next step is also a generalization. Instead of drawing squares,
polygon draws regular polygons with any number of sides. Here is a
solution:

下一个练习也是一个泛化。不再是画一个正方形，polygon可以画任意的正多边形。
下面是一个解法：

::

    def polygon(t, n, length):
        angle = 360 / n
        for i in range(n):
            t.fd(length)
            t.lt(angle)

    polygon(bob, 7, 70)

This example draws a 7-sided polygon with side length 70.

这个示例代码画了一个七边形，边长为70。

If you are using Python 2, the value of angle might be off because of
integer division. A simple solution is to compute angle = 360.0 / n.
Because the numerator is a floating-point number, the result is floating
point.

如果你在使用Python 2，angle的值可能由于整型数除法（integer division）出现偏差。一个简单的解决办法是这样计算angle：angle = 360.0 / n。因为分子（numerator）是一个浮点数，最终的结果也会是一个浮点数。

When a function has more than a few numeric arguments, it is easy to
forget what they are, or what order they should be in. In that case it
is often a good idea to include the names of the parameters in the
argument list:

如果一个函数有几个数字实参，很容易忘记它们是什么或者它们的顺序。在这种情况下，
将在实参列表中加入形参的名称是通常是一个很好的办法：

::

    polygon(bob, n=7, length=70)

These are called **keyword arguments** because they include the
parameter names as “keywords” (not to be confused with Python keywords
like while and def).

这些被称作\ **关键字实参（keyword arguments）**\ ，
因为它们使用了形参名作为“关键字”（不要和Python的关键字搞混了，如while和def）。

This syntax makes the program more readable. It is also a reminder about
how arguments and parameters work: when you call a function, the
arguments are assigned to the parameters.

这一语法使得程序更可读。 [4]_ 它也提醒了我们实参和形参的工作方式：
当你调用函数时，实参被赋给形参。

---

接口设计
----------------

The next step is to write circle, which takes a radius, r, as a
parameter. Here is a simple solution that uses polygon to draw a
50-sided polygon:

下一个练习是写circle函数，它接受半径r作为形参。
下面是一个使用polygon画一个50边形的简单解法：

::

    import math

    def circle(t, r):
        circumference = 2 * math.pi * r
        n = 50
        length = circumference / n
        polygon(t, n, length)


The first line computes the circumference of a circle with radius r
using the formula :math:`2 \pi r`. Since we use math.pi, we have to
import math. By convention, import statements are usually at the
beginning of the script.

函数的第一行通过半径r计算圆的周长，公式是\ :math:`2 \pi r`\ 。
由于我们用了math.pi，我们需要导入math模块。
按照惯例，import语句通常位于脚本的开始位置。

n is the number of line segments in our approximation of a circle, so
length is the length of each segment. Thus, polygon draws a 50-sides
polygon that approximates a circle with radius r.

n是我们的近似圆中线段的条数，所以length是每一段的长度。
这样polygon画了一个50边形来近似一个半径为r的圆。

One limitation of this solution is that n is a constant, which means
that for very big circles, the line segments are too long, and for small
circles, we waste time drawing very small segments. One solution would
be to generalize the function by taking n as a parameter. This would
give the user (whoever calls circle) more control, but the interface
would be less clean.

这种解法的一个局限在于n是常数，意味着对于非常大的圆，
线段会非常长，而对于小圆，我们会浪费时间画非常小的线段。
一个解决方案是通过将n作为形参来泛化函数。
这将给用户（调用circle的人）更多的掌控力， 但是接口就不那么干净了。

The **interface** of a function is a summary of how it is used: what are
the parameters? What does the function do? And what is the return value?
An interface is “clean” if it allows the caller to do what they want
without dealing with unnecessary details.

函数的\ **接口（interface）**\ 是一份关于如何使用的总结：
形参是什么？函数做什么？返回值是什么？
如果接口“尽可能简单，又不过于简单（爱因斯坦）”的话，则说它是“干净的”。

In this example, r belongs in the interface because it specifies the
circle to be drawn. n is less appropriate because it pertains to the
details of *how* the circle should be rendered.

在这个例子中，r属于接口的一部分，因为它指定了要画多大的圆。
n就不太合适，因为它是关于*如何*画圆的细节。

Rather than clutter up the interface, it is better to choose an
appropriate value of n depending on circumference:

与其把接口弄乱，不如根据circumference选择一个合适的n值。

::

    def circle(t, r):
        circumference = 2 * math.pi * r
        n = int(circumference / 3) + 1
        length = circumference / n
        polygon(t, n, length)

Now the number of segments is an integer near circumference/3, so the
length of each segment is approximately 3, which is small enough that
the circles look good, but big enough to be efficient, and acceptable
for any size circle.

现在线段的数量是大小约为circumference/3的整型数，
所以每条线段的长度（大概）是3，小到足以使圆看上去不错，
又大到对任何大小的圆都又快又合适。

---

重构
-----------

When I wrote circle, I was able to re-use polygon because a many-sided
polygon is a good approximation of a circle. But arc is not as
cooperative; we can’t use polygon or circle to draw an arc.

当我写circle的时候，我能够重用polygon，
因为一个多边形是与圆形非常近似。
但是arc就不那么实现了；我们不能使用polygon或者circle来画一个弧。

One alternative is to start with a copy of polygon and transform it into
arc. The result might look like this:

一种替代方案是从复制polygon开始，
并将它转化为arc。结果看上去像这样：

::

    def arc(t, r, angle):
        arc_length = 2 * math.pi * r * angle / 360
        n = int(arc_length / 3) + 1
        step_length = arc_length / n
        step_angle = angle / n
        
        for i in range(n):
            t.fd(step_length)
            t.lt(step_angle)

The second half of this function looks like polygon, but we can’t re-use
polygon without changing the interface. We could generalize polygon to
take an angle as a third argument, but then polygon would no longer be
an appropriate name! Instead, let’s call the more general function
polyline:

该函数的后半部分看上去很像polygon，
但是在不改变接口的条件下，我们不能重用polygon。
我们可以泛化polygon来接受一个角度作为第三个实参，
但是这样polygon就不再是一个合适的名字了！
让我们称这个更通用的函数为polyline：

::

    def polyline(t, n, length, angle):
        for i in range(n):
            t.fd(length)
            t.lt(angle)

Now we can rewrite polygon and arc to use polyline:

现在，我们可以用polyline重写polygon和arc：

::

    def polygon(t, n, length):
        angle = 360.0 / n
        polyline(t, n, length, angle)

    def arc(t, r, angle):
        arc_length = 2 * math.pi * r * angle / 360
        n = int(arc_length / 3) + 1
        step_length = arc_length / n
        step_angle = float(angle) / n
        polyline(t, n, step_length, step_angle)

Finally, we can rewrite circle to use arc:

最后，我们可以用arc重写circle：

::

    def circle(t, r):
        arc(t, r, 360)

This process—rearranging a program to improve interfaces and facilitate
code re-use—is called **refactoring**. In this case, we noticed that
there was similar code in arc and polygon, so we “factored it out” into
polyline.

重新整理一个程序以改进函数接口和促进代码重用的这个过程，
被称作\ **重构（refactoring）**\ 。
在此例中，我们注意到arc和polygon中有相似的代码，
因此，我们“将它分解出来”（factor it out）放入polyline。

If we had planned ahead, we might have written polyline first and
avoided refactoring, but often you don’t know enough at the beginning of
a project to design all the interfaces. Once you start coding, you
understand the problem better. Sometimes refactoring is a sign that you
have learned something.

如果我们提前已经计划好了，我们可能会首先写polyline，避免重构，
但是在一个项目开始的时候，你常常并不知道那么多，不能设计好全部的接口。
一旦你开始编码后，你才能更好地理解该问题。
有时重构是一个说明你已经学到某些东西的预兆。

---

开发方案
------------------

A **development plan** is a process for writing programs. The process we
used in this case study is “encapsulation and generalization”. The steps
of this process are:

**开发计划（development plan）**\ 是编写程序的过程。
此例中我们使用的过程是“封装和泛化”。 这个过程的具体步骤是：

#. Start by writing a small program with no function definitions.
   从写一个没有函数定义的小程序开始。

#. Once you get the program working, identify a coherent piece of it,
   encapsulate the piece in a function and give it a name.
   一旦该程序运行正常，找出其中相关性强的部分，将它们封装进一个函数并给它一个名字。

#. Generalize the function by adding appropriate parameters.

   通过增加适当的形参泛化该函数。

#. Repeat steps 1–3 until you have a set of working functions. Copy and
   paste working code to avoid retyping (and re-debugging).
   重复1–3步，直到你有一些可正常运行的函数。
   复制粘贴有用的代码，避免重复输入（和重新调试）。

#. Look for opportunities to improve the program by refactoring. For
   example, if you have similar code in several places, consider
   factoring it into an appropriately general function.
   寻找机会通过重构改进程序。
   例如，如果在多个地方有相似的代码，考虑将它分解到一个合适的通用函数中。

This process has some drawbacks—we will see alternatives later—but it
can be useful if you don’t know ahead of time how to divide the program
into functions. This approach lets you design as you go along.

这个过程也有一些缺点—后面我们将介绍其他替代方案—
但是如果你事先不知道如何将程序分解为函数，这是个很有用办法。
该方法可以让你一边编程，一边设计。

---

文档字符串
---------

A **docstring** is a string at the beginning of a function that explains
the interface (“doc” is short for “documentation”). Here is an example:

一个\ **文档字符串（docstring）**\ 是位于函数开始位置的字符串，
解释了函数的接口（“doc”是“documentation”的缩写）。 下面是一个例子：

::

    def polyline(t, n, length, angle):
        """Draws n line segments with the given length and
        angle (in degrees) between them.  t is a turtle.
        """    
        for i in range(n):
            t.fd(length)
            t.lt(angle)

By convention, all docstrings are triple-quoted strings, also known as
multiline strings because the triple quotes allow the string to span
more than one line.

按照惯例，所有的文档字符串都是三重引号字符串，也被称为多行字符串，
因为三重引号允许字符串超过一行。

It is terse, but it contains the essential information someone would
need to use this function. It explains concisely what the function does
(without getting into the details of how it does it). It explains what
effect each parameter has on the behavior of the function and what type
each parameter should be (if it is not obvious).

它很简要（terse），但是包括了他人使用此函数时需要了解的关键信息。
它扼要地说明该函数做什么（不介绍背后的具体细节）。
它解释了每个形参对函数的行为有什么影响，以及每个形参应有的类型
（如果它不明显的话）。

Writing this kind of documentation is an important part of interface
design. A well-designed interface should be simple to explain; if you
have a hard time explaining one of your functions, maybe the interface
could be improved.

写这种文档是接口设计中很重要的一部分。 一个设计良好的接口应该很容易解释，
如果你很难解释你的某个函数，那么你的接口也许还有改进空间。

Debugging
---------

An interface is like a contract between a function and a caller. The
caller agrees to provide certain parameters and the function agrees to
do certain work.

接口就像是一个函数和调用者之间的合同。
调用者同意提供合适的参数，函数同意完成相应的工作。

For example, polyline requires four arguments: t has to be a Turtle; n
has to be an integer; length should be a positive number; and angle has
to be a number, which is understood to be in degrees.

例如，polyline函数需要4个实参：t必须是一个Turtle；
n必须是一个整型数； length应该是一个正数；
angle必须是一个数，单位是度数。

These requirements are called **preconditions** because they are
supposed to be true before the function starts executing. Conversely,
conditions at the end of the function are **postconditions**.
Postconditions include the intended effect of the function (like drawing
line segments) and any side effects (like moving the Turtle or making
other changes).

这些要求被称作\ **先决条件（preconditions）**\ ，
因为它们在函数开始执行之前应当是成立的（true）。
相反，函数结束时的条件是\ **后置条件（postconditions）**\ 。
后置条件包括函数预期的效果（如画线段）以及任何其他附带效果
（如移动Turtle或者做其它改变）。

Preconditions are the responsibility of the caller. If the caller
violates a (properly documented!) precondition and the function doesn’t
work correctly, the bug is in the caller, not the function.

先决条件由调用者负责。如果调用者违反一个（已经充分记录文档）
先决条件，导致函数没有正确工作，则故障（bug）出现在调用者一方，而不是函数。

If the preconditions are satisfied and the postconditions are not, the
bug is in the function. If your pre- and postconditions are clear, they
can help with debugging.

---

词汇表
--------

method:
    A function that is associated with an object and called using dot
    notation.

方法（method）：
    与对象相关联的函数，并使用点标记法（dot notation）调用。

loop:
    A part of a program that can run repeatedly.

循环（loop）：
    程序中能够重复执行的那部分代码。

encapsulation:
    The process of transforming a sequence of statements into a function
    definition.

封装（encapsulation）：
    将一个语句序列转换成函数定义的过程。

generalization:
    The process of replacing something unnecessarily specific (like a
    number) with something appropriately general (like a variable or
    parameter).

泛化（generalization）：
    使用某种可以算是比较通用的东西（像变量和形参），替代某些没必要那么具体的东西（像一个数字）的过程。

keyword argument:
    An argument that includes the name of the parameter as a “keyword”.

关键字实参（keyword argument）：
    包括了形参名称作为“关键字”的实参。

interface:
    A description of how to use a function, including the name and
    descriptions of the arguments and return value.

接口（interface）：
    对如何使用一个函数的描述，包括函数名、参数说明和返回值。

refactoring:
    The process of modifying a working program to improve function
    interfaces and other qualities of the code.

重构（refactoring）：
    修改一个正常运行的函数，改善函数接口及其他方面代码质量的过程。

development plan:
    A process for writing programs.

开发计划（development plan）：
    编写程序的一种过程。

docstring:
    A string that appears at the top of a function definition to
    document the function’s interface.

文档字符串（docstring）：
    出现在函数定义顶部的一个字符串，用于记录函数的接口。

precondition:
    A requirement that should be satisfied by the caller before a
    function starts.

先决条件（preconditions）：
    在函数运行之前，调用者应该满足的一个要求。

postcondition:
    A requirement that should be satisfied by the function before it
    ends.

后置条件（postconditions）：
    函数结束执行之前应该满足的一个条件。

---

练习题
---------

习题 4-1.

Download the code in this chapter from
http://thinkpython2.com/code/polygon.py.

可从\ http://thinkpython.com/code/polygon.py \ 下载本章的代码。

#. Draw a stack diagram that shows the state of the program while
   executing circle(bob, radius). You can do the arithmetic by hand or
   add print statements to the code.

   画一个执行circle(bob, radius)程序时的堆栈图（stack diagram），说明程序的各个状态。你可以手动进行计算，也可以在代码中加入print语句。

#. The version of arc in Section [refactoring] is not very accurate
   because the linear approximation of the circle is always outside the
   true circle. As a result, the Turtle ends up a few pixels away from
   the correct destination. My solution shows a way to reduce the effect
   of this error. Read the code and see if it makes sense to you. If you
   draw a diagram, you might see how it works.

   重构一节中给出的arc函数版本并不太精确，因为原型的线性近似用于处在真正的圆形之外。因此，Turtle总是和正确的终点相差几个像素。阅读其中的代码，看看是否能够理解。如果你画一个堆栈图的话，你可能会更容易明白为什么会这样。

.. figure:: figs/flowers.png
   :alt: Turtle绘制的花朵。

   Turtle绘制的花朵。

习题 4-2.

Write an appropriately general set of functions that can draw flowers as
in Figure [fig.flowers].

编写比较通用的一个函数集，可以画出像图-4-1中那样的花朵。

Solution: http://thinkpython2.com/code/flower.py, also requires
http://thinkpython2.com/code/polygon.py.

答案： http://thinkpython2.com/code/flower.py ，还要求这个模块
http://thinkpython2.com/code/polygon.py.


习题 4-3.

.. figure:: figs/pies.png
   :alt: Turtle饼状图。

   Turtle饼状图。
 
Write an appropriately general set of functions that can draw shapes as
in Figure [fig.pies].

编写比较通用的一个函数集，可以画出下面图-4-3中那样的图形。

Solution: http://thinkpython2.com/code/pie.py.

答案： http://thinkpython2.com/code/pie.py 。

The letters of the alphabet can be constructed from a moderate number of
basic elements, like vertical and horizontal lines and a few curves.
Design an alphabet that can be drawn with a minimal number of basic
elements and then write functions that draw the letters.

字母表中的字母可以由少量基本元素构成，例如竖线和横线，以及一些曲线。
设计一种可以经由最少的基本元素写出的字母表，然后编写能画出各个字母的函数。

You should write one function for each letter, with names ``draw_a``,
``draw_b``, etc., and put your functions in a file named letters.py. You
can download a “turtle typewriter” from
http://thinkpython2.com/code/typewriter.py to help you test your code.

你应该为每个字母写一个函数，起名为\ ``draw_a``\ ，\ ``draw_b``\ 等等，
然后将你的函数放在一个名为letters.py的文件里。
你可以从\ http://thinkpython.com/code/typewriter.py
下载一个“海龟打字员”来帮你测试代码。

You can get a solution from http://thinkpython2.com/code/letters.py; it
also requires http://thinkpython2.com/code/polygon.py.

你可以在 http://thinkpython2.com/code/letters.py 找到答案；这个解法还要求已经下载了 http://thinkpython2.com/code/polygon.py 。

Read about spirals at http://en.wikipedia.org/wiki/Spiral; then write a
program that draws an Archimedian spiral (or one of the other kinds).
Solution: http://thinkpython2.com/code/spiral.py.

上\ http://en.wikipedia.org/wiki/Spiral \ 阅读螺线（spiral）的相关知识；
然后编写一个绘制阿基米德螺线（或者其他种类的螺线）的程序。

答案：\ http://thinkpython.com/code/spiral.py \ 。