第九章：文字游戏 word play
=========================================

这一章将介绍第二个案例研究，即通过查找具有特定属性的单词来解答字谜游戏。
例如，我们将找出英文中最长的回文单词，以及字母按照字母表顺序出现的单词。
另外，我还将介绍另一种程序开发方法：简化为之前已解决的问题。

读取单词列表
-------------------------------

为了完成本章的习题，我们需要一个英语单词的列表。
网络上有许多单词列表，但是最符合我们目的列表之一是由 Grady
Ward收集并贡献给公众的列表，这也是Moby词典项目的一部分
（见：\ http://wikipedia.org/wiki/Moby_Project \ ）。
它由113,809个填字游戏单词组成，即在填字游戏以及其它文字游戏中被认为有效的单词。
在Moby集合中，该列表的文件名是113809of.fic ；你可以从\ http://thinkpython.com/code/words.txt \ 下载一个拷贝，文件名已被简化为 words.txt。


该文件是纯文本，因此你可以用一个文本编辑器打开它，但是你也可以从Python中读取它。
内建函数 ``open`` 接受文件名作为形参，并返回一个 **文件对象（file object）** ，你可以使用它读取该文件。

::

    >>> fin = open('words.txt')

\ ``fin``\ 是输入文件对象的一个常用名。该文件对象提供了几个读取方法，
包括 ``readline`` ，其从文件中读取字符直到碰到新行，并将结果作为字符串返回：
::

    >>> fin.readline()
    'aa\r\n'


在此列表中，第一个单词是“aa”，它是一种岩浆。
序列\ ``\r\n``\ 代表两个空白字符，回车和换行， 它们将这个单词和下一个分开。

此文件对象跟踪它在文件中的位置，
所以如果你再次调用readline，你获得下一个单词：

::

    >>> fin.readline()
    'aah\r\n'


下一个单词是“aah”，它是一个完全合法的单词， 所以不要那样看我。
或者，如果空格困扰了你，我们可以用字符串方法 ``strip`` 删掉它：

::

    >>> line = fin.readline()
    >>> word = line.strip()
    >>> word
    'aahed'


你也可以将文件对象用做for循环的一部分。
此程序读取 ``words.txt`` 并打印每个单词，每行一个：

::

    fin = open('words.txt')
    for line in fin:
        word = line.strip()
        print(word)

Exercises 习题
--------------

下一节给出了这些习题的答案。
在你看这些答案之前，应该至少试着解答一下。

习题 9-1

编程写一个程序，使得它可以读取 ``words.txt``　，然后只打印出那些长度超过20个字母的单词(不包括空格)。

习题 9-2

1939年，Ernest Vincent Wright出版了一本名为 *《Gadsby》* 的小说，
该小说里完全没有使用字母“e”。由于“e”是最常用的英文字母，因此这并容易做到。

事实上，不使用这个最常用的符号(字母e)来构建一个孤立的想法是很难的。
开始进展缓慢，但是经过有意识的、长时间的训练，你可以逐渐地熟练。

好啦，不再说题外话了(让我们开始编程练习)。

写一个叫做\ ``has_no_e``\ 的函数，如果给定的单词中不包含字母“e”，其返回 ``True`` 。

修改上一节中的程序，只打印不包含“e”的单词，并且计算列表中不含“e”单词的比例。

习题 9-3

编写一个名为 ``avoids`` 的函数，接受一个单词和一个指定禁止使用字母的字符串，
如果单词中不包含任意被禁止的字母，则返回True 。

修改你的程序，提示用户输入一个禁止使用的字母，然后打印不包含这些字母的单词的数量。
你能找到一个5个禁止使用字母的组合，使得其排除的单词数目最少么？

习题 9-4

编写一个名为\ ``uses_only``\ 的函数，接受一个单词和一个字符串。
如果该单词只包括此字符串中的字母，则返回True。
你能只用 ``acefhlo`` 这几个字母造一个句子么？ 除了“Hoe alfalfa”外。

习题 9-5

编写一个名为\ ``uses_all``\ 的函数，接受一个单词和一个必须使用的字母组成的字符串。
如果该单词包括此字符串中的全部字母至少一次，则返回True。
你能统计出多少单词包含了所有的元音字母aeiou吗？如果换成aeiouy呢？

习题 9-6

编写一个名为\ ``is_abecedarian``\ 的函数，
如果单词中的字母以字母表的顺序出现（允许重复字母），则返回True 。
有多少个具备这种特征的单词？

搜索
-----------

All of the exercises in the previous section have something in common;
they can be solved with the search pattern we saw in Section [find]. The
simplest example is:

前一节的所有习题有一个共性，它们可以用我们在[find]节中看到的搜索模式解决。
最简单的例子是：

::

    def has_no_e(word):
        for letter in word:
            if letter == 'e':
                return False
        return True

