Files文件
=====

This chapter introduces the idea of “persistent” programs that keep data
in permanent storage, and shows how to use different kinds of permanent
storage, like files and databases.
这一章介绍了“持久（persistent）”程序的概念，即那些将数据保存在永久储存（permanent storage）中的程序。同时还展示了如何使用不同种类的永久存储，例如文件（files）和数据库（databases）。

Persistence持久性
-----------

Most of the programs we have seen so far are transient in the sense that
they run for a short time and produce some output, but when they end,
their data disappears. If you run the program again, it starts with a
clean slate.
目前我们所见到的大多数的程序都是瞬态的，即它们在短时间内运行并输出一些结果，但当它们结束时，数据也就消失了。如果你再次运行程序，它将从一个初始的状态开始。

Other programs are **persistent**: they run for a long time (or all the
time); they keep at least some of their data in permanent storage (a
hard drive, for example); and if they shut down and restart, they pick
up where they left off.
另一类程序是**持久**的：它们长时间运行（或者一直在运行）；它们至少将一部分数据记录在永久存储（如一个硬盘中）；当你关闭然后重新启动它们时，它们将从上次中断的地方开始继续。

Examples of persistent programs are operating systems, which run pretty
much whenever a computer is on, and web servers, which run all the time,
waiting for requests to come in on the network.
一个持久程序的例子是操作系统，在一台电脑开机后的绝大多数时间都在运行。另一个例子是web服务器，不停的在运行着在等待来自网络中的请求。

One of the simplest ways for programs to maintain their data is by
reading and writing text files. We have already seen programs that read
text files; in this chapter we will see programs that write them.
读写文本文件是一个程序维护它的数据的最简单的方法之一。我们已经接触过读取文本文件的程序，在本章，我们将接触写入文本的程序。

An alternative is to store the state of the program in a database. In
this chapter I will present a simple database and a module, pickle, that
makes it easy to store program data.
另一种记录程序状态的方法是使用数据库。在本章节我将给出一个简单的数据库和简化存储数据过程的pickle模块。

Reading and writing读取和写入
-------------------

A text file is a sequence of characters stored on a permanent medium
like a hard drive, flash memory, or CD-ROM. We saw how to open and read
a file in Section [wordlist].
文本文件是储存在类似硬盘，闪存，或者CD-ROM等永久介质上的字符序列。我们在章节[wordlist]中接触了文件的打开和读取。

To write a file, you have to open it with mode ``'w'`` as a second
parameter:
要写入一个文件，你必须在打开文件时用第二个参数来使用``'w'``模式：

::

    >>> fout = open('output.txt', 'w')

If the file already exists, opening it in write mode clears out the old
data and starts fresh, so be careful! If the file doesn’t exist, a new
one is created.
如果文件已经存在，那么用写入模式打开它将会清空原来的数据并从新开始，所以要小心！如果文件不存在，那么将创建一个新的文件。

open returns a file object that provides methods for working with the
file. The write method puts data into the file.
open会返回一个文件对象，一个文件对象有许多方法来对文件进行操作。write方法将数据写入文件。

::

    >>> line1 = "This here's the wattle,\n"
    >>> fout.write(line1)
    24

The return value is the number of characters that were written. The file
object keeps track of where it is, so if you call write again, it adds
the new data to the end of the file.
返回值是被写入的字符的个数。文件对象将跟踪这个位置，所以下次你调用write的时候，它会在文件末尾添加新的数据。

::

    >>> line2 = "the emblem of our land.\n"
    >>> fout.write(line2)
    24

When you are done writing, you should close the file.
当你完成文件写入，你应该关闭文件。

::

    >>> fout.close()

If you don’t close the file, it gets closed for you when the program
ends.
如果你不关闭这个文件，当程序结束时它会关闭。

Format operator格式运算符（或许翻译为操作符？）
---------------

