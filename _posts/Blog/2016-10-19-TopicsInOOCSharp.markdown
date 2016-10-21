---
title: "Topics in Object Oriented C#"
categories: Blog
type: post
---
I assume that the reader of this post already knows the basics about objects and classes, structs, and interfaces.
This post will dive into their nitty-gritty details.

# Access Modifiers
An access modifier is a keyword assigned to classes, structs, interfaces, and member data to warrant where it may be used in the codebase. More details with examples later. First, I'd like to introduce the keywords used as access modifiers.

**public**: When code is refered to as public, it means that it can be accessed anywhere within the codebase or assemblies (that use its namespace).

**protected**: This is similar to the private modifier but not as strict. Protected data is private to the client of the class, just as private data, *but* it is not private to a class that is inheriting from it. Thus, the benefits of this are only seen when using inheritance.

**private**: This data can only be accessed by other data within the class (for example, a class' functions can access private data). This is the least permissive access level. *Member data within a class is defaulted to private!*

**internal**: This data can be accessed only within the same assembly.

**protected internal**: This data can be accessed only within the same assembly *and* within an inheriting class in another assembly.

# Inheritance
Inheritance is used when a class is similar to another class but has its differences. For example, a class called Honda can inherit from a class called Cars since a Honda would have everything a typical car would have such as tires, windows, and engine, etc. 

Inheritance is a good technique for following the **D**on't **R**epeat **Y**ourself software development principal.

# Polymorphism

## Useful keywords
**assembly:** 

### Resources
https://msdn.microsoft.com/en-us/library/ms173121.aspx "Access Modifiers"
http://www.cplusplus.com/doc/tutorial/inheritance/ "Inheritance in C++"
http://www.cplusplus.com/doc/tutorial/polymorphism/ "Polymorphism in C++"

