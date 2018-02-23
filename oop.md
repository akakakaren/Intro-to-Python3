# Object Oriented Programming(OOP)

## Introduction

OOP is an idea of programming design.The program design based on the process-oriented idea is executed under command one by one.If commands become more, they are divided into functions we mentioned in the previous labs.The object-oriented programming thought is to view the object as the composed unit of the program, and the execution is through the interface provided by the calling object.

The concept of object-oriented programming is an impalpable through theory, and we will encounter with this concept frequently in the following tasks.This lab is just a warm-up which will not be too tough.

Four Core Conceptions of Object-Oriented Programming

- Abstract
- Encapsulation
- Inheritance
- Polymorphism

Next, we will give examples and code to understand these four conceptions and how to apply them in Python.

### Knowledge Points

- Object-oriented idea
- Abstract
- Encapsulations, classes, and instances
- Inheritance and overriding
- Polymorphism
- Private properties and methods
- Static variables and class methods
- property

## Start from Process-Oriented

There‘s a word 

> A dog called Doge and a cat called Kitty are barking.Doge squawks like woof woof woof and Kitty squawks like meow meow meow. 

If we are to turn the sentence into programming language, using process-oriented way, we probably get code like this, this part is just a figurative explanation and cannot be carried out

```c
def main():
    dog_name = 'Doge';
    dog_sound = 'woof woof woof...';
    cat_name = 'Kitty';
    cat_sound = 'meow meow meow...';
    print(dog_name + ' is making sound ' + dog_sound);
    print(cat_name + ' is making sound ' + cat_sound);

if __name__ == '__main__':
	main() 
```

the result will be

```
Doge is making sound woof woof woof...
Kitty is making sound meow meow meow...
```

That's normally the style of process-oriented code. You can write this program into a file using sublime (or other text editor), save it to desktop.


![image desc](/upload/S/H/Y/aaGDq5Ok6YtE.png)


## Abstract

How to write the program above using object-oriented idea? First is to abstract. The abstract is the process of selecting common features and behavior from specific examples.

In the program, "Doge" is a kind of dog, and it has a name.It can bark like"woof woof woof". We can abstract such a type of dog:
```
dog {
  name(feature)
  bark()(behaviour)
}
```

It is the same for the cat. Kitty can be abstracted as a type of cat, and it has a name, but its behavior(sound) is different

```
cat {
  name(feature)
  mew()(behaviour)
}
```


Features and behavior are usually called Attribute and Method in the programming language.

## Encapsulations, classes and instances

In the process-oriented language, encapsulation is using classes to gather data and operation based on data, and hide internal data and provide external access to the public interface.

To turn the abstraction into Python

```py
class Dog(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name
    def set_name(self, value):
        self._name = value
    def bark(self):
        print(self.get_name() + ' is making sound woof woof woof...')

class Cat(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name
    def set_name(self, value):
        self._name = value
    def mew(self):
        print(self.get_name() + ' is making sound meow meow meow...')

if __name__ == '__main__':
	# Instantiate an Object in Python
    dog = Dog('Doge')
    cat = Cat('Kitty')
    dog.bark()
    cat.mew()
```

`object`  is the ancestor of all objects in Python. It is the fundamental type of all types. And a type need a construction method, `__init__`  is the construction method of Python. Attention, there is two underline  `_` in front and behind `self` represents the current object.

The class is an abstraction concept, while the instance is a concrete object.For instance, the dog is an abstraction concept, because there are many kinds of dogs, and that dog called Doge which is barking ''woof'' is an instance.

the result will be

```
Doge is making sound woof woof woof...
Kitty is making sound meow meow meow...
```

The 'bark' method in dog class realizes the information output of dog sound, but you have to create an object using `Dog()` first.


![image desc](/upload/S/B/U/r3jwTOaMOOJG.png)


What's the benefit to hide data access? The biggest one is to provide us access control. For instance, in the cat class, usernames could have lowercase and uppercase. While we hope to provide to the public with nouns in boldface capital and lowercase letters, thus we can achieve access control with`get_name` method.

```py
def get_name(self):
    return self._name.lower().capitalize()
```

In the class of Python, function `__init__()` is executed in the object creation, not a necessary function for creating object. Actually, the function for creating objects is `__new__()`while `__new__()` inherited from  functions of object class, thus here we do not realize it again, and in `__new__()`  we even could appoint whether to execute `__init__()`.

## Inheritance and Overriding

It is obvious to abstract Doge as a dog and Kitty as a cat that you may not notice that we have already completed an abstraction. We can have a further abstraction for dog and cat: they are both animals with names, and they can give a sound though different. Then we have an abstract class

```py
class Animal(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name
    def set_name(self, value):
        self._name = value
    def make_sound(self):
        pass
```

Since each animal has their own sound, we do not have a way to realize `make_sound` in the abstract class, using the pass to directly skip this function.

Dog and Cat are different kind of animal, so there is inheritance between Animal class and each of them. In Python that is

```py
class Dog(Animal):
    def make_sound(self):
        print(self.get_name() + ' is making sound woof woof woof...')

class Cat(Animal):
    def make_sound(self):
        print(self.get_name() + ' is making sound meow meow meow...')
```

Dog and Cat inherit the construction method from its parent class Animal: `get_name` and `set_name` , and rewrite  `make_sound` method from the parent class.

Now the main program is

```py
dog = Dog('Doge')
cat = Cat('Kitty')
dog.make_sound()
cat.make_sound()
```