The for loop traverses the characters in word. If we find the letter
“e”, we can immediately return False; otherwise we have to go to the
next letter. If we exit the loop normally, that means we didn’t find an
“e”, so we return True.

for循环遍历word中的字符。
如果我们找到字母“e”，那么我们可以马上返回False；
否则我们不得不到下一个字母。
如果我们正常停止循环，这意味着我们没有找到一个“e”， 所以我们返回True。

You could write this function more concisely using the in operator, but
I started with this version because it demonstrates the logic of the
search pattern.

你也可以用in操作符简化上述函数，但是我将从这个版本开始因为它展示了搜索模式处理问题的罗辑。

``avoid`` is a more general version of ``has_no_e`` but it has the same structure:

``avoid``　是\ ``has_no_e``\ 的更一般的版本，但是它有相同的结构：

::

    def avoids(word, forbidden):
        for letter in word:
            if letter in forbidden:
                return False
        return True

We can return False as soon as we find a forbidden letter; if we get to
the end of the loop, we return True.

一旦我们找到一个禁止字母，我们返回False；
如果我们到达循环结尾，我们返回True。

``uses_only`` is similar except that the sense of the condition is
reversed:

除了条件的意思相反外，\ ``uses_only``\ 也是相似的：

::

    def uses_only(word, available):
        for letter in word: 
            if letter not in available:
                return False
        return True

Instead of a list of forbidden letters, we have a list of available
letters. If we find a letter in word that is not in available, we can
return False.

不是有一个禁止字母的列表，而是我们有一个允许字母的列表。
如果我们在word中找到一个不在available中的字母， 我们可以返回False。

``uses_all`` is similar except that we reverse the role of the word and
the string of letters:

除了我们翻转了单词和字母字符串的角色外，\ ``uses_all``\ 也类似：

::

    def uses_all(word, required):
        for letter in required: 
            if letter not in word:
                return False
        return True

Instead of traversing the letters in word, the loop traverses the
required letters. If any of the required letters do not appear in the
word, we can return False.

不是在word中遍历字母，该循环遍历需要的字母。
如果任何需要的字母没出现在单词中， 则我们返回False。

If you were really thinking like a computer scientist, you would have
recognized that ``uses_all`` was an instance of a previously solved
problem, and you would have written:

如果你真的像计算机科学家一样思考，
你可能已经意识到\ ``uses_all``\ 是前面已经解决的问题的一个实例，
你可能会写成：

::

    def uses_all(word, required):
        return uses_only(required, word)

This is an example of a program development plan called **reduction to a
previously solved problem**, which means that you recognize the problem
you are working on as an instance of a solved problem and apply an
existing solution.

这是一个被称作\ **转化,把未解决的问题转化成已经解决的问题（reduction to a
previously solved problem）**\ 的程序开发方法的实例，
意思是你将正在解决的问题看做是之前已经解决的问题的一个实例，
并用用之前开发的解决方案。

Looping with indices 使用索引的循环
-----------------------------------

I wrote the functions in the previous section with for loops because I
only needed the characters in the strings; I didn’t have to do anything
with the indices.

前一节我用for循环写函数，因为我只需要字符串中的字符，
我不必用索引做任何事情。

For ``is_abecedarian`` we have to compare adjacent letters, which is a
little tricky with a for loop:

对于\ ``is_abecedarian``\ ，我们必须比较邻接的字母，
这是一个用for循环的小技巧。

::

    def is_abecedarian(word):
        previous = word[0]
        for c in word:
            if c < previous:
                return False
            previous = c
        return True

An alternative is to use recursion:

另外的替代方法是使用递归：

::

    def is_abecedarian(word):
        if len(word) <= 1:
            return True
        if word[0] > word[1]:
            return False
        return is_abecedarian(word[1:])

Another option is to use a while loop:

另一个选择是使用while循环：

::

    def is_abecedarian(word):
        i = 0
        while i < len(word)-1:
            if word[i+1] < word[i]:
                return False
            i = i+1
        return True

The loop starts at i=0 and ends when i=len(word)-1. Each time through
the loop, it compares the :math:`i`\ th character (which you can think
of as the current character) to the :math:`i+1`\ th character (which you
can think of as the next).

循环起始于i=0，终止于i=len(word)-1。
每次循环比较第\ :math:`i`\ 个字符（我们可以将其认为是当前字符）
和第\ :math:`i+1`\ 个字符（我们可以将其认为是下一个字符）。

If the next character is less than (alphabetically before) the current
one, then we have discovered a break in the abecedarian trend, and we
return False.

如果下一个字符比当前的小（字母序靠前），
那么我们在递增趋势中找到了停止点并返回False。

