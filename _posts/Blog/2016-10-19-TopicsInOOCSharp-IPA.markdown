---
title: "Topics in Object Oriented C#: Inheritance, Polymorphism, & Access Modifiers"
categories: Blog
type: post
---
I assume that the reader of this post already knows the basics about objects and classes, structs, and interfaces.
This post will dive into their nitty-gritty details.

# Access Modifiers
An access modifier is a keyword assigned to classes, structs, interfaces, and member data to warrant where it may be used in the codebase. More details with examples later. First, I'd like to introduce the keywords used as access modifiers.

**public**: When code is refered to as public, it means that it can be accessed anywhere within the codebase or assemblies (that use its namespace).

**protected**: This is similar to the private modifier but not as strict. Protected data is private to the client of the class, just as private data, *but* it is not private to a class that is inheriting from it. Thus, the benefits of this are only seen when using inheritance.

**private**: This data can only be accessed by other data within the class (for example, a class' functions can access private data). This is the least permissive access level. *Note:* Member data within a class is defaulted to private! 

**internal**: This data can be accessed only within the same assembly.

**protected internal**: This data can be accessed only within the same assembly *and* within an inheriting class in another assembly.

To differentiate which access modifier a data member can have, you must discern the scope it lies within. The surrounding scope must have an equivalent or greater *accessibility* than what the data would be assigned. Otherwise, an Inconsistent Accessibility error will arise. 

# Inheritance
Inheritance is used when a class is similar to another class but has its differences. For example, a class called Honda can inherit from a class called Cars since a Honda would have everything a typical car would have such as tires, windows, and engine, etc. 

Inheritance is a good technique for following the **D**on't **R**epeat **Y**ourself software development principal.

# Polymorphism
This topic can not be fully discussed without inheritance so please make sure you understand that first. 
The purposes of polymorphism is to extend or change the functionality of a function while using the same or similar function signature. Hence the name polymorphism where "poly" means that the function can take different forms, or have a varying definition/ implementation, and "-morphism" such that function implementation can be modified. I hope this makes the subject less intimidating.

There are two types of polymorphism: static & dynamic. **Static polymorphism** is associated with operator and function overloading which intuitively makes sense since *static* implies fixed (early binding) code, which occurs at compile time, when function overloading is handled. In other words, the overloaded functions "overload" each other(their function names) because of a variation in their signature (because of different parameters). 
{% highlight C# %}
class TestClass {
  public void func(double a, double b) {...}  // function overloaded
  public void func(int a, int b) {...}  // function overloaded
  public static TestClass operator+(TestClass a, TestClass b) {...}  // operator overloading
}
{% endhighlight %}

**abstract:** this modifier is used with classes, methods, properties, indexers, and events in order to state that their implementation is incomplete or missing. Data members marked as abstract or included in an abstract class must be implemented by the inheriting class.
**virtual:**

**override:**

## Useful keywords
**assembly:** 

### Resources
https://msdn.microsoft.com/en-us/library/ms173121.aspx "Access Modifiers"
http://www.cplusplus.com/doc/tutorial/inheritance/ "Inheritance in C++"
http://www.cplusplus.com/doc/tutorial/polymorphism/ "Polymorphism in C++"
https://msdn.microsoft.com/en-us/library/ms973875.aspx "Variable & Method Scope"
