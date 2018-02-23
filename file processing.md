# File Processing

## Overview of File Processing

File processing is the main way in the project to make data persistent. We are in face of a variety of files in daily work, such as word, video, txt text and so on. Python provides a very convenient function to read and write files. You can easily handle all types of files.

In this lab, we will learn how to use Python to do the following file processing:

1. Open and close the file
2. Read the contents of the file
3. Write the file
4. Serialization of pickle and JSON 
5. os.path module

### Knowledge Points

- Open and close files
- Read and write files
- Read the file by line
- Serialization of pickle 
- Serialization of JSON 
- os.path module

## Open and Close

We use the open () function to open the file. This function will return a file object, and we will read and write the file using this object.

The open () function takes two arguments. The first argument is the file path or file name, and the second is the file's open mode. The pattern is usually like this:

- " r ", open in read-only mode, you can only read the file but can not edit / delete any of the contents of the file
- " w " to open in write mode, if the file exists, the content inside will be deleted, and then open and write
- " a ", open in the additional mode, any data written to the file will be automatically added to the end
- " b ", opened in binary form

The default mode is read-only, that is, if you do not provide any mode, the open () function will open the file in read-only mode.

We will try to open a file in the interactive mode of Python:

    >>> file = open('/etc/protocols')
    >>> type(file)
    <class '_io.TextIOWrapper'>
    >>> file
    <_io.TextIOWrapper name='/etc/protocols' mode='r' encoding='ANSI_X3.4-1968'>


![image desc](/upload/W/M/J/crc1Cls6C6Bz.png)


From the information above , you can see the open file / etc / protocols.The mode is read-only mode, encoding UTF-8.

When the program is finished, we need to close the file. If we do not shut down, it will continue to take up some memory and operating system resources and also it may lead to the data loss. We use close () to complete this operation, repeating the closure will not have any effect:

    >>> file.close()
    >>> file
    <_io.TextIOWrapper name='/etc/protocols' mode='r' encoding='ANSI_X3.4-1968'>
    >>> file.close()


![image desc](/upload/S/U/K/q45jIGp62rCm.png)


In fact, we should try to use the statement `with`  to handle the file object, which will automatically shut down after the file runs out, even an exception does not matter. It is a shorthand for `try-finally` block:

    >>> with open('/etc/protocols') as file:
    ...     count = 0
    ...     for line in file:
    ...         count += 1
    ...     print(count)
    ...
    64

In this program we will print the number of lines of the file, you can see 'close' is not used in the code block, but when the code is executed outside the code block, the file will be automatically closed.


![image desc](/upload/P/D/T/KmBd45ifGJBk.png)


## Read File Contents

Here we first use the echo command to create a file. The content of this file includes two lines:

    I love python
    lab+ at labex.io

Create the file path for / home / labex/ test.txt.The command we create:

    $ echo 'I love Python' > /home/labex/test.txt
    $ echo 'lab+ at labex.io' >> /home/labex/test.txt
    $ cat test.txt
    I love Python
    lab+ at labex.com


![image desc](/upload/V/I/X/wS2ZgIkxoeys.png)


Use read () to read the contents of the entire file at once, return contents in string type：

    >>> filename = '/home/labex/test.txt'
    >>> file = open(filename)
    >>> file.read()
    'I love Python\nlab+ at labex.io\n'
    >>> file.close()


![image desc](/upload/H/X/M/0re4zd3OFJgf.png)


Of course you can also use 'with', to avoid forgetting the 'close'：

    >>> filename = '/home/labex/test.txt'
    >>> with open(filename) as file:
    ...     file.read()
    ...


![image desc](/upload/C/T/E/amMgJvvwFEnY.png)


In project development, we need to be careful using read () to read the entire file, because it is possible that your system memory is not enough to store the contents of the entire file. When read () is executed, there will be no more output.

We usually deal with text files step by step. readline() is to read one line at one time, while readlines() can read all lines. But different from read (), this function returns a list.Each element in the list is a string corresponding to the contents of a line in the text file:

    >>> filename = '/home/labex/test.txt'
    >>> file = open(filename)
    >>> file.readline()
    'I love Python\n'
    >>> file.readline()
    'lab+ at labex.io\n'
    >>> file.close()