The argument of write has to be a string, so if we want to put other
values in a file, we have to convert them to strings. The easiest way to
do that is with str:
write的参数必须是字符串，所以如果我们想要在文件中写入其它值，我们需要将他们转化为字符串。最简单的转化方法是使用str：

::

    >>> x = 52
    >>> fout.write(str(x))

An alternative is to use the **format operator**, %. When applied to
integers, % is the modulus operator. But when the first operand is a
string, % is the format operator.
另一个方法是使用**格式运算符（format operator）**，即%。在作用于整数的时候，%是取模运算符，而当第一个运算数（operand）（或者翻译为操作数？《深入理解计算机系统》中就是这么翻译的）是字符串时%是格式运算符。

The first operand is the **format string**, which contains one or more
**format sequences**, which specify how the second operand is formatted.
The result is a string.
第一个运算数是**格式字符串（format string）**，它包含一个或多个**格式序列（format sequence）**。格式序列指定了第二个运算数是如何格式化的。运算结果是一个字符串。

For example, the format sequence ``'%d'`` means that the second operand
should be formatted as a decimal integer:
例如，格式序列``'%d'``意味着第二个运算数应该被格式化为一个十进制整数：

::

    >>> camels = 42
    >>> '%d' % camels
    '42'

The result is the string ``'42'``, which is not to be confused with the
integer value 42.
结果是字符串``'42'``，需要和整数值42区分开来。

A format sequence can appear anywhere in the string, so you can embed a
value in a sentence:
一个格式序列可以出现在字符串中的任何位置，所以亦可以将一个值嵌入到一个语句中：

::

    >>> 'I have spotted %d camels.' % camels
    'I have spotted 42 camels.'

If there is more than one format sequence in the string, the second
argument has to be a tuple. Each format sequence is matched with an
element of the tuple, in order.
如果字符串中有多个格式序列，那么第二个参数必须为一个元组。每个格式序列按次序和元组中的元素对应。

The following example uses ``'%d'`` to format an integer, ``'%g'`` to
format a floating-point number, and ``'%s'`` to format a string:
下面的例子中使用``'%d'``来格式化一个整数，``'%g'``来格式化一个浮点数，以及``'%s'``来格式化一个字符串。

::

    >>> 'In %d years I have spotted %g %s.' % (3, 0.1, 'camels')
    'In 3 years I have spotted 0.1 camels.'

The number of elements in the tuple has to match the number of format
sequences in the string. Also, the types of the elements have to match
the format sequences:
元组中元素的个数必须等于字符串中格式序列的个数，同时元素的类型也必须符合对应的格式序列。

::

    >>> '%d %d %d' % (1, 2)
    TypeError: not enough arguments for format string
    >>> '%d' % 'dollars'
    TypeError: %d format: a number is required, not str

In the first example, there aren’t enough elements; in the second, the
element is the wrong type.
在第一个例子中，元组中没有足够的元素；在第二个例子中，元素的类型错误。

For more information on the format operator, see
https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting.
A more powerful alternative is the string format method, which you can
read about at
https://docs.python.org/3/library/stdtypes.html#str.format.
可以在https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting 中了解关于格式运算符的更多信息。一个更为强大的方法是使用字符串（string）的format方法，可以在https://docs.python.org/3/library/stdtypes.html#str.format 中了解它。

Filenames and paths文件名和路径
-------------------

Files are organized into **directories** (also called “folders”). Every
running program has a “current directory”, which is the default
directory for most operations. For example, when you open a file for
reading, Python looks for it in the current directory.
文件以**目录（directory）**（也称为“文件夹（folder）”）的形式组织起来。每个正在运行的程序都有一个“当前目录（current directory）”作为大多数操作的默认目录。例如，当你打开一个文件夹来读取时，Python在当前目录下寻找这个文件。

The os module provides functions for working with files and directories
(“os” stands for “operating system”). os.getcwd returns the name of the
current directory:
os模块提供了操作文件和目录的函数（“os”代表“operating system”）。os.getcwd返回当前目录的名称。

