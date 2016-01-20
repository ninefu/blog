title: Java Interview Questions
date: 2016-01-20 09:02:27
categories:
- Interview
tags: 
- Technical Interview
- TODO
comments: true
---
未整理

### what's the difference between interface and abstract? 

* Abstract classes can have constants, members, method stubs (methods without a body) and defined methods, whereas interfaces can only have constants and methods stubs.
* Methods and members of an abstract class can be defined with any visibility, whereas all methods of an interface must be defined as public (they are defined public by default).
* Variables declared in a Java interface is by default final. An abstract class may contain non-final variables. 
* When inheriting an abstract class, a concrete child class must define the abstract methods, whereas an an abstract class can extend another abstract class and abstract methods from the parent class don't have to be defined.
* Similarly, an interface extending another interface is not responsible for implementing methods from the parent interface. This is because interfaces cannot define any implementation.
* A child class can only extend a single class (abstract or concrete), whereas an interface can extend or a class can implement multiple other interfaces.
* A child class can define abstract methods with the same or less restrictive visibility, whereas a class implementing an interface must define the methods with the exact same visibility (public).

### interface / implements 
解释一下interface以及其内部结构；interface里面可以有变量和常量，接口内部全是public
An interface is an empty shell, there are only constants and the signatures of the methods, which implies that the methods do not have a body. It's just a pattern. An interface is similar to an abstract class; indeed interfaces occupy the same namespace as classes and abstract classes. For that reason, you cannot define an interface with the same name as a class. An interface is a fully abstract class。

### abstract in Java / extends
Abstract classes, unlike interfaces, are classes. you can define a method for them. An abstract class is a class that is only partially implemented by the programmer. It may contain one or more abstract methods. An abstract method is simply a function definition that serves to tell the programmer that the method must be implemented in a child class.
### Recursion: a way to travers tree
what's recursion? a method where the solution to a problem depends on solutions to smaller instances of the same problem (as opposed to iteration).

举个例子: N! = N × (N-1) × (N-2) × ... × 2 × 1. N! is easy to compute with a for loop, but an even easier method in Factorial.java is to use the following recursive function:

```
public static int factorial(int N) { 
   if (N == 1) return 1; 
   return N * factorial(N-1); 
}
```

* The base case returns a value without making any subsequent recursive calls. It does this for one or more special input values for which the function can be evaluated without recursion. For factorial(), the base case is N = 1. 
* The reduction step is the central part of a recursive function. It relates the function at one (or more) inputs to the function evaluated at one (or more) other inputs. Furthermore, the sequence of parameter values must converge to the base case. For factorial(), the reduction step is N * factorial(N-1) and N decreases by one for each call, so the sequence of parameter values converges to the base case of N = 1

以及什么情况下停止: 到底层的base case

recursion有什么要注意的？有什么坏处: 
* Missing base case; 
* No guarantee of convergence; 
* Excessive space requirements: Java needs to keep track of each recursive call to implement the function abstraction as expected. If a function calls itself recursively an excessive number of times before returning, the space required by Java for this task may be prohibitive. 
* Excessive recomputation

### what's transient?
transient is a Java keyword which marks a member variable not to be serialized when it is persisted to streams of bytes. When an object is transferred through the network, the object needs to be 'serialized'. Serialization converts the object state to serial bytes. Those bytes are sent over the network and the object is recreated from those bytes. Member variables marked by the java transient keyword are not transferred; they are lost intentionally.

### what's volatile?
It guarantees visibility of changes to variables across threads. This implies that every thread accessing a volatile field will read its current value before continuing, instead of (potentially) using a cached value. 


Each thread may copy the variables into the CPU cache of different CPUs. If the counter variable is not declared volatile there is no guarantee about when the value of the counter variable is written from the CPU cache back to main memory. This means, that the counter variable value in the CPU cache may not be the same as in main memory. 

if two threads are both reading and writing to a shared variable, then using the volatile keyword for that is not enough. As soon as a thread needs to first read the value of a volatile variable, and based on that value generate a new value for the shared volatile variable, a volatile variable is no longer enough to guarantee correct visibility. The short time gap in between the reading of the volatile variable and the writing of its new value, creates an race condition where multiple threads might read the same value of the volatile variable, generate a new value for the variable, and when writing the value back to main memory - overwrite each other's values.

### thread implements runnable
A thread is a thread of execution in a program. The Java Virtual Machine allows an application to have multiple threads of execution running concurrently. There are two ways to create a new thread of execution. 

One is to declare a class to be a subclass of Thread. This subclass should override the run method of class Thread. An instance of the subclass can then be allocated and started. 

The other way to create a thread is to declare a class that implements the Runnable interface. That class then implements the run method. An instance of the class can then be allocated, passed as an argument when creating Thread, and started. 

### static
The static keyword in Java means that the variable or function is shared between all instances of that class as it belongs to the type, not the actual objects themselves. It can be used without instantiating an object. you don't have to have an instance of the class to use the method.
final: stop value change (variable and parameter), method overriding (method) and inheritance (class)

### HashTable和HashMap对于处理collision的机制: pros and cons
hash table: multi thread safe
A hash function maps keys to positions in the hash table. Collision: maps two keys to the same position
* Linear probing: If position p contains a different key, then examine positions p+1, p+2, etc.* until an empty position is found and insert k there/ or the key is found. If we remove a key, we may not be able to find a key after the removed key.
* HashMap and HashSet use chained hashing. Average search time (1 + 1/(1-α)) / 2 using linear probing*.  1 + α/2 using chained hashing. This tends to produce clustering —long sequences of non-null elements. This is because two Strings that hash to k and k+1 use almost the same probe sequence. 
* Quadratic probing: then examine positions p+1^2, p+2^2. a more efficient algorithm in a closed hash table, since it better avoids the clustering problem that can occur with linear probing, although it is not immune. It also provides good memory caching because it preserves some locality of reference; however, linear probing has greater locality and, thus, better cache performance. Should not exceed half full. This has been shown to remove the “primary clustering” that happens with linear probing. However, Strings that hash to the same value k still use the same sequence of probes. size of the array to be prime
* Double hashing: Like linear probing, it uses one hash value as a starting point and then repeatedly steps forward an interval until the desired value is located, an empty location is reached, or the entire table has been searched; but this interval is decided using a second, independent hash function (hence the name double hashing). Unlike linear probing and quadratic probing, the interval depends on the data, so that even values mapping to the same location have different bucket sequences; this minimizes repeated collisions and the effects of clustering. 
* Linear probing and, to a lesser extent, quadratic probing are able to take advantage of the data cache by accessing locations that are close together. Double hashing has, on average, larger intervals and is not able to achieve this advantage.
### implement hashtable, HashMap

