Strings - 字符串
=======

Strings are not like integers, floats, and booleans. A string is a
**sequence**, which means it is an ordered collection of other values.
In this chapter you’ll see how to access the characters that make up a
string, and you’ll learn about some of the methods strings provide.

字符串不像整数, 浮点数, 和布鲁尔型. 一个字符串是一个**序列(sequence)**, 这就意味着
它是其他值的一个有序的集合. 在这章你会看到怎么去访问字符串里的字符, 同时你也会学习到一
些字符串提供的方法.


A string is a sequence - 字符串是一个序列
----------------------

A string is a sequence of characters. You can access the characters one
at a time with the bracket operator:

一个字符就是一些字符的序列. 你可以用括号运算符一次访问一个字符: 


::

    >>> fruit = 'banana'
    >>> letter = fruit[1]

The second statement selects character number 1 from fruit and assigns
it to letter.

第2条语句从fruit中选择编号为1的字符并将它赋给letter. 

The expression in brackets is called an **index**. The index indicates
which character in the sequence you want (hence the name).

括号中的表达式被称作**索引(index)**.索引指出在序列中你想要哪个字符(因此而得名).

But you might not get what you expect:

但是你可能不会获得你期望的东西:

::

    >>> letter
    'a'

For most people, the first letter of ``'banana'`` is b, not a. But for
computer scientists, the index is an offset from the beginning of the
string, and the offset of the first letter is zero.

对于大多数人,'banana'的第一个字母是b而不是a。 但是对于计算机科学家,索引是从字
符串开始的偏移量, 并且第一个字母的偏移量是0。

::

    >>> letter = fruit[0]
    >>> letter
    'b'

So b is the 0th letter (“zero-eth”) of ``'banana'``, a is the 1th letter
(“one-eth”), and n is the 2th letter (“two-eth”).

所以b是'banana'的第0个字母(“zero-eth”), a是第1个字母(“one-eth”),n是第2个字
母(“two-eth”)。

As an index you can use an expression that contains variables and
operators:

你可以使用一个包含变量名和运算符的表达式作为索引:

::

    >>> i = 1
    >>> fruit[i]
    'a'
    >>> fruit[i+1]
    'n'

But the value of the index has to be an integer. Otherwise you get:

但是索引的值必须是一个整数。否则你会得到:

::

    >>> letter = fruit[1.5]
    TypeError: string indices must be integers

len
---

len is a built-in function that returns the number of characters in a
string:

len是一个内建函数,其返回字符串中的字符数:

::

    >>> fruit = 'banana'
    >>> len(fruit)
    6

To get the last letter of a string, you might be tempted to try
something like this:

为了获得一个字符串的最后一个字符, 你可能想尝试像这样:

::

    >>> length = len(fruit)
    >>> last = fruit[length]
    IndexError: string index out of range

The reason for the IndexError is that there is no letter in ’banana’
with the index 6. Since we started counting at zero, the six letters are
numbered 0 to 5. To get the last character, you have to subtract 1 from
length:

IndexError的理由是在’banana’中没有索引为6的字母。 既然我们从0开始数数,6个字母
的编号是0到5。 为了获得最后一个字符,你必须从length中减1。

::

    >>> last = fruit[length-1]
    >>> last
    'a'

Or you can use negative indices, which count backward from the end of
the string. The expression fruit[-1] yields the last letter, fruit[-2]
yields the second to last, and so on.

或者你可以使用负索引,其从字符串的结尾往后数。表达式fruit[-1]产生最后 一个字母,
fruit[-2]产生倒数第二个字母, 以此类推。

Traversal with a for loop - 使用for循环遍历
-------------------------

A lot of computations involve processing a string one character at a
time. Often they start at the beginning, select each character in turn,
do something to it, and continue until the end. This pattern of
processing is called a **traversal**. One way to write a traversal is
with a while loop:

许多计算每次处理一个字符串的字符。 它们经常从头开始,依次选择每个字符,对其做一些工作,
然后继续直到结束。 词处理模式被称作**遍历**(traversal)。 一种写遍历的方法是使用
while循环:

