# more concurrency with concurrent collections and atomic operations

When we use a synchronized block, Java internally uses a monitor, also know as a monitor lock or intrinsic lock, to provide synchronization. These monitors are bound to an Object: therefore, all synchronized blocks of the same object can have only one thread executing at the same time.

**Synchronized instance methods**

```java
public class SynchronizedMethods {

    private int sum = 0;

    public synchronized void synchronisedCalculate(){
    setSum(getSum() + 1);
		}

    // standard setters and getters
}

@Test
public void givenMultiThread_whenMethodSync() {
    ExecutorService service = Executors.newFixedThreadPool(3);
    SynchronizedMethods method = new SynchronizedMethods();
    
    IntStream.range(0 , 1000)
            .forEach(count -> service.submit(method::synchronisedCalculate));
    service.awaitTermination(1000, TimeUnit.MILLISECONDS);
    
    assertEquals(1000, method.getSum());
}
```

Notice that once we synchronize the method, the test case passes with the actual output as 1000. Instance methods are synchronized over the instance of the class owning the method, which means only one thread per instance of the class can execute this method.

- problems with synchronization
    
    ```java
    public class BiCounter {
        private int i = 0;
        private int j = 0;
        synchronized public void incrementI(){
            i++;
        }
    
        synchronized public void incrementJ(){
            j++;
        }
    
        public int getI(){
            return i;
        }
    
        public int getJ(){
            return j;
        }
    }
    ```
    
    Basically, the problem with synchronization using synchronized, is the fact that only one thread can be executed out of all the synchronized code on an instance. So, if there is a lot of synchronized code on a specific instance, it would have significant performance issue.
    
- solutions to the problem
    
    the first solution is to use Lock. With Lock, if two threads are trying to execute incrementI() and incrementJ(), they will be allowed to execute them at the same time. However, if two threads are waiting for incrementI(), they can only execute it one after the other.