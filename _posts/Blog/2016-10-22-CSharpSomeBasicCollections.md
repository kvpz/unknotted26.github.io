---
title: C# Data Structures (aka Collections)
categories: Blog
type: post
---

The world of .NET Collections

### IList<T> Generic Interface
This interface is an abstraction that allows list types to be used through a single
reference type. Using it we can create a single method to receive, for example, an T[] or List<T>.
The reason for this is because they can be implicitly cast to their base interface IList<T>.


Ex.
static void Display(IList<int> list)
{
	foreach(int value in list) Console.WriteLine(value);
}

### SortedDictionary<TKey, TValue>
A generic class implemented as a binary search tree with O(log n) retrieval. It is thus similar to SortedList<TKey, TValue> with respect
to O(log N) retrieval. 
Differences between SortedList and Sorted Dictionary:
- SortedList uses less memory than SortedDictionary.
- SortedDictionary has faster insertion and removal operations for unsorted data: O(log n) as opposed to O(n) for SortedList.
- If the list is populated all at once from sorted data, SortedList is faster than SortedDictionary.

Key value pairs in SortedDictionary can be retrieved as **KeyValuePair<TKey, TValue>** structure, or as a DictionaryEntry through the nongeneric IDictionary interface.

Keys must be immutable, unique, not null. The values, TValue, however can be null if it's a reference type.

A comparison implementation is required. You can specify a IComparer<T> generic interface by using a constructor that accepts a comparer. Else a default comparer will be used. Also,
if the TKey type implements the IComparable<T> generic interface, the default comparer uses that implementation.

If an OrderedDictionary object is used with a foreach iterator, a KeyValuePair<TKey, TValue> is return. Keys and values can be accessed by the Key and Value properties.

SortedDictionary can support multiple readers concurrently, but it cannot be modified. To guarantee thread safety during enumeration, you can lock the collection during the entire enumeration.
Your own synchronization must be provided if the collection is being accessed by multiple threads. This applies to other Collections.

### LinkedList vs List
LinkedList<T> represents a double linked list such that each node, which is of type LinkedListNode<T>, opints forward to the Next node and backward to the Previous node, where Next and Previous are properties.

Insertion and removal are O(1) operations.

It maintains an internal counter that represents its size (number of nodes). O(1) to retriece its size unlike some other collections... which ones?

If the LinkedList is empty, the First and Last properties are null.

It does not support chaining splitting, cycles, or other features that can leave the list in an inconsistent state. It will remain consistent on a single thread. The only multithreaded
scenario it supports is multithreaded read operations.

LinkedList do not have random access so finding a specific node is a O(n) operation.

Now a **List** is different. It implements the IList<T> generic interface unlike LinkedList<T> which implements ICollection interface. It contains within an array that can be dynamically increased.

Items are added using Add and AddRange methods. A List can accept null as a valid value for reference types and it allows duplicates.

For comparisons, List<T> uses an equality and ordering comparer. The methods Contains, IndexOf, LastIndexOf, and Remove use an equality comparer for the list elements. There are several default equality
comparers that can be used. If type T implements IEquatable<T> generic interface then the equality comparer is the Equals(T) method; otherwise, the default equality comparer is Object.Equals(Object).

Methods that use an ordering comparer are BinarySearch and Sort. If type T implements the IComparable<T> generic interface, then the default comparer is the CompareTo(T) method of that interface; otherwise
if the type T implements the nongeneric IComparable interface, then the default comparer is the CompareTo(Object) method of that interface. If neither interface is implemented, then there is no default 
and a comparer or comparison delegate must be provided explicitly.

One thing that is misleading the class name List is that it is usually associated with a linked list in other languages. So what may come to a surprise to those unfamiliar with its implementation is 
the use of the random access [] operator (zero-based). 

As for scaling, a List can have a maximum capacity of 2 billion elements on a 64-bit system. To do this the **enabled** attribute in the configuration must be set to **true** in the run-time environment. 