### 对HashMap的理解

based on hash table, initial capacity (16, number of buckets), load factor (0.75 how full the hash table is allowed to get before its capacity is automatically increased). When the number of entries in the hash table exceeds the product of the load factor and the current capacity, the hash table is rehashed (that is, internal data structures are rebuilt) so that the hash table has approximately twice the number of buckets. Map m = Collections.synchronizedMap(new HashMap(...));

The iterators returned by all of this class's "collection view methods" are fail-fast: if the map is structurally modified at any time after the iterator is created, in any way except through the iterator's own remove method, the iterator will throw a ConcurrentModificationException.
clear(), clone(), containsKey(), containsValue(), Set<Map.Entry<K,V>> = entrySet(), get(), isEmpty(), keySet(), put(key,value), putAll(Map<? extends K,? extends V> m), remove(Object key), size(), values()

### iterator: Thread safe. hasNext(), next(), remove(),  allow the caller to remove elements from the underlying collection during the iteration with well-defined semantics. 
* Enumeration: hasMoreElements(), nextElement(), No remove()

### for loop和for-each loop的区别
	For each: Designed specifically for iterating over arrays and collections.
			Array: still using index.
			Collections and objects that implements the Iterator interface, then use Iterator
			if you need to use i.remove(); in your loop, or access the actual iterator in some way, you cannot use the for( : ) idiom, since the actual Iterator is merely inferred.
	For loop: use index

### 数据库的left-outer join
It preserves the unmatched rows from the first (left) table, joining them with a NULL row in the shape of the second (right) table

### Java里Generics

（They allow "a type or method to operate on objects of various types while providing compile-time type safety."）
* Stronger type checks at compile time.
* No more cast. The compiler can now check the type correctness of the program at compile-time. improved readability and robustness
* wildcard: <?> unknown. Cannot add(), but can get() objects
* Bounded wildcard: public void drawAll(List<? extends Shape> shapes)
* Enabling programmers to implement generic algorithms that work on collections of different types.

### 比较inheritance和composition
Composition: using instance variables that are references to other objects. In a composition relationship, the front-end class holds a reference in one of its instance variables to a back-end class. Reuse code. provides stronger encapsulation. because a change to a back-end class needn't break any code that relies only on the front-end class. 

```
class Fruit {

    //...
}
class Apple {

    private Fruit fruit = new Fruit();
    //...
}
```

Inheritance: subclass extends the superclass. dynamic binding and polymorphism. inheritance helps make code easier to change if the needed change involves adding a new subclass. reuse superclass code. provide "weak encapsulation," Make sure inheritance models the is-a relationship

With inheritance, a subclass automatically inherits an implemenation of any non-private superclass method that it doesn't override. With composition, by contrast, the front-end class must explicitly invoke a corresponding method in the back-end class from its own implementation of the method. This explicit call is sometimes called "forwarding" or "delegating" the method invocation to the back-end object.

* It is easier to change the interface of a back-end class (composition) than a superclass (inheritance). As the previous example illustrated, a change to the interface of a back-end class necessitates a change to the front-end class implementation, but not necessarily the front-end interface. Code that depends only on the front-end interface still works, so long as the front-end interface remains the same. By contrast, a change to a superclass's interface can not only ripple down the inheritance hierarchy to subclasses, but can also ripple out to code that uses just the subclass's interface.
* It is easier to change the interface of a front-end class (composition) than a subclass (inheritance). Just as superclasses can be fragile, subclasses can be rigid. You can't just change a subclass's interface without making sure the subclass's new interface is compatible with that of its supertypes. For example, you can't add to a subclass a method with the same signature but a different return type as a method inherited from a superclass. Composition, on the other hand, allows you to change the interface of a front-end class without affecting back-end classes.
* Composition allows you to delay the creation of back-end objects until (and unless) they are needed, as well as changing the back-end objects dynamically throughout the lifetime of the front-end object. With inheritance, you get the image of the superclass in your subclass object image as soon as the subclass is created, and it remains part of the subclass object throughout the lifetime of the subclass.
* It is easier to add new subclasses (inheritance) than it is to add new front-end classes (composition), because inheritance comes with polymorphism. If you have a bit of code that relies only on a superclass interface, that code can work with a new subclass without change. This is not true of composition, unless you use composition with interfaces. Used together, composition and interfaces make a very powerful design tool. I'll talk about this approach in next month's Design Techniques article.
* The explicit method-invocation forwarding (or delegation) approach of composition will often have a performance cost as compared to inheritance's single invocation of an inherited superclass method implementation. I say "often" here because the performance really depends on many factors, including how the JVM optimizes the program as it executes it.
* With both composition and inheritance, changing the implementation (not the interface) of any class is easy. The ripple effect of implementation changes remain inside the same class.

### int 和Integer的区别
primitive,mutable,32-bit, faster
object that contains an int field, immutable, a wrapper, methods to dealing with an int, like toString()

### how to implement hashtable
underlying an array
CC 311
linear probing - primary clusterings
quadratic probing - size is prime and at least 1/2 empty

### sorting算法
* Insertion Sort: O(n^2), O(n) best
* Selection Sort: O(n^2)
* Quick sort: pivot value-partition, nlogn. chose pivot value: median of first, middle, last, values GOOD! 

```java
/** Sort b[h..k]. **/
public static void QS(int[] b, int h, int k){
	if (b[h..k] has less than 2 elements) return;
	int j= partition(b, h, k);
	// We know b[h..j–1] <= b[j] <= b[j+1..k]
	// Sort b[h..j-1] and b[j+1..k] 
	QS(b, h, j-1); 
	QS(b, j+1, k);
}
```