::

    >>> import os
    >>> cwd = os.getcwd()
    >>> cwd
    '/home/dinsdale'

cwd stands for “current working directory”. The result in this example
is /home/dinsdale, which is the home directory of a user named dinsdale.
cwd代表“current working directory”，即“当前工作目录”。在本例中返回结果是/home/dinsdale，即用户名为dinsdale的主目录。

A string like ``'/home/dinsdale'`` that identifies a file or directory
is called a **path**.
一个类似``'/home/dinsdale'``的确定了一个文件或者目录的字符串叫做**路径（path）**。

A simple filename, like memo.txt is also considered a path, but it is a
**relative path** because it relates to the current directory. If the
current directory is /home/dinsdale, the filename memo.txt would refer
to /home/dinsdale/memo.txt.
一个简单的文件名例如memo.txt同样被看做是一个路径，只不过是**相对路径（relative path）**，因为它是和当前目录相联系了。如果当前目录是/home/dinsdale，那么文件名memo.txt就代表/home/dinsdale/memo.txt。

A path that begins with / does not depend on the current directory; it
is called an **absolute path**. To find the absolute path to a file, you
can use os.path.abspath:
一个以/开头的路径和当前目录无关，叫做“绝对路径（absolute path）”。要找一个文件的绝对路径，你可以使用os.path.abspath。

::

    >>> os.path.abspath('memo.txt')
    '/home/dinsdale/memo.txt'

os.path provides other functions for working with filenames and paths.
For example, os.path.exists checks whether a file or directory exists:
os.path提供其它函数来对文件名和路径进行操作。例如，os.paht.exists检查一个文件或者目录是否存在：

::

    >>> os.path.exists('memo.txt')
    True

If it exists, os.path.isdir checks whether it’s a directory:
如果存在，os.path.isdir可以检查它是否是一个目录：

::

    >>> os.path.isdir('memo.txt')
    False
    >>> os.path.isdir('/home/dinsdale')
    True

Similarly, os.path.isfile checks whether it’s a file.
类似的，os.path.isfile检查它是否是一个文件。

os.listdir returns a list of the files (and other directories) in the
given directory:
os.listdir返回给定目录下的文件列表（以及其它目录）。

::

    >>> os.listdir(cwd)
    ['music', 'photos', 'memo.txt']

To demonstrate these functions, the following example “walks” through a
directory, prints the names of all the files, and calls itself
recursively on all the directories.
为了演示这些函数，下面的例子“走过”一个目录，打印所有文件的名字，并且递归的调用自身。

::

    def walk(dirname):
        for name in os.listdir(dirname):
            path = os.path.join(dirname, name)

            if os.path.isfile(path):
                print(path)
            else:
                walk(path)

os.path.join takes a directory and a file name and joins them into a
complete path.
os.path.join读取一个目录和一个文件名并把它们合并成一个完整的路径。

The os module provides a function called walk that is similar to this
one but more versatile. As an exercise, read the documentation and use
it to print the names of the files in a given directory and its
subdirectories. You can download my solution from
http://thinkpython2.com/code/walk.py.
os模块提供提供了一个叫做walk的函数，和我们写的类似但是功能更加更富。作为练习，阅读文档并且使用walk打印出给定目录下的文件名和子目录。你可以从http://thinkpython2.com/code/walk.py 下载我的解答。

Catching exceptions捕获异常
-------------------

A lot of things can go wrong when you try to read and write files. If
you try to open a file that doesn’t exist, you get an IOError:
当你试图读写文件的时候，很多地方会发生错误。如果你试图打开一个不存在的文件夹，会得到一个输入输出错误（IOError）：

::

    >>> fin = open('bad_file')
    IOError: [Errno 2] No such file or directory: 'bad_file'

If you don’t have permission to access a file:
如果你没有权限访问一个文件：