::

    index = 0
    while index < len(fruit):
        letter = fruit[index]
        print(letter)
        index = index + 1

This loop traverses the string and displays each letter on a line by
itself. The loop condition is index < len(fruit), so when index is equal
to the length of the string, the condition is false, and the body of the
loop doesn’t run. The last character accessed is the one with the index
len(fruit)-1, which is the last character in the string.

该循环遍历字符串并在每行显示一个字符串。该循环的条件是index < len(fruit), 所以当
index和字符串的长度相等时, 条件为假, 并且循环体不被执行。 被访问的最后一个字符的索
引为len(fruit)-1, 这是字符串的最后一个字符。

As an exercise, write a function that takes a string as an argument and
displays the letters backward, one per line.

作为一个练习, 写一个函数, 它将一个字符串作为参数, 按照从后向前的顺序每行只显示一个字符.

Another way to write a traversal is with a for loop:

另一种写遍历的方法是用for循环:

::

    for letter in fruit:
        print(letter)

Each time through the loop, the next character in the string is assigned
to the variable letter. The loop continues until no characters are left.

每次通过循环,字符串中的下一个字符被赋给变量char。 循环继续,直到没有剩余的字符串了。

The following example shows how to use concatenation (string addition)
and a for loop to generate an abecedarian series (that is, in
alphabetical order). In Robert McCloskey’s book *Make Way for
Ducklings*, the names of the ducklings are Jack, Kack, Lack, Mack, Nack,
Ouack, Pack, and Quack. This loop outputs these names in order:

下面的例子显示如何使用叠加(字符串相加)和for循环生成一个字母序列(以字母序)。 
在Robert McCloskey的书《Make Way for Ducklings》中, 小鸭子的名字是
Jack, Kack, Lack, Mack, Nack, Ouack, Pack, and Quack。此循环按顺
序输出这些名字:


::

    prefixes = 'JKLMNOPQ'
    suffix = 'ack'

    for letter in prefixes:
        print(letter + suffix)

The output is:

::

    Jack
    Kack
    Lack
    Mack
    Nack
    Oack
    Pack
    Qack

Of course, that’s not quite right because “Ouack” and “Quack” are
misspelled. As an exercise, modify the program to fix this error.

当然,这不是非常正确,因为“Ouack”和“Quack”被错误拼写了。作为一个练习, 修改这
个程序使之正确。

String slices - 字符串切片
-------------

A segment of a string is called a **slice**. Selecting a slice is
similar to selecting a character:

一段字符串被称作**切片(slice)**。 选择一个切片类似于选择一个字符:

::

    >>> s = 'Monty Python'
    >>> s[0:5]
    'Monty'
    >>> s[6:12]
    'Python'

The operator returns the part of the string from the “n-eth” character
to the “m-eth” character, including the first but excluding the last.
This behavior is counterintuitive, but it might help to imagine the
indices pointing *between* the characters, as in Figure [fig.banana].

[n:m]操作符返回从第n个字符到第m个字符的部分字符串, 包括第一个, 但是不包括最后一个。 
这个行为违反直觉,但是它可能会帮助想象指向这两个字符之间的索引, 如图 [fig.banana]。

.. figure:: figs/banana.pdf
   :alt: Slice indices.

   Slice indices.

If you omit the first index (before the colon), the slice starts at the
beginning of the string. If you omit the second index, the slice goes to
the end of the string:

如果你省略第一个索引(冒号前面的),切片起始于字符串首位。 如果你省略第二个索引,切片一直
到字符串结尾:

::

    >>> fruit = 'banana'
    >>> fruit[:3]
    'ban'
    >>> fruit[3:]
    'ana'

If the first index is greater than or equal to the second the result is
an **empty string**, represented by two quotation marks:

::

    >>> fruit = 'banana'
    >>> fruit[3:3]
    ''

An empty string contains no characters and has length 0, but other than
that, it is the same as any other string.

一个空字符串不包括字符而且长度为0,但除此之外, 它和其它任何字符串一样。

