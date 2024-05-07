# SMA v. DMA

**memory allocation:** memory allocation is a process by which computer programs and services are assigned with physical or virtual memory space. The memory allocation is done either before at the time of program execution. There are two types of memory allocations:

1. compile-time or static memory allocation
    
    static memory is allocated for declared variables by the compiler. The address can be found using the `address of` operator and can be assigned to a pointer. The memory is allocated during compile time.
    
2. run-time or dynamic memory allocation
    
    memory allocation done at the time of execution(run time) is known as dynamic memory allocation. Functions calloc() and malloc() support allocating dynamic memory. In the Dynamic allocation of memory space is allocated by using these functions when the value is returned by the functions and assigned to pointer variables.
    

**Stack Allocation**:

- a temporary memory allocation scheme where the data members are accessible only if the method() that contained them is currently running.
- allocates or de-allocates the memory automatically as soon as the corresponding method completes its execution.
- e receive the corresponding error Java. lang. **[StackOverFlowError](https://www.geeksforgeeks.org/stackoverflowerror-in-java-with-examples/)** by **[JVM](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/)**, If the stack memory is filled completely.
- Stack memory allocation is considered safer as compared to heap memory allocation because the data stored can only be accessed by the owner thread.
- Memory allocation and de-allocation are faster as compared to Heap-memory allocation
- Stack memory has less storage space as compared to Heap-memory
- Stack memory grows in different direction than the growth direction of the Heap memory.

**Heap Allocation:**

The memory is allocated during the execution of instructions written by programmers. Note that the name has nothing to do with the **[heap data structure](https://www.geeksforgeeks.org/heap-data-structure/).** It is called a heap because it is a pile of memory space available to programmers to allocate and de-allocate. Every time when we made an object it always creates in Heap-space and the referencing information to these objects is always stored in Stack-memory. Heap memory allocation isn’t as safe as Stack memory allocation because the data stored in the space is accessible or visible to all threads. If a programmer does not handle this memory well, a **[memory leak](https://www.geeksforgeeks.org/what-is-memory-leak-how-can-we-avoid/)** can happen in the program.

**The Heap-memory allocation is further divided into three categories:-** These three categories help us to prioritize the data(Objects) to be stored in the Heap-memory or in the **[Garbage collection](https://www.geeksforgeeks.org/garbage-collection-java/)**.

- **Young Generation –** It’s the portion of the memory where all the new data(objects) are made to allocate the space and whenever this memory is completely filled then the rest of the data is stored in Garbage collection.
- **Old or Tenured Generation –** This is the part of Heap-memory that contains the older data objects that are not in frequent use or not in use at all are placed.
- **Permanent Generation –** This is the portion of Heap-memory that contains the JVM’s metadata for the runtime classes and application methods.

key points:

- We receive the corresponding error message if Heap-space is entirely full, **[java. lang.OutOfMemoryError](https://www.geeksforgeeks.org/understanding-outofmemoryerror-exception-java/)** by JVM.
- This memory allocation scheme is different from the Stack-space allocation, here no automatic de-allocation feature is provided. We need to use a Garbage collector to remove the old unused objects in order to use the memory efficiently.
- The processing time(Accessing time) of this memory is quite slow as compared to Stack-memory.
- Heap memory is also not as threaded-safe as Stack-memory because data stored in Heap-memory are visible to all threads.
- The size of the Heap-memory is quite larger as compared to the Stack-memory.
- Heap memory is accessible or exists as long as the whole application(or java program) runs.

![Untitled](SMA%20v%20DMA%20efb3b0c1ba364a75a9af9241e1ec7082/Untitled.png)