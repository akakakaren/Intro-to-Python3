# The use of List, Tuple, Set and Dict

## Introduction

We are going to learn four most commonly used data structures in this lab: List, Tuple, Set and Dictionary

### Key Points

- The concept and operation of list
- The concept and operation of tuple
- The concept and operation of set
- The concept and operation of dict

## List

### What is List

List is an ordered assemble of data.

For instance, enter the following code in the enviornment. courses in the code is a list：

```
>>> courses = ['Linux', 'Python', 'Vim', 'C++']
>>> courses.append('PHP')
>>> courses
['Linux', 'Python', 'Vim', 'C++', 'PHP']
```

First, we establish a list called `courses`, and then use invocation list `courses.append('PHP')` to add element `PHP` to the end of the list. You can see that `PHP` has been added to the very end of the list.


![image desc](/upload/D/K/B/8DLdH68voHxS.png)


The index in the list is similar to the index reference in C language. You can have access to every element in the list through the index. The index of the first element is 0 , and the last one is -1.

```
>>>
>>> courses[0]
'Linux'
>>> courses[-1]
'PHP'
>>> courses[-2]
'C++'
>>> courses[9]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```


![image desc](/upload/R/P/G/7BUrAYHjefok.png)


It will show IndexError exception if exceeding the maximum index number limit. If you are not sure about what exception is, please go back to what we have talked about exception in the previous lab.

How do I know the number of elements in the list? Try to use `len()`：

```
>>> len(courses)
5
```


![image desc](/upload/K/U/T/x853YiMwKjyp.png)


### Operation of List

We have known the basic operation of list  `append()` from the example above that list is ordered, and `append()` is to add new elements to the end.

Sometimes we need to insert data to random location in the list, then we can use `insert()`.

```
>>> courses.insert(0, 'Java')
>>> courses
['Java', 'Linux', 'Python', 'Vim', 'C++', 'PHP']
>>> courses.insert(1, 'Ruby')
>>> courses
['Java', 'Ruby', 'Linux', 'Python', 'Vim', 'C++', 'PHP']
```


![image desc](/upload/K/B/Y/TMKkQKCTgiRv.png)


Method `count(s)` will return to the number of  element `s`. Let's check how many times `Java` appears in the list.

```
>>> courses.count('Java')
1
```


![image desc](/upload/A/H/P/JKarC300vVYN.png)


If you want to remove any appointed value in the list, use `remove()`.

```
>>> courses.remove('Java')
>>> courses
['Ruby', 'Linux', 'Python', 'Vim', 'C++', 'PHP']
```

Attention: if Java appears several times, then only the first one will be removed.


![image desc](/upload/M/B/U/EPNzfWCmZ1NO.png)


Another way is to use keyword `del` to remove. This keyword could delete elements in appointed place in the list, but we need the index of elements being removed：

```
>>> courses
['Ruby', 'Linux', 'Python', 'Vim', 'C++', 'PHP']
>>> del courses[-1]
>>> courses
['Ruby', 'Linux', 'Python', 'Vim', 'C++']
>>> courses.append('PHP')
>>> courses
['Ruby', 'Linux', 'Python', 'Vim', 'C++', 'PHP']
```


![image desc](/upload/R/M/Q/7pnvDWX6BUR5.png)


We should keep in mind that when executing all operations of list, the list is ordered and it could be reversed：

```
>>> courses
['Ruby', 'Linux', 'Python', 'Vim', 'C++', 'PHP']
>>> courses.reverse()
>>> courses
['PHP', 'C++', 'Vim', 'Python', 'Linux', 'Ruby']
```


![image desc](/upload/K/S/S/ojLU5uz0dXg5.png)


If we have two lists and want to combine them, we could merge one list to the end of the other list, using `extend()`：

```
>>> new_courses = ['BigData', 'Cloud']
>>> courses.extend(new_courses)
>>> courses
['PHP', 'C++', 'Vim', 'Python', 'Linux', 'Ruby', 'BigData', 'Cloud']
```


![image desc](/upload/R/O/M/zDRgDVgDlk4Q.png)


To put lists into order, we use `sort()`. The premise is that thr elements in that list are comparable. For example, numbers are sorted in terms of the magnitude, while character strings are sorted in alphabet order. In our example, we should use the default function order, that is the alphabet：

```
>>> courses
['PHP', 'C++', 'Vim', 'Python', 'Linux', 'Ruby', 'BigData', 'Cloud']
>>> courses.sort()
>>> courses
['BigData', 'C++', 'Cloud', 'Linux', 'PHP', 'Python', 'Ruby', 'Vim']
```


![image desc](/upload/D/D/Q/J78xIBUUvuzc.png)


Also, it could use function `pop()` to go back to the last element. `pop()` will delete the element when returning. Given a parameter i, that is `pop(i)` , the i element will pop up：

