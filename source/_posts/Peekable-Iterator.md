title: Peekable Iterator
date: 2016-03-09 09:45:59
categories:
- Interview
tags:
- Technical Interview
- Design
comments: true
---


Given an iterator, implement a peekable iterator with peek() which will return the value without advancing the underlying iterator

```java
public class peekableIterator<T> implements Iterator<T>{
	private Iterator iter;
	private T prev;
	
	peekableIterator(Iterator it){
			iter = it;
			prev = it.hasNext() ? it.next() : null;}
	
	boolean hasNext(){
		return prev != null || iter.hasNext();
	}
	
	T next(){
		T res = prev;
		prev = it.hasNext() ? it.next() : null;
		return res;
	}
	
	T peek(){
		return prev;
	}
}
```