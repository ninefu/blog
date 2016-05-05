title: License Plate
date: 2016-01-06 16:56:38
tags:
- Interview
comments: true
sitemap: false
---

```java
import java.util.Iterator;
import java.util.NoSuchElementException;
import java.util.regex.Pattern;
import java.util.ArrayList;
import com.google.common.collect.Lists;
import java.util.Objects;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class Solution {

  static enum State {
    CA,
    UT,
    NV,
    OR,
    WA
  }

  static class LicensePlate {
    State state;
    String number;

    /**
     * @param licensePlateString a license plate string starting with a two-letter state code
     *                           followed by a series of letters and numbers
     * @throws IllegalArgumentException if state is not recognized
     */
    private LicensePlate(String licensePlateString) {
      state = State.valueOf(licensePlateString.substring(0, 2));
      number = licensePlateString.substring(2);
    }

  }

  /**
   * This iterator produces a series of LicensePlate objects. These are constructed
   * from the plate number strings passed to the constructor, with plates from unrecognized
   * states filtered out.
   */
  static class LicensePlateIterator implements Iterator<LicensePlate> {

    // add instance variables here
    private ArrayList<LicensePlate> array;
    private int next;

    LicensePlateIterator(Iterator<String> plateNumbers) {
      // implement me
      array = new ArrayList<LicensePlate>();
      next = 0;
      //add to the iterator;
      addToIterator(plateNumbers, array);
    }
    
    public void addToIterator(Iterator<String> plate, ArrayList<LicensePlate> plateArray){
      while (plate.hasNext()){
        String curPlate = plate.next();
        // filter unrecognized state
        try {
          LicensePlate licensePlate = new LicensePlate(curPlate);
          plateArray.add(licensePlate);
        }catch(IllegalArgumentException e){
          continue;
        }
        
      }
    }

    @Override
    public LicensePlate next() {
      // implement me
      if (next <= (array.size() - 1)){
        LicensePlate lp = array.get(next);
        next++;
        return lp;
      }else{
        throw new NoSuchElementException();
      }
      //return null;
    }

    @Override
    public boolean hasNext() {
      // implement me
      //return false;
      if (next > (array.size() - 1)){
        return false;
      }else{
        return true;
      }
    }
  }
  
  //TESTS
  
  public static void testFirstNext() {
    ArrayList<String> input = Lists.newArrayList("CA123456");
    LicensePlateIterator licensePlateProcessor = new LicensePlateIterator(input.iterator());

    LicensePlate next = licensePlateProcessor.next();
    assertNotNull(next);
    assertEquals(State.CA, next.state);
    assertEquals("123456", next.number);
  }

  public static void testHasNextTwice() {
    ArrayList<String> input = Lists.newArrayList("CA123456");
    LicensePlateIterator licensePlateProcessor = new LicensePlateIterator(input.iterator());

    assertEquals(true, licensePlateProcessor.hasNext());
    assertEquals(true, licensePlateProcessor.hasNext());
  }

  public static void testHasNext() {
    ArrayList<String> input = Lists.newArrayList("CA123456");
    LicensePlateIterator licensePlateProcessor = new LicensePlateIterator(input.iterator());

    assertEquals(true, licensePlateProcessor.hasNext());
    licensePlateProcessor.next();
    assertEquals(false, licensePlateProcessor.hasNext());
  }

  public static void testNextThrowsNoSuchElementException() {
    ArrayList<String> input = Lists.newArrayList("CA123456");
    LicensePlateIterator licensePlateProcessor = new LicensePlateIterator(input.iterator());
    licensePlateProcessor.next();
    try {
      licensePlateProcessor.next();
      fail();
    } catch (NoSuchElementException e) {
    }
  }

  public static void testNextSkipsUnrecognized() {
    ArrayList<String> input = Lists.newArrayList("CA123456", "YY121212", "UT432156");
    LicensePlateIterator licensePlateProcessor = new LicensePlateIterator(input.iterator());

    assertEquals(true, licensePlateProcessor.hasNext());
    LicensePlate next = licensePlateProcessor.next();
    assertEquals(State.CA, next.state);
    assertEquals("123456", next.number);

    assertEquals(true, licensePlateProcessor.hasNext());
    next = licensePlateProcessor.next();
    assertEquals(State.UT, next.state);
    assertEquals("432156", next.number);

    assertEquals(false, licensePlateProcessor.hasNext());
    try {
      licensePlateProcessor.next();
      fail();
    } catch (NoSuchElementException e) {
    }

  }

  public static void testHasNextReturnsFalseIfAllStatesUnrecognized() {
    // implement me
    //fail();
    
    ArrayList<String> input = Lists.newArrayList("YY121212", "MA123456","NY456789");
    LicensePlateIterator licensePlateProcessor = new LicensePlateIterator(input.iterator());
    
    assertEquals(false, licensePlateProcessor.hasNext());
  }
  
  public static void main(String[] args) {
    runTests();
  }
  
  private static void runTests() {
    System.out.println();
    for (Method method : Solution.class.getMethods()) {
      if (method.getName().startsWith("test") && method.getParameterTypes().length == 0) {
        try {
          method.invoke(null);
          System.out.println("  [PASS] " + method.getName());
        } catch (IllegalAccessException e) {
          System.out.println("X [FAIL] " + method.getName());
          throw new RuntimeException(e);
        } catch (InvocationTargetException e) {
          Throwable cause = e.getCause(); 
          System.out.println("X [FAIL] " + method.getName());
          if (cause instanceof AssertionError) { 
            System.out.println("     On line " + cause.getStackTrace()[1].getLineNumber() + ", " + cause.getMessage()); 
          } else { 
            System.out.print("     ");
            cause.printStackTrace(System.out); 
          }
        }  
      }
    } 
    System.out.println();
  }
  
  private static void assertEquals(Object a, Object b) {
    assert Objects.equals(a, b) : "[" + a + "] does not equal [" + b + "]";
  }
  
  private static void assertNotNull(Object a) {
    assert a != null : "object is null";
  }
  
  private static void fail() {
    assert false : "call to fail()";
  }
}
```
