title: Queue
date: 2016-05-05 15:39:22
categories:
- Interview
tags:
- Technical Interview
- Design
comments: true
sitemap: false
---

<!--more-->

```java
class Queue{
	Element[] array;
	int enqueueIndex;
	int dequeueIndex;
	int size;
	
	Queue(int length){
		array = new Element[length];
		size = length;
		enqueueIndex = 0;
		dequeueIndex = 0;
	}
	
	synchronized Element dequeue(){
		if (dequeueIndex == enqueueIndex){
			return null;
		}else{
		Element cur = array[dequeuIndex];
		array[dequeueIndex] = null; // deferencing the dequeued object
		dequeueIndex = (dequeueIndex + 1) % size;
		return cur;
		}
	}
	
	synchronized void enqueue(Element e){
		if ((enqueueIndex + 1) % size == dequeueIndex){
			throw new ArrayIndexOutOfBoundsException
		}else{
			array[enqueueIndex] = e;
			enqueueIndex = (enqueueIndex + 1) % size;
		}
	}
	
}
```