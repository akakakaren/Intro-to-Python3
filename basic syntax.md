# [Basic Syntax of Python](https://labex.io/courses/10)

## 1. Introduction

This lab contains the most commonly used concepts and [syntax](https://labex.io/courses/10), and is mainly based on hands-on practice. Some advanced use of Python will be elaborated in later labs.

If you are new to Python, please go through all steps carefully. Make sure you understand every point, and if you have any questions, don't hesitate to let us know in the discussion forum. 

### 1.1 Learning objectives

- Development environment for Python
- Variables and data types
- Input and output
- Operations
- String operations
- Control structures
- Exception handling

## 2. What is Python

Python is a programming language, which is fast to learn and has powerful functions. It provides abundant basic modules and third-party modules that could be directly used in programs. It contains a series of functions like database, web development, file operations, and etc. Flask Web framework is a powerful development module that will be involved in this week's test.

Python currently has two versions: Python 2 and Python 3, and they are code-incompatible. Python 3 has improved a lot, and has access to most libraries. That's why we choose Python 3. If you're familiar with Python 2, then Python 3 should be pretty easy for you.

### 2.1 Advantages and Disadvantages

Life is short, and I use Python.

This is not a sportive remark because the highlight of Python is simplicity, using a few code to realize complex functions. Compared with other programming languages, C language needs 1,000 lines to carry out a simple command line chat room, while Python only needs approximately100 lines. Besides, because Python has many basic libraries and third-party libraries, we could greatly enhance working productivity in development phase.

In terms of disadvantages, Python is an explanatory language, and it will interpret execution line by line every time, which is no match for compiled language in execution. In addition to performance cost, the source code of Python program is completely open, because it is a script, other than being compiled into binary distribution, which is usually hard to protect.

### 2.2 Applied Situation for Python

LabEx is developed through Python. Most of our components, such as experiment environment control module, course management, and Web service are all constructed by Python. The main reason why we choose Python is that it is rapid to develop and economic for team learning.Although there is a loss in performance, it is acceptable within our business.In addition, our domestic web douban is developed by Python.

At present, Python is mainly used in Web Crawlers, Web development, automated operation, data analysis and so on.Among these major fields,lou+ Course offers you practical programs respectively, and allow you to think independently within a wide range of extended function challenges after every project.

These courses can not assure you becoming a master of Python. Please do not count on any shortcut without efforts to make your skill set perfect. After all, it takes a long time to practice. However, the aim of this tutorial is to help you grasp the main application development approach within the shortest time and to solve similar problems quickly with Python on your own.

## 3. Operation Environment

### 3.1 Installation

The operating system environment Ubuntu 14.04 provided by LabEx has already installed Python 3.x. It is also easy for you to install Python under Linux if necessary. Default package management all support installment directly, like using apt-get under Ubuntu：

    sudo apt-get update
    sudo apt-get install python3

Mac users can use brew to install python3, while Windows users can download from the official website.

### 3.2 Interaction

We use Python3 command to enter into the interactive environment, where input code can be executed immediately and produce output. The interactive environment is often used in development to debug and test code.

Click Xfce terminal on the right to start Linux and input python3 to enter into the interactive environment：


![image desc](/upload/B/F/A/KqE423VK7Gwo.png)


Input the code after >>> . First you can enter print("hello labex").

It is not difficult to exit interactive environment, either by shortcut key Ctrl-D or inputting code exit().


![image desc](/upload/N/O/R/QragBwLprB4b.png)



### 3.3 Run Script

The simplest Python program is a script containing one or more source code, usually stored as an extension ended up with .py.

When finishing writing script, we use Python interpreter to run the script.

When we establish a simple script and try to execute it, this script only contains a line of code from last interactive environment. Pay attention , the echo command needs to be in Linux terminal in order to establish documents and write things.

    $ echo "print('hello labex')" > /home/labex/labex.py

To run script directly by Python 3 interpreter：

    $ python3 /home/labex/labex.py

![image desc](/upload/X/D/E/o0P2KZxk5wQc.png)


### First Attempt

Now let's try to write your first Python program, aiming to calculate the area of a circle with 5 radius and display output.

In this program, we will get in touch with the concept of script writing and execution, module introduced and usage for the first time.

### Choose an Editor

We have various built-in code editing tools, and you can choose according to needs：

1. vim：one of the most favorable editors for programmers, executing via command line. It is relatively difficult to start with. If you're interested, you can practice on your own to get yourself familiarized.
2. gedit：It is like a notebook, and code is highlighted when being written.
3. sublime：Another frequently used editor. A lot of plug-ins with functions like code highlighting and prompt can be chosen.

If you are familiar and comfortable with Linux, Vim is recommended; if not, sublime is recommended. In the following steps, we are going to use Vim editor.

### Open a File

Input `vim circle.py` in Xfce terminal to start Vim and edit circle.py. Do not fiddle with buttons.

Then press button "i" to enter into insert mode. You will see "insert" at the bottom left corner, and now you can type code below.


![image desc](/upload/M/M/X/jzvC5kE1M84h.png)


#### First Line

Input code in the first line as below：

    #!/usr/bin/env python3

In particular, the first two characters #! are called Shebang, aiming to tell shell to use Python 3 interpreter to execute code.

#### Modules and Introduction

Since we are to calculate the area of a circle, we need to know π, that is 3.1415... We will use a basic library math , containing a huge number of commonly used formulas and change handlers related to math, and also π.

Input code：

    from math import pi 

This means to introduce pi from math library, making pi available to the current document.

#### Calculation

Use the introduced π  to calculate the area of the circle with 5 radius. Hopefully you still remember the formula and then input the code：

    # Calculate
    result = 5 * 5 * pi

Here the line starting with # is a comment for the program. Comment is for us to read and understand the code. A good comment habit can increase program's maintainability. Even with well-written code, it would be hard for writers to modify them without comments.

In the followng line, we define a variable called result to save computation of 5 * 5 * pi.

#### Output

Output is easy. It is the print function we used in the last section.

    print(result)

#### All Code

To merge all code:

    #!/usr/bin/env python3
    from math import pi
    # calculate
    result = 5 * 5 * pi
    print(result)

#### Save

Then press Esc to exit insert mode. Next, we type `:wq` and press Enter. Vim will save files and exit.


![image desc](/upload/H/W/N/uXakHwWKMZNA.png)


#### Code Execution

There are two ways for code execution. One is through appointed script python3 written before, and the second is executing a script directly, which we are going to talk about later.

To run file circle.py, we have to give executable permissions ：

    $ chmod +x circle.py

Then execute it：

    $ ./circle.py

When executing a script we need to put ./ ahead to represent that it is under the current directory.

The result is shown as follows：


![image desc](/upload/W/W/H/9JGFWYVLkelf.png)


**Note**

1. Vim is not easy to get started. Please switch to sublime or gedit if needed.
2. Space character is significant for Python. In the example, all code are required to be put by the very left side, otherwise, there will be mistakes.

## Variables and Data Types

### Variables

In order to process data better, we usually need some variables. Variables of Python language could be any types, and we use them directly without declaration.

### Variable Names

Python 3 strictly requires the name starting with alphabets and underscores. Other symbols could be numbers, alphabets or underscores. Naming is case sensitive, and without key words that are reserved by Python like import.

You can check key words using the keyword module in the enviornment：


![image desc](/upload/L/G/C/oERhqurG3P4J.png)


### Fundamental Data Types

Several types are contained in Python 3：

1. Integer: such as 100, -200, 0 
2. Boolean: True or False
3. Floating point: such as 1.5, 2.5
4. None: it is no like zero, and you can regard it as an undefined value.

Apart from these four types, there are other types which are not commonly used. For example, complex number. 

### Variables Employment and Print

Input python3 in the Xfce terminal and enter interactive environment. Try to input the following code and figure out what the output measn. Do not exit after execution and continue to the next test：

    >>> a = 10
    >>> b = 10.6
    >>> c = True
    >>> d = None
    >>> print(a,b,c,d)
    >>> print(type(a),a)
    >>> print(type(b),b)
    >>> print(type(c),c)
    >>> print(type(d),d)

Among the code above, type is a built-in function in Python 3 to indicate the type of variables.


![image desc](/upload/U/N/O/1f3GBHHSUEf7.png)


## Operation

Let's continue and underatand the operation in Python 3：

    e = a + b
    print(e)
    f = b/a
    print(f)
    g = b - a
    print(g)
    h = b * a
    print(h)

We can see the integer will be changed into floating point in the hybrid computation of integer and floating point.


![image desc](/upload/U/Q/P/evSrg4JveZzf.png)



Apart from arithmetical calculation, there is logical calculation such as and, or：

    True and False
    True or False
    c and False
    c or False

Only when both results are True, it will return True. While or indicates nor-operation, it will return to True with only one True.

### Character String

Strings in Python 3 can be indicated by double quotation marks or single quotation mark. If the quotation marks is shown in strings, then we can use \ to remove the special function of quotation.

Several expressions of character string：

    str1 = "hello"
    str2 = 'labex'
    str3 = 'hello, \'labex\''
    str4 = "hello, 'labex'"
    str5 = 'hello, "labex"'

Pay attention here. str4 and str5 do not have \，but they can still use quotation, and I believe you have already discovered the reason.

If you need to input several lines of character strings, how to accomplish that? Try to use three double quotation """：

    str6 = """ hello, 
    labex """

Support the use of connection strings + ：

    str1 + ' ' + str2

Character strings could use numbers to index. Number 0 is the first character, and so on. Number -1 is the last character, using a colon to slice it：

    str1
    str1[0]
    str1[1]
    str1[-1]
    str1[-2]
    str1[:2]
    str1[3:]

We get easily consufed with the location of slices，that's why we need to practice more to understand it.

The built-in function len() in Python 3 can acquire the number of characters the string contains：

    len(str2)

![image desc](/upload/H/E/G/kXEDKi3KLibL.png)


## Control Structures

We are going to learn the control structures of Python 3 in this section, including select control and loop control. 

## Select Control

Many programming languages will use if as keywords to control the process. Apart from this, the process control also includes two keywords elif and else, which are all optional in the control structure. elif means else if, to make a further judgment whether to choose this path.

Look at the example below：

    >>> a = int(input("Please enter: "))
    Please enter: 10
    >>> if a > 10:
    ...     print('a > 10')
    ... elif a == 10:
    ...     print('a == 10')
    ... else:
    ...     print('a < 10')

input("Please enter: ") These code use function input to acquire users'input. The parameter string will show on the screen, and the content inputd by users will be returned by the function. The returned value is a character string. If you do not input things, the procedure will be blocked waiting.

int(input("Please enter: ")) To turn character strings users input into integers and assign numbers to the variable a.

This example will choose different paths according to different values of a. You can write code in a script and execute repeatedly through various inputs.

But pay attention to the indent of Python 3. Unlike C language using { to manage code blocks, Python 3 has strict indent rules. Code sharing the same indent belong to one code block, for example, code blocks of if or else have to keep the same indent.

Do not mix Space and TAB. We strongly suggest only using Space. To maintain a good style of coding, tapping Space four times as indent is recommended.

The screenshot of program execution：


![image desc](/upload/V/C/Y/bQ9RqoxgGPFB.png)


## Loop Control

There are two kinds of loop controls in Python.One is for, the other is while.

for is to pick out projects sequentially from a list, and traverse the list. We will carefully explain the data structure of lists and now can simply regard it as a set of values.

example shown as below：

    strlist = ['hello','labex','.io']
    for s in strlist:
        print(s)


![image desc](/upload/P/P/F/3tmOj1OmuoCr.png)


If you need to iterate a set of number lists, and lists show certain rules, you may use the built-in function range()：

    for a in range(10):
        print(a)


![image desc](/upload/K/H/C/1rnh7EBeRPQl.png)


Function range() has other usages. Look up help documentation if interested.

In terms of while, it is different from for in that it could stop when conditions are not met, unlike for using only one expression as judging conditions.

    w = 100
    while w > 10:
        print(w)
        w -= 10

Here should notice that w -= 10 equals w = w - 10.When w is equal or less than 10, it loops out.


![image desc](/upload/X/K/H/2cEEkJV4P2k7.png)


We can use break and continue these two keywords in the loop control.Break means to stop the current loop and continue means to skip the rest code of current round and to execute next round.

example：

    for a in range(10):
        if a == 5:
            break
        print(a)

Execution is as follows. When a is 5, it loops out：


![image desc](/upload/J/E/C/lR4tz2HAjeKc.png)



    w = 100
    while w > 10:
        w -= 10
        if w == 50:
            continue
        print(w)

Execution is as follows. When w is 50,  it does not execute succeeding code print：


![image desc](/upload/C/S/I/tU0yr1Hs42GR.png)


## Exception Handling

### What is Exception

Exception handling is a necessary part of code writing. The procedure will always have exceptions if there are unexpected operations or data input. Therefore, being able to tackle problems is one of the critical tasks to maintain the stability of programs.

There are many reasons contributing to exceptions, such as logical errors and user-input errors.

"Give us an example to tell us what is exception"：

    filename = input("Enter file path:")
    f = open(filename)
    print(f.read())


![image desc](/upload/X/E/J/viLDENHEWRrM.png)


In this simple procedure, we will use the operation that will be discussed in later lab. Function open() is used to open a file, and function read() to read file contents.

First, function input() will read users' input as file path. What if the file users inputting does not exist?

The file does not exist, and you will find Traceback. That is the exception system throw out. The type is FileNotFoundError.

There are many types of exceptions of Python. We do not need to remember all of them, but we need to know how to search files and understand them when receiving exceptions. Here are some of the most frequent exceptions：

- NameError: to visit an undefined variable
- SyntaxError: syntax mistakes. Strictly, this is an error of program.
- IndeError: as for a sequence, the index access exceeds the range of sequence (the concept of sequence will be discussed in later labs). You can imagine that there are three elements in my sequence, but I want to visit the fourth element.
- KeyError: to get access to a non-existent dictionary Key. This will also be explained later, if Key does not exist, the dictionary will indicate this exception.
- ValueError: input invalid parameter
- AttributeError: accessing attributes that do not exist in class objects

### Exception Handling

If there is an exception, we should use methods provided by Python to capture and tackle the exception. We'll use 3 keywords to solve the problem: try, except and finally. 

Among them, we put those code which are likely to have exception in try block and add dealing methods in except block. Back to the file read class, we put open and read into try and except block to process.

Code format is as follows：

    try:
        possibly throw an exception code
    except exception type name：
        processing code
    except exception type name：
        processing code

You should notice that it could be more than one except. They deal with different exceptions and also deal with all exceptions captured when no type name given.

Read program of improved files：

    filename = input("Enter file path:")
    try:
        f = open(filename)
        print(f.read())
        f.close()
    except FileNotFoundError:
        print("File not found")


![image desc](/upload/D/J/Q/WobJA7t5JXGu.png)


As long as there is something wrong in the try block, the rest of the code will stop executing, and will directly enter except to block try.

We write this procedure to /home/labex/fileexc.py and execute it. Then input the non-existent file mentioned above, it will be captured and processed by except.


Key word finally is used to clean up, often used with except. In another word, be it abnormal or exceptional, this code will execute.

If the error happens to f.write() when writing data to file, close cannot be executed. Using finally can make sure the content in code block will be carried out and closed files no matter block try will detect exceptions or not.

Modification of program above is as follows. Change into write operation and introduce finally to make sure files could be closed safely.

    filename = '/etc/protocols'
    f = open(filename)
    try:
        f.write('labex')
    except:
        print("File write error")
    finally:
        print("finally")
        f.close()

Result of operation：

    File write error
    finally


![image desc](/upload/E/C/B/pKVX5w2J4Tln.png)


Although it is exceptional, it still goes to the code block finally.

To point out that the reason of exception is that one opens a file in read-only mode but tries to write things. Besides, `except:` does not add any parameter behind, representing all errors in try block will be dealt with.

### Throw Exception

If we want to throw some exceptions in the program, we could use raise sentence.

    raise Exceptional name

For instance, we want to throw a ValueError in the procedure, then use it directly：

    raise ValueError()

Then external code could use except ValueError to capture and process.

## 4. Wrap Up

[In this section](https://labex.io/courses/10), we do not require code from Github code repository. If you need to save some code, you can submit by yourself.

This is all for this lab. Things are very basic, since it is almost impossible to introduce Python comprehensively in a single lab, and these are the most common and important key points：

- Development environment for Python

- Variables and data types
- Input and output
- Operations
- String operations
- Control structures
- Exception handling

Please type all the sample code in the file on your own, and try not to copy and paste. Because you get familiarized with Python code much faster by typing and practicing. If you have a question, drop us a message in the discussion forum. The basic syntax of Python 3 is not difficult. The toughest thing is to persist on programming and always have a desire to learn.