::

    >>> fout = open('/etc/passwd', 'w')
    PermissionError: [Errno 13] Permission denied: '/etc/passwd'

And if you try to open a directory for reading, you get
如果你试图打开一个目录来读取，你会得到：

::

    >>> fin = open('/home')
    IsADirectoryError: [Errno 21] Is a directory: '/home'

To avoid these errors, you could use functions like os.path.exists and
os.path.isfile, but it would take a lot of time and code to check all
the possibilities (if “Errno 21” is any indication, there are at least
21 things that can go wrong).
为了避免这些错误，你可以使用类似os.path.exists和os.path.isfile的函数来检查，但这将会耗费大量的时间和代码去检查所有的可能性（如果“Errno 21”是一个指示信息，那么至少有21种可能出错的情况）。

It is better to go ahead and try—and deal with problems if they
happen—which is exactly what the try statement does. The syntax is
similar to an if...else statement:
更好的办法是当问题出现的时候才去处理，而这正是try语句做的事情。它的语法类似if语句：

::

    try:
        fin = open('bad_file')
    except:
        print('Something went wrong.')

Python starts by executing the try clause. If all goes well, it skips
the except clause and proceeds. If an exception occurs, it jumps out of
the try clause and runs the except clause.
Python从try语句开始执行，如果一切正常，那么except语句将被跳过；如果发生异常，则跳出try语句，执行except语句。

Handling an exception with a try statement is called **catching** an
exception. In this example, the except clause prints an error message
that is not very helpful. In general, catching an exception gives you a
chance to fix the problem, or try again, or at least end the program
gracefully.
使用try语句处理异常被称为是“捕获（catching）”。在本例中，except语句打印出一个并非很有帮助的错误信息。挺长来说，捕获异常给了你修补问题的机会，你可以继续尝试，或者至少可以优雅的结束程序。

Databases数据库
---------

A **database** is a file that is organized for storing data. Many
databases are organized like a dictionary in the sense that they map
from keys to values. The biggest difference between a database and a
dictionary is that the database is on disk (or other permanent storage),
so it persists after the program ends.
一个**数据库**是一个用来存储数据的文集。大多数的数据库采用字典的形式，即将键映射到值。数据库和字典的最大区别是数据库是存储在硬盘上（或者其他永久存储中），所以即使程序结束它们依然存在。

The module dbm provides an interface for creating and updating database
files. As an example, I’ll create a database that contains captions for
image files.
dbm模块提供了一个创建和更新数据库文件的接口。作为例子，我将船建一个包含图片文件标题的数据库。

Opening a database is similar to opening other files:
打开数据库和打开其它文件类似：

::

    >>> import dbm
    >>> db = dbm.open('captions', 'c')

The mode ``'c'`` means that the database should be created if it doesn’t
already exist. The result is a database object that can be used (for
most operations) like a dictionary.
模式 ``'c'`` 代表如果数据库不存在则被创建。这个操作的返回结果是一个数据库对象，可以像字典一样使用它（对于大多数操作）。

When you create a new item, dbm updates the database file.
当你创建一个新项目时，dnm将更新数据库文件。

::

    >>> db['cleese.png'] = 'Photo of John Cleese.'

When you access one of the items, dbm reads the file:
当你访问某个项目时，dbm将读取文件：

::

    >>> db['cleese.png']
    b'Photo of John Cleese.'

The result is a **bytes object**, which is why it begins with b. A bytes
object is similar to a string in many ways. When you get farther into
Python, the difference becomes important, but for now we can ignore it.
返回结果是一个**字节对象（bytes object）**，这就是为什么以b开头。一个字节对象在很多方面都和一个字符串很像。当你深入了解Python时它们之间的差别会变得很重要，但是目前我们可以忽略掉那些差别。

If you make another assignment to an existing key, dbm replaces the old
value:
如果你对已有的键再次进行赋值，dbm将把旧的值替换掉：