**ArrayList**
ArrayList and List have similar behaviors when type T is a reference type. But if a value type is used for List, you have to consider implementation and boxing issues. If T is a value type, the compiler
generates an implementation of the List<T> class specifically for that value type. That means a list element of a List<T> object does not have to be boxed before the element can be used, and after about 500 list
elements are created, the MEMORY SAVED not boxing list elements is greater than the memory used to generate the class implementation.  Also make sure the type T implements the IEquatable<T> interface. If not, methods
such as **Contains** must call Object.Equals(Object) which boxes the affected list element. If the value type implements the IComparable interface and you own the source code, also implement the IComparable<T> interface
to prevent the BinarySearch and Sort methods from boxing list elements. If you don't own the source code, pass an IComparable<T> object to the BinarySearch and Sort methods.

ArrayList are meant to store only Object types which has a negative impact on performance for most use cases. Why? An object has has to be boxed and unboxed before accessing the desired value. 

### Enumerators
Enumerators can be used to read the data in the collection, but they cannot be used to modify the collection. 

#### IEnumerable 
This interface contains only one method, GetEnumerator(), which returns an IEnumerator. IEnumerator provides the ability to iterate through the collection byexposing a Current property and
MoveNext and Reset methods. 


### Collection<T>
The collection class is a useful class to inherit because it's child will gain the ease of adding and removing items, clearing the collection, and setting the value of
and existing item (unless T is unmodifiable). Duplicate items are allowed.
{% highlight C# %}
class Node<T> { ... }
class NodeList<T> : Collection<Node<T>>
{
	public NodeList(){}
}

class BinaryTree<T> : Node<T>
{
	NodeList<T> Children { get; set; }
	public BinaryTree(Node<T> left, Node<T> right) {
		NodeList<T> Children = new NodeList<T>();
		Children[0] = left;  // [] operator is inherited from Collection<Node<T>>
		Children[1] = right;
		// Alternatively: use an element initializer as provided by Collection
		NodeList<T> Children = new NodeList<T>{left, right}; 
	}
}
{% endhighlight %}

I think the reason why classes that inherit from Collection can utilize the provided methods as if they were their own is because Collection implements them as extension methods.

### (Jagged Arrays)[https://msdn.microsoft.com/en-us/library/2s05feca.aspx] vs Multidimensional Arrays
To those who can't decide why whether to use jagged or multidimensional arrays, for better performance, use jagged arrays.

A jagged array is essentially an array of arrays. When it comes to initializing a jagged array, you have to initialize arrays in order to put them within the array... Let me show you.
{% highlight c# %}
int[][] jagwrong = new int[10][30]; // ERROR
int[][] jagarr = new int[size][];
for(int i = 0; i < size; ++i)
  jagarr[i] = new int[];
{% endhighlight %}
Why is the initialization of *jagwrong* incorrect? I think (i.e. take this with a grain of salt) that calling int[10][30] is like telling the compiler: assign 10 int-sized spots in the (contiguous) memory that *new* was so nice to find for us, then can you perhaps assign each of those 10 spots with 30 spots of int-sized memory? The compiler is not going to like that. It is also just part of the rules of C# and I guess the compiler writers didnt want to implement something like this. 

There is another solution in C# however that can allow you to simulate what you are trying to do. The solution is multidimensional arrays; and the reason why they simulate arrays of arrays of arrays... is because multidimensional arrays stores the elements contiguously (in one connected block of memory).

### Boxing vs Unboxing


### Miscellaneous but relevant
Stable sort vs unstable sort: if the keys of two elements are equal, a stable sort would preserve their order. An unstable sort would not. OrderBy<> is stable.

A cool thing about interfaces is that you can declare an interface object and assign that object whatever class that inherites from that interface. For example, IList obj = new List(); This is useful
technique when implementing similar methods with similar parameters and using only one object instead of multiple. It's a form of polymorphism.
See dependency injections[https://en.wikipedia.org/wiki/Dependency_injection] where a dependency is a service (can be reused by different clients for different purposes), and an injection is 
the passing of a dependency to a dependent object (a client) that would use it. In the above example, obj is the client being passed th List service.

Resources
[https://msdn.microsoft.com/en-us/library/bb384062.aspx] Object and COllection Initializers