```
>>> courses
['BigData', 'C++', 'Cloud', 'Linux', 'PHP', 'Python', 'Ruby', 'Vim']
>>> c = courses.pop()
>>> c
'Vim'
>>> courses
['BigData', 'C++', 'Cloud', 'Linux', 'PHP', 'Python', 'Ruby']
>>> courses.pop()
'Ruby'
>>> courses.pop()
'Python'
>>> courses
['BigData', 'C++', 'Cloud', 'Linux', 'PHP']
>>> courses.pop(0)
'BigData'
>>> courses
['C++', 'Cloud', 'Linux', 'PHP']
```


![image desc](/upload/Q/U/F/2hE9ODpl1J32.png)


##Tuple 

tuple is a special list. It can't be modified when established. All the operation mentioned above like `sort()`、`append()` and so on are no longer applicable for tuple:

```
>>> courses = ('C++', 'Cloud', 'Linux', 'PHP')
>>> courses
('C++', 'Cloud', 'Linux', 'PHP')
>>> courses[0]
'C++'
>>> courses.sort()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'sort'
>>> del courses[0]
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'tuple' object doesn't support item deletion
```


![image desc](/upload/O/Y/I/eYEbAULsT87w.png)


When writing progarms, tuple is more reliable than list. If it's read-only data, try to use tuple and do remember tuple is unchangeable. But if there are changeble elements in tuple, they can be modified. For instance, the content could be modified when tuple has one list：

```
>>> new_courses = ('Linux', ['BigData1','BigData2','BigData3'], 'Vim')
>>> new_courses[1]
['BigData1', 'BigData2', 'BigData3']
>>> new_courses[1].append('BigData4')
>>> new_courses
('Linux', ['BigData1', 'BigData2', 'BigData3', 'BigData4'], 'Vim')
```


![image desc](/upload/G/D/I/a37gzrHk7Aol.png)


Another reminder - you cannot directly use the element in the bracket. You have to add a comma at the end of the element if you wish to establish a tuple with one element：

```
>>> courses = ('Linux')
>>> courses
'Linux'
>>> type(courses)
<type 'str'>
>>> courses = ('Linux',)
>>> courses
('Linux',)
>>> type(courses)
<type 'tuple'>
```


![image desc](/upload/L/S/M/PJwajIDz3mGZ.png)


## Set

### What is Set

Set is a collection of data that are unordered and non-repetitive. Compared with List, it is out of order, which means we cannot access it according to the index. Also there is no repeated data.

In the program development phase, set is used to remove the duplication of data elements and to test result. It also supports some of the mathematical operations, such as union，intersection, difference and symmetric difference.

To establish a set is easy, simply using braces or function set, but take note that blank set could not be established by using `{}`; only by function set because what `{}` establishes is a blank set ：

```
>>> courses = set()
>>> type(courses)
<class 'set'>
>>> courses = {'Linux', 'C++', 'Vim', 'Linux'}
>>> courses
{'Linux', 'Vim', 'C++'}
```


![image desc](/upload/L/X/H/TakCDU7jPD6V.png)


As shown from the above code, those redundant Linux character strings are eliminated automatically.

Set also can be directly created by character stings and function set together. It will break the string into different characters and eliminate the repeated one：

```
>>> nameset = set('https://labex.io')
>>> nameset
{'l', ':', '.', 't', 's', 'a', 'e', 'o', 'p', 'i', 'x', 'h', 'b', '/'}
```


![image desc](/upload/K/Y/K/L5tZH9FPgiKd.png)


### Operation of Set

We have learned the deduplication of set in the last section. But how to test whether a set exists? We could use `in`：

```
>>> 'Linux' in courses
True
>>> 'Python' in courses
False
>>> 'Python' not in courses
True
```


![image desc](/upload/H/K/T/4fXfihuPPMYn.png)


Attention. `not in` is to make sure whether `Python` is in the set. `in` also applicable for list and tuple.

We can use  `add()` to increase elements in the set, and use `remove()` to delete elements. If an element is non-existed, we'll see KeyError exception：

```
>>> courses
{'C++', 'Vim', 'Linux'}
>>> courses.add('Python')
>>> 'Python' in courses
True
>>> courses
{'C++', 'Vim', 'Python', 'Linux'}
>>> courses.remove('Python')
>>> 'Python' in courses
False
>>> courses.remove('Python')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'Python'
```


![image desc](/upload/P/T/J/PrL8q5Phx7C4.png)


Now let's try two set operation：

```
>>> set1 = {1,2,3,4}
>>> set2 = {3,4,5,6}
```

'|' can combine elements in set1 and set2, which equals to `union`:

```
>>> set1 | set2
{1, 2, 3, 4, 5, 6}
>>> set1.union(set2)
{1, 2, 3, 4, 5, 6}
```

`&` can return elements that are both in set1 and set2:

```
>>> set1 & set2
{3, 4}
```

`-` can return elements in set1 and **not** in set2:

```
>>> set1 - set2
{1, 2}
```

`^` can return elements which are unique to set1 and set2 (elements are only in set1 or set2)：