::

    >>> db['cleese.png'] = 'Photo of John Cleese doing a silly walk.'
    >>> db['cleese.png']
    b'Photo of John Cleese doing a silly walk.'

Some dictionary methods, like keys and items, don’t work with database
objects. But iteration with a for loop works:
一些字典方法，例如keys和items将不适用于数据库对象，但是for循环依然适用：

::

    for key in db:
        print(key, db[key])

As with other files, you should close the database when you are done:
像其它文件一样，当你完成操作后需要关闭文件：

::

    >>> db.close()

Pickling序列化
--------

A limitation of dbm is that the keys and values have to be strings or
bytes. If you try to use any other type, you get an error.
dbm的一个限制在于键和值必须是字符串或者字节。如果你尝试去用其它数据类型，你会得到以一个错误。

The pickle module can help. It translates almost any type of object into
a string suitable for storage in a database, and then translates strings
back into objects.
pickle模块可以解决这个问题。它能将几乎所有类型的对象转化为适合在数据库中存储的字符串，以及将那些字符串还原为原来的对象。

pickle.dumps takes an object as a parameter and returns a string
representation (dumps is short for “dump string”):
pickle.dumps读取一个对象作为参数，并返回一个字符串表示（string representation）（dumps是“dump string（转储字符串）”的缩写）：

::

    >>> import pickle
    >>> t = [1, 2, 3]
    >>> pickle.dumps(t)
    b'\x80\x03]q\x00(K\x01K\x02K\x03e.'

The format isn’t obvious to human readers; it is meant to be easy for
pickle to interpret. pickle.loads (“load string”) reconstitutes the
object:
这个格式对人类来说不是很直观，但是对pickle来说很容易去解释。pickle.loads（“load string”，载入字符串）可以重建对象：

::

    >>> t1 = [1, 2, 3]
    >>> s = pickle.dumps(t1)
    >>> t2 = pickle.loads(s)
    >>> t2
    [1, 2, 3]

Although the new object has the same value as the old, it is not (in
general) the same object:
尽管新对象和旧对象有相同的值，但它们（在一般意义上来说）不是同一个对象：

::

    >>> t1 == t2
    True
    >>> t1 is t2
    False

In other words, pickling and then unpickling has the same effect as
copying the object.
换言之，序列化然后反序列化等效于复制一个对象。

You can use pickle to store non-strings in a database. In fact, this
combination is so common that it has been encapsulated in a module
called shelve.
你可以使用pickle来将存储非字符串对象存储在数据库中。事实上，这个组合非常常用，已经被封装进了模块shelve中。

Pipes管道
-----

Most operating systems provide a command-line interface, also known as a
**shell**. Shells usually provide commands to navigate the file system
and launch applications. For example, in Unix you can change directories
with cd, display the contents of a directory with ls, and launch a web
browser by typing (for example) firefox.
大多数的操作系统西贡一个命令行的接口，称为**shell**。shell通常提供浏览文件系统和启动程序的命令。例如，在Unix中你可以使用cd改变目录，使用ls显示一个目录的内容，通过输入firefox（举例来说）来启动一个网页浏览器。

Any program that you can launch from the shell can also be launched from
Python using a **pipe object**, which represents a running program.
任何你在shell中可以启动的程序也可以在Python中通过使用**管道对象（pipe object）**来启动。一个管道是一个表示活动进程的对象。

For example, the Unix command ls -l normally displays the contents of
the current directory in long format. You can launch ls with
os.popen [1]_:
例如，Unix命令ls -l将以详细格式显示当前目录下的内容。你可以使用op.popen [1]_来启动ls：

::

    >>> cmd = 'ls -l'
    >>> fp = os.popen(cmd)

The argument is a string that contains a shell command. The return value
is an object that behaves like an open file. You can read the output
from the ls process one line at a time with readline or get the whole
thing at once with read:
参数是一个包含shell命令的字符串，就像打开文件一样，返回值是一个对象。你可以使用readline来每次从ls进程的输出中读取一行，或者使用read来一次读取所有内容：