Continuing this example, what do you think fruit[:] means? Try it and
see.

继续这个例子, 你认为fruit[:]是什么. 尝试运行看看。

Strings are immutable - 字符串是不可变的
---------------------

It is tempting to use the operator on the left side of an assignment,
with the intention of changing a character in a string. For example:

在一个赋值的左边使用[]很有诱惑力, 意图是改变字符串的一个字符。 例如:

::

    >>> greeting = 'Hello, world!'
    >>> greeting[0] = 'J'
    TypeError: 'str' object does not support item assignment

The “object” in this case is the string and the “item” is the character
you tried to assign. For now, an object is the same thing as a value,
but we will refine that definition later (Section [equivalence]).

此例中的“object(对象)”是该字符串,“item(项)”是你要赋值的字符。到目前, 
一个对象(object)和值是同一样的东西, 但是我们后面将改进此定义(10.10对象和值). 

The reason for the error is that strings are **immutable**, which means
you can’t change an existing string. The best you can do is create a new
string that is a variation on the original:

此错误的原因是字符串是**不可变的(immutable)**, 这意味着你不能改变一个已存在的字符串。 
最好是生成一个新的字符串,它是原字符串的一个变种:

::

    >>> greeting = 'Hello, world!'
    >>> new_greeting = 'J' + greeting[1:]
    >>> new_greeting
    'Jello, world!'

This example concatenates a new first letter onto a slice of greeting.
It has no effect on the original string.

此例连接一个新的第一个字母到greeting的一个切片上。它不影响原字符串。

Searching - 搜索
---------

What does the following function do?

下面的函数做什么?

::

    def find(word, letter):
        index = 0
        while index < len(word):
            if word[index] == letter:
                return index
            index = index + 1
        return -1

In a sense, find is the inverse of the operator. Instead of taking an
index and extracting the corresponding character, it takes a character
and finds the index where that character appears. If the character is
not found, the function returns -1.

在某种意义上,find和[]运算符相反。与接受一个索引并抽取相应的字符不同, 它接受一个
字符并找到该字符出现的位置的索引。如果没有找到该字符,函数返回-1。

This is the first example we have seen of a return statement inside a
loop. If word[index] == letter, the function breaks out of the loop and
returns immediately.

这是我们已经见过的第一个return语句在循环内部的例子。如果word[index] == letter,
函数停止循环并马上返回。

If the character doesn’t appear in the string, the program exits the
loop normally and returns -1.

如果字符没出现在字符串中,那么程序正常退出循环并返回-1。

This pattern of computation—traversing a sequence and returning when we
find what we are looking for—is called a **search**.

这种计算的模式—遍历一个序列并在我们找到我们正在寻找的东西时返回— 被称作**搜索(search)**。

As an exercise, modify find so that it has a third parameter, the index
in word where it should start looking.

作为一个练习, 修改这个函数使得它有第三个参数, 作为在何处开始搜索的索引.

Looping and counting-循环和计数
--------------------

The following program counts the number of times the letter a appears in
a string:

下面的程序计算字母a在字符串中出现的次数:

::

    word = 'banana'
    count = 0
    for letter in word:
        if letter == 'a':
            count = count + 1
    print(count)

This program demonstrates another pattern of computation called a
**counter**. The variable count is initialized to 0 and then incremented
each time an a is found. When the loop exits, count contains the
result—the total number of a’s.

此程序演示另一种被称作**计数器(counter)**的计算模式。变量count初始化为0然后
每次出现a时递增。当循环结束时,count包含结果—a的总数。

As an exercise, encapsulate this code in a function named count, and
generalize it so that it accepts the string and the letter as arguments.

作为一个练习, 将这段代码包含在一个函数中, 命名为count, 并且使得这个函数更一般化, 
能够接受字符串和字母作为参数.

Then rewrite the function so that instead of traversing the string, it
uses the three-parameter version of find from the previous section.

然后重写这个函数, 取代遍历字符串, 它使用前一部分的含有第三个参数的版本.

String methods-字符串方法
--------------