```
>>> set1 ^ set2
{1, 2, 5, 6}
```


![image desc](/upload/C/K/X/TjBTKrEpxIGB.png)


## Dict

dict is a collection of disordered key-value pairs. Every single element in it is a combination of a key and a value. Key must be the unique one in the dict so that we can easily find the corresponding value of that key.

It is the same to use braces to create a dict as to create a key. We have mentioned before that `{}` will establish a blank set, and if it is not blank, every single element in the braces is written in `key:value` . Now let's create a dict to save our courses'ID and name. ID is key，and name is value：

```
>>> coursesdict = {1:'Linux', 2:'Vim'}
>>> coursesdict
{1: 'Linux', 2: 'Vim'}
>>> coursesdict[1]
'Linux'
>>> coursesdict[2]
'Vim'
```


![image desc](/upload/B/Q/F/2GEJNY2sGfVo.png)


Attention - Key does not have to be figures, but can have various types, such as this one：

```
testdict = {1:2, 'teststr':'labex.io', 9:[1,2,3]}
```

In testdict, one pair of key-value is number 1 and 2, one is two strings, and the other  is a pair of key-value composed of figures and lists. Although they seem meaningless when mixing together, they are applicable.

If key does not exist,`dict[key]` will show KeyError. Sometimes in order to avoid this mistake,we will use function `get()` to gain the corresponding value of key. If key does not exist at present, it will return to None autometically. You could also give a default value in  `get()` , it will return back to the default value if key is non-existent：

```
>>> testdict
{1:2, 'teststr':'labex.io', 9:[1,2,3]}
>>> coursesdict[2]
'Vim'
>>> coursesdict[4]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 4
>>> coursesdict[2]
'Vim'
>>> coursesdict.get(2)
'Vim'
>>> coursesdict.get(4)
>>> coursesdict.get(4, 'default')
'default'
```


![image desc](/upload/F/H/P/Qa2zUNG6ukl5.png)


Same as set, dict could use function dict to create. Parameter is a tuple containing more than one binary groups (a bit tricky, pay attention to the number of brackets)：

```
>>> dict_from_tuple = dict(((1,'Linux'), (2,'Vim')))
>>>
>>> dict_from_tuple
{1: 'Linux', 2: 'Vim'}
```


![image desc](/upload/R/V/W/uWPDnY5e5qoz.png)


Attention, dict is through `[]` to collect data, but is different from List in that the thing in `[]` is key which means it could be figures or any other types, not merely the index. Since dict is out of order, it cannot be accessed through the index. Plus, the key in dict is unchangeble.

To add elements into dict, you only need to give value to one key. If the key already exists, it should update the corresponding value. If not, it means to add `key: value` to the dict：

```
>>> coursesdict[5] = 'Bash'
>>> coursesdict[6] = 'Python'
>>> coursesdict
{1: 'Linux', 2: 'Vim', 5: 'Bash', 6: 'Python'}
```


![image desc](/upload/B/A/M/eIMv5mGUmh6g.png)


To eliminate an element from the dict, you only have to use `del` . If key is non-existent,then give KeyError：

```
>>> del coursesdict[1]
>>> del coursesdict[1]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 1
```


![image desc](/upload/T/C/H/w1kDnINhugqX.png)


In dict, we could use function `items()` to acquire all the `dict_items` type element . You can use `for` to traverse the dict. Elements are all two-tuples. Please notice that you have to input four blank mannually which is the requirement we mentioned before：

```
>>> for key,value in coursesdict.items():
...     print(key,value)
...
2 Vim
5 Bash
6 Python
>>>
```


![image desc](/upload/M/X/L/op68t8MjBGdM.png)


In addition, we can use `keys()` and `values()` to get all lists of key or value respectively：

```
>>> coursesdict
{2: 'Vim', 5: 'Bash', 6: 'Python'}
>>> coursesdict.keys()
dict_keys([2, 5, 6])
>>> coursesdict.values()
dict_values(['Vim', 'Bash', 'Python'])
```


![image desc](/upload/U/G/B/I4PYxMxyNSYe.png)


There is a function `pop(key)` in the dict, which can return to the corresponding value of key and delete the key-value pair：

```
>>> coursesdict
{2: 'Vim', 5: 'Bash', 6: 'Python'}
>>> coursesdict.pop(2)
'Vim'
>>> coursesdict
{5: 'Bash', 6: 'Python'}
```


![image desc](/upload/X/D/H/4mr3GIgIMvk5.png)


## Concusion

In this lab, we learned list, tuple, set and dict, the four commonly used storage methods, through a series of practical experience. In reality, these methods are all very useful. Remember to practice when you get a chance. 

1. list：can modify ordered data collection
2. tuple：cannot modify ordered data collection
3. set：disordered and non-repeating data collection
4. dict：disordered storage for key-value data collection 


Please enter all the sample code ny yourself. And please try not to copy and paste. Only in this way, you can practice your coding skill. Whenever you encounter a question, stop by our discussion forum. 