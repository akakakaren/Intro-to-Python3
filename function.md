# Function

##  Introduction

### What is Function

We usually need to use the same code repeatedly in a program, and function can help us with that. Functions have parameters and return values. They process the parameter inwardly and then give back the result to users.

### Built-in Functions

Built-in functions are the function which can be applied all the time without introducing any package in Python interpreter. We have tried some built-in functions before, like `len()` and `type()`.

The built-in functions and references of Python 3 could be seen from the [document](https://docs.python.org/3/library/functions.html).

The most commonly used function is still the one you defined in the program development.

### Key Points

- The concept of function
- Definition and calling of function
- Variable scope
- Parameter transmission
- Default parameter
- Variable arity methods
- Modification of function parameter

## Definition and Calling of Function

We use the keyword `def` to define a function. To define a  function, we need to put parameters in the braces ,and plus`:`, and then enter built-in code in another line. Pay attention to the indent：

```
def functionname(params):
    statement1
    statement2
```

The function we wrote accepts a string and a letter as a parameter, and regard the frequency of this letter as the return value. Remember we have said previously that the string is a special list which could use function`count()` to return appointed amount of elements.

```
>>> def char_count(str, char):
...     return str.count(char)
...
```

In the second line, the keyword `return` enables the function to return the frequency of char in str to users.

How to use the function? We have to do the following:

```
>>> char_count('https://labex.io', 't')
2
>>> result = char_count('https://labex.io', 's')
>>> result
1
```


![image desc](/upload/A/V/N/JJzARqocICST.png)


To be specific, the variable result is to save return value of functions, and the two parameters we entered are the string and letter for testing.

Now we want to change the function `char_count()` . First to accept a parameter, and then print out all letters and their frequency, which is realized in a Python script.

First, to use editors like sublime or vim to create a file, and then give command as follows in the Xfce terminal: 

```
$ vim count_str.py
```

Type code in following order：


```py
#!/usr/bin/env python3

def char_count(str):
    char_list = set(str)
    for char in char_list:
        print(char, str.count(char))
        
if __name__ == '__main__':

    s = input("Enter a string: ")

    char_count(s)
```

Save and execute - the procedure will ask you to give a string, and print the frequency of all characters in the string.

```
$ python3 count_str.py
Enter a string: labex.io
o 1
a 1
e 1
l 1
x 1
. 1
b 1
i 1
```


![image desc](/upload/Y/K/S/8nMO5AVLcdGV.png)


Now let's talk about this program in details：

1. The first line means we need Python 3 interpreter to execute the current script.
2. Function char_count does not have returned value, which is no keyword returned. It is permissible because the returned value and parameters are optional.
3. char_count would acquire all those non-repeated character set initially
4. then to use `for` to traverse the set, and use `str.count()` we mentioned in the last example to count the frequency of every character.
5. finally to print character and the corresponding frenquncy
6. `if __name__ == '__main__':` this sentence equals to the function `main` in C. As the entry of execution, its actual use is to run the program independently and also work in other programs.

## Variable Scope

We are going to use some examples to understand local or global variables. First, let's use the same variable `a` within a function and calling, use `vim local.py` to creat a file and write code below：

```python
#!/usr/bin/env python3
# local.py
def change():
    a = 90
    print(a)
a = 9
print("Before the function call ", a)
print("inside change function", end=' ')
change()
print("After the function call ", a)
```

execution：


![image desc](/upload/Q/G/W/ZFyaxThhq1TR.png)


Fisrt, we give value 9 to  `a` , and then change the function in calling. In this function, we give value 90 to  `a` , and print it. After calling, we print  `a` again.

When we write `a = 90`  ,it actually creates a new local variable called  `a` ，which can only be used in the function, and will be destroyed when the function is finished. So even if the two variables have the same name, they are not the same in fact.

If we define  `a` in the first place, could it be used directly in the function? Now we use `global` as keyword to mark the external  `a`  of funtion as glabal variable. As a result, `a` in the program would be like this：

```python
#!/usr/bin/env python3
# global.py
global a
a = 9
def change():
    print(a)
print("Before the function call ", a)
print("inside change function", end=' ')
change()
print("After the function call ", a)
```

The result will not mention the mistake anymore, because within the function, the global variable `a` is already accessible within the function：

```
Before the function call  9
inside change function 9
After the function call  9
```


![image desc](/upload/P/Y/E/6OBfYQNdjHkE.png)


What if using `global` inside the function? Try these code：

```
#!/usr/bin/env python3
def change():
    global a
    a = 90
    print(a)
a = 9
print("Before the function call ", a)
print("inside change function", end=' ')
change()
print("After the function call ", a)
```

result：

```
Before the function call  9
inside change function 90
After the function call  90
```

Here, through the keyword `global` , `a` is defined as a whole, therefore, the change of `a` within the function also leads to the change in  `a` outside the function.

execution：


![image desc](/upload/Q/O/J/zIcJDs1Bnkd1.png)


## Parameter Transmission

Here are a few things we should keep in mind. If not performed accurately, they are bug-prone：

1. The order of parameter - if parameter transmission is not through the name of argument, then the order of argument should be in accordance with function's definition
2. When calling the function, the parameter not being transmitted will use the default value
3. Transimit the parameter by name
4. Variable-length parameters 
5. Modify the parameter value in the function

Now let's explain these one by one. 

### Parameter Order and Parameter Name

This is easy to understand. Because the order is given in definition, and if not following the order, it has to transmit by name.

For example, to realize a program connecting to the server in the interactive environment, IP address and the port number are needed as parameter:

```
>>> def connect(ipaddress, port):
...     print("IP: ", ipaddress)
...     print("Port: ", port)
...
>>> connect('192.168.1.1', 22)
IP:  192.168.1.1
Port:  22
>>> connect(22, '192.168.1.1')
IP:  22
Port:  192.168.1.1
>>> connect(port=22, ipaddress='192.168.1.1')
IP:  192.168.1.1
Port:  22
>>>
```


![image desc](/upload/Q/Q/Y/YAY1Im6kx3k0.png)


Examples above have tried three times to pass parameter respectively. First time uses the default order; second time the wrong number, and the third time is passing by name although in wrong order.

We can also mark the function paramer as only allowing to transmit parameter by name. When user is calling a function, they can only use a specific name in accordance with each parameter. If not, TypeError will show:

```python
>>> def hello(*, name='User'):
...     print("Hello", name)
...
>>> hello('labex')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: hello() takes 0 positional arguments but 1 was given
>>> hello(name='labex')
Hello labex
```


![image desc](/upload/N/H/Y/ud40L1N4Okc8.png)


### Default Parameter Values

The parameter variable can have default value which means if we do not give any value to the appointed parameter, it will be default value and change the program above, using default port 22:

```python
>>> def connect(ipaddress, port=22):
...     print("IP: ", ipaddress)
...     print("Port: ", port)
...
```

This means if a user does not give value to `port`, then `port` will be 22. This is a very simple example on default parameter.

You can test code by calling function

```python
>>> connect('192.168.1.1', 2022)
IP:  192.168.1.1
Port:  2022
>>> connect('192.168.1.1')
IP:  192.168.1.1
Port:  22
>>>
```


![image desc](/upload/M/N/N/MhUGo7uncBhr.png)


There are two significant parts. One is the first parameter with the default value no longer followed by normal parameter. For example, `f(a,b=90,c)` is wrong.

Second is the default value can only be assigned once. So it would be different if the default value is changeable, such as list, dict or instances of most classes

```python
>>> def f(a, data=[]):
...     data.append(a)
...     return data
...
>>> print(f(1))
[1]
>>> print(f(2))
[1, 2]
>>> print(f(3))
[1, 2, 3]
```

![image desc](/upload/V/K/H/mVAu7rWQni0M.png)

To avoid this problem, do the following:

```python
>>> def f(a, data=None):
...     if data is None:
...         data = []
...     data.append(a)
...     return data
...
>>> print(f(1))
[1]
>>> print(f(2))
[2]
```


![image desc](/upload/O/I/I/e47gV1yuus4g.png)


### Variable Length Parameters

If a function has unstable number of parameters, maybe one or more than one, what are you supposed to do?

For instance, we are going to count the sum of numbers, then the transmission could be directly introducing a list or a tuple (tuple would be better when the value is not changed), or passing several changeable parameters.

Changeable parameters needs to add  `*` before the parameter list. For example, the function connection is to connect multiple port of taget server:

```
>>> def connect(ipaddress, *ports):
...     print("IP: ", ipaddress)
...     for port in ports:
...         print("Port: ", port)
...
```

You can pass 0 or multiple ports during function calling:

```
>>> connect('192.168.1.1')
IP:  192.168.1.1
>>>
>>> connect('192.168.1.1', 22, 23, 24)
IP:  192.168.1.1
Port:  22
Port:  23
Port:  24
>>> connect('192.168.1.1', 22)
IP:  192.168.1.1
Port:  22
```


![image desc](/upload/K/D/I/XGXvZr8562T7.png)


### Modification of Function Parameter

Is it possible to change the value of parameter in the function when passing?

There is a concept of pass and pass (pointer) in C/C++ , affecting whether the function could change the value of parameter directly.

Function parameter value means that during the calling, the parameter used within the function is only a local variable. It will be destroyed after finishing execution, and will not affect the value of the external parameter of the function.

Function parameter reference means that the parameter passed to the function is the external parameter. Execution would maintain any modification of the parameter, and when the calling is over, this parameter will contain the modified data even used in other code.

But it is differrent in Python. Python's parameters do not have types and can pass an object as a parameter randomly. But different types of parameter will not perform the same in functions if being modified. Use `vim test.py` to create a file and type code below.

Example：

```
#!/usr/bin/env python3

def connect(ipaddress, ports):
    print("IP: ", ipaddress)
    print("Ports: ", ports)
    ipaddress = '10.10.10.1'
    ports.append(8080)

if __name__=="__main__":
    ipaddress = '192.168.1.1'
    ports = [22,23,24]
    print("Before connect:")
    print("IP: ", ipaddress)
    print("Ports: ", ports)
    print("In connect:")
    connect(ipaddress, ports)
    print("After connect:")
    print("IP: ", ipaddress)
    print("Ports: ", ports)
```

Result：

```
Before connect:
IP:  192.168.1.1
Ports:  [22, 23, 24]
In connect:
IP:  192.168.1.1
Ports:  [22, 23, 24]
After connect:
IP:  192.168.1.1
Ports:  [22, 23, 24, 8080]
```


![image desc](/upload/D/G/R/uHkWSgVBb3Xt.png)


You will see the changed value of IP address does not work in the function, but the list of ports changes.

The unchangeble object in Python are value, string, and tuple. Changeable objects are list, and dict. If the parameter is a unchangeable object, then it's passing the value, and the modification of the parament will not be saved in the function, and if it is a changebale object, which is passing reference, the modification will be saved.

## Conclusion

Through this lab, you should know how to define functions, and have a clear understanding of local and global variables. Also,you need to know what is default value and different kinds of pass parameters.

In addition, Python does not have *Function overload* whihc is quite common in other advanced languages. This is because Python has default value which can replace *function overload* in most cases.