* Merge sort: nlogn, O(n) space

```java
/** Sort b[h..k] **/
public static mergesort(int[] b, int h, int k]) { 
	if (size b[h..k] is less than 2) return;
	int t= (h+k)/2; 
	mergesort(b, h, t); 
	mergesort(b, t+1, k); 
	merge(b, h, t, k); 
} 
```

### DNS
Domain Name System: translate human-memorable domain name to numerical IP address needed for computer services and devices. Send request to the domain server or a local copy server. Cache

### TCP vs UDP
Both are used to send bits of data - packets - over the internet, build on top of the internet protocol. Error-correction and robustness vs speed and reduced overhead
Transmission Control Protocol. It’s the most commonly used protocol on the Internet. TCP isn’t just one way communication — the remote system sends packets back to acknowledge it’s received your packets. TCP guarantees the recipient will receive the packets in order by numbering them. The recipient sends messages back to the sender saying it received the messages. If the sender doesn’t get a correct response, it will resend the packets to ensure the recipient received them. Packets are also checked for errors. TCP is all about this reliability — packets sent with TCP are tracked so no data is lost or corrupted in transit. 

UDP stands for User Datagram Protocol — a datagram is the same thing as a packet of information. The UDP protocol works similarly to TCP, but it throws all the error-checking stuff out. All the back-and-forth communication and deliverability guarantees slow things down. When using UDP, packets are just sent to the recipient. The sender won’t wait to make sure the recipient received the packet — it will just continue sending the next packets. If you’re the recipient and you miss some UDP packets, too bad — you can’t ask for those packets again. There’s no guarantee you’re getting all the packets and there’s no way to ask for a packet again if you miss it, but losing all this overhead means the computers can communicate more quickly.
UDP is used when speed is desirable and error correction isn’t necessary. For example, UDP is frequently used for live broadcasts and online games. Ditching TCP’s error correction helps speed up the game connection and reduce latency.

### 什么是OO
model object, it’s state and behavior, instead of logic. Attribute and methods

### OO和procedural programming的区别
extensible, easy to maintain, function based.

### OO的优势
#### 1.encapsulation
Encapsulation provides objects with the ability to hide their internal characteristics and behavior. Each object provides a number of methods, which can be accessed by other objects and change its internal data. In Java, there are three access modifiers: public, private and protected. Each modifier imposes different access rights to other classes, either in the same or in external packages. Some of the advantages of using encapsulation are listed below: 

* The internal state of every objected is protected by hiding its attributes.
* It increases usability and maintenance of code, because the behavior of an object can be independently changed or extended.
* It improves modularity by preventing objects to interact with each other, in an undesired way. 

#### 2.inheritance
Inheritance provides an object with the ability to acquire the fields and methods of another class, called base class. Inheritance provides re-usability of code and can be used to add additional features to an existing class, without modifying it. 

#### 3. polymorphism
Polymorphism is the ability of programming languages to present the same interface for differing underlying data types. A polymorphic type is a type whose operations can also be applied to values of some other type. provision of a single interface to entities of different types.
 
* Ad hoc: function overloading
* Parametric: generic
* Subtyping: subclasses extend common a superclass. can use a variable of a superclass type to hold a reference to an object whose class is the superclass or any of its subclasses.

### How does error handling works? Do you know what is exception handling
Error is handled by exception object. A try-with-resources statement can have catch and finally blocks just like an ordinary try statement. In a try-with-resources statement, any catch or finally block is run after the resources declared have been closed.
throw – We know that if any exception occurs, an exception object is getting created and then Java runtime starts processing to handle them. Sometime we might want to generate exception explicitly in our code, for example in a user authentication program we should throw exception to client if the password is null. throw keyword is used to throw exception to the runtime to handle it.

throws – When we are throwing any exception in a method and not handling it, then we need to use throws keyword in method signature to let caller program know the exceptions that might be thrown by the method. The caller method might handle these exceptions or propagate it to it’s caller method using throws keyword. We can provide multiple exceptions in the throws clause and it can be used with main() method also.

try-catch – We use try-catch block for exception handling in our code. try is the start of the block and catch is at the end of try block to handle the exceptions. We can have multiple catch blocks with a try and try-catch block can be nested also. catch block requires a parameter that should be of type Exception.
finally – finally block is optional and can be used only with try-catch block. Since exception halts the process of execution, we might have some resources open that will not get closed, so we can use finally block. finally block gets executed always, whether exception occurred or not.

As stated earlier, when any exception is raised an exception object is getting created. Java Exceptions are hierarchical and inheritance is used to categorize different types of exceptions. Throwable is the parent class of Java Exceptions Hierarchy and it has two child objects – Error and Exception. Exceptions are further divided into checked exceptions and runtime exception.

* Errors: Errors are exceptional scenarios that are out of scope of application and it’s not possible to anticipate and recover from them, for example hardware failure, JVM crash or out of memory error. That’s why we have a separate hierarchy of errors and we should not try to handle these situations. Some of the common Errors are OutOfMemoryError and StackOverflowError.
* Checked Exceptions: Checked Exceptions are exceptional scenarios that we can anticipate in a program and try to recover from it, for example FileNotFoundException. We should catch this exception and provide useful message to user and log it properly for debugging purpose. Exception is the parent class of all Checked Exceptions and if we are throwing a checked exception, we must catch it in the same method or we have to propagate it to the caller using throws keyword.
* Runtime Exception: Runtime Exceptions are cause by bad programming, for example trying to retrieve an element from the Array. We should check the length of array first before trying to retrieve the element otherwise it might throw ArrayIndexOutOfBoundException at runtime. RuntimeException is the parent class of all runtime exceptions. If we are throwing any runtime exception in a method, it’s not required to specify them in the method signature throws clause. Runtime exceptions can be avoided with better programming.

### How do you implement multiple inheritance in Java? 
Java does not support multiple inheritance. Each class is able to extend only on one class, but is able to implement more than one interfaces. 