If we get to the end of the loop without finding a fault, then the word
passes the test. To convince yourself that the loop ends correctly,
consider an example like ``'flossy'``. The length of the word is 6, so
the last time the loop runs is when i is 4, which is the index of the
second-to-last character. On the last iteration, it compares the
second-to-last character to the last, which is what we want.

如果到达循环结束，我们也没有找到一点错误，那么该单词通过测试。
为了说服你自己循环正确的结束了，考虑一个类似\ ``'flossy'``\ 的例子。
其长度为6，因此最后一次循环运行时，i是4，这是倒数第2个字符。
最后一次迭代，它比较倒数第二个和最后一个字符，这正是我们希望的。

Here is a version of ``is_palindrome`` (see Exercise [palindrome]) that
uses two indices; one starts at the beginning and goes up; the other
starts at the end and goes down.

这是\ ``is_palindrome``\ 的一个版本（见练习[palindrome]），
其使用两个索引，一个从最前面开始并往前上， 另一个从最后面开始并往下走。

::

    def is_palindrome(word):
        i = 0
        j = len(word)-1

        while i<j:
            if word[i] != word[j]:
                return False
            i = i+1
            j = j-1

        return True

Or we could reduce to a previously solved problem and write:

或者你可以把问题转化为我们已经解决的问题比如这样写这个函数:

::

    def is_palindrome(word):
        return is_reverse(word, word)

Using ``is_reverse`` from Section [isreverse].

使用[isreverse]章节的``is_reverse``来解决这个问题。

Debugging 调试
--------------

Testing programs is hard. The functions in this chapter are relatively
easy to test because you can check the results by hand. Even so, it is
somewhere between difficult and impossible to choose a set of words that
test for all possible errors.

测试程序很难。本章的函数相对容易测试，因为你可以手工检查结果。
即使这样，选择一个单词的集合来测试所有可能的错误，
在某些方面也是介于困难和不可能的。

Taking ``has_no_e`` as an example, there are two obvious cases to check:
words that have an ‘e’ should return False, and words that don’t should
return True. You should have no trouble coming up with one of each.

例如\ ``has_no_e``\ ，有两个明显的用例需要检查：
含有‘e’的单词应该返回False，不含的单词应该返回True。
你应该可以很轻松的想到这两种情况。

Within each case, there are some less obvious subcases. Among the words
that have an “e”, you should test words with an “e” at the beginning,
the end, and somewhere in the middle. You should test long words, short
words, and very short words, like the empty string. The empty string is
an example of a **special case**, which is one of the non-obvious cases
where errors often lurk.

在每个用例中，还有一些不明显的子用例。
在含有“e”的单词中，你应该测试“e”在开始、结尾以及在中间的单词。
你应该测试长单词、短单词以及非常短的单词，如空字符串。
空字符串是\ **特殊用例（special case）**\ 的一个例子，
其是一个经常隐藏错误的不明显的用例。

In addition to the test cases you generate, you can also test your
program with a word list like words.txt. By scanning the output, you
might be able to catch errors, but be careful: you might catch one kind
of error (words that should not be included, but are) and not another
(words that should be included, but aren’t).

除了你生成的测试用例，你也可以用一个类似words.txt的单词列表测试你的程序。
通过扫描输出，你可能会捕获错误，但是请小心：
你可能捕获一类错误（包括了不应该包括的单词）
但不会捕获另一类错误（没有包括应该包括的单词）。

In general, testing can help you find bugs, but it is not easy to
generate a good set of test cases, and even if you do, you can’t be sure
your program is correct. According to a legendary computer scientist:

    Program testing can be used to show the presence of bugs, but never
    to show their absence!

    — Edsger W. Dijkstra
    
一般来讲，测试能帮助你找到错误， 但是生成好的测试用例的集合并不容易，
并且即便你做到了，你仍然不能保证你的程序是正确的。据一个传奇计算机科学家所说：

    程序测试能被用于展现错误的存在，但是从不会显示其不存在！

    — Edsger W. Dijkstra    

Glossary 术语表
---------------

file object:
    A value that represents an open file.
    
文件对象:
    代表打开文件的变量。

reduction to a previously solved problem:
    A way of solving a problem by expressing it as an instance of a
    previously solved problem.

转化：
    通过把未知问题转化为已经解决的问题来解决问题的方法。
　　　

special case:
    A test case that is atypical or non-obvious (and less likely to be
    handled correctly).
    
特殊用例:
    一种不典型或者不明显的测试用例(包括很可能无法正确解决的用例)。

Exercises　习题
------------------

习题 9-7
^^^^^^^^