![image desc](/upload/I/R/L/dqgQILHRru5s.png)


## Polymorphism

In short, polymorphism is using the same method to different objects and to get different results.

Now we are going to explain it with an example.Imagine that we are using a strongly typed language like Java, we have to claim the class before using the variable.


Imagine that we have another dog called "Doty" and a cat called "Betty", they are barking too. Then we may have code like this

```py
# more animal
dog1 = Cat('Doge')
cat1 = Cat('Kitty')
dog2 = Dog('Doty')
cat2 = Cat('Betty')
dog1.make_sound()
cat1.make_sound()
dog2.make_sound()
cat2.make_sound()
```

![image desc](/upload/D/C/L/0n1HJXAHQegn.png)


Dog and Cat both inherit from Animal and realize their  make_sound method so with the feature that strongly typed language parent class reference can point to the subclass object, we can write polymorphic code.

```py
# iterate a list of animals
animals = [Dog('Doge'), Cat('Kitty'), Dog('Doty'), Cat('Betty')]
for animal in animals:
    # Polymorphism
    animal.make_sound()
```


![image desc](/upload/J/H/G/cJN5jtVnLKea.png)


You can see that regardless of whether the specific animal is Dog or Cat, you can execute the make_sound method in the for loop. This is the object-oriented polymorphism.

## Private Attributes and Methods

In Java and C ++, you can use the `private` and` protected` keywords to modify properties and methods that confine whether properties and methods can be accessed by an external class or subclass. In Python, you can add `__` (two Underlined `_`) to deny external access.


```py
>>> class Labex:                                                                                                                                                                                                
...   __private_name = 'labex'                                                                                                                                                                                
...   def __get_private_name(self):                                                                                   
...     return self.__private_name                                                                                    
...                                                                                                                   
>>> s = Labex()                                                                                                                                                                                                                
>>> s.__private_name                                                                                                  
Traceback (most recent call last):                                                                                    
  File "<stdin>", line 1, in <module>                                                                                 
AttributeError: 'Labex' object has no attribute '__private_name'                                                                                                                                                               
>>> s.__get_private_name()                                                                                            
Traceback (most recent call last):                                                                                    
  File "<stdin>", line 1, in <module>                                                                                 
AttributeError: 'Labex' object has no attribute '__get_private_name'
```


![image desc](/upload/Y/N/R/YdvBbHJIN3JU.png)


Why is it an "convention" because it is not absolutely private in Python, or through `obj._Classname__privateAttributeOrMethod`

```py
>>> s._Labex__private_name                                                                                        
'labex'
>>> s._Labex__get_private_name()                                                                                  
'labex'
```


![image desc](/upload/V/F/C/zL77Bq9rJf1S.png)


Thus `__`  is just a convention, indicating that external users do not use this property and method directly.

## Static Variables and Class Methods

Static variables and class methods are accessible directly from classes and can be accessed without instantiating objects. Assuming that the animals in the example above both belong to 'jack', then you can use a static variable in the `Animal` class, usually in front of` __init__`:

```py
class Animal(object):
    owner = 'jack'
    def __init__(self, name):
        self._name = name
class Cat(Animal):
	pass
```

Can now be accessed directly via Animal or subclasses

```py
if __name__=='__main__':
	print(Animal.owner)  # 'jack'
	print(Cat.owner)     # 'jack'
```


![image desc](/upload/H/I/E/I23k8k7yFW1t.png)


Class method and static variables are similar.It can also be directly accessed through the class name.Class method with `@ classmethd` decoration can access the class static variables,The following add a class method` get_owner`:

```py
class Animal(object):
    owner = 'jack'
    def __init__(self, name):
        self._name = name
    @classmethod
    def get_owner(cls):
        return cls.owner
```

Note that the first argument passing to the class method is the class object, not the instance object, so it is `cls`.

Get the owner by class method:

```py
print(Animal.get_owner())  # 'jack'
print(Cat.get_owner())     # 'jack'
```


![image desc](/upload/W/G/Y/VbN15gwy8JJZ.png)


## property

In Python, the property can be used as a property to implement a Python-style getter/setter, which can be used to get and modify a property of an object.

Use the property to rewrite the Animal class

```py
class Animal(object):
    def __init__(self, name):
        self._name = name
    @property
    def name(self):
        return self._name
    @name.setter
    def name(self, value):
        self._name = value
    def make_sound(self):
        pass
```

So that we can get `name` through access the property.

```
cat = Cat('Kitty')
print(cat.name)
```


![image desc](/upload/Q/U/I/s3YvTx56a7x0.png)


## Static Method

The static method is decorated with `@ staticmethod`, which is somewhat similar to` classmethod`. Staticmethod does not require instance participation in runtime, it is placed in the class just because it has a little relationship with the class, but not like a class method that needs to pass a class parameter.

For example, there is a method in Animal, the owner jack can call it to get food for the animal. The way to call static methods is as follows.

```
Animal.order_animal_food()
```


![image desc](/upload/Q/C/J/YAtBRYYbtjlU.png)


## Conclusion

This section of the experiment, we  learn four core concepts of the object-oriented programming through several examples.

- abstract
- Package
- inheritance
- polymorphism

At the same time, we have learned object-oriented programming and how to use it, as well as the private properties and methods, static variables and class methods, and static methods that are often used in development. Object-oriented programming in the follow-up project will be of practical use.