Strings provide methods that perform a variety of useful operations. A
method is similar to a function—it takes arguments and returns a
value—but the syntax is different. For example, the method upper takes a
string and returns a new string with all uppercase letters.

字符串提供了一些**方法(method)**, 这些方法可以做各种有用的运算. 方法和函数类似
—接受参数并返回一个值—但是语法不同。 例如, **upper**方法接受一个字符串并返回一
个新的都是大写字母的字符串:

Instead of the function syntax upper(word), it uses the method syntax
word.upper().

不是用函数的语法upper(word), 而是用方法的语法word.upper()。

::

    >>> word = 'banana'
    >>> new_word = word.upper()
    >>> new_word
    'BANANA'

This form of dot notation specifies the name of the method, upper, and
the name of the string to apply the method to, word. The empty
parentheses indicate that this method takes no arguments.

点标记法的形式指出方法的名字,upper,以及应用该方法的字符串的名字,word. 空括号指出该方法不接受实参。

A method call is called an **invocation**; in this case, we would say
that we are invoking upper on word.

方法的调用被称作**调用(invocation)**,在此例中, 我们说我们正在word上调用upper。

As it turns out, there is a string method named find that is remarkably
similar to the function we wrote:

事实上,有一个被称为find的字符串方法, 其和我们写的函数异常相似:

::

    >>> word = 'banana'
    >>> index = word.find('a')
    >>> index
    1

In this example, we invoke find on word and pass the letter we are
looking for as a parameter.

此例中,我们在word上调用find并将我们要找的字母作为参数。

Actually, the find method is more general than our function; it can find
substrings, not just characters:

事实上,find方法比我们的函数更通用,它可以找到子串而不仅仅是字符:

::

    >>> word.find('na')
    2

By default, find starts at the beginning of the string, but it can take
a second argument, the index where it should start:

find默认从字符串的首字母开始, 但是它还可以接受第二个参数, 即从何处开始的索引。

::

    >>> word.find('na', 3)
    4

This is an example of an **optional argument**; find can also take a
third argument, the index where it should stop:

下面是一个**可选择的参数(optional argument)**例子; find也可以将在哪个索引结束作为第三个实参:

::

    >>> name = 'bob'
    >>> name.find('b', 1, 2)
    -1

This search fails because b does not appear in the index range from 1 to
2, not including 2. Searching up to, but not including, the second index
makes find consistent with the slice operator.

此搜索失败是因为b没有出现在从1到2的索引之间, 不包括2。 一直搜索到第二个索引, 但是不包
括它, 这使得find跟切片运算符一致.

The in operator - in运算符
---------------

The word in is a boolean operator that takes two strings and returns
True if the first appears as a substring in the second:
单词in是一个布尔运算符,其接受两个字符串, 如果第一个作为子串出现在第二个中则返回True:

::

    >>> 'a' in 'banana'
    True
    >>> 'seed' in 'banana'
    False

For example, the following function prints all the letters from word1
that also appear in word2:

例如,下面的函数打印即出现在word1中也出现在word2中的字母:

::

    def in_both(word1, word2):
        for letter in word1:
            if letter in word2:
                print(letter)

With well-chosen variable names, Python sometimes reads like English.
You could read this loop, “for (each) letter in (the first) word, if
(the) letter (appears) in (the second) word, print (the) letter.”

使用精心挑选的变量名,Python有时候读起来像是英语。你可以读此循环,“对于(每个)
在(第一个)单词中的字母, 如果(该)字母(出现)在(第二个)单词中,打印(该)字母”。

Here’s what you get if you compare apples and oranges:

如果你比较apples和oranges,这是你获得的东西:

::

    >>> in_both('apples', 'oranges')
    a
    e
    s

String comparison-字符串比较
-----------------

The relational operators work on strings. To see if two strings are
equal:

关系运算符在字符串上也工作。为了看两个字符串是否相等:


::

    if word == 'banana':
        print('All right, bananas.')

Other relational operations are useful for putting words in alphabetical
order:

其它的关系运算符对于按字母序放置单词也很有用:

::

    if word < 'banana':
        print('Your word, ' + word + ', comes before banana.')
    elif word > 'banana':
        print('Your word, ' + word + ', comes after banana.')
    else:
        print('All right, bananas.')

Python does not handle uppercase and lowercase letters the same way
people do. All the uppercase letters come before all the lowercase
letters, so:

Python处理大写和小写字母的方式和人不同。所有的大写字母出现在所有小写字母之前,所以:

::

    Your word, Pineapple, comes before banana.

A common way to address this problem is to convert strings to a standard
format, such as all lowercase, before performing the comparison. Keep
that in mind in case you have to defend yourself against a man armed
with a Pineapple.

解决此问题的通常的方式是在执行比较之前, 将字符串转化为标准格式, 例如都是小写字母。
以防你必须保卫自己免受一名手持菠萝的男子的袭击,记住这一点。


Debugging-调试
---------

When you use indices to traverse the values in a sequence, it is tricky
to get the beginning and end of the traversal right. Here is a function
that is supposed to compare two words and return True if one of the
words is the reverse of the other, but it contains two errors:

当你使用索引在一个序列中遍历值的时候,正确的获得遍历的开始和结束是一个技巧。
这是一个函数,其被假设用来比较两个单词,如果一个单词是另一个的倒序,则返回真, 
但是它包含两个错误:

::

    def is_reverse(word1, word2):
        if len(word1) != len(word2):
            return False
        
        i = 0
        j = len(word2)

        while j > 0:
            if word1[i] != word2[j]:
                return False
            i = i+1
            j = j-1

        return True

The first if statement checks whether the words are the same length. If
not, we can return False immediately. Otherwise, for the rest of the
function, we can assume that the words are the same length. This is an
example of the guardian pattern in Section [guardian].

第一条if语句检查两个单词是否等长。如果不是,我们可以马上返回False,否则,对于函数其余的部分,
 我们可以假设单词是等长的。 这是6.8节中的监护人模式的一个例子。

i and j are indices: i traverses word1 forward while j traverses word2
backward. If we find two letters that don’t match, we can return False
immediately. If we get through the whole loop and all the letters match,
we return True.

i和j是索引:i向前遍历word1,j向后遍历word2。如果我们找到两个不匹配的字母,我们可以立即返回
False。 如果我们通过整个循环并且所有字母都匹配,我们返回True。

If we test this function with the words “pots” and “stop”, we expect the
return value True, but we get an IndexError:

如果我们用单词“pots”和“stop”测试该函数,我们期望返回True, 但是我们得到一个IndexError: 

::

    >>> is_reverse('pots', 'stop')
    ...
      File "reverse.py", line 15, in is_reverse
        if word1[i] != word2[j]:
    IndexError: string index out of range

For debugging this kind of error, my first move is to print the values
of the indices immediately before the line where the error appears.

为了调试该类错误, 我的第一步是在错误出现的行之前, 马上打印索引的值。

::

        while j > 0:
            print(i, j)        # print here
            
            if word1[i] != word2[j]:
                return False
            i = i+1
            j = j-1

Now when I run the program again, I get more information:

现在, 当我再次运行该程序时, 我获得更多的信息:

::

    >>> is_reverse('pots', 'stop')
    0 4
    ...
    IndexError: string index out of range

The first time through the loop, the value of j is 4, which is out of
range for the string ``'pots'``. The index of the last character is 3,
so the initial value for j should be len(word2)-1.

第一次通过循环, j的值是4, 其超出字符串'post'的范围了. 最后一个字符的索引是3, 所以
j的初始值应该是len(word2)-1. 

If I fix that error and run the program again, I get:

如果我修正了这个错误运行程序, 我获得:

::

    >>> is_reverse('pots', 'stop')
    0 3
    1 2
    2 1
    True

This time we get the right answer, but it looks like the loop only ran
three times, which is suspicious. To get a better idea of what is
happening, it is useful to draw a state diagram. During the first
iteration, the frame for ``is_reverse`` is shown in Figure [fig.state4].