This question is based on a Puzzler that was broadcast on the radio
program *Car Talk* (http://www.cartalk.com/content/puzzlers):

这个根据一个经由广播节目*Car Talk*(http://www.cartalk.com/content/puzzlers)广泛传播的谜语:

    Give me a word with three consecutive double letters. I’ll give you
    a couple of words that almost qualify, but don’t. For example, the
    word committee, c-o-m-m-i-t-t-e-e. It would be great except for the
    ‘i’ that sneaks in there. Or Mississippi: M-i-s-s-i-s-s-i-p-p-i. If
    you could take out those i’s it would work. But there is a word that
    has three consecutive pairs of letters and to the best of my
    knowledge this may be the only word. Of course there are probably
    500 more but I can only think of one. What is the word?
    
    给我一个包括三个连续双字母的单词。我将给你一系列单词尽可能符合但是并不完全符合。比如，你给出一个单词，c-o-m-m-i-t-t-e-e。
    并不奇怪字母i破坏了连续性。或者Mississippi: M-i-s-s-i-s-s-i-p-p-i。加入这些i不存在就对了。但是确实存在一个单词，在我的认知
    中似乎也是唯一的单词符合包括连续三对字母的单词。当然也可能有500个或者更多，但是我只能想到一个，那么这个单词是什么？

Write a program to find it. Solution:
http://thinkpython2.com/code/cartalk1.py.

写一个程序来找到它。解答在:http://thinkpython2.com/code/cartalk1.py

习题 9-8
^^^^^^^^

Here’s another *Car Talk* Puzzler
(http://www.cartalk.com/content/puzzlers):

这里是另一个*Car Talk*谜题:

    “I was driving on the highway the other day and I happened to notice
    my odometer. Like most odometers, it shows six digits, in whole
    miles only. So, if my car had 300,000 miles, for example, I’d see
    3-0-0-0-0-0.
    
    一天我正在高速公路上开车，我偶然注意到我的里程表。和大多数里程表显示，它只给出6位数字的整数英里数。
    所以比如，如果我的车开了300,000英里，我能够看到的示数是:3-0-0-0-0-0。

    “Now, what I saw that day was very interesting. I noticed that the
    last 4 digits were palindromic; that is, they read the same forward
    as backward. For example, 5-4-4-5 is a palindrome, so my odometer
    could have read 3-1-5-4-4-5.
    
    那天我看到的里程表示数非常有意思，我注意到后四位数字是回文数，也就是说正序读和逆序读是一样的。比如,5-4-4-5就是回文数。
    所以我的里程表示数可能是3-1-5-4-4-5。    

    “One mile later, the last 5 numbers were palindromic. For example,
    it could have read 3-6-5-4-5-6. One mile after that, the middle 4
    out of 6 numbers were palindromic. And you ready for this? One mile
    later, all 6 were palindromic!
    
    一英里后，后五位数字变成了回文数。比如示数可能是3-6-5-4-5-6。又一个一英里后，6位示数的中间四位变成了回文数，
    你收购了这些？(还没有呢！)一英里后，所有的6位数字都变成了回文数。

    “The question is, what was on the odometer when I first looked?”
    
    问题是，当我第一次看到里程表的时候示数是多少?

Write a Python program that tests all the six-digit numbers and prints
any numbers that satisfy these requirements. Solution:
http://thinkpython2.com/code/cartalk2.py.

写一个程序，检测所有的6位数字然后输出所有符合要求的结果。解答在:http://thinkpython2.com/code/cartalk2.py

习题 9-9
^^^^^^^^

Here’s another *Car Talk* Puzzler you can solve with a search
(http://www.cartalk.com/content/puzzlers):

还是*Car Talk*的谜题，你可以通过搜索来解决它:

    “Recently I had a visit with my mom and we realized that the two
    digits that make up my age when reversed resulted in her age. For
    example, if she’s 73, I’m 37. We wondered how often this has
    happened over the years but we got sidetracked with other topics and
    we never came up with an answer.
    
    最近我探望了我的妈妈，我们忽然意识到把我的年纪数字反过来就是她的年龄。比如，如果她73岁，我37岁。
    我们想知道多久这样的巧合可能发生但是我们很快被其他话题打扰所以我们并没有找到答案。

    “When I got home I figured out that the digits of our ages have been
    reversible six times so far. I also figured out that if we’re lucky
    it would happen again in a few years, and if we’re really lucky it
    would happen one more time after that. In other words, it would have
    happened 8 times over all. So the question is, how old am I now?”
    
    当我回到家，我计算出我的年龄有6次反过来就是妈妈的年龄。同时我也发现将来几年还可能发生这样的巧合，如果我们真的非常幸运，
    这样的巧合还将发生一次。换句话说，总的来说，这样的巧合一共会发生8次。那么，问题是我现在几岁？

Write a Python program that searches for solutions to this Puzzler.
Hint: you might find the string method zfill useful.

Solution: http://thinkpython2.com/code/cartalk3.py.

写一个Python函数来找到这个谜题的答案。提示，你会发现字符串的zfill方法特别有用。
答案在:http://thinkpython2.com/code/cartalk3.py。