### What is an inner class?
As with instance methods and variables, an inner class is associated with an instance of its enclosing class and has direct access to that object's methods and fields. Also, because an inner class is associated with an instance, it cannot define any static members itself.
* It is a way of logically grouping classes that are only used in one place: If a class is useful to only one other class, then it is logical to embed it in that class and keep the two together. Nesting such "helper classes" makes their package more streamlined.
* It increases encapsulation: Consider two top-level classes, A and B, where B needs access to members of A that would otherwise be declared private. By hiding class B within class A, A's members can be declared private and B can access them. In addition, B itself can be hidden from the outside world.
* It can lead to more readable and maintainable code: Nesting small classes within top-level classes places the code closer to where it is used.

### python 和java的区别，type checking是否重要
Python: dynamically typed/weak typing. But you will not be able to catch many errors until you run the program.

Type checking is useful because you can eliminate certain classes of errors before you run the program. 

For example, say you have a (dumb) function add1, that takes an int and returns an int that is one larger. Java style typechecking will guarantee that this function is only operating on ints. So before you run the program, you will catch any case where you call add1 on the wrong type, e.g. add1("5") will cause a compiler error.

Types can also help the compiler optimize your code, by using machine instructions specific to the data type you are operating on.

### JVM how it works
A Java virtual machine (JVM) is a process virtual machine that can execute Java bytecode. Each Java source file is compiled into a bytecode file, which is executed by the JVM. Java was designed to allow application programs to be built that could be run on any platform, without having to be rewritten or recompiled by the programmer for each separate platform. A Java virtual machine makes this possible, because it is aware of the specific instruction lengths and other particularities of the underlying hardware platform. 

### garbage collection
Question 1 - What is structure of Java Heap ? What is Perm Gen space in Heap ?
Answer : In order to better perform in Garbage collection questions in any Java interview, It’s important to have basic understanding of  Java Heap space. To learn more about heap, see my post 10 points on Java heap space. By the way Heap is divided into different generation e.g. new generation, old generation and PermGen space.PermGen space is used to store class’s metadata and filling of PermGen space can cause java.lang.OutOfMemory:PermGen space. Its also worth noting to remember JVM option to configure PermGen space in Java.

Question 2 - How do you identify minor and major garbage collection in Java?
Answer: Minor collection prints “GC” if garbage collection logging is enable using –verbose:gc or -XX:PrintGCDetails, while Major collection prints “Full GC”. 

Question 3 - What is difference between ParNew and DefNew Young Generation Garbage collector?
 ParNew and DefNew is two young generation garbage collector. ParNew is a multi-threaded GC used along with concurrent Mark Sweep while DefNew is single threaded GC used along with Serial Garbage Collector.

Question 4 - How do you find GC resulted due to calling System.gc()?
Similar to major and minor collection, there will be a word “System” included in Garbage collection output.

Question 5 - What is difference between Serial and Throughput Garbage collector?
Answer : Serial Garbage collector is a stop the world GC which stops application thread from running during both minor and major collection. Serial Garbage collector can be enabled using JVM option -XX:UseSerialGC and it's designed for Java application which doesn't have pause time requirement and have client configuration. Serial Garbage collector was also default GC in JDK 1.4 before ergonomics was introduced in JDK 1.5. Serial GC is most suited for small application with less number of thread while throughput GG is more suited for large applications. On the other hand Throughput garbage collector is parallel collector where minor and major collection happens in parallel taking full advantage of all the system resources available like multiple processor. Though both major and minor collection runs on stop-the-world fashion and introduced pause in application. Throughput Garbage collector can be enable using -XX:UseParallelGC or -XX:UseOldParallelGC. It increases overall throughput of application my minimizing time spent in Garbage collection but still has long pauses during full GC.

Question 6 – When does an Object becomes eligible for Garbage collection in Java ?
Answer : An object becomes eligible for garbage collection when there is no live reference for that object or it can not be reached by any live thread. Cyclic reference doesn’t count as live reference and if two objects are pointing to each other and there is no live reference for any of them, than both are eligible for GC. Also Garbage collection thread is a daemon thread which will run by JVM based upon GC algorithm and when runs it collects all objects which are eligible for GC.

Question 7 - What is finalize method in Java ? When does Garbage collector calls finalize method in Java ?
Answer : Finalize method in Java also called finalizer is a method defined in java.lang.Object and called by Garbage collector before collecting any object which is eligible for GC. Finalize() method provides last chance to object to do cleanup and free any remaining resource, to learn more about finalizers, read What is finalize method in Java.

Question 8 - If Object A has reference to Object B and Object B refer to Object A, apart from that there is no live reference to either object A or B, Does they are eligible to Garbage collection ?
 An object becomes eligible for Garbage collection if there is no live reference for it. It can not be accessible from any Thread and cyclic dependency doesn’t prevent Object from being Garbage collected. Which means in this case both Object A and Object B are eligible of Garbage collection. See How Garbage collection works in Java for more details.

Question 9 -Can we force Garbage collector to run at any time ?
Answer : No, you can not force Garbage collection in Java. Though you can request it by calling Sytem.gc() or its cousin Runtime.getRuntime().gc(). It’s not guaranteed that GC will run immediately as result of calling these method.

Question 10 - Does Garbage collection occur in permanent generation space in JVM?
 Garbage Collection does occur in PermGen space and if PermGen space is full or cross a threshold, it can trigger Full GC. If you look at output of GC you will find that PermGen space is also garbage collected. This is why correct sizing of PermGen space is important to avoid frequent full GC. You can control size of PermGen space by JVM options -XX:PermGenSize and -XX:MaxPermGenSize.

Question 11 : How to you monitor garbage collection activities?
. You can monitor garbage collection activities either offline or real-time. You can use tools like JConsole and VisualVM VM with its Visual GC plug-in to monitor real time garbage collection activities and memory status of JVM or you can redirect Garbage collection output to a log file for offline analysis by using -XlogGC=&lt;PATH&gt; JVM parameter. Anyway you should always enable GC options like -XX:PrintGCDetails -X:verboseGC and -XX:PrintGCTimeStamps as it doesn't impact application performance much but provide useful states for performance monitoring.