这次, 我获得正确的答案, 但是看起来循环只运行了三次, 这很奇怪。但是为了更好的理解发成了什么,
 画出栈图会很有用。在第一次循环期间, is_reverse的框架显示在图 [fig.state4]中。

.. figure:: figs/state4.pdf
   :alt: State diagram.

   State diagram.

I took some license by arranging the variables in the frame and adding
dotted lines to show that the values of i and j indicate characters in
word1 and word2.

我安排了框图中变量的为此并且增加了虚线展示i和j的值来指明 word1 和 word2。 

Starting with this diagram, run the program on paper, changing the
values of i and j during each iteration. Find and fix the second error
in this function. [isreverse]

利用这个图标, 将程序运行在纸上, 并在每次迭代改变i和j的值。 找到并修改这个函数中的第二个错误。

Glossary-术语
--------

object(对象):
    Something a variable can refer to. For now, you can use “object” and
    “value” interchangeably.

object(对象):
    一个变量可以引用对象. 现在你既可以可以使用"对象", 也可以使用"值".

sequence(序列):
    An ordered collection of values where each value is identified by an
    integer index.

sequence(序列):
    一个有序的值的集合, 每个值都与一个整数的索引联系起来.

item(项):
    One of the values in a sequence.
item(项):
    序列中的一个

index(索引):
    An integer value used to select an item in a sequence, such as a
    character in a string. In Python indices start from 0.
index(索引):
    整数值, 被用来选择序列中的一项, 例如字符串中的一个字符. 在Python中索引从0开始.

slice(切片):
    A part of a string specified by a range of indices.
slice(切片):
   以指定的索引范围选择字符串的一部分.

empty string(空字符串):
    A string with no characters and length 0, represented by two
    quotation marks.
empty string(空字符串):
   一个没有字符的字符串, 长度为0, 用两个引号表示.

immutable(不可变的):
    The property of a sequence whose items cannot be changed.
immutable(不可变的):
    一个序列的所有项不能被改变的性质.


traverse(遍历):
    To iterate through the items in a sequence, performing a similar
    operation on each.
traverse(遍历):
    按照一个序列的项迭代, 并且对每一项都有相似的操作.
    

search(搜索):
    A pattern of traversal that stops when it finds what it is looking
    for.
search(搜索):
    遍历的一种模式, 当找到它所需要的就停止.

counter(计数器):
    A variable used to count something, usually initialized to zero and
    then incremented.
counter(计数器):
    被用来计数的变量, 通常从0开始增加.	

invocation(调用):
    A statement that calls a method.
invocation(调用):
    使用一个方法的声明.
    
optional argument(可选参数):
    A function or method argument that is not required.
optional argument(可选参数):
    一个函数或者一个方法中的参数并不是必要的.

Exercises- 练习
---------

Read the documentation of the string methods at
http://docs.python.org/3/library/stdtypes.html#string-methods. You might
want to experiment with some of them to make sure you understand how
they work. strip and replace are particularly useful.

在如下链接阅读字符串方法的文档
http://docs.python.org/3/library/stdtypes.html#string-methods.
为了确保你理解他们是怎么工作的, 你可能要去实验其中的一些方法. strip和 replace非常有用.

The documentation uses a syntax that might be confusing. For example, in
``find(sub[, start[, end]])``, the brackets indicate optional arguments.
So sub is required, but start is optional, and if you include start,
then end is optional.

这个文档使用了可能会引起困惑的句法. 例如, 在``find(sub[, start[, end]])``中, 
方括号意味着可选参数. 所以sub是必须有的, 但是start是可选的, 并且如果你包含了start, 那么
end是可选的.

There is a string method called count that is similar to the function in
Section [counter]. Read the documentation of this method and write an
invocation that counts the number of a’s in ``'banana'``.

有一个字符串方法叫count, 它类似于前边部分的counter. 阅读这个方法的文档, 写一个调用
计算banana中a的个数.

A string slice can take a third index that specifies the “step size”;
that is, the number of spaces between successive characters. A step size
of 2 means every other character; 3 means every third, etc.

