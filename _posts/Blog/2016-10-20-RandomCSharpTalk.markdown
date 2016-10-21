---
title: C# Gems & Subtleties
Category: Blog
Type: Post
font-size: 1.0em
---
  
After several sightings of unconventional & idea provoking C# code, I've decided to amalgamate these sources and maybe elaborate these gems.

**Expression functions**... what are they? They are a new and short way for expressing that a variable returns a value.  Also, because of Intellisense, I noticed that expression functions are considered *properties*. http://www.kunal-chowdhury.com/2014/12/csharp-6-expression-bodied-method.html#mgykar31jw6Rgewb.97

**Should using statements be placed within a local namespace?** http://stackoverflow.com/questions/125319/should-using-statements-be-inside-or-outside-the-namespace To elaborate what's going on in the code within that link, I'm going to rewrite it.
{% highlight C# %}
namespace Outer {
  class Math { // empty }
  using System;
  namespace Inner {
    class Foo {
      static void Bar() { double d = Math.PI; }
    }
  }
}
{% endhighlight %}

The purpose of this is argue why a using statement is sometimes best to be included within a namespace or a more local scope than global scope. Looking at the code, you'd hope Math.PI would execute properly since Math is part of the System namespace. BUT the compiler will first look in the local namespace which is Outer (ok, second most local). And because class Math is empty, this program will generate an error. But if *public static PI* existed within class Math, then it would still run... that's probably not what you want.

## Resources
http://stackoverflow.com/questions/9033/hidden-features-of-c