Question 12: Look at below Garbage collection output and answer following question :
[GC
       [ParNew: 1512K->64K(1512K), 0.0635032 secs]
       15604K->13569K(600345K), 0.0636056 secs]
       [Times: user=0.03 sys=0.00, real=0.06 secs]

 1. Is this output of Major Collection or Minor Collection ?
 2. Which young Generation Garbage collector is used ?
 3. What is size of Young Generation, Old Generation and total Heap Size?
 4. How much memory is freed from Garbage collection ?
 5. How much time is taken for Garbage collection ?
 6. What is current Occupancy of Young Generation ?

Answer 1:  It's Minor collection because of "GC" word, In case of Major collection, you would see "Full GC".

Answer 2: This output is of multi-threaded Young Generation Garbage collector "ParNew", which is used along with CMS concurrent Garbage collector.

Answer 3: [1512K] which is written in bracket is total size of Young Generation, which include Eden and two survivor space. 1512K on left of arrow is occupancy of Yong Generation before GC and 64K is occupancy after GC. On the next line value if bracket is total heap size which is (600345K). If we subtract size of young generation to total heap size we can calculate size of Old Generation. This line also shows occupancy of heap before and after Garbage collection.

Answer 4: As answered in previous garbage collection interview question, second line shows heap occupancy before and after Garbage collection. If we subtract value of right side 13569K, to value on left side 15604K, we can get total memory freed by GC.

Answer 5: 0.0636056 secs on second line denotes total time it took to collect dead objects during Garbage collection. It also include time taken to GC young generation which is shown in first line (0635032 secs).

Answer 6: 64K 
L



### Java如何产生memory leak
Static field holding object reference [esp final field]

```
class MemorableClass {
    static final ArrayList list = new ArrayList(100);
}
(Unclosed) open streams ( file , network etc... )
try {
    BufferedReader br = new BufferedReader(new FileReader(inputFile));
    ...
    ...
} catch (Exception e) {
    e.printStacktrace();
}
Unclosed connections
try {
    Connection conn = ConnectionFactory.getConnection();
    ...
    ...
} catch (Exception e) {
    e.printStacktrace();
}
```

Areas that are unreachable from JVM's garbage collector, such as memory allocated through native methods
In web applications, some objects are stored in application scope until the application is explicitly stopped or removed.
getServletContext().setAttribute("SOME_MAP", map);
Incorrect or inappropriate JVM options, such as the noclassgc option on IBM JDK that prevents unused class garbage collection

### difference between linux and windows
File structure, registry, package manager, command terminal

### Thread
Concurrency refers to a single program in which several threads are running simultaneously
Implements runnable or extends Thread. Class Thread has methods to allow more control over threads. You can interrupt a thread, maintain a group of threads, set/change its priority, sleep it for a while, etc. 


