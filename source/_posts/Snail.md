title: Snail
date: 2015-12-18 11:44:48
categories:
- Interview
tags: 
- Technical Interview
comments: true
---
A snail in a well can climbs 3 meters up in the day, and slide 2 meters down at the night. Given the height of the well h, how many days does it take for the snail to climb out of the well?

<!--more-->
```java
public class Snail {
  private int distance; // distance to the top
  private static int height; // wall height
  private int day;
  
	public Snail(){
		distance = 0;
	   height = 0;
	   day = 0;
	}
  
	public void setHeight(int high){
	   height = high;
	}
	  
	public void setDistance(int dist){
		distance = dist;
	}
	  
	public void day(){
	    if (distance <= 0){
	    	System.out.println("This snail has climbed out of wall");
	    	return;
	    }
	    distance -= 3;
	}
	  
	public void night(){
	  	if (distance > 0 && distance < height){
	  		day += 1;
	  		distance += 2;
	  	}
	}
	  
	public int getDay(){
	    return day;
	}
	  
	public int getDistance(){
	    return distance;
	}
  
	public static void main(String[] args){
	    Snail snail = new Snail();
	    // the well is 10 meters tall
	    snail.setHeight(10);
	    snail.setDistance(10);
	    
	    while (snail.getDistance() > 0){
	      snail.day();
	      snail.night();
	    }
	    System.out.println(snail.getDay());
	}
}
```