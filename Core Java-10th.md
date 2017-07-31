# Book Guide myself

泛型 - Generic Programming

父类引用指向子类对象 - 属于“多态”的范畴，polymorphism



# Chapter 5: Inheritance



## 5.1  Classes, Superclasses, and Subclasses



### 5.1.5 Polymorphism

A simple rule can help you decide whether or not inheritance is the right design for your data. The "is-a" rule states that every object of the subclass is an object of the superclass. For example, every **manager** is an **employee**. Thus, it makes sense for the `Manager` class to be a subclass of the `Employee` class.  Naturally, the opposite is not true -- not every **employee** is a **manager**.

Another way of formulating the "is-a" rule is the *substitution principle*. That principle states that you can use a subclass object whenever the program expects a superclass object.

For example, you can assign a subclass object to a superclass variable.

```java
Employee e;
e = new Employee(...); // Employee object excepted
e = new Manager(...);  // Ok, Manager can be used as well
```

In the Java programming language, object variables are *polymorphic*. A variable of type `Employee`  can refer to an object of type `Employee` or to an object of any subclass of the `Employee` class(such as `Manager`, `Executive`, `Secretary`, and so on).



# Chapter 8: Generic Programming



## 8.1  Why Generic Programming?

Generic programming means writing code that can be reused for objects of many different types. For example, you don't want to program separate classes to collect `String` and `File` Objects. And you don't have to -- the single class `ArrayList` collects objects of any class. This is one example of generic programming. 

Actually, Java had an `ArrayList` class before it had generic classes. Let us investigate how the mechanism for generic programming has evolved, and what that means for users and implementors.