### How does multithreading works? Advantages and Disadvantages? What is the race condition?A race condition arises if two or more threads access the same variables or objects concurrently and at least one does updates Synchronization barrierOnly one thread can “hold” a lock at a time. If several request the same lock, Java somehow decides which will get it. The lock is released when the thread leaves the synchronization blocksynchronized(someObject) { protected code }The protected code has a mutual exclusion guarantee: At most one thread can be in it. When released, some other thread can acquire the lock High priority thread runs before the low priority, and the latter starves. Finer grained synchronization: can only be used inside a synchronization block. wait/notify ### StarvationStarvation describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress. This happens when shared resources are made unavailable for long periods by "greedy" threads. For example, suppose an object provides a synchronized method that often takes a long time to return. If one thread invokes this method frequently, other threads that also need frequent synchronized access to the same object will often be blocked.### deadlockA deadlock occurs when two or more competing threads are waiting for one-another... forever Acquire a lock, use it, then promptly release it, or ... acquire locks in some “fixed” order ### LivelockA thread often acts in response to the action of another thread. If the other thread's action is also a response to the action of another thread, then livelock may result. As with deadlock, livelocked threads are unable to make further progress. However, the threads are not blocked — they are simply too busy responding to each other to resume work. This is comparable to two people attempting to pass each other in a corridor: Alphonse moves to his left to let Gaston pass, while Gaston moves to his right to let Alphonse pass. Seeing that they are still blocking each other, Alphone moves to his right, while Gaston moves to his left. They're still blocking each other, so...### remove duplicate tuples from database* The simplest way to eliminate the duplicate records is to SELECT DISTINCT into a temporary table, truncate the original table and SELECT the records back into the original table. If this is a large table, it can quickly fill up your tempdb. This also isn't very fast. It makes a copy of your data and then makes another copy of your data. Also while this script is running, your data is unavailable. It may not be the best solution but it certainly works. * The second option is to rename the original table to something else, and copy the unique records into the original table.  This has a couple of benefits over the first option. It doesn't use tempdb and it only makes one copy of the data. On the downside, you'll need to rebuild any indexes or constraints on the table when you're done. This one also makes the data unavailable during the process * Our last option is more complex. It has the benefit of not making a copy of the data and only deleting the records that are duplicates. It's main drawback is that we have to alter the original table and add a sequential record number field to uniquely identify each record. It's actually possible to combine the SELECT INTO #dupes and the DELETE into one DELETE statement. ### how to make sure that a database is secure for a customer Separate the Database and Web ServersEncrypt Stored FilesEncrypt Your Backups TooUse a WAF Employ web application firewalls.Minimize Use of 3rd Party AppsDon't Use a Shared ServerEnable Security Controls### index有什么用An index on a file speeds up selections on the search key fields for the index ### B+ tree的indexSupports equality and range-searches efficiently. Hash-based indexes are best for equality selections. Cannot support range searches. ### 数据库normalize的定义，好处Database normalization (or normalisation) is the process of organizing the columns (attributes) and tables (relations) of a relational database to minimize data redundancy. Normalization involves decomposing a table into less redundant (and smaller) tables without losing information; defining foreign keys in the old table referencing the primary keys of the new ones. The objective is to isolate data so that additions, deletions, and modifications of an attribute can be made in just one table and then propagated through the rest of the database using the defined foreign keys.Use foreign key, Information is only stored once, Reduce redundancy, but require expensive joinDenormalization is commonly used to create highly scalable systems.Design:### What is singletonThe Singleton pattern ensures that a class has only one instance and ensures access to the instance through the application. It can be useful in cases where you have a "global" object with exactly one instance. For example, we may want to implement Restaurant such that it hasexactly one instance of Restaurant. ### Factory methodThe Factory Method offers an interface for creating an instance of a class, with its subclasses deciding which class to instantiate. You might want to implement this with the creator class being abstract and not providing an implementation for the Factory method. Or,you could have the Creator class be aconcrete class that providesan imple- mentation for the Factory method. In this case, the Factory method would take a param- eter representing which class to instantiate. ### Builder patternThe builder pattern is an object creation software design pattern. Unlike the abstract factory pattern and the factory method pattern whose intention is to enable polymorphism, the intention of the builder pattern is to find a solution to the telescoping constructor anti-pattern[citation needed]. The telescoping constructor anti-pattern occurs when the increase of object constructor parameter combination leads to an exponential list of constructors. Instead of using numerous constructors, the builder pattern uses another object, a builder, that receives each initialization parameter step by step and then returns the resulting constructed object at once.The builder pattern has another benefit. It can be used for objects that contain flat data (html code, SQL query, X.509 certificate...), that is to say, data that can't be easily edited. This type of data cannot be edited step by step and must be edited at once. The best way to construct such an object is to use a builder class.[citation needed]Builder often builds a Composite. Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed. Sometimes creational patterns are complementary: Builder can use one of the other patterns to implement which components are built. Builders are good candidates for a fluent interface.### 如果client和server相连之后client执行操作非常慢，可能是什么问题，如何优化	Could be any of these A. Hardware/OS-related causes B. 3rd party application interference C. Database Design D. Database corruption### waterfall的缺点In a waterfall model, each phase must be completed fully before the next phase can begin. This type of model is basically used for the for the project which is small and there are no uncertain requirements. At the end of each phase, a review takes place to determine if the project is on the right path and whether or not to continue or discard the project. In this model the testing starts only after the development is complete. In waterfall model phases do not overlap.Advantages of waterfall model:* This model is simple and easy to understand and use.* It is easy to manage due to the rigidity of the model – each phase has specific deliverables and a review process.* In this model phases are processed and completed one at a time. Phases do not overlap.* Waterfall model works well for smaller projects where requirements are very well understood. Disadvantages of waterfall model:* Once an application is in the testing stage, it is very difficult to go back and change something that was not well-thought out in the concept stage.* No working software is produced until late during the life cycle.* High amounts of risk and uncertainty.* Not a good model for complex and object-oriented projects.* Poor model for long and ongoing projects.* Not suitable for the projects where requirements are at a moderate to high risk of changing.### MVC pattern: When you receive a request in an MVC app, what happens? As with other software patterns, MVC expresses the "core of the solution" to a problem while allowing it to be adapted for each system.[9] Particular MVC architectures can vary significantly from the traditional description here.[10]Components[edit]The central component of MVC, the model, captures the behavior of the application in terms of its problem domain, independent of the user interface.[11] The model directly manages the data, logic and rules of the application. A view can be any output representation of information, such as a chart or a diagram; multiple views of the same information are possible, such as a bar chart for management and a tabular view for accountants. The third part, the controller, accepts input and converts it to commands for the model or view.[12]Interactions[edit]In addition to dividing the application into three kinds of components, the model–view–controller design defines the interactions between them.[13]* A controller can send commands to the model to update the model's state (e.g., editing a document). It can also send commands to its associated view to change the view's presentation of the model (e.g., by scrolling through a document).* A model stores data that is retrieved according to commands from the controller and displayed in the view.* A view generates an output presentation to the user based on changes in the model.* A view controller generates an output view and an embedded controller### Checked vs Unchecked Exceptions in Java1) Checked: are the exceptions that are checked at compile time. If some code within a method throws a checked exception, then the method must either handle the exception or it must specify the exception using throws keyword.2) Unchecked are the exceptions that are not checked at compiled time. In C++, all exceptions are unchecked, so it is not forced by the compiler to either handle or specify the exception. It is up to the programmers to be civilized, and specify or catch the exceptions.In Java exceptions under Error and RuntimeException classes are unchecked exceptions, everything else under throwable is checked.1、throws出现在方法函数头；而throw出现在函数体。2、throws表示出现异常的一种可能性，并不一定会发生这些异常；throw则是抛出了异常，执行throw则一定抛出了某种异常。3、两者都是消极处理异常的方式，只是抛出或者可能抛出异常，但是不会由函数去处理异常，真正的处理异常由函数的上层调用处理。```void doA(int a) throws IOException,{           try{                 ......           }catch(Exception1 e){              throw e;           }catch(Exception2 e){              System.out.println("出错了！");           }           if(a!=b)              throw new  Exception3("自定义异常");}```reflection:http://stackoverflow.com/questions/37628/what-is-reflection-and-why-is-it-usefulsingletonhttp://www.javaworld.com/article/2073352/core-java/simply-singleton.htmlEnsure a class has only one instance, and provide a global point of access to it.it's appropriate to have exactly one instance of a class: window managers, print spoolers, and filesystems are prototypical examples.are accessed by disparate objects throughout a software system, and therefore require a global point of access```public class ClassicSingleton {   private static ClassicSingleton instance = null;   protected ClassicSingleton() {      // Exists only to defeat instantiation.   }   public static ClassicSingleton getInstance() {      if(instance == null) {         instance = new ClassicSingleton();      }      return instance;   }}Best, Thread safepublic class Singleton {   public final static Singleton INSTANCE = new Singleton();   private Singleton() {         // Exists only to defeat instantiation.      }}Thread safe, but may fail at compile levelpublic static Singleton getInstance() {  if(singleton == null) {     synchronized(Singleton.class) {       if(singleton == null) {         singleton = new Singleton();       }    }  }  return singleton;}```synchronized getInstance method? only need to synchronized when the first time it is called, synchronized function is expensive. ### abstract vs interfacegeneral rule is if you are creating something that provides common functionality to unrelated classes, use an interface. If you are creating something for objects that are closely related in a hierarchy, use an abstract class. Abstract classes allow you to provide default functionality for the subclasses.If you plan on updating this base class throughout the life of your program, it is best to allow that base class to be an abstract class. Because you can make a change to it and all of the inheriting classes will now have this new functionality. If the base class will be changing often and an interface was used instead of an abstract class, we are going to run into problems. Once an interface is changed, any class that implements that will be broken. Now if its just you working on the project, that’s no big deal. However, once your interface is published to the client, that interface needs to be locked down. At that point, you will be breaking the clients code.### java garbage collection, how it worksJava garbage collection is a function of JVM. It can recycle unreferenced spaces dynamically automatically .You can use System.gc(), Runtime.getRuntion().gc() to call garage collection.It allows developers to create new objects without worrying explicitly about memory allocation and deallocation, because the garbage collector automatically reclaims memory for reuse.Live objects are tracked and everything else designated garbage.All objects are allocated on the heap area managed by the JVM. Every item that the developer uses is treated this way, including class objects, static variables, and even the code itself. As long as an object is being referenced, the JVM considers it alive. Once an object is no longer referenced and therefore is not reachable by the application code, the garbage collector removes it and reclaims the unused memory.Therefore, a simple Java application has the following GC roots:Local variables in the main methodThe main threadStatic variables of the main classAs long as the application can reach those roots, the whole tree is reachable.Marking and Sweeping Away GarbageTo determine which objects are no longer in use, the JVM intermittently runs what is very aptly called a mark-and-sweep algorithm. two-step process:1.The algorithm traverses all object references, starting with the GC roots, and marks every object found as alive.2.All of the heap memory that is not occupied by marked objects is reclaimed. It is simply marked as free, essentially swept free of unused objects.Java的垃圾回收机制是Java虚拟机提供的能力，用于在空闲时间以不定时的方式动态回收无任何引用的对象占据的内存空间。需要注意的是：垃圾回收回收的是无任何引用的对象占据的内存空间而不是对象本身。System.gc()Runtime.getRuntime().gc()  上面的方法调用时用于显式通知JVM可以进行一次垃圾回收，但真正垃圾回收机制具体在什么时间点开始发生动作这同样是不可预料的，这和抢占式的线程在发生作用时的原理一样Object creation is faster because global synchronization with the operating system is not needed for every single object. An allocation simply claims some portion of a memory array and moves the offset pointer forward (see Figure 2.1). The next allocation starts at this offset and claims the next portion of the array. When an object is no longer used, the garbage collector reclaims the underlying memory and reuses it for future object allocation. This means there is no explicit deletion and no memory is given back to the operating system.It’s possible to have unused objects that are still reachable by an application because the developer simply forgot to dereference them. Such objects cannot be garbage-collected. ### consumer & producer// cubbyhole multi-thead// wait(), give up lock// available, because contents can’t be null, if contents can be null, then use content == null// notifyAll(), notify all wait() to continue(include all producers and all consumers) and get lock```class CubbyHole {   private int contents;   private boolean available = false;   public synchronized int get() {      while (available == false) {         try {            wait();         }         catch (InterruptedException e) {         }      }      available = false;      notifyAll();      return contents;   }   public synchronized void put(int value) {      while (available == true) {         try {            wait();         }         catch (InterruptedException e) {          }       }      contents = value;      available = true;      notifyAll();   }}```http://en.wikipedia.org/wiki/Producer%E2%80%93consumer_problemhttp://en.wikipedia.org/wiki/Semaphore_(programming)semaphore is atomicmutex is binary semaphore, 1 or 0.The emptyCount is initially N, fullCount is initially 0, and useQueue is initially 1.produce:    P(emptyCount)    P(useQueue)    putItemIntoQueue(item)    V(useQueue)    V(fullCount)consume:    P(fullCount)    P(useQueue)    item ← getItemFromQueue()    V(useQueue)    V(emptyCount)Example1. A single consumer enters its critical section. Since fullCount is 0, the consumer blocks.2. Several producers enter the producer critical section. No more than N producers may enter their critical section due to emptyCount constraining their entry.3. The producers, one at a time, gain access to the queue through useQueue and deposit items in the queue.4. Once the first producer exits its critical section, fullCount is incremented, allowing one consumer to enter its critical section.why use useQueue?1.Two producers decrement emptyCount2.One of the producers determines the next empty slot in the buffer3.Second producer determines the next empty slot and gets the same result as the first producer4.Both producers write into the same slot### use a class to present a enum```public class DayHalf {         static final DayHalf AM = new DayHalf();     static final DayHalf PM = new DayHalf();     private DayHalf() {             }}DayHalf dh1 = DayHalf.AM;DayHalf dh2 = DayHalf.PM;public enum Day {    SUNDAY, MONDAY, TUESDAY, WEDNESDAY,    THURSDAY, FRIDAY, SATURDAY }public class EnumTest {    Day day;        public EnumTest(Day day) {        this.day = day;    }        public void tellItLikeItIs() {        switch (day) {            case MONDAY:                System.out.println("Mondays are bad.");                break;                                case FRIDAY:                System.out.println("Fridays are better.");                break;                                     case SATURDAY: case SUNDAY:                System.out.println("Weekends are best.");                break;                                    default:                System.out.println("Midweek days are so-so.");                break;        }    }        public static void main(String[] args) {        EnumTest firstDay = new EnumTest(Day.MONDAY);        firstDay.tellItLikeItIs();        EnumTest thirdDay = new EnumTest(Day.WEDNESDAY);        thirdDay.tellItLikeItIs();        EnumTest fifthDay = new EnumTest(Day.FRIDAY);        fifthDay.tellItLikeItIs();        EnumTest sixthDay = new EnumTest(Day.SATURDAY);        sixthDay.tellItLikeItIs();        EnumTest seventhDay = new EnumTest(Day.SUNDAY);        seventhDay.tellItLikeItIs();    }}```###  What is difference between fail-fast and fail-safe Iterators?Fail-fast Iterators throws ConcurrentModificationException when one Thread is iterating over collection object and other thread structurally modify Collection either by adding, removing or modifying objects on underlying collection. They are called fail-fast because they try to immediately throw Exception when they encounter failure. fail-safe Iterators works on copy of collection instead of original collection### What is difference between poll() and remove() method of Queue interface?Though both poll() and remove() method from Queue is used to remove object and returns head of the queue, there is subtle difference between them. If Queue is empty() then a call to remove() method will throw Exception, while a call to poll() method returns null. How do you remove an entry from a Collection? what is difference between remove() method of Collection and remove() method of Iterator, which one you will use, while removing elements during iteration?You can use any of these method to remove an entry from Collection, while not iterating.If you use Collection's or List's remove() method during iteration then your code will throw ConcurrentModificationException. That's why it's advised to use Iterator remove() method to remove objects from Collection. ### What is difference between Synchronized Collection and Concurrent Collection?Concurrent Collections has better performance than synchronized Collection because they lock only a portion of Map to achieve concurrency and Synchronization.### ConcurrentHashMapBlockingQueueuse BlockingQueue to solve Producer Consumer problema Queue that supports operations that wait for the queue to become non-empty when retrieving and removing an element, and wait for space to become available in the queue when adding an element.CopyOnWriteArrayListprovides better concurrent access than Synchronized List. CopyOnWriteArrayList doesn't throw any ConcurrentModification Exception. Its different than ArrayList because its thread-safe and ArrayList is not thread safe and its different than Vector in terms of Concurrency. arraylist vectornon-synchronized, synchronizediterator, enumerationresize: grow by half of current size, double current sizeHow does HashSet is implemented in Java, How does it uses Hashing ?you will find that that it uses a HashMap with same values for all keys8. What do you need to do to use a custom object as key in Collection classes like Map or Set?If you are using any custom object in Map as key, you need to override equals() and hashCode() methodOn the other hand if you are storing a custom object in Sorted Collection e.g. SortedSet or SortedMap, you also need to make sure that your equals() method is consistent to compareTo() method10. When do you use ConcurrentHashMap in Java?ConcurrentHashMap is better suited for situation where you have multiple readers and oneWriter or fewer writers since Map gets locked only during write operation. If you have equal number of reader and writer than ConcurrentHashMap will perform in line of Hashtable or synchronized HashMap.17) Can we replace Hashtable with ConcurrentHashMap?Answer 3 : Yes we can replace Hashtable with ConcurrentHashMap and that's what suggested in Java documentation of ConcurrentHashMap. but you need to be careful with code which relies on locking behavior of Hashtable. Since Hashtable locks whole Map instead of portion of Map.ListIterator has add() method but Iterator doesn't or Why add() method is declared in ListIterator and not on Iterator.ListIterator has add() method because of its ability to traverse or iterate in both direction of collection. it maintains two pointers in terms of previous and next call and in position to add new element without affecting current iteration.Override允许子类改变父类的一些行为。 2.方法被定义为private或static或final的则不能被覆盖。 4.在方法调用时先会在子类中找覆盖的方法，如果子类中没有则会在父类中去找。 2) Explain Collection’s hierarchy?Java Collections Framework:Collection: [set:[SortedSet], list, queue]Map:[SortedMap]Framework also consist of Map interface, which is part of collection framework. but it does not extend Collection interface.4) Why Map interface does not extend Collection interface?A good answer to this interview question is “because they are incompatible“. Collection has a method add(Object o). Map can not have such method because it need key-value pair. There are other reasons also such as Map supports keySet, valueSet etc. Collection classes does not have such views.Due to such big differences, Collection interface was not used in Map interface, and it was build in separate hierarchy.array to arraylistInteger[] nums = {1,2,3,4};List numsList = Arrays.asList(nums);reverse listCollections.reverse(list);10) Can a null element added to a TreeSet or HashSet?As you see, There is no null check in add() method in previous question. And HashMap also allows one null key, so one “null” is allowed in HashSet.TreeSet uses NavigableMap for storing the elements.NavigableMap is subtype of SortedMap which does not allow null keys. So essentially, TreeSet also does not support null keys.17) When to use HashMap or TreeMap?TreeMap is special form of HashMap. It maintains the ordering of keys which is missing in HashMap class. This ordering is by default “natural ordering”. The default ordering can be override by providing an instance of Comparator class, whose compare method will be used to maintain ordering of keys.25) Difference between TreeSet and SortedSet?SortedSet is an interface which TreeSet implements32) What is difference between fail-fast and fail-safe?Fail-fast Iterators fail as soon as they realized that structure of Collection has been changed since iteration has begun. Fail-safe iterators are just opposite to fail-fast. They never fail if you modify the underlying collection on which they are iterating, because they work on clone of Collection instead of original collection.Iterator of CopyOnWriteArrayList is an example of fail-safe Iterator also iterator written by ConcurrentHashMap keySet is also fail-safe iterator and never throw ConcurrentModificationException.35) Which collection classes provide random access of it’s elements?ArrayList, HashMap, TreeMap, Hashtable classes provide random access to it’s elements.3) Why Collection interface does not extend Cloneable and Serializable interface?Well, simplest answer is “there is no need to do it“.not everybody will have a reason to have Cloneable collection because if it has very large data, then every unnecessary clone operation will consume a big memory.What is the benefit of Generics in Collections Framework?Stronger type checks at compile time.Elimination of casts.Enabling programmers to implement generic algorithms that work on collections of different types.How to avoid ConcurrentModificationException while iterating a collection?We can use concurrent collection classes to avoid ConcurrentModificationException while iterating over a collection, for example CopyOnWriteArrayList instead of ArrayList.Check this post for ConcurrentHashMap Example.### Can we use any class as Map key?If the class overrides equals() method, it should also override hashCode() method.The class should follow the rules associated with equals() and hashCode() for all instances.Best practice for user defined key class is to make it immutable, so that hashCode() value can be cached for fast performance. Also immutable classes make sure that hashCode() and equals() will not change in future that will solve any issue with mutability.Which collection classes provide random access of it’s elements?ArrayList, HashMap, TreeMap, Hashtable classes provide random access to it’s elements. Which collection classes are thread-safe?Vector, Hashtable, Properties and Stack are synchronized classes, so they are thread-safe