::

    >>> res = fp.read()

When you are done, you close the pipe like a file:
当你完成操作后，像关闭一个文件一样关闭管道：

::

    >>> stat = fp.close()
    >>> print(stat)
    None

The return value is the final status of the ls process; None means that
it ended normally (with no errors).
返回值是ls进程的最终状态。None表示（没有错误的）正常结束。

For example, most Unix systems provide a command called md5sum that
reads the contents of a file and computes a “checksum”. You can read
about MD5 at http://en.wikipedia.org/wiki/Md5. This command provides an
efficient way to check whether two files have the same contents. The
probability that different contents yield the same checksum is very
small (that is, unlikely to happen before the universe collapses).
例如，大多数Unix系统提供一个叫做md5sum的命令来读取一个文件的内容并计算出一个“校验和（checksum）”。你可以在http://en.wikipedia.org/wiki/Md5 中了解更多MD5的信息。不同内容产生相同校验和的概率非常小（即是说在宇宙坍塌之前是不可能的）。

You can use a pipe to run md5sum from Python and get the result:
你可以使用一个管道来从Python中运行md5sum并得到计算结果：

::

    >>> filename = 'book.tex'
    >>> cmd = 'md5sum ' + filename
    >>> fp = os.popen(cmd)
    >>> res = fp.read()
    >>> stat = fp.close()
    >>> print(res)
    1e0033f0ed0656636de0d75144ba32e0  book.tex
    >>> print(stat)
    None

Writing modules编写模块
---------------

Any file that contains Python code can be imported as a module. For
example, suppose you have a file named wc.py with the following code:
任何包含Python代码的文件可以作为模块被导入。例如，假设你有包含以下代码的文件wc.py：

::

    def linecount(filename):
        count = 0
        for line in open(filename):
            count += 1
        return count

    print(linecount('wc.py'))

If you run this program, it reads itself and prints the number of lines
in the file, which is 7. You can also import it like this:
如果你运行这个程序，它将读取自身并打印文件的行数，结果是7.你也可以这样导入模块：

::

    >>> import wc
    7

Now you have a module object wc:
现在你有了一个模块对象wc：

::

    >>> wc
    <module 'wc' from 'wc.py'>

The module object provides ``linecount``:
这个模块对象提供了``linecount``函数：

::

    >>> wc.linecount('wc.py')
    7

So that’s how you write modules in Python.
以上就是如何编写Python模块。

The only problem with this example is that when you import the module it
runs the test code at the bottom. Normally when you import a module, it
defines new functions but it doesn’t run them.
这个例子中唯一的问题在于当你导入模块后，它将自动运行其中的代码。通常当你导入一个模块时，你定义了一些新的函数，但是并不运行它们。

Programs that will be imported as modules often use the following idiom:
作为模块的程序通常写成一下结构：

::

    if __name__ == '__main__':
        print(linecount('wc.py'))

``__name__`` is a built-in variable that is set when the program starts.
If the program is running as a script, ``__name__`` has the value
``'__main__'``; in that case, the test code runs. Otherwise, if the
module is being imported, the test code is skipped.
``__name__`` 是一个在程序开始时设置好的内建变量。如果程序以脚本的形式运行，``__name__`` 的值为 ``__main__`` ，这时其中的代码将被执行。否则当被作为模块导入时，其中的代码将被跳过。

As an exercise, type this example into a file named wc.py and run it as
a script. Then run the Python interpreter and import wc. What is the
value of ``__name__`` when the module is being imported?
作为练习，将例子输入到文件wc.py中去然后以脚本形式运行。接着，打开Python解释器并导入wc。当模块被导入后``__name__``的值是什么？