一个字符串切片可以有第三个索引, 叫做步长; 也就是连续字符间空格的个数. 步长为2就是
每隔一个字符; 步长为三就是每个两个字符, 以此类推.

::

    >>> fruit = 'banana'
    >>> fruit[0:5:2]
    'bnn'

A step size of -1 goes through the word backwards, so the slice
``[::-1]`` generates a reversed string.

步长为-1就是从单词的后边开始进行, 所以切片``[::-1]``生成一个倒序的字符串.
Use this idiom to write a one-line version of ``is_palindrome`` from
Exercise [palindrome].

根据函数``is_palindrome``的练习, 使用这个短语写一个一行的版本.


The following functions are all *intended* to check whether a string
contains any lowercase letters, but at least some of them are wrong. For
each function, describe what the function actually does (assuming that
the parameter is a string).

下面这些函数都想检查一个字符串是否包含一些小写字母, 但是其中一些事错误的.
对于每个函数, 请描述这个函数实际上做了什么(假设参数是字符串).

::

    def any_lowercase1(s):
        for c in s:
            if c.islower():
                return True
            else:
                return False

    def any_lowercase2(s):
        for c in s:
            if 'c'.islower():
                return 'True'
            else:
                return 'False'

    def any_lowercase3(s):
        for c in s:
            flag = c.islower()
        return flag

    def any_lowercase4(s):
        flag = False
        for c in s:
            flag = flag or c.islower()
        return flag

    def any_lowercase5(s):
        for c in s:
            if not c.islower():
                return False
        return True

[exrotate] A Caesar cypher is a weak form of encryption that involves
“rotating” each letter by a fixed number of places. To rotate a letter
means to shift it through the alphabet, wrapping around to the beginning
if necessary, so ’A’ rotated by 3 is ’D’ and ’Z’ rotated by 1 is ’A’.

凯撒密码是一种弱编码, 它一个固定数目的位置轮换每一个字母.轮换字母的意思就是按着字母表
切换, 如果有必要绕回开头, 所以A轮换3个位置是D, Z轮换一个是A.
  
To rotate a word, rotate each letter by the same amount. For example,
“cheer” rotated by 7 is “jolly” and “melon” rotated by -10 is “cubed”.
In the movie *2001: A Space Odyssey*, the ship computer is called HAL,
which is IBM rotated by -1. 

轮换一个单词就是以相同的数目轮换每一个字母. 例如, "cheer"以7轮换是"jolly", "melon"
以-10轮换是"cubed". 在电影*2001: A Space Odyssey*里, 飞船上的电脑叫做"HAL",
以-1轮换后是"IBM".
 
Write a function called ``rotate_word`` that takes a string and an
integer as parameters, and returns a new string that contains the
letters from the original string rotated by the given amount.

写一个函数叫做"rotate_word", 可以接受一个字符串和一个整数作为参数, 并返回一个新的
由原字符以给定数目轮换后的字符串. 

You might want to use the built-in function ord, which converts a
character to a numeric code, and chr, which converts numeric codes to
characters. Letters of the alphabet are encoded in alphabetical order,
so for example:

你可能想要用内建的函数ord, 它可以将字符转化成数值代码, 还有chr, 它可以将数值代码转
化成字符. 字母表的字母以字母表顺序编码, 例如:
 
::

    >>> ord('c') - ord('a')
    2

Because ``'c'`` is the two-eth letter of the alphabet. But beware: the
numeric codes for upper case letters are different.

因为'c'是字母表中的第二个字母. 但是注意: 数值代码对于大写字母是不同的.

Potentially offensive jokes on the Internet are sometimes encoded in
ROT13, which is a Caesar cypher with rotation 13. If you are not easily
offended, find and decode some of them. Solution:
http://thinkpython2.com/code/rotate.py.

在网上一些隐含的荤段子(Potentially offensive jokes)有时以ROT13编码, 即以13轮转的凯撒
密码. 如果你不是很容易就被冒犯, 那么找到并解码他们. 答案:
http://thinkpython2.com/code/rotate.py.