![image desc](/upload/D/Y/L/WHwy09DBSRE0.png)


Since we have used readline() twice, to use it a second time will have no more output, so we need re-open the file:

    >>> file = open(filename)
    >>> file.readlines()
    ['I love Python\n', 'lab+ at labex.io\n']
    >>> file.close()


![image desc](/upload/H/Q/H/ajoMae4FcHHt.png)


You can loop through the file object for loops to read every line in the file：

    >>> file = open(filename)
    >>> for x in file:
    ...     print(x, end = '')
    ... 
    I love Python
    lab+ at labex.io
    >>> file.close()


![image desc](/upload/X/S/O/5ObM57MyMcpl.png)


Let's write a program that accepts the user-entered string as the file name to be read, and print the number of lines and the contents of the file on the screen：


    #!/usr/bin/env python3
    filename = input("Enter the file name: ")
    with open(filename) as file:
        count = 0
        for line in file:
            count += 1
            print(line)
        print('Lines:', count)

program running：

    $ ./test.py
    Enter the file name: /home/labex/test.txt
    I love Python
    
    lab+ at labex.io
    
    Lines: 2


![image desc](/upload/G/B/A/fya4dxWi7iUW.png)


## Files-writing

The most commonly used function to write a file is write(). Let's open a file using write() and then write some text.

    >>> filename = '/home/labex/test.txt'
    >>> with open(filename, 'w') as file:
    ...     file.write('testline1')
    ...     file.write('testline2')
    ...
    9
    9


![image desc](/upload/Y/R/P/q9UXeE4SOfXV.png)


In this program, we will open the file in 'w' mode, and then write two pieces of content. The output of the two 9 during the implementation of the process indicates the number of characters we write twice respectively.

To view whether the contents of the file that has just been written has changed, we use readlines():

Let's read the file we created just now.

    >>> with open(filename) as file:
    ...     file.readlines()
    ...
    ['testline1testline2']


![image desc](/upload/O/S/G/F30BVjGLxzIL.png)


We will find that the original content of the file has been completely covered. And the contents are written in takes up a line (because there is no line break).

What if we want to add content to the file? You can use the add mode `a` to open a file

    >>> filename = '/home/labex/test.txt'
    >>> with open(filename, 'a') as file:
    ...     file.write('testline3')
    ...     file.write('testline4')
    ...
    9
    9


![image desc](/upload/Q/P/G/NWOJqWKomdLN.png)


Read again, and you can see the newly added string attached to the original content behind:

    >>> with open(filename, 'r') as file:
    ...     file.readlines()
    ...
    ['testline1testline2testline3testline4']


![image desc](/upload/O/O/R/u131VpP19V3W.png)


## Example of File-copying

In this example, we copy the given text file to another given text file to achieve the similar command of the Linux cp.The program accept two parameters, the first parameter indicates the path of original file, the second parameter indicates the path of new  copied file. The code is as follows, please to understand the code for each line:


    #!/usr/bin/env python3
    # copyfile.py
    import sys
    def copy_file(src, dst):
        with open(src, 'r') as src_file:
            with open(dst, 'w') as dst_file:
                dst_file.write(src_file.read())
    
    if __name__ == '__main__':
        if len(sys.argv) == 3:
            copy_file(sys.argv[1], sys.argv[2])
        else:
            print("Parameter Error")
            print(sys.argv[0], "srcfile dstfile")
            sys.exit(-1)
        sys.exit(0)


![image desc](/upload/G/Q/Y/ICNWlBQjqcag.png)


You can see that we are using a new module sys here. sys.argv contains all arguments.

the first value of sys.argv, that is sys.argv [0], is the name of the program itself, and the following program prints parameters:


    #!/usr/bin/env python3
    # argvtest.py
    import sys
    print("Program:", sys.argv[0])
    print("Parameters:")
    for i, x  in enumerate(sys.argv):
        if (i == 0):
            continue
        print(i, x)

execution:

    $ chmod +x argvtest.py
    $ ./argvtest.py lab+ labex.io
    Program: ./argvtest.py
    Parameters:
    1 lab+
    2 labex.io


![image desc](/upload/N/E/O/73x33mQQn3M3.png)


