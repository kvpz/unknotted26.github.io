---
permalink: /Blog/CSharpVsCCPlusPlus
title: "C# vs C/C++"
categories: Blog
type: post
---

In my first few days coding in C# I probably wrote more code than I would have written in one week using C/C++. The C# language itself and the amount of
useful libraries provided for it (.NET, ..etc. lol) have made me more productive.

# Differences between C/C++ and C\#

1) C# is not compiled to assembly, but to the Microsoft Intermediate Language. A benefit of this is not having to recompile
for different platforms. C# can be compiled once to obtain the Common Language Runtime(CLR) which can compile just-in-time during
runtime.

2) In C# implicit casting is not allowed.
{% highlight C %}
  bool = true;
  int i = 1;
  if (bool == i) printf("TRUE"); // this would not be true in C#
{% endhighlight %}

3) C# is a managed language. Compared to C, it is not native nor interpreted, the compiler generates no assembly code (see MSIL, CLR, JIT), optimizations occur at runtime
instead of during compilation,


## Miscellaneous

### Similarities

### Differences

- Every method and variable needs to be encapsulated in a class making C# a strongly object-oriented language. In other words, C# doesn't allow global variables or method definitions/ prototypes.
- Arrays of all data types in C# have the field Length which returns the size of the array. In C, the length of an array is determined by sizeof, but it does not always work.
A programmer must be aware of the underlying technicalities of C to understand when to use sizeof and when it would fail. Putting it shortly, sizeof only works actual arrays, not pointers.
A declared array is not necessarily always an array as some may think. This confusion arises when an array is passed as a function parameter where it is decayed to a pointer (and
sizeof doesn't work on pointers, at least not how naive programmer would hope).
Also sizeof doesn't calculate the amount of elements in an array, but the amount of memory that array uses. Example: int iarr[] = {1,2,3}; char carr[] = {'1','2', '3'}; sizeof(iarr)
equals 12 whereas sizeof(carr) equals 3, since char is equal to 1 byte and and int is 4 bytes.

{% highlight C %}
    char * c_arr = {'a','b','c'};
    int * i_arr = {1,2,3};
    printf("%i", sizeof(c_arr)); // 3
    printf("%i", sizeof(i_arr)); // 12
    printf("%i", sizeof(i_arr) / sizeof(int)); // 3
{% endhighlight %}

- "Using" only impacts the namespace scope where it is placed. "using namespace" in C++ impacts every file that includes the file this is used in.
- C# uses access modifiers explicitly for every member data and methods in a class, otherwise all data is considered private. In C, everything in a struct is considered public
and in C++ classes, member data are implicitly private unless it is below an access modifier of another type.
- C# requires the 'new' keyword to create an object, or instance of a class. In C++ this can be avoided and an object would be considered an "automatic variable" meaning that it will be
deleted upon going out of scope.

## C\# Collections vs C++ STL
### std::queue vs. Collections.Generic.Queue
C++ definition
-template <class T, class Container = deque<T> > class queue