Warning: If you import a module that has already been imported, Python
does nothing. It does not re-read the file, even if it has changed.
警告：如果你导入一个已经被导入了的模块，Python将不会做任何事情。它并不会重新读取文件，即使文件的内容已经发生了改变。

If you want to reload a module, you can use the built-in function
reload, but it can be tricky, so the safest thing to do is restart the
interpreter and then import the module again.
如果你要重载一个模块，可以使用内建函数reload，但它可能会出错。因此最安全的方法是重启解释器然后重新导入模块。

Debugging调试
---------

When you are reading and writing files, you might run into problems with
whitespace. These errors can be hard to debug because spaces, tabs and
newlines are normally invisible:
当你读写文件时，可能会遇到空白带来的问题。这些问题会很难调试因为空格、制表符和换行符通常是看不见的：

::

    >>> s = '1 2\t 3\n 4'
    >>> print(s)
    1 2  3
     4

The built-in function repr can help. It takes any object as an argument
and returns a string representation of the object. For strings, it
represents whitespace characters with backslash sequences:
内建函数repr可以用来解决这个问题。它读取任意一个作为参数，并返回一个该对象的字符串表示。对于空白符号它将用反斜杠序列表示：

::

    >>> print(repr(s))
    '1 2\t 3\n 4'

This can be helpful for debugging.
这个对于调试会很有用。

One other problem you might run into is that different systems use
different characters to indicate the end of a line. Some systems use a
newline, represented ``\n``. Others use a return character, represented
``\r``. Some use both. If you move files between different systems,
these inconsistencies can cause problems.
另一个你可能会遇到的问题是不同的的系统使用不同的符号来表示一行的结束。有些系统使用一个换行符 ``\n`` ，有的使用一个返回符号 ``\r`` ，有些两者都使用。如果你在不同的系统中移动文件，这些差异会导致问题。

For most systems, there are applications to convert from one format to
another. You can find them (and read more about this issue) at
http://en.wikipedia.org/wiki/Newline. Or, of course, you could write one
yourself.
对大多数的系统，有一些在不同格式之间进行转换的应用。你可以在http://en.wikipedia.org/wiki/Newline 中找到（并阅读更多相关内容）。当然你也可以自己编写一个转换程序。

Glossary术语
--------

persistent:
    Pertaining to a program that runs indefinitely and keeps at least
    some of its data in permanent storage.
持久性：
	对于程序来说就是长期的运行并至少将一部分自身的数据保存在永久存储中。

format operator:
    An operator, %, that takes a format string and a tuple and generates
    a string that includes the elements of the tuple formatted as
    specified by the format string.
格式运算符：
	运算符%。读取一个格式字符串和一个元组，生成一个包含元组中元素的字符串，那些元组中的元素已经按照格式字符串指定的方式格式化。

format string:
    A string, used with the format operator, that contains format
    sequences.
格式字符串：
	一个包含格式序列的和和格式运算符一起使用的字符串。

format sequence:
    A sequence of characters in a format string, like %d, that specifies
    how a value should be formatted.
格式序列：
	格式字符串中的一个字符序列，例如%d，指定了一个值的格式。

text file:
    A sequence of characters stored in permanent storage like a hard
    drive.
文本文件：
	保存在类似硬盘的永久存储设备上的字符序列。

directory:
    A named collection of files, also called a folder.
目录：
	一个被命名的文件的集合，也叫做文件夹。

path:
    A string that identifies a file.
路径：
	一个指定一个文件的字符串。

relative path:
    A path that starts from the current directory.
相对路径：
	从当前目录开始的路径。

absolute path:
    A path that starts from the topmost directory in the file system.
绝对路径：
	从文件系统顶部开始的路径。

catch:
    To prevent an exception from terminating a program using the try and
    except statements.
捕获：
	为了防止程序因为异常而终止，使用try和except语句来捕捉异常。

database:
    A file whose contents are organized like a dictionary with keys that
    correspond to values.