Here we use a new function enumerate (iterableobject). When used in the loop, the list, the index position and the corresponding value can be acquired at the same time. Here in the parameter list we use 'continue' to remove the sys.argv [0] program's own name.

## Serialization of pickle and JSON

What if we want to save a Python object with a text file?

Serialization refers to converting the object of memory into a format that coulde be stored. The most common two ways of Python are:

1. pickle module
2. JSON format

### pickle

We first create a dictionary of courses, we write the courses information into a file in serilization, then we read data from the file deserilization:

    >>> import pickle
    >>> courses = { 1:'Linux', 2:'Vim', 3:'Git'}
    >>> with open('./courses.data', 'wb') as file:
    ...     pickle.dump(courses, file)
    ...
    >>> with open('./courses.data', 'rb') as file:
    ...     new_courses = pickle.load(file)
    ...
    >>> new_courses
    {1: 'Linux', 2: 'Vim', 3: 'Git'}
    >>> type(new_courses)
    <class 'dict'>
    >>>

Note that writing and reading files requires the use of binary mode `b`.

Eventually, we write and read the file. And it still can turn back into the original dictionary object. If you just want to serialize the object into a byte stream, you can use pickle.dumps (obj).


![image desc](/upload/U/B/S/00po3SUNBOt9.png)


### JSON

JSON(JavaScript Object Notation, JS object tag) is a lightweight data exchange format.

JSON format in the Internet application development is used very extensively. It can be used as a different service components for data transfer among different format. In a variety of APIs provided by the Internet application, return values are basically JSON format.

Python also provides the json module to support JSON serialization. We still use the example above  and we use the JSON format for serialization:

    >>> import json
    >>> courses = { 1:'Linux', 2:'Vim', 3:'Git'}
    >>> json.dumps(courses)
    '{"1": "Linux", "2": "Vim", "3": "Git"}'
    >>> with open('courses.json', 'w') as file:
    ...     file.write(json.dumps(courses))
    ...
    38
    >>> with open('courses.json', 'r') as file:
    ...     new_courses = json.loads(file.read())
    ...
    >>> new_courses
    {'1': 'Linux', '2': 'Vim', '3': 'Git'}
    >>> type(courses)
    <class 'dict'>

dumps and works perform serialization and deserialization respectively, and the content after JSON serialization is a string, so text writing and reading do not need to be in binary format.


![image desc](/upload/R/C/W/iyQHpWakauF1.png)


## os.path File and Folder Operation

Here is a brief introduction to the os.path. This is a very commonly used standard library, and the main purpose of this library is to obtain and process file and folder properties.

The following code examples introduce a few commonly used methods. More content could be looked up in documents in use.

- os.path.abspath (path) Returns the absolute path to the file
- os.path.basename (path) Returns the file name
- os.path.dirname (path) Returns the file path
- os.path.isfile (path) to determine whether the path is a file
- os.path.isdir (path) to determine whether the path is a directory
- os.path.exists (path) to determine whether the path exists
- os.path.join (path1 [, path2 [, ...]]) Synthesize directory and file name into a path

experiment code content needs to be handled in a Python interactive environment:

    >>> import os
    >>> filename = '/home/labex/test.txt'
    >>> os.path.abspath(filename)
    '/home/labex/test.txt'
    >>> os.path.basename(filename)
    'test.txt'
    >>> os.path.dirname(filename)
    '/home/labex'
    >>> os.path.isfile(filename)
    True
    >>> os.path.isdir(filename)
    False
    >>> os.path.exists(filename)
    True
    >>> os.path.join('/home/labex', 'test.txt')
    '/home/labex/test.txt'
    >>>


![image desc](/upload/X/J/C/TPgId1X5DnfI.png)


## Conclusion

In this lab, we have learned about the opening and reading  a file and the basic usage of serialization and file path operations. Here, review these key points：

- Open and close a file
- The use of keywords 'with'
- File reading method
- Write the file
- Serialization pickle
- Serialization JSON
- os.path file and folder operation

These are used very commonly in real project development, and in each programming language studying, the files opoerations will be important content . In Internet projects, JSON serialization is a commonly used method, provided as a Web Service API to connect different services. You must understand why we need to use serialization.