数据库：
	一个内容结构类似字典的使用键值对的文件。

bytes object:
    An object similar to a string.
字节对象：
	和字符串类的对象。

shell:
    A program that allows users to type commands and then executes them
    by starting other programs.
shell：
	一个允许用户输入命令，并通过启用其它程序执行命令的程序。

pipe object:
    An object that represents a running program, allowing a Python
    program to run commands and read the results.
管道对象：
	一个代表某个运行的程序的对象。允许一个Python程序去运行命令并得到运行结果。

Exercises练习
---------

Write a function called sed that takes as arguments a pattern string, a
replacement string, and two filenames; it should read the first file and
write the contents into the second file (creating it if necessary). If
the pattern string appears anywhere in the file, it should be replaced
with the replacement string.
写一个叫做sed的函数，它的参数是一个模式字符串，一个替换字符串和两个文件名。它应该读第一个文件并将内容写入到第二个文件（需要时创建它）。如果在文件的任何地方出现了模式字符串，就用替换字符串替换它。

If an error occurs while opening, reading, writing or closing files,
your program should catch the exception, print an error message, and
exit. Solution: http://thinkpython2.com/code/sed.py.
如果在打开、读取、写入或者关闭文件时出现了错误，你的程序应该捕获这个异常，打印一个错误信息，并推出。解答：http://thinkpython2.com/code/sed.py。

If you download my solution to Exercise [anagrams] from
http://thinkpython2.com/code/anagram_sets.py, you’ll see that it creates
a dictionary that maps from a sorted string of letters to the list of
words that can be spelled with those letters. For example, ``'opst'``
maps to the list ``['opts', 'post', 'pots', 'spot', 'stop', 'tops']``.
如果你从http://thinkpython2.com/code/anagram_sets.py 下载了我对于练习[anagrams]的解答，你会看到解答中创建了一个字典，字典是从一个排序后的字母组成的字符串映射到一个可以由这些字母拼成的单词组成的列表。例如，``'opst'``映射到列表``['opts', 'post', 'pots', 'spot', 'stop', 'tops']``。

Write a module that imports ``anagram_sets`` and provides two new
functions: ``store_anagrams`` should store the anagram dictionary in a
“shelf”; ``read_anagrams`` should look up a word and return a list of
its anagrams. Solution: http://thinkpython2.com/code/anagram_db.py.
写一个模块，其中导入``anagram_sets``并提供两个新函数：函数``store_anagrams``在“shelf”中保存anagram字典；``read_anagrams``查找一个单词并返回它的anagram列表。解答：http://thinkpython2.com/code/anagram_db.py。

[checksum]
校验和

In a large collection of MP3 files, there may be more than one copy of
the same song, stored in different directories or with different file
names. The goal of this exercise is to search for duplicates.
在一个很大的MP3文件集合中，或许会有同一首歌的不同拷贝，它们存放在不同的目录下或者有不同的名字。这个练习的目的是搜索出这些拷贝。

#. Write a program that searches a directory and all of its
   subdirectories, recursively, and returns a list of complete paths for
   all files with a given suffix (like .mp3). Hint: os.path provides
   several useful functions for manipulating file and path names.

#. 写一个程序来搜索一个目录和它的所有子目录，并返回一个列表，包含所有的有给定后缀（例如.mp3）的文件的完整路径。提示：os.path提供了一些有用的操作文件和路径名的函数。

#. To recognize duplicates, you can use md5sum to compute a “checksum”
   for each files. If two files have the same checksum, they probably
   have the same contents.

#. 为了识别副本，你可以使用md5sum来计算每个文件的“校验和”。如果两个文件的校验和相同，它们很可能有相同的内容。

#. To double-check, you can use the Unix command diff.

#. 你可以使用Unix命令diff来检验一下。

Solution: http://thinkpython2.com/code/find_duplicates.py.
解答：http://thinkpython2.com/code/find_duplicates.py。
