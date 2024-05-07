# C/C++

Status: Done
Assign: GenuineLukas
subject: Algorithm

Basic understanding of c/c++ and its inner workings.

[https://www.abdulbari.incourses](https://www.abdulbari.in/courses)

### need to know

execution always starts from the `main()`

### Why C?

C is a general-purpose, high-level language that was originally developed by Dennis M. Ritchie to develop the UNIX operating system at Bell Labs. While Assembly language wasn’t portable, C was portable(able to run your code anywhere you want).

- Portability
- less lines of code compared to Assembly language.

### High Level vs Low Level

- Degree of Abstraction
- High level language → high level of Abstraction ex) C++, Python, Java …
- Low level language → Low level of Abstraction ex) Assembly Language
- **Middle level** language  ex) C
    - Direct access to memory through pointers
    - Bit manipulation using bitwise operators
    - Writing assembly code within C code

so….. C is 

- Procedural programming, middle-level language, and the popular choice for system-level apps

### .c and .h files

In your software repositories, you will often see pairs of files with the same name but different extensions (`.c` and `.h`) The `.c` file is often called the C file or implementation, while the `.h` file is often called the header file or interface.

`.c` files contain the implementation of the code, while`.h` files exist to provide interfaces that allow a file to access functions, global variables, and macros from other files.

When you `#include "file.h"` or `#include <folder/file.h>` in a file, it includes the header file in the current file so that you can call functions from `file.h`.

So in the end, .h file contains just an interface of the functions you will use. Inside the .c file, it has the actual implementation of the functions. There is something called “Linker” between .c and .h files which makes the division of labor possible, decreasing the amount of hecticness of one file if it was the solely working file for compilation. 

### memory Layout

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled.png)

A typical memory representation of a C program consists of the following sections.

1. Text Segment (i.e instructions)
2. Initialized data segment
3. Uninitialized data segment
4. Heap
5. Stack
- 1. Text Segment
    
    A text segment, also known as a code segment or simply as text, is one of the sections of a program in an object file or in memory, which contains executable instructions. As a memory region, a text segment may be placed below the heap or stack in order to prevent heaps and stack overflows from overwriting it.
    
    Usually, the text segment is sharable so that only a single copy needs to be in memory for frequently executed programs, such as text editors, the C compiler, the shells, and so on. Also, the text segment is often read-only to prevent a program from accidentally modifying its instructions.
    
- 2. Initialized Data Segment
    
    Initialized data segment, usually called simply the Data Segment. A data Segment is a portion of the virtual address space of a program, which contains the global variables and static variables that are initialized by the programmer.
    
    Note that, the data segment is not read-only since the values of the variables can be altered at run time.
    
    This segment can be further classified into the initialized read-only area and the initialized read-write area.
    
    For instance, the global string defined by char s[]= ”hello world” in C and a C statement like int debug = 1 outside the main(i.e.global) would be stored in the initialized read-write area. A global C statement like const char* string = ”hello world” makes the string literal “hello world” to be stored in the initialized read-only area and the character pointer variable string in the initialized read-write area.
    
    Ex: static int i = 10 will be stored in the data segment and global int i = 10 will also be stored in the data segment
    
- 3. Uninitialized Data Segment
    
    The uninitialized data segment often called the “**bss**” segment, is named after an ancient assembler operator that stood for “**block started by symbol**.” Data in this segment is initialized by the kernel to arithmetic 0 before the program starts executing uninitialized data starts at the end of the data segment and contains all global variables and static variables that are initialized to zero or do not have explicit initialization in the source code.
    
    For instance, a variable declared static int i; would be contained in the BSS segment.
    
    For instance, a global variable declared int j; would be contained in the BSS segment.
    
- 4. Stack
    
    The stack area traditionally adjoined the heap area and grew in the opposite direction; when the stack pointer met the heap pointer, free memory was exhausted. (With modern large address spaces and virtual memory techniques they may be placed almost anywhere, but they still typically grow in opposite directions.) The stack area contains the program stack, a LIFO structure, typically located in the higher parts of memory. On the standard PX x86 computer architecture, it grows towards address zero; on some other architectures, it grows in the opposite direction. A “stack pointer” register tracks the top of the stack; it is adjusted each time a value is “pushed” onto the stack. The set of values pushed for one function call is termed a “stack frame”; A stack frame consists at minimum of of a return address. Stack, where automatic variables are stored, along with information that is saved each time a function is called. Each time a function is called, the address of where to return to and certain information about the caller’s environment, such as some of the machine registers, are saved on the stack. The newly called function then allocates room on the stack for its automatic valuables. This is how recursive functions in C can work. Each time a recursive function calls itself, a new stack frame is used so one set of variables doesn’t interfere with the variables from another instance of the function.
    
- 5. Heap
    
    Heap is the segment where dynamic memory allocation usually takes place. The heap are begins at the end of the BSS segment and grows to larger addresses from there. The Heap area is managed by malloc, realloc, and free, which may use the brk and sbrk system calls to adjust its size (note that the use of brk/sbrk and a single “heap area” is not required to fulfill the contract of malloc/realloc/free; they may also be implemented using mmap to reserve potentially non-contiguous regions of virtual memory into the process’ virtual address space). The Heap area is shared by all shared libraries and dynamically loaded modules in a process.
    

### lvalue rvalue

lvalue(left value): simply means an object that has an identifiable location in memory*i.e.having an address).

- In any assignment statement “lvalue” must have the capability to hold the data.
- lvalue must be a variable because they have the capability to store the data.
- lvalue cannot be a function, expression (like a+b) or a constant(like 3,4,etc.)

rvalue(right value): simply means an object that has no identifiable location in memory.

- anything which is capable of returning a constant expression or value.
- Expressions like a + b will return some constant value.

### Token Generation

- Lexical analysis is the first phase in the compilation process.
- A lexical analyzer (scanner) scans the whole source program and when it finds the meaningful sequence of characters(lexemes) it converts it into a token
- Token: lexemes mapped into token-name and attribute-value.
    - Example: int → <keyword, int>
- It always matches the longest character sequence.

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%201.png)

### Arrays

What if the number of elements are lesser than the length specified?

→ the remaining locations of the array are filled by value 0.

### Pointers

**pointer[2] = 2[pointer]** because,

pointer[2] = *(p+2) = *(2+p) = 2[pointer]

### C Programming

- practice set 1
    
    Q1. What is the output of the following C program fragment:
    
    ```c
    int main() {
    		printf("%d", printf("%s", "Hello World!"));;
    		return 0;
    }
    ```
    
    - Answer
        
        Hello World!12
        
    - Printf not only prints the content on the screen. It also returns the number of characters that it successfully prints on the screen.
    
    Q2. What is the output of the following C program fragment:
    
    ```c
    int main() {
    		printf("%s", "Hello");
    		printf("%10s", "Hello");
    		return 0;
    }
    //Hello
    //     Hello
    ```
    
    - “%10s” means print the 10-character wide string.
    
    Q3. What is the output of the following C program fragment:
    
    ```c
    int main() {
    		char c = 255;
    		c = c + 10;
    		printf("%d", c);
    		return 0;
    }
    //9
    ```
    
    - since the 265%256 = 9.
    - 265 exceeds the max value of a char (8-bit)
    
    Q4. What is the output of the following C program fragment:
    
    ```c
    int main() {
    		unsigned i = 1;
    		int j = -4;
    		printf("%u", i + j);
    		return 0;
    }
    ```
    
    - answer
        
        Integer value depends from machine to machine
        
    - -3 in 2s complement of 3
        - 3 = 00000000 00000000 00000000 00000011
        - 1s complement of 3 = 11111111 11111111 11111111 11111100
        - Add 1 to the result. it will give
            
            11111111 11111111 11111111 11111101 = 4294967293 in my computer
            
- practice set 2
    
    Q1. what is the output of the following C program?
    
    ```c
    int main() {
    		int var = 052;
    		printf("%d", var); 
    		return  0;
    }
    ```
    
    - answer
        
        42
        
    
    if you write “0” in front of the number, it is going to be the octal number. 5x(8^1)+2x(8^0) is equivalent to 42 decimal number.
    
    Q2. what is the output of the following C program?
    
    ```c
    int main() {
    		int var = 052;
    		printf("%o", var);
    		return 0;
    }
    ```
    
    - answer
        
        52
        
    
    “%o” option is for octal value. Therefore, the output will print the octal value as it is.
    
    Q3. What is the output of the following C program?
    
    ```c
    #include <stdio.h>
    
    #define STRING "%s\n"
    #define GT "Welcome to Georgia Tech!"
    
    int main() {
    		printf(STRING, GT);
    		return 0;
    }
    ```
    
    - answer
        
        Welcome to Georgia Tech!
        
- practice set 3
    
    Q1. What is the output of the following C program fragment:
    
    ```c
    #include <stdio.h>
    
    int main() {
    		int var = 0x43FF;
    		printf ("%x", var);
    		return 0;
    }
    ```
    
    - answer
        
        43ff
        
    
    if you put 0x/0X in front of a number the number will be interpreted as a hexadecimal number. 
    
    Q2. wha is the output of the following C program fragment:
    
    ```c
    #include <stdio.h>
    
    static int i;
    static int i = 27;
    static int i;
    int main() {
    		static int i;
    		printf("%d", i);
    		return 0;
    }
    ```
    
    - answer
        
        0
        
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%202.png)
    
- practice set 5
    
    Q1. What is the output of the following program snippet?
    
    ```c
    int main() {
        int a = 4, b = 3;
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;
    
        printf("After XOR, a = %d and b = %d", a, b);
        return 0;
    }
    ```
    
    - answer
        
        After XOR, a = 3 and b = 4
        
    
    Q2. What is the output of the following program segment?
    
    ```c
    int main() {
        char a = 7;
        a ^= 5;
        printf("%d", printf("%d", a+=3));
        return 0;
    }
    ```
    
    - answer
        
        51
        
        inner printf first prints the 5 and the outer one prints the length of 5
        
    
    Q3. What is the output of the following program segment?
    
    ```c
    int main() {
        int var = 75;
        int var2 = 56;
        int num;
    
        num = sizeof(var) ? (var2 > 23 ? ((var == 75) ? 'A' : 0) : 0) : 0;
        printf("%d", num);
        return 0;
    }
    ```
    
    - answer
        
        65
        
    
    Q4. What is the output of the following C program fragment?
    
    ```c
    #incldue<stdio.h>
    
    int main(){
        int var;
        int num;
    
        num = (var = 15, var + 35);
        printf("%d", num);
        return 0;
    }
    ```
    
    - answer
        
        50
        
        when the comma operator is used like that, The comma operator returns the rightmost operand in the expression and **it simply evaluates the rest of the operands** and finally rejects them.
        
- practice set 6
    
    Q1. What is the output of the following C program fragment? Assume size of integer is 4 bytes.
    
    ```c
    #include <stdio.h>
    
    int main() {
    		int i = 5;
    		int var = sizeof(i++);
    		printf("%d %d", i, var);
    		return 0;
    }으
    ```
    
    - answer
        
        5 4
        
        according to C99 standard:
        
        The sizeod operator yields the size (in bytes) of its operand, which my be an expression of a parenthesized name of a type. The size is determined from the type of the operand. If the type of them operand is a variable length array type, then the operand is evaluated; otherwise, the operand is not evaluated an the result if an integer constant.
        
    
    Q2. What is the output of the following C program fragment?
    
    ```c
    int a = 1;
    int b = 1;
    int c = ++a || b++;
    int d = b-- && --a;
    
    printf("%d %d %d %d", d, c, b, a);
    ```
    
    - answer
        
        1 1 0 1 
        
    
    Q3. Predict the output
    
    ```c
    #include <stdio.h>
    int main() {
    		unsigned int var = 10;
    		printf("%d", ~var);
    }
    ```
    
    - answer
        
        -11
        
        10 in binary → 0000 0000 0000 1010
        
        NOT operation→ 1111 1111 1111 0101 
        
        음수이므로 십진수로 바꾸려면
        
        이거를 2의 보수로 인식 후 마이너스 붙여주기 →  - 0000 0000 0000 1011 → -11
        
        thinking process: 양수인 수를 bitwise NOT 계산을 해줬다. 그랬더니 음수가 됨(맨 앞 비트가 1이 되었기 때문) 그럼 이 아이가 십진수로 뭘까? 본래 7이라는 0111이 있으면 -7을 이진수로 표현해주고 싶을 때 2의 보수를 해준다. 0111 ⇒ 1001(이게 -7. 2의 보수는 다시 2의 보수해주면 본래 자신이 되므로 여기서 음수가 된 수에 2의 보수를 취해주고 앞에 -를 붙여주면 우리가 원하는 십진수를 얻을 수 있다.
        
- practice set 7
    
    Q1. how many times does the following C program print Hello, World?
    
    ```c
    int main() {
        int i = 1024;
        for(; i; i>>=1)
            printf("Hello, World");
        return 0;
    }
    ```
    
    - answer
        
        11
        
    
    Q2. what is the output of the following c program fragment.
    
    ```c
    #include <stdio.h>
    
    int main(){
    		int i;
    		for(i=0; i<20; i++){
    				switch(i){
    						case 0: i+= 5;
    						case 1: i+= 2;
    						case 2: i+= 5;
    						default: i+= 4;
    				}
    				printf("%d ", i);
    		}
    }
    ```
    
    Q3. How many times will “Neso” be printed on the screen?
    
    ```c
    int main(){
        int i = -5;
        while(i <= 5){
            if(i > 0)
                break;
            else
            {
                i++;
                continue;
            }
            printf("Neso");
        }
    }
    ```
    
    - answer
        
        0 times
        
    
    Q4. what is the output of the following C program fragment? Assuming size of unsigned int is 4 bytes.
    
    ```c
    int main(){
        unsigned int i = 500;
        while(i++ != 0);
        printf("%d", i);
        return  0;
    }
    ```
    
    - answer
        
        1
        
        Range of unsigned int (4 bytes) 0 to 4294967295
        
        When i reaches 4295967295, then because of i++, it comes back again to 0.
        
        As 0 not equal to 0 is false therefore we come outside of the white loop.
        
        After we come out of the loop, i will contain 1 because of post increment operaotr. Therefore, 1 will be printed on the screen.
        
    
    Q5. what is the output of the following C program fragment?
    
    ```c
    int main(){
        int x = 3;
        if(x == 2); x=0;
        if(x == 3) x++;
        else x += 2;
    
        printf("x = %d", x);
        return 0;
    }
    ```
    
    - answer
        
        x = 2
        
- practice set 8
    
    Q1. What is the output of the following C code?
    
    ```c
    int func(int num){
        int count = 2;
        while(num){
            count++;
            num >>= 2;
        }
        return(count);
    }
    
    int main() {
        printf("%d", func(435));
        return 0;
    }
    ```
    
    - answer
        
        7
        
    
    Q2. What is the output of the following C code?
    
    ```c
    void f1(int a, int b){
        int c;
        c =a; a=b; b= c;
    }
    void f2(int *a, int *b){
        int c;
        c = *a; *a = *b; *b = c;
    }
    
    int main() {
        int a = 4, b = 5, c = 6;
        f1(a, b);
        f2(&b, &c);
        printf("%d", c-a-b);
        return 0;
    }
    ```
    
    - answer
        
        -5
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%203.png)
        
    
    Q3. What is the output of the following C code?
    
    ```c
    int fun() {
        static int num = 16;
        return num--;
    }
    
    int main(){
        for(fun() ; fun(); fun())
        printf("%d ", fun());
        return 0;
    }
    ```
    
    - answer
        
        14 11 8 5 2 
        
- practice set 9
    
    What will be the output of the following program snippet:
    
    ```c
    int a,b;
    
    void print(){
        printf("%d %d", a, b);
    }
    
    int fun1() {
        int a, c;
        a = 0; b = 1; c = 2;
        return c;
    }
    
    void fun2() {
        int b;
        a = 3; b = 4;
        print();
    }
    
    int main(){
        a = fun1();
        fun2();
    }
    ```
    
    - with static scoping
        
        3 1
        
    - with dynamic scoping
        
        2 4
        
- practice set 10
    
    Q1. Consider the program below in a hypothetical programming language which allows global variables and a choice of static or dynamically scoping.
    
    ```c
    int i ;
    program main()
    {
    		i = 10;
    		call f();
    }
    
    procedure f()
    {
    		int i = 20;
    		call g();
    }
    procedure g()
    {
    		print i;
    }
    ```
    
    Let x be the value printed under static scoping and y be the value printed under dynamic scoping. Then, x and y are
    
    - answer
        
        x = 10, y = 20
        
    
    Q2. What will be the output of the following pseudocode when parameters are passed by reference and dynamically scoping is assumed?
    
    ```c
    a = 3;
    void n(x) {
    		x = x * a;
    		print(x);
    }
    void m(y) {
    		a = 1;
    		a = y - a;
    		n(a);
    		print(a);
    }
    void main() {
    		m(a);
    }
    ```
    
    - answer
        
        4 4
        
- practice set 11
    
    Q1. 
    
    when get(6)’d in main(), there are 25 invocation of get functions
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%204.png)
    
    Q2
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%205.png)
    
    - answer
        
        b
        
    
    Q3
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%206.png)
    
    - answer
        
        d
        
    
    Q4
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%207.png)
    
    - answer
        
        c
        
    
    Q5
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%208.png)
    
    - answer
        
        a
        
        the reason why the c is not the answer is that there are activation stacks of Act c2 and c3 still existing in stack, and they will come back to where they left off.
        
- practice set 12
    
    Q1. Which of the following statement is true about static functions in C?
    
    a) Static functions are global functions
    
    b) Static functions are restricted to the files where they are declared.
    
    c) There is no concept like static functions in C
    
    d) None of the above 
    
    - answer
        
        b
        
    
    Q2. State True or False. In C, is it mandatory to declare a function before use?
    
    - answer
        
        False
        
    
    Q3. Which of  the following ways to write a function prototype is correct?
    
    i. int fun(int var1, in var2)
    
    ii. int fun(int, int)
    
    iii.func(int, int)
    
    - answer
        
        only i and ii
        
    
    Q4. In C, parameters are always
    
    a) Passed by value
    
    b) Passed by reference
    
    c) Both
    
    d) None of the above
    
    - answer
        
        a:
        
        Parameters are always passed by value. Pass by reference is simulated in C explicitly passing pointer values
        
    
    Q5. In C, what is the meaning of the following function prototype with empty parameter list?
    
    void fun();
    
    - answer
        
        Function can be called with any number of parameters of any type.
        
- practice set 13
    
    Q1. WAP to sort numbers in reverse orders
    
    - answer
        
        ```c
        int main() {
            int a[9] = {34, 56, 54, 43, 67, 89, 32, 21};
            int i;
            //Original order
            for(i = 0; i<9; i++){
                printf("%d ", a[i]);
            }
        
            printf("\n");
        
            for(i = 8; i>=0; i--){
                printf("%d ", a[i]);
            }
        }
        ```
        
    
    Q2. WAP to check whether any of the digits in a number appears more than once:
    
    Example: 
    
    Input: 67827 → Output: YES
    
    - answer
        
        ```c
        int number, rem;
        
        int main(){
            printf("Please enter a number you want to check.\n");
            scanf("%d", &number);
        
            int arr[10] = {0};
            while(number != 0){
                rem = number%10;
                if(arr[rem] == 1){break;}
                arr[rem] = 1;
                number /= 10;
            }
        
            if(number > 0){
                printf("YES");
            }else{
                printf("NO");
            }
            return 0;
        }
        ```
        
    
    Q3. WAP that reads a 5x5 array of integers and then prints the row sum and column sum:
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%209.png)
    
    - answer
        
        ```c
        int main(){
            int arr[5][5] = {{8, 3, 9, 0, 10},
                {3, 5, 17, 1, 1},
                {2, 8, 6, 23, 1},
                {15, 7, 3, 2, 9},
                {6, 14, 2, 6, 0}};
        
            printf("Row total: ");
            int rowSum = 0;
            for(int i = 0; i<5; i++){
                for(int j = 0; j < 5; j++){
                    rowSum += arr[i][j];
                }
                printf(" %d", rowSum);
                rowSum = 0;
            }
        
            printf("\n");
        
            printf("Column total: ");
            int columnSum = 0;
            for(int i = 0; i<5; i++){
                for(int j = 0; j<5; j++){
                    columnSum += arr[j][i];
                }
                printf(" %d", columnSum);
                columnSum = 0;
            }
        
            return 0;
        }
        ```
        
- practice set 14
    
    Q1. Predict the output of the following program
    
    ```c
    int main(){
        int i = 1;
        int *p = &i;
        int *q = p;
        *q = 5;
        printf("%d", *p);
    }
    ```
    
    - answer
        
        5
        
    
    Q2. What is the output of the following program
    
    ```c
    void fun(const int *p){
    		*p = 0;
    }
    
    int main() {
    		const int i = 10;
    		fun(&i);
    		return 0;
    }
    ```
    
    - answer
        
        Output: Error: Assignment of read-only location *p
        
        main function에서 fun()이라는 함수를 불러서 main 안에서 정의된 i의 address를 넘겨 주었는데, fun 함수 안에서는 포인터로 그 address를 받았고, const 인 i 값을 바꾸려고 시도했다. 그러니까 당연히 error가 떴다. 여기서 주의할 점은 const인 i를 넘겨주므로 fun함수의 argument type은 const int로 선언해주어야함.
        
    
    Q3. How to print the address of a variable?
    
    - answer
        
        use %p as a format specifier in printf function.
        
        ```c
        #include <stdio.h>
        
        int main(){
            int i = 10;
            int *p = &i;
            printf("The address of variable i is %p", p);
            return 0;
        }
        //The address of variable i is 0x7ff7b96dd398
        ```
        
    
    Q4. If i is a variable and p points to i, which of the following expressions are aliases of i?
    
    a) **p      b) *&p     c) &p     d)*i      e)**&i 
    
    - answer
        
        a, e
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2010.png)
        
    
    Q5. What is the output of the following program?
    
    ```c
    #include <stdio.h>
    
    int main(){
        int a[] = {5, 16, 7, 89, 45, 32, 23, 10};
        int *p = &a[1], *q = &a[5];
    
        printf("%d ", *(p+3));
        printf("%d ", *(q-3));
        printf("%d ", q - p);
        printf("%d ", p < q);
        printf("%d", *p < *q);
        return 0;
    }
    ```
    
    - answer
        
        45 7 4 1 1
        
    
    Q6. How to access the second last element of the below array using pointer arithmetic?
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2011.png)
    
    - answer
        
        ```c
        int main(){
            int a[2][2][2] = {{{1,2},{3,4}},{{5,6}, {7,8}}};
            printf("%d", **(*(a+1)+1));
            return 0;
        }
        ```
        
- practice set 15
    
    Q1. consider the following declaration of two dimensional array in C char a[100][100]
    
    Assuming that the main memory is byte addressable and that the array is stored starting from the memory address 0, the address of a[40][50] is:
    
    - answer
        
        4050
        
    
    Q2. what is the output of the following C code? Assume that the address of x is 2000 (in decimal) and an integer requires four bytes of memory
    
    ```c
    #include <stdio.h>
    
    int main(){
        unsigned int x[4][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}, {10, 11, 12}};
        printf("%u %u %u", x+3, *(x+3), *(x+2) + 3);
    }
    ```
    
    - answer
        
        2036, 2036, 2036
        
    
    Q3. What is the output of the following program:
    
    ```c
    #include <stdio.h>
    
    int main() {
        int a[][3] = {1, 2, 3, 4, 5, 6};
        int (*ptr)[3] = a;
        printf("%d %d ", (*ptr)[1], (*ptr)[2]);
        ++ptr;
        printf("%d %d ", (*ptr)[1], (*ptr)[2]);
        return 0;
    }
    ```
    
    - answer
        
        2 3 5 6
        
    
    Q4. What is the output of the following C program:
    
    ```c
    #include <stdio.h>
    
    void f(int *p, int *q){
        p = q;
        *p = 2;
    }
    
    int i = 0, j = 1;
    int main() {
        f(&i, &j);
        printf("%d %d\n", i, j);
        return 0;
    }
    ```
    
    - answer
        
        0 2
        
    
    Q5. What is value printed by the following C program:
    
    ```c
    #include <stdio.h>
    
    int f(int *a, int n){
        if(n <=0){return 0;}
        else if(*a % 2 == 0){return *a + f(a+1, n-1);}
        else{
            return *a - f(a+1, n-1);
        }
    }
    
    int main() {
        int a[] = {12, 7, 13, 4, 11, 6};
        printf("%d", f(a, 6));
        return 0;
    }
    ```
    
    - answer
        
        15
        
    
    Q6. What is printed by the following C program:
    
    ```c
    #include <stdio.h>
    
    int f(int x, int *py, int **ppz){
        int y, z;
        **ppz += 1;
        z = **ppz;
        *py += 2;
        y = *py;
        x += 3;
        return x + y + z;
    }
    
    int main(){
        int c, *b, **a;
        c = 4, b = &c, a = &b;
        printf("%d", f(c,b,a));
        return 0;
    }
    ```
    
    - answer
        
        19
        
    
    Q7. What is printed by the following C program
    
    ```c
    #include <stdio.h>
    
    void swap (int *x, int *y){
        static int *temp;
        temp = x;
        x = y;
        y = temp;
    }
    void printab () {
        static int i, a = -3, b = -6;
        i = 0;
        while (i<=4){
            if((i++)%2 == 1) continue;
            a = a + i;
            b = b + i;
        }
        swap(&a, &b);
        printf("a = %d, b = %d\n", a, b);
    }
    
    int main(){
        printab();
        printab();
    }
    ```
    
    - answer
        
        a = 6, b = 3
        a = 15, b = 12
        
    
    Q8. c program is given below. What should be the contents of the arry b at the end of the program?
    
    ```c
    #include <stdio.h>
    
    int main(){
        int i, j;
        char a[2][3] = {{'a', 'b', 'c'}, {'d', 'e', 'f'}};
        char b[3][2];
        char *p = *b;
        for(i=0; i<2; i++){
            for(j = 0; j<3; j++){
                *(p + 2*j + i) = a[i][j];
            }
        }
    }
    ```
    
    - answer
        
        a d
        
        b e
        
        c 
        
- practice set 16
    
    Q1. The output of the program is
    
    ```c
    char p[20];
    char *s = "string";
    int length = strlen(s);
    int i;
    for (i = 0; i < length; i++) 
    		p[i] = s[length - i];
    printf("%s", p);
    ```
    
    - answer
        
        nothing.
        
        printf function will print everything before the null character and will not see anything after null character. Therefore, nothing will be printed on the screen. null character means the end of the array.
        
    
    Q2. What does the following fragment of C program print?
    
    ```c
    char c[] = "GATE2011";
    char *p = c;
    printf("%s", p + p[3] - p[1]);
    
    ```
    
    - answer
        
        2011
        
        if we assume the first char of the char array’s address is 1000, p is 1000 since it is the pointer to the 0’th element of the array. And p[3] is going to E, p[1] is going to be A. remember char is internally integer in C. E - A = 4.
        
        printf(”%s”, 1004); is going to be memory addy of 1004 upto the null character, which is 2011. 
        
    
    Q3. Consider the following function written in the C programming language. The output of the below function on input “ABCD EFGH” is
    
    ```c
    void foo(char *a){
    	if(*a && *a != ' ')
    	{
    		foo(a+1);
    		putchar(*a);
    	}
    }
    ```
    
    - answer
        
        DCBA
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2012.png)
        
    
    Q4. What is going to be the output
    
    ```c
    void func1(char *s1, char *s2) {
    		char *tmp;
    		tmp = s1;
    		s1 = s2;
    		s2 = tmp;
    }
    
    void fun2(char **s1, char **s2) {
    		char *tmp;
    		tmp = *s1;
    		*s1 = *s2;
    		*s2 = tmp;
    }
    
    int main() {
    		char *str1 = "Hi", *str2 = "Bye";
    		fun1(str1, str2);  printf("%s %s", str1, str2);
    		fun2(&str1, &str2);  printf("%s %s", str1, str2);
    		return 0; 
    }
    ```
    
    - answer
        
        Hi Bye Bye Hi
        
    
    Q5. Determine the output of the following program
    
    ```jsx
    #include<stdio.h>
    #include<string.h>
    
    int main(){
    		char *c = "GATESIT2017";
    		char *p = c;
    		printf("%d", (int)strlen(c+2[p] - 6[p] - 1));
    		return 0;
    }
    ```
    
    - answer
        
        2
        
- practice set 17
    
    Q1. Predict the output of the following C program
    
    ```c
    #include<stdio.h>
    struct Point{
    		int x, y, z;
    };
    
    int main()
    {
    		struct Point p1 = {.y = 0, .z = 1, .x = 2};
    		printf("%d %d %d", p1.x, p1.y, p1.z);
    		return 0;
    }
    ```
    
    - answer
        
        2 0 1
        
    
    Q2. Consider the following C program:
    
    ```c
    #include<stdio.h>
    struct Ournode{
    		char x, y, z;
    }
    
    int main() {
    		struct Ournode p = {'1', '0', 'a'+2};
    		struct Outnode *q=&p;
    		printf("%c %c", *((char*)q+1), *((char*)q+2));
    		return 0;
    }
    ```
    
    - answer
        
        0, c
        
        here the pointer q contains the address of the whole(entire) structure. after we are casting the type of pointer to the pointe to a character, it points to a character now.
        
    
    Q3. The following C declarations define s to be:
    
    ```c
    struct node
    {
    		int i;
    		float j;
    };
    struct node *s[10];
    ```
    
    - answer
        
        a
        
    
    a) an array, each element of which is a pointer to a structure of type node.
    
    b) a structure of 2 fields, each field being a pointer to an array of 10 elements.
    
    c) a structure of 3 fields: an integer, a float, and an array of 10 elements.
    
    d) an array, each element of which is a structure of type node.
    
- practice set 18
    
    Q1. Assume that objects of the type short, float and long occupy 2 bytes, 4 bytes and 8 bytes, respectively. The memory requirement for variable t, ignoring alignment considerations, is
    
    ```c
    struct {
    		short s[5];
    		union {
    				float y;
    				long z;
    		}
    }
    ```
    
    - answer
        
        18 bytes
        
    
    Q2. Suppose that s is the following structure
    
    ```c
    struct {
    		double a;
    		union {
    				char b[4];
    				double c;
    				int d;
    		} e;
    		char f[4];
    }s;
    ```
    
    If char values occupy 1 byte, int values occupy 4 bytes, and double values occupy 8 bytes, how much space will a C compiler allocate for u? (Assume that the compiler leaves no “holes” between members.)
    
    - answer
        
        20 bytes
        
        sizeof(s) = 20 bytes
        
    
    Q3. Suppose that s is the following union
    
    ```c
    union {
    		double a;
    		struct {
    				char b[4];
    				double c;
    				int d;
    		} e;
    		char f[4];
    }u;
    ```
    
    If char values occupy 1 byte, int values occupy 4 bytes, and double values occupy 8 bytes, how much space will a C compiler allocate for u? (Assume that the compiler leaves no “holes” between members.)
    
    - answer
        
        16 bytes
        
        sizeof(u) 16 bytes
        
- practice set 19
    
    Q. does it take constant time to delete the last node of the linked list given the the pointers to the first and last node of the list?
    
    - answer
        
        In order to delete the last node of the linked list, we need the address of the second last node. We only have a pointer to the last node. Therefore, we need to traverse the list in order to get the address of the second last node of the list. This will take O(n) time.
        
    
    Q.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2013.png)
    
    - answer
        
        the answer is c. to delete the last element of the list, we need the address of the second last element which will take us O(n) to traverse the list.
        
        - option b is just
            
            F→ link = T→ link;
            
            T→link = F;
            
            F = T;
            
    
    Q.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2014.png)
    
    - answer
        
        the answer is d
        
    
    Q.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2015.png)
    
    - answer
        
        answer is b
        
    
    Q. Let P be a singly linked list. Let Q be the pointer to an intermediate node x in the list. What is the worst-case time complexity of the best known algorithm to delete the node x from the list?
    
    - answer
        
        ```c
        struct node* temp = Q → link;
        Q → data = temp → data;
        Q → link - temp → link;
        free(temp);
        temp = NULL
        ```
        
        although this doesn’t work when the node to be deleted is the last node, it is the fastest algorithm for deleting the intermediate node of a list.
        
        so the answer is O(1) 
        
- practice set 20 (doubly linked list)
    
    Q1. Consider an implementation of unsorted doubly linked list. Suppose it has its representation with a head pointer and tail pointer. Given the representation, which of the following operation can be implemented in O(1) time?
    
    a) insertion at the front of the linked list.
    
    b) insertion at the end of the linked list.
    
    c) deletion of the front node of the linked list.
    
    d) deletion of the last node of the linked list.
    
    - answer
        
        All of the above
        
    
    Q2. Consider an implementation of unsorted doubly linked list. Suppose it has it representation with a head pointer only. Given the representation, which of the following operation can be implemented in O(1) time? 
    
    a) insertion at the front of the linked list
    
    b) insertion at the end of the linked list.
    
    c) deletion of the front node of the linked list.
    
    d) deletion of the last node of the linked list.
    
    - answer
        
        a and c
        
- practice set 21 (stack)
    
    Q1. if the sequence of operations - push(1), push(2), pop, push(1), push(2), pop, pop, pop, push(2), pop are performed on a stack, the sequence of popped out values are
    
    - answer
        
        22112
        
    
    Q2. Consider the following operations performed on.a stack of size 5 : push(a); pop(); push(b); push(c); pop(); push(d); pop(); pop(); push(e); which of the following statements is correct?
    
    a) underflow occurs b) stack operations are performed smoothly c) overflow occurs d) none of the mentioned
    
    - answer
        
        b
        
    
    Q3. which of the following permutation can be obtained in the same order using a stack assuming that input is the sequence 5, 6, 7, 8, 9 in that order?
    
    a) 7,8,9,5,6   b)5,9,6,7,8  c)7,8,9,6,5  d)9,8,7,5,6
    
    - answer
        
        c
        
    
    Q4. stack A has the entries a, b, c (with a on top). Stack B is empty. An entry popped out of stack A can be printed immediately or pushed to stack B. An entry popped out of the stack B can be printed. In this arrangement, which of the following permutations of a, b, c are not possible?
    
    a) b, a, c   b) b, c, a   c)c, a, b   d)a, b, c
    
    - answer
        
        c
        
    
    Q5. The following postfix expression with single digit operands is evaluated using a stack:
    
    8 2 3 ^ / 2 3 * + 5 1 * -
    
    The top two elements of the stack after the first * is evaluated are:
    
    - answer
        
        (from top)6 1
        
    
    Q6. Assume that the operators +, -, *, / are left associative and ^ is right associative. The order of precedence (from highest to lowest) is ^, x, +, -. The postfix expression corresponding to the infix expression a + b x c - d ^ e ^ f is 
    
    - answer
        
        abcx+def^^-
        
    
    Q7. The result evaluating the postfix expression 10 5 + 60 6 / * 8 - is
    
    - answer
        
        142
        
    
    Q8. Convert the following infix expression into its equivalent postfix expression
    
    (A + B ^ D) / (E - F) + G
    
    - answer
        
        ABD^+EF-/G+
        

### Data Types

### Integer

$$
sizeof(short) <= sizeof(int) <= sizeof(long)
$$

- Range
    
    integer types have these sizes depending on the machine.
    
    - 2bytes
        - Unsigned range: 0 to 65535 (by applying the equation below)
        
        $$
        2^n - 1
        $$
        
        - Signed range: -32768 to 32768
        
        $$
        -(2^{n-1}) to +(2^{n-1})
        $$
        
    - 4bytes
        - Signed range: 0 to 4294967595(by applying the same equation above)
        - Signed range: -2147483648 to 2147483647(using the same equation above)
    
    ```c
    #include <stdio.h> //standard input output file
    
    int main()
    {
        printf("%lu", sizeof(int)); //4
        return 0;
    }
    ```
    
- Long and Short
    
    given integer is 4 bytes,
    
    - integer
    
    ```c
    #include <stdio.h> 
    #include <limits.h>
    
    int main()
    {
        int var1 = INT_MIN;
        int var2  = INT_MAX;
    
        printf("range of signed integer is from %d to %d", var1, var2);
        //range of signed integer is from -2147483648 to 2147483647
        return 0;
    }
    
    int main()
    {
        unsigned int var1 = 0;
        unsigned int var2  = UINT_MAX;
    
        printf("range of signed integer is from %u to %u", var1, var2);
        //range of unsigned integer is from 0 to 4294967295
        return 0;
    }
    ```
    
    - short
    
    ```c
    #include <stdio.h> 
    #include <limits.h>
    
    int main()
    {
        printf("%lu", sizeof(short int)); //2
        return 0;
    }
    
    int main()
    {
        short int var1 = SHRT_MIN;
        short int var2  = SHRT_MAX;
    
        printf("range of signed integer is from %d to %d", var1, var2);
        //range of signed integer is from -32768 to 32767
        return 0;
    }
    
    int main()
    {
        unsigned short int var1 = 0;
        unsigned short int var2  = USHRT_MAX;
    
        printf("range of signed integer is from %u to %u", var1, var2);
        //range of signed integer is from 0 to 65535
        return 0;
    }
    ```
    
    - long
    
    ```c
    #include <stdio.h> 
    #include <limits.h>
    
    int main()
    {
        printf("%lu", sizeof(long int)); //8
        return 0;
    }
    
    int main()
    {
        long int var1 = LONG_MIN;
        long int var2  = LONG_MAX;
    
        printf("range of signed integer is from %ld to %ld", var1, var2);
        //range of signed integer is from -9223372036854775808 to 9223372036854775807
        return 0;
    }
    
    int main()
    {
        unsigned long int var1 = 0;
        unsigned long int var2  = ULONG_MAX;
    
        printf("range of signed integer is from %lu to %lu", var1, var2);
        //range of signed integer is from -9223372036854775808 to 9223372036854775807
        return 0;
    }
    ```
    
    - long long
    
    ```c
    int main()
    {
        printf("%lu", sizeof(long long int)); //8
        return 0;
    }
    ```
    
- exceeding the valid range
    - unsigned value
    
    ```c
    int main()
    {
        unsigned int var = 4294967296; //0
        printf("%u", var);
    }
    ```
    
    the valid range of the unsigned int is up to 4294967295. The reason why the phenomenon above happens is that the extra bit represents the exceeding number that is not available for us. 우리에게 available한 비트 수는 한정적이기 때문이다.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2016.png)
    
    - signed value
    
    ```c
    int main()
    {
        int var = -2147483649; //2147483647
        printf("%d", var);
    }
    ```
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2017.png)
    

### Character

```c
char some_variable_name = 'N'
char var = 65;

int main() 
{
	char var = 65;
	printf("%c", var); //A
	return 0;
}
```

- size and range
    - Size: 1byte = 8bits
    - Range
        - Unsigned: 0 to 255
        - Signed: -128 to +127
    
    In character, the negative value won’t give you any special power. In this case, a negative number is equivalent to a positive number in an extended ASCII set.
    
    In a traditional ASCII table, each character requires 7 bits.
    
    In the extended ASCII table, each character utilizes all 8 bits.
    
    ex)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2018.png)
    

### Float, Double, and Long Double

These Data types are for representing fractional numbers 

ex)  3.14, 0.678, -3276.789 … 

```c
int main()
{
    printf("%lu", sizeof(float)); //4
    printf("%lu", sizeof(double)); //8
    printf("%lu", sizeof(long double)); //16
    return 0;
}
```

Float → IEEE 754 Single Precision Floating Point

Double → IEEE 754 Double Precision Floating Point

Long Double → Extended Precision Floating Point

- overview on fixed and floating point
    
    the reason why Floating point representation is preferred over fixed point representation
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2019.png)
    
- the need for 3 different ways to represent fractional numbers
    - the degree of precision
    
    ```c
    int main()
    {
        float var1 = 3.1415926535897932;
        double var2 = 3.1415926535897932;
        long double var3 = 3.141592653589793213456;
    
        printf("%lu\n", sizeof(float)); //4
        printf("%lu\n", sizeof(double)); //8
        printf("%lu\n", sizeof(long double)); //16
        printf("%.16f\n", var1); //3.1415927410125732
        printf("%.16f\n", var2); //3.1415926535897931
        printf("%.21Lf\n", var3); //3.141592653589793115998
        return 0;
    }
    ```
    
- float arithmetic
    
    ```c
    int main()
    {
        int var = 4/9;
        printf("%d\n", var);
    
        float var1 = 4/9;
        printf("%.2f\n", var1);
    
        float var2 = 4/9.0;
        printf("%.2f\n", var2);
    
        float var3 = 4.0f/9.0f; //default is double 
        printf("%.2f\n", var3);
        
        return 0;
    }
    ```
    

### Scope of Variable

```c
int fun();

int var = 10; //global variable

int main() {
		int var = 3;
		printf("%d\n", var); //3
		fun(); //10
		return 0;
}

int fun(){
		printf("%d", var);
}
```

### Variable Modifiers

- Auto and Extern
    - Auto
        
        variables declared inside a scope by default are automatic variables.
        
        ```c
        #include <studio.h>
        
        int main() {
        		int var;
        		return 0;
        }
        
        //THE SAME THING
        
        int main() {
        		auto int var;
        		return 0;
        }
        ```
        
        - if you don’t initialize the auto variable, by default it is initialized with some garbage (random) value.
        
        ```c
        int main() {
        		auto int var;
        		printf("%d", var); //210919296
        		return 0;
        }
        ```
        
        - on the other hand, the global variable by default is initialized with 0.
        
        ```c
        int var;
        int main() {
            printf("%d", var);//0
        }
        ```
        
    - Extern
        
        `int var;` → Declaration and Definition
        
        `extern int var;` → Declaration
        
        → “Declare an int typed variable but do not allocate the memory”
        
        - Extern is the short name for external.
        - Used when a particular file needs to access a variable from another file.
        
        but if you use the extern keyword with declaration, the memory will be allocated.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2020.png)
        
        ```c
        //main.c
        
        extern int a;
        main() {
        	printf("%d", a); //5
        	return 0;
        }
        ```
        
        ```c
        //other.c
        
        int a = 5;
        ```
        
    - Register
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2021.png)
        
        - Register keyword hints the compiler to store a variable in register memory.
        - This is done because access time reduces greatly for the most frequently referred variables.
        - This is the choice of the compiler whether it puts the given variable in the register or not. (putting a register keyword in front doesn’t assure you that the variable will be stored inside the register memory)
        - Usually, compilers themselves do the necessary optimizations.
        
        ```c
        #include <stdio.h>
        
        int main() {
        		register int i = 10;
        
        		int* a = &i;
        		printf("%d", *a);
        		getChar();
        		retun 0;
        }
        ```
        
    - Static
        
        Static variables have the property of preserving their value even after they are out of their scope. Hence, a static variable preserves its previous value in its previous scope and is not initialized again in the new scope.
        
        - A static int variable remains in memory while the program is running. A normal or auto variable is destroyed when a function call where the variable was declared is over.
        
        ```c
        #include <stdio.h>
        
        int fun() {
        		static int count = 0;
        		count++;
        		return count;
        }
        
        int main(){
        		printf("%d", fun()); //1
        		printf("%d", fun()); //2
        		return 0;
        }
        ```
        
        - if it was a local auto variable
            
            ```c
            #include <stdio.h>
            
            int fun() {
            		int count = 0;
            		count++;
            		return count;
            }
            
            int main(){
            		printf("%d", fun()); //1
            		printf("%d", fun()); //1
            		return 0;
            }
            ```
            
        - static variables are allocated memory in the data segment, not the stack segment.
        - static variables (like global variables) are initialized as 0 if not initialized explicitly. For example in the blow program, the value of x is printed. as 0, while the value of y is something garbage.
            
            ```c
            #include <stdio.h>
            
            int main(){
            		static int x;
            		int y;
            		printf("%d \nd", x, y);
            }
            
            /*
            0
            34578
            */
            ```
            
        - In C, static variables can only be initialized using constant literals. For example, the following program fails in the compilation.
        
        ```c
        #include <stdio.h>
        
        int initializer(void){
        		return 50;
        }
        
        int main(){
        		static int i = initializer();
        		printf(" value of i = %d", i);
        		getChar();
        		return 0;
        }
        
        /*
        In function 'main':
        9:5: error: initializer element is not constant
             static int i = initializer();
             ^
        */
        ```
        
    

### Constants in C

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2022.png)

- using #define
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2023.png)
    
    - Please don’t add a semicolon at the end.
    - choosing capital letters for NAME is good practice.
    - whatever is inside double quotes “” won’t get replaced even if it has the same name as the constant defined.
    - we can use macros like functions
        
        ```c
        #include <stdio.h>
        #define add(x, y) x+y
        
        int main() {
        		printf("addition of two numbers: %d", add(4, 3));
        		return 0;
        }
        ```
        
    - we can write multiple lines using \
        
        ```c
        #include <stdio.h>
        #define greater(x, y) if(x > y) \
        													printf("%d is greater than %d", x, y);\
        											else \
        													printf("%d is lesser than %d", x, y);
        
        int main() {
        		greater(5, 6);
        		return 0;
        }												
        ```
        
    - First expansion then evaluation
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2024.png)
        
    - some predefined macros can print current date and time, etc.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2025.png)
        
- using const
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2026.png)
    
    ### Properties of Constant in C
    
    The important properties of constant variables in C defined using the const keyword are as follows:
    
    ### 1. Initialization with Declaration
    
    We can only initialize the constant variable in C at the time of its declaration. Otherwise, it will store the garbage value.
    
    ### 2. Immutability
    
    The constant variables in c are immutable after its definition, i.e., they can be initialized only once in the whole program. After that, we cannot modify the value stored inside that variable.
    

### scanf()

- stands for scan formatted string
- accept character, string, and numeric data from the user using standard input - Keyboard.
- Scanf also uses format specifiers like printf.
    - ex) %d, %c, %s …
- example
    
    ```c
    int var;
    scanf("%d", &var);
    ```
    
    - why &?
        - while scanning the input, scanf needs to store that input data somewhere.
        - To store this input data, scanf needs to know the memory location of a variable.
        - & is also called as address-of operator.
        
        &var === Address of var
        
    
    ```c
    int main() {
        int a;
        int b;
        printf("please enter the first number: \n");
        scanf("%d", &a);
        printf("please enter the second number: \n");
        scanf("%d", &b);
        printf("%d + %d = %d", a, b, a+b);
        return 0;
    }
    ```
    

### Operators in C

I write down only personally important things …

- concept of short circuits in logical operators
    - short circuit in the case of &&: simply means if there is a condition anywhere in the expression that returns false, then the rest of the conditions after that will not be evaluated.
        
        ```c
        int main() {
            int a = 5, b = 3;
            int incr;
            
            incr = (a < b) && (b++);
            printf("%d\n", incr); //0
            printf("%d", b); //4
            return 0;
        }
        ```
        
    - short circuit in case of ||: simply means if there is a condition anywhere in the expression that returns True, then the rest of the conditions after that will not be evaluated.
        
        ```c
        int main() {
        		int a = 5, b = 3;
        		int incr;
        	
        		incr = (a > b) || (b++);
        		printf("%d\n", incr); //1
        		printf("%d", b); //3
        		return 0;
        }
        ```
        
- bitwise operators
    
    &, |, ~, <<, >>, ^
    
    - bitwise and (&) operator
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2027.png)
        
    - bitwise or (|) operator
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2028.png)
        
    - bitwise not(~) operator
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2029.png)
        
    - difference between bitwise and logical operators
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2030.png)
        
    - left shift operator
        
        ```c
        First operand << Second operand
        ```
        
        - First operand: whose bits get left shifted
        - Second operand: Decides the number of places to shift the bits
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2031.png)
        
        1. when bits are shifted, left trailing positions are filled with zeros.
        2. left shifting is equivalent to multiplication by 
            
            $$
            2^{rightOperand}
            $$
            
            ex)
            
            var = 3 
            
            var << 4 ouput: 48 [3 x 2^4]
            
    - right shift operator
        
        ```c
        First operand >> Second operand
        ```
        
        First operand: Whose bits get right shifted?
        
        Second operand: Decides the number of places to shift the bits.
        
        1. when bits are shifted, right trailing positions are filled with zeros.
            
            ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2032.png)
            
        2. right shifting is equivalent to division by 
            
            $$
            2^{rightOperand}
            $$
            
            ex)
            
            var = 3 
            
            var >> 1 output: 1 [3/2^1]
            
    - bitwise XOR(^) operator
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2033.png)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2034.png)
        
- assignment operator
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2035.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2036.png)
    
- conditional operator
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2037.png)
    
    - conditional operator is the only ternary operator available in the list of operators in the C language.
    
- comma operator
    - comma operator can be used as an ‘operator’.
        
        ```c
        int a = (3, 4, 8);
        printf("%d", a);
        //OUTPUT: 8
        ```
        
        - The comma operator returns the rightmost operand in the expression and **it simply evaluates the rest of the operands** and finally rejects them.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2038.png)
        
    - comma operator has the least precedence among all the operators available in the C language.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2039.png)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2040.png)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2041.png)
        

### Precedence and Associativity of Operators

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2042.png)

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2043.png)

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2044.png)

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2045.png)

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2046.png)

### Special Programs

- pyramid of stars
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2047.png)
    
    ```c
    int main(){
        int numOfRows;
        printf("Enter the number of rows");
        scanf("%d", &numOfRows);
        for(int i = 1; i <= numOfRows; i++){
            for(int j = 1; j <= 2*numOfRows - 1; j++){
                if(j >= numOfRows-(i-1) && j<= numOfRows+(i-1)){
                    printf("*");
                } else {
                    printf(" ");
                }
            }
            printf("\n");
        }
    }
    ```
    
- palindrome(number)
    
    A number or a word or a phase if read backwards gives the same word or a phrase as it is being read forward
    
    ```c
    #include <stdio.h>
    
    int main(){
    	int n, result=0, q, rem ;
    	printf("write a number: \n");
    	scanf("%d", &n);
    
    	q = n;
    
    	while(q != 0) {
    		rem = q%10;
    		result = 10*result + rem;
    		q = q/10;
    	}
    	
    	if(result == n){
    		printf("Yes! It's a palindrome.");
    	}else{
    		printf("No! It;s not a palindrome.");
    	}
    	return 0;
    }
    ```
    
- armstrong number
    
    an Armstrong number of order n is a number in which each digit when multiplied by itself n number of times and finally added together, results in the same number.
    
    ex) 371 = 3^3 + 7^3 + 1^3 = 371
    
- strong number
    
    strong number is a number in which the sum of factorial of individual digits of a number is equal to the original number.
    
    145 = 1! + 4! + 5! = 145
    
    ```c
    int main(){
        int n,q, rem, result = 0, factorial = 1;
    
        printf("Please enter a number:\n");
        scanf("%d", &n);
    
        q = n;
    
        while(q != 0){
            rem = q%10;
    
            for(int i = 1; i<=rem; i++){
                factorial *= i;
            }
    
            result = result + factorial;
            factorial = 1;
            q = q/10;
        }
    
        if(result == n){
            printf("Yes, it is a strong number!");
        }else{
            printf("No, it is not a strong number!");
        }
    
        return 0;
    }
    ```
    
- prime number
    
    prime number is a number greater than 1 and has only two factors, namely 1 and the number itself.
    
    ex) 2, 3, 5, 7, 11…
    
    composite number is a positive integer which is not prime i.e. which has factors other than 1 and itself.
    
    Is 1 a prime number?
    
    No, it’s not a prime number because according to the definition of prime numbers - A prime number is a number which has exactly two divisors, 1 and itself. But 1 has only one divisor i.e. itself. Therefore it is not a prime number.
    
    Another reason - it violates the fundamental theorem of arithmetic
    
    According to this theorem - Every positive integer greater than one can be written **uniquely** as the product of primes.
    
    9 = 3*3*1 = 3*3*1*1 = 3*3*1*1*1…
    
    해설: In order to find whether a number is prime or not, We first need to calculate the square root of that number and then we divide that number by numbers less than or equal to the square root of that number. If it is divisible by any of the numbers then we can say that the number is not a [rime number else it is a prime number.
    
    ```c
    int main(){
        float sqrtNum;
        int n, sqrtNatural, flag = 0;
    
        printf("Please enter a number(only positive intergers):\n");
        scanf("%d", &n);
    
        sqrtNum = sqrt(n);
        sqrtNatural = ceil(sqrtNum);
    
        if(sqrtNatural >= 2){
            for(int i = 2; i <= sqrtNatural; i++){
                if(n%i == 0){
                    flag = 1;
                    break;
                }
            }
            if(flag == 1){
                printf("No!, it is not a prime number!");
            } else {
                printf("Yes!, it is a prime number!");
            }
        }
        return 0;
    }
    ```
    
- addition without ‘+’ operator
    
    Algorithm:
    
    step1: x++; y--;
    
    step2: repeat step 1 until y becomes 0;
    
    ```c
    int main(){
        int x,y;
    
        printf("Please enter two numbers you want to add:\n");
        scanf("%d %d", &x, &y);
    
        while(y != 0){
            x++;
            y--;
        }
    
        printf("Sum of two values is %d", x);
        return 0;
    }
    ```
    
    when we want to consider negative numbers also
    
    ```c
    int main(){
        int x,y;
    
        printf("Please enter two numbers you want to add:\n");
        scanf("%d %d", &x, &y);
    
        if(y > 0){
            while(y != 0){
                x++;
                y--;
            }
        }else if(y < 0){
            while(y!=0){
                x--;
                y++;
            }
        }
    
        printf("Sum of two values is %d", x);
        return 0;
    }
    ```
    
- addition without ‘+’ operator(half adder logic)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2048.png)
    
    ```c
    int main(){
        int x, y, sum, carry;
    
        printf("Please enter two numbers");
        scanf("%d %d", &x, &y);
    
        while(y != 0){
            sum = x^y;
            carry = (x&y) << 1;
            x=sum;
            y=carry;
        }
        printf("%d", x^y);
    
        return 0;
    }
    ```
    
- fibonacci
    
    In fibonacci series, next term is obtained by taking sum of previous two terms.
    
    What is so magical about the fibonacci number?
    
    it is found in nature.
    
    ```c
    int main(){
    
        int n, a=0, b=1, result;
    
        printf("please enter a number");
        scanf("%d", &n);
    
        for(int i=1; i<=n; i++){
            printf("%d", a);
            result = a + b;
            a = b;
            b = result;
        }
    
    }
    ```
    
- floyd’s triangle
    
    Floyd’s Triangle (named after a computer scientist - Robert W.Floyd) is a right-angled triangular array of natural numbers. It is filled by natural numbers consecutively starting with 1 in the top left corner.
    
    For example: A floyd’s triangle with 5 rows
    
    1
    
    2 3
    
    4 5 6
    
    7 8 9 10
    
    11 12 13 14 15
    
    ```c
    int main(){
    
        int row, prtNum =1;
    
        printf("please enter the number of rows.");
        scanf("%d", &row);
    
        for(int i = 1; i<=row; i++){
            for(int j = 0; j<i; j++){
                printf("%d", prtNum);
                prtNum++;
            }
            printf("\n");
        }
        return 0;
    }
    ```
    
- binary to decimal conversion
    
    ```c
    int main(){
    
        const int base = 2;
        int binary, rem, weight = 1, result = 0;
    
        printf("please enter a binary number.");
        scanf("%d", &binary);
    
        while(binary != 0){
            rem = binary%10;
            result = result + rem*weight;
            binary /= 10;
            weight *= 2;
        }
    
        printf("the decimal form of the binary number you plugged in is: %d", result);
    
        return 0;
    }
    ```
    
- calculating power of an integer
    
    ```c
    int main(){
    
        int base, power, result = 1;
    
        printf("please enter a base and a power number.");
        scanf("%d %d", &base, &power);
    
        if(power < 0){
            int absValOfPow = 0 - power;
            for(int i = 0; i < absValOfPow; i++){
                result /= absValOfPow;
            }
        }else {
            for (int i = 0; i < power; i++) {
                result *= base;
            }
        }
    
        printf("the number you want is: %d", result);
    
        return 0;
    }
    ```
    
- check Leap year
    
    Leap year is a year having 366 days.
    
    The extra day is the 29th February.
    
    Leap year arrives after every four years.
    
    every year that is exactly divisible by 4 is a leap year, except the centurial year that is exactly divisible by 100. But these centurial years are leap years if they are exactly divisible by 400.
    
    ```c
    int main(){
    
        int year;
    
        printf("please enter an year.");
        scanf("%d", &year);
    
        if(year%400 == 0){
            printf("Yes! %d is a leap year.", year);
        }else if(year%100 == 0){
            printf("NO! %d is NOT a leap year.", year);
        }else if(year%4 == 0){
            printf("Yes! %d is a leap year.", year);
        }else{
            printf("NO! %d is NOT a leap year.", year);
        }
    
        return 0;
    }
    ```
    
- perfect number
    
    perfect number is a positive integer that is equal to the sum of all its proper positive divisors excluding the number itself.
    
    For example… 6 is a perfect number 1 + 2 + 3 = 6.
    
    ```c
    int main(){
    
        int num, sqrtNum, result = 1;
    
        printf("please enter a number.");
        scanf("%d", &num);
    
        sqrtNum = ceil(sqrt(num));
    
        for(int i = 2; i<sqrtNum; i++){
            if(num%i == 0){
                result = result + i + num/i;
            }
        }
    
        if(result == num){
            printf("Yes! %d is a perfect number.", num);
        }else {
            printf("No! %d is NOT a perfect number.", num);
        }
    
        return 0;
    }
    ```
    

### Functions in C

Function is basically a set of statements that takes inputs, perform some computation and produces output. functions ensure Reusability and Abstraction in your code.

- calling function before defining it?
    
    In C , if a function is called before its declaration, the compiler assumes the return type of function as int.
    
    ```jsx
    #include <stdio.h>
    int main(void){
    	printf("%c\n", fun());
    	return 0;
    }
    
    char fun(){
    	return 'G';
    }
    ```
    
    if the function char fun() in the above code is defined later to main() and the calling statement, then it will NOT compile successfully. Because the compiler assumes the return type as “int” by default. And at declaration, if the return type is not matching with int then the compiler will give an error. 
    
    Even though you changed the return type to int, however, it will return the following error:
    
    > Call to undeclared function 'fun'; ISO C99 and later do not support implicit function declarations
    > 
    
    The following code works fine though.
    
    ```jsx
    #include <stdio.h>
    
    int fun(){
    	return 'G';
    }
    
    int main(void){
    	printf("%d\n", fun());
    	return 0;
    }
    ```
    
    What about parameters? compiler assumes nothing about parameters. Therefore the compiler will not be able to perform compile-time checking of argument types and arity when the function is applied to some arguments.
    
    ```jsx
    #include <stdio.h>
    
    int main(void){
    	printf("%d", sum(10, 5));
    }
    
    int sum (int b, int c, int a){
    	return (a+b+c);
    }
    ```
    
- function prototype
    
    just a prototype of function in c.
    
    - there is no need to mention names of the parameters in a function prototype.
        
        ```jsx
        int sum(int, int, int); //function prototype
        
        int main (void)
        {
            printf("%d", sum(10, 5,3));
            return 0;
        }
        int sum (int b, int c, int a)
        {
            return (a+b+c);
        }
        ```
        
- argument v. parameter
    - parameter: a variable in the declaration and definition of the function.
    - argument: the actual value of the parameter that gets passed to the function.
    
    Parameter is also called as Formal Parameter and Argument is also called as Actual Parameter.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2049.png)
    
- call by value v. call by reference
    
    **Call by value**
    
    Here values of actual parameters will be copied to formal parameters and these two different parameters store values in different locations.
    
    ```c
    int x= 10, y= 20;
    int fun(int x, int y){
        x= 20;
        y = 10;
        return 0;
    }
    int main(){
        fun(x,y);
        printf("x=%d y=%d", x, y);
        return 0;
    }
    
    // x= 10 y = 20
    ```
    
    **Call by reference**
    
    Here both actual and formal parameters refers to same memory location. Therefore, any changes made to the formal parameters will get reflected to actual parameters. Here instead of passing value, we pass addresses.
    
    ```c
    int x = 10, y = 20;
    int fun(int *ptr1, int *ptr2)
    {
        *ptr1 = 20;
        *ptr2 = 10;
        return 0;
    }
    int main(){
        fun(&x, &y);
    
        printf("x=%d y=%d", x, y);
        return 0;
    }
    
    // x= 20 y = 10
    ```
    
- static functions in C
    - In C, functions are global by default.
    - This means if we want to access the function outside from the file where it’s declared, we can access  it easily.
    - Now if we **want to restrict** this access, then we make our function static by simply putting a keyword static in front of the function.
    
    ```c
    //file1.c
    static int fun(int a, int b){
    		int c;
        c = a+b;
        return c;
    }
    
    //main.c
    int fun(int, int);
    int main(){
        int sum = fun(3, 4);
        printf("%d", sum);
        return 0;
    }
    //clang: error: linker command failed with exit code 1 (use -v to see invocation)
    ```
    

### Static & Dynamic Mapping

- **Static and Dynamic scoping (part1)**
    
    **Properties of Stack**
    
    - Stack is a container (or memory segment) which holds some data.
    - Data is retrieved in LIFO fashion.
    - There are two operations which can be performed on Stack: **Push** and **Pop**
    
    ```c
    main() 
    {
        fun1();           
    } 
    fun1() 
    {  
        fun2();
    } 
    fun2() 
    { 
        fun3(); 
    }
    ```
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2050.png)
    
    When compiler comes across return statement in a function, it stops executing the current function and jumps back to the previous function from where it left off.
    
    In reality, it is the **activation record** of each function that is stored and maintained inside the call stack after the function call.
    
    Activation Record is a portion of a stack which is generally composed of:
    
    1.  Locals of the callee
    2. Return address to the caller
    3. Parameters of the callee
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2051.png)
    
- **Static and Dynamic scoping (part2)**
    
    **What is Static Scoping?**
    
    In Static Scoping (or Lexical Scoping), definition of a variable is resolved by searching its containing block or function. If that fails, then searching the outer containing block and so on.
    
    C uses Static Scoping. In most programming languages including C, C++, and Java, variables are always statically(or lexically) scoped.
    
    - right before the code flow meets the return statement in fun2.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2052.png)
    
    그리고 순차적으로 stack에서 pop out 되어 나온다.
    
    **What is Dynamic Scoping?**
    
    In dynamic scoping, the definition of a variable gets resolved by searching its containing block. If it fails, then it is looked for in the calling function, and if still not found, the caller of the calling function is searched, and so on.
    
    Dynamically scoped programming languages include bash, LaTeX, and the original version of Lisp.
    
    - right before the code flow meets the return statement in fun2.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2053.png)
    
    그리고 순차적으로 stack에서 pop out 되어 나온다.
    
- **Static and Dynamic scoping (part3)**
    1. in most of the programming languages, static scoping is followed instead of dynamic scoping
    2. Languages, including Algol, Pascal, C, Haskell, Scheme etc. are statically scoped.
    3. Some languages, including SNOBOL, APL, Lisp etc. are dynamically scoped.
    4. As C follows static scoping therefore it is not possible to see programmatically, how dynamic scoping works in C.
    5. Perl is a programming language which supports both static as well s dynamic scoping 
    

### Recursion

- Program to demonstrate recursion
    
    ```c
    int fun(int n){
        if(n==1){
            return 1;
        } else {
            return 1 + fun(n-1);
        }
    }
    
    int main() {
        int n = 3;
        printf("%d", fun(n));
        return 0;
    }
    
    //output: 3
    ```
    
- Different Types of Recursion
    - Direct recursion
        
        A function is called direct recursive if it calls the same function again.
        
        ```c
        fun() {
        		//some code
        		func();
        		//some code
        }
        ```
        
    - Indirect recursion
        
        A function(let’s say fun) is called indirect recursive if it calls another  function (let’s say fun2) and then fun2 calls fun directly or indirectly.
        
        ```c
        fun() {
        		//some code
        		fun2();
        		//some code
        }
        
        fun2() {
        		//some code
        		fun();
        		//some code
        }
        ```
        
        example:
        WAP to print numbers from 1 to 1- in such a way that when number is odd, add 1 and when number is even, subtract 1.
        
        ```c
        void odd();
        void even();
        
        int main(){
            odd();
        }
        
        int n =1;
        void odd(){
            if(n <= 10){
                printf("%d ", n+1);
                n++;
                even();
            }
            return ;
        };
        
        void even(){
            if(n <= 10){
                printf("%d ", n - 1);
                n++;
                odd();
            }
            return;
        };
        ```
        
    - Tail recursion
        
        A recursive function is said to be tail recursive if the recursive call is the last thing done by the function. There is no need to keep record of the previous state.
        
        ```c
        void fun(int n) {
            if(n == 0) {
                return;
            } else {
                printf("%d ", n);
                return fun(n - 1);
            }
        }
        
        int main() {
            fun(3);
            return 0;
        }
        ```
        
    - Non-tail recursion
        
        A recursive function is said to be non-tail recursive if the recursive call is not the last thing done by the function. After returning back, there is something left to evaluate.
        
        ```c
        void fun(int n) {
            if(n == 0){
                return;
            }
            fun(n-1);
            printf("%d ", n);
        }
        
        int main() {
            fun(3);
            return 0;
        }
        //1 2 3
        ```
        
        ```c
        int fun(int n) {
            if(n == 1){
                return 0;
            }else{
                return 1 + fun(n/2);
            }
        }
        
        int main() {
            printf("%d", fun(8));
            return 0;
        }
        //3
        ```
        
    
- Advantage and Disadvantage of Recursion
    - Every recursive program can be modeled into an iterative program but recursive programs are more elegant and requires relatively less lines of code.
        
        ex) Factorial
        
        ```c
        //ITERATIVE
        int fact(int n) {
        		int res=1;
        		while(n!=0){
        			res = res*n;
        			n--;
        		}
        		return res;
        }
        
        int main() {
        		printf("%d", fact(5));
        		return 0;
        }
        
        //RECURSIVE
        int fact(int n){
        	if(n==1){
        		return 1;
        	} else {
        		return n*fact(n-1);
        	}
        }
        int main() {
        		printf("%d", fact(5));
        		return 0;
        }
        
        ```
        
    - Recursive programs require more space than iterative programs do. More space needed for activition records.
    

### Arrays in C

> An array is a data structure containing a number of data values (all of which are of same type)
> 
- What is Data Structure?
    
    Data Structure is a format for organizing and storing data.
    
    each data structure is designed to organize data to suit a specific purpose.
    
- one dimensional array
    
    The simplest form of array one can imagine is one dimensional array.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2054.png)
    
    - **declaration and definition of 1d array**
        
        `int arr[5]`
        
        → compiler will allocate a contiguous block of memory of size = 5*sizeof(int)
        
        - Specifying the length of an array using macro is considered to be an excellent practice
            
            ```c
            #define N 10
            int arr[N];
            ```
            
            the reason why it is such a good practice is that it offers you a good Developer Experience. To change the length of arrays, you can just change the value of the Macro.
            
        
        **accessing elements from 1d array**
        
        `array_name[index]`
        
    - **how to initialize one dimensional array**
        
        Method 1:
        
        `arr[5] = {1, 2, 5, 67, 32};`
        
        Method 2:
        
        `arr[] = {1, 2, 5, 67, 32}`
        
        Method 3:
        
        ```c
        int arr[5]
        
        arr[0] = 1;
        arr[1] = 2;
        arr[2] = 5;
        arr[3] = 67;
        arr[4] = 32;
        ```
        
        Method 4:
        
        ```c
        int arr[5];
        
        for(i = 0; i< 5; i++){
        		scanf("%d", &arr[i]);
        }
        ```
        
        Method 5:
        
        `int arr[10] ={0}` → easiest way to initialize an array with all zeros
        
    - **Designated Initialization of Arrays**
        
        say we want to achieve this.
        
        ```c
        int arr[10] = {1, 0, 0, 0, 0, 2, 3, 0, 0, 0}
        ```
        
        this will work
        
        `int arr[10] = {[0] = 1, [5] = 2, [6] = 3};`
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2055.png)
        
        - what if I won’t mention the length?
            - designators could be any non-negative integer.
            - compiler will deduce the length of the array from the largest designator in the list.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2056.png)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2057.png)
        
    - **Count Array Elements using sizeof() Operator**
        
        `sizeof(name_of_arr)/sizeof(name_of_arr[0]);`
        
- multidimensional array
    - size calculation
        
        size of multidimensional array can be calculated by multiplying the size of all the dimensions.
        
        size of a[10][20] = 200X4 = 800 bytes.
        
        size of a[4][10][20] = 800X4 = 3200bytes.
        
    - two dimensional array
        
        int arr[4][5]
        
        - 4 → # of rows
        - 5 → # of rows
        - how to initialize two dimensional array
            
            Method 1:
            
            int[2][3] = {1, 2, 3, 4, 5, 6}
            
            ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2058.png)
            
            Method 2:
            
            int a[2][3] = {{1, 2, 3}, {4, 5, 6}};
            
            ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2059.png)
            
        - how to access 2d array elements
            
            ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2060.png)
            
        - how to print 2d array elements
            
            2d array elements can be printed using two nested for loop
            
            ```c
            int main(){
                int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
                for(int i = 0; i<2; i++){
                    for(int j = 0; j<3; j++){
                        printf("%d ", arr[i][j]);
                    }
                }
                return 0;
            }
            ```
            
- three-dimensional array
    
    int arr[2][3][3] //initialization
    
    arr[0][0][2]
    
    - 0 → first 2d array
    - 0 → first row
    - 2 → third column
    - how to initialize 3d array
        
        Method 1:
        
        int a[2][2][3] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2061.png)
        
        Method 2:
        
        int a[2][2][3] = {{{1, 2, 3}, {4, 5, 6}},{{7, 8, 9}, {10, 11, 12}}} 
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2062.png)
        
    - how to print 3d array
        
        3d array elements can be printed using three nested for loops.
        
        ```c
        int main(){
            int a[2][2][3] = { {{1, 2, 3},
                                {4, 5, 6}},
                               {{7, 8, 9}, 
                                {10, 11, 12}}};
        
            for(int i = 0; i<2; i++){
                for(int j = 0; j<2; j++){
                    for(int k = 0; k < 3; k++){
                        printf("%d ", a[i][j][k]);
                    }
                }
            }
            return 0;
        }
        ```
        
- C Program for Matrix Multiplication
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2063.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2064.png)
    
    and goes on…
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2065.png)
    
    IMPORTANT POINT
    
    - In order to multiply two matrices, # of columns of 1st matrix = # of rows of 2nd matrix
    - Also, size of the resultant matrix depends on # of rows of 1st matrix and # of columns of 2nd matrix
    - so, how to write?
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2066.png)
        
        ```c
        #define MAX 50
        
        int main(){
            int i, j, k;
            int a[MAX][MAX], b[MAX][MAX], product[MAX][MAX];
            int arow, acolumn, brow, bcolumn, sum =0;
        
            printf("Enter the rows and columns of matrix a: \n");
            scanf("%d %d", &arow, &acolumn);
        
            printf("enter the elements of matrix a:\n");
            for(i=0; i<arow; i++){
                for(j=0; j<acolumn; j++){
                    scanf("%d", &a[i][j]);
                }
            }
        
            printf("Enter the rows and columns of the matrix b: ");
            scanf("%d %d", &brow, &bcolumn);
        
            if(brow != acolumn){
                printf("Sorry! We cannot multiply the matrices a and b");
            }else{
                printf("enter the elements of matrix b:\n");
                for(i=0; i<brow; i++){
                    for(j=0; j<bcolumn; j++){
                        scanf("%d", &b[i][j]);
                    }
                }
            }
        
            printf("\n");
        
            for(i = 0; i<arow; i++){
                for(j=0; j<bcolumn; j++){
                    for(k=0; k<brow; k++){
                        sum += a[i][k] * b[k][j];
                    }
                    product[i][j] = sum;
                    sum=0;
                }
            }
        
            printf("Resultant matrix\n");
            for(i=0; i<arow; i++){
                for(j=0; j<bcolumn; j++){
                    printf("%d ", product[i][j]);
                }
                printf("\n");
            }
        
            return 0;
        }
        ```
        
- Constant Arrays in C
    
    
    Either one dimensional or multi-dimensional arrays can be made constant by starting the declaration with the keyword const.
    
    For example:
    
    const int a[10] = {1, 2,3,4, 5, 6, 7, 8, 9, 10};
    
    a[1] = 45; → ERROR! 
    
    error: cannot assign to variable 'a' with const-qualified type 'const int[10]’
    
    Advantages of constant array 
    
    - It assures us that the program will not modify the array which may contain some valuable information.
    - It also helps the compiler to catch errors by informing that there is no intention to modify this array.

### Pointers in C

- Pointer is a special variable that is capable of storing some address.
- 포인터에 주소를 할당해준다고 생각하면 쉽다
- It points to a memory location where the first byte is stored.
- declaring and initializing pointers in C
    
    **declaring**
    
    `data_type *pointer_name`
    
    Here data type refers to the type of the value that the pointer will point to. ex) int *ptr,  float *ptr
    
    **initializing**
    
    - simply declaring a pointer is not enough.
    - It is important to initialize pointer before use.
    - One way to initialize a pointer is to assign address of some variable.
    
    ```c
    int x = 5;
    int *ptr;
    ptr = &x;
    
    //SAME
    int x = 5, *ptr = &x;
    ```
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2067.png)
    
- passing by reference
    
    ```c
    void change_value(int *nb);
    
    int main(){
        int nb;
        nb = 47;
        change_value(&nb);
        printf("%d\n", nb);
    }
    
    void change_value(int *nb){
         *nb = 122;
    }
    ```
    
    ```c
    void swap(int *n, int *n1){
        int tmp;
        tmp = *n;
        *n = *n1;
        *n1 = tmp;
    }
    
    int main(){
        int a, b;
    
        a = 42;
        b = 1337;
        printf("a->%d\tb->%d\n", a, b);
        swap(&a, &b);
        printf("a->%d\tb->%d\n", a, b);
    }
    ```
    
- pass by value vs. pass by reference
    - **Pass by Value**
        - Easy to understand
            - You just pass copies
        - Safe
            - original data won’t be modified by the called function
        - Perfomance overhead
            - A big object like a struct to be copied it’s really bad performance-wise.
            - Time consuming and memory intensive.
        - Short reach (Lack of direct access)
            - Called functions can only modify local copies (this can be a + but also a -)
            
        
    - **Pass by Reference**
        - Efficiency
            - YOU just pass an address, it can point to a gigantic structure, not a problem.
        - Direct access
            - I can modify data outside the called function. This trick allows me to kinda “return multiple values”
        - Side effects
            - I can write impossible to read code given that pointer can change values in other locations. “With great power comes great responsibility”
        - Complexity
            - Taming pointers can be indeed complex, especially multilevel pointers (i.e.******ptr)
            
- value of operator
    
    value of operator/indirection operator/deference operator is an operator that is used to access the value stroed at location pointer by the pointer.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2068.png)
    
    We can also change the value of the object pointed by the pointer.
    
    ```c
    int x = 10;
    int *ptr = &x;
    
    *ptr = 4;
    
    printf("%d", *ptr);
    ```
    
    - A word of caution
        - Never apply the indirection operator to the uninitialized pointer.
            
            ex) int *ptr;
            
            printf(”%d”, *ptr);
            
            output: Undefined behavior
            
        - Assigning value to an uninitialized pointer is dangerous.
            
                  int *ptr;
            
            *ptr = 1;
            
             output: Segmentation Fault (SIGSEGV)
            
            usually, segmentation fault is caused by program trying to read or write an illegal memory location.
            
- pointer assignment
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2069.png)
    
    **pointer applications**
    
    ```c
    #include <stdio.h>
    
    void minMax(int arr[], int len, int *min, int *max){
        *min = *max = arr[0];
        int i;
        for(i = 1; i<len; i++){
            if(arr[i] > *max){
                *max = arr[i];
            }
            if(arr[i] < *min){
                *min = arr[i];
            }
        }
    }
    
    int main(){
        int a[] = {23, 4, 21, 98, 987, 45, 32, 10, 123, 986, 50, 3, 4, 5};
        int min, max;
        int len = sizeof(a)/sizeof(a[0]);
        minMax(a, len, &min, &max);
        printf("MIN: %d MAX: %d", min, max);
        return 0;
    }
    ```
    
- Returning Pointers
    
    ```c
    #include <stdio.h>
    
    int *findMid(int a[], int n){
        return &a[n/2];
    }
    
    int main(){
        int a[] = {1, 2, 3, 4, 5};
        int n = sizeof(a)/sizeof(a[0]);
        int *mid = findMid(a, n);
        printf("%d", *mid);
        return 0;
    }
    //3
    ```
    
    - a word of caution
        - Never ever try to return the address if an automatic variable.
            
            if a function returns the address of the local variable the function will disappear.
            
            ```c
            int *unsafe(void) { 
              int variable; 
              // ... 
              return &variable; 
            }
            ```
            
            Object lifetime is the punchline. Make sure you don’t dereference pointers to objects after their lifetime has ended. That’s what actually matters.
            
            ```c
            int get_int() { 
              int i = 0; 
              if (scanf("%d", &i) == 1) { 
                return i; 
              } else { 
                return -1; 
              } 
            }
            ```
            
            This passes a pointer to a local variable to `scanf` with no issues. It’s fine, because `scanf` returns before `get_int` returns.
            
    
- Pointers(important questions)
    
    consider the following two statements 
    
    ```c
    int *p = &i;
    p = &i;
    ```
    
    First statement is the declaration and second is simple assignment statement. Why isn’t in second statement, p is preceded by * symbol?
    
    - solution
        
        In C, * symbol has different meaning depending on the context in which it’s used. At the time of declaration, * symbol is not acting as an indirection operator. * symbol in the first statement tells the compiler that p is a pointer to an integer. But, if we write `*p=&i` after declaration, then it’s wrong, because here *symbol indicates the indirection operator and we cannot assign the address to some integer variable.
        
        Therefore, in the second statement, there is no need of * symbol in front of p. It simply means we are assigning the address to a pointer.
        
    
- Pointer Arithmetic
    
    **Addition**
    
    addition in pointer means moving the pointer n positions in forward direction.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2070.png)
    
    if p points to a[0], then p = p + 3 == &a[0+3] == &a[3]
    
    - what happens behind the scene
        
        p 포인터가 array a의 시작 부분을 가르키는 순간  memory location의 base memory 주소를 가질 것이다. p = p + 1을 한다면 메모리 한 칸만큼 앞으로 옮기는 것이므로 int 타입의 사이즈인 4byte 만큼 실제 memory location을 옮기는 것이다.
        
    
    **Subtraction**
    
    subtraction in pointer means moving the pointer n positions in backward direction
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2071.png)
    
    if p points to a[3], then p = p - 3 == &a[3-3] == &a[0]
    
    - a word of caution
        
        performing arithmetic on pointers which are not pointing to array element leads to undefined behavior.
        
        ```c
        #include <stdio.h>
        
        int main(){
            int i = 0;
            int *p = &i;
            printf("%d", *(p+3));
            return 0;
        }
        //32759
        ```
        
        If two pointers are pointing to different arrays then performing subtraction between them leads to undefined behavior.
        
        ```c
        int main() {
        		int a[] = {1, 2, 3, 4};
        		int b[] = {10, 20, 30, 40};
        		int *p = &a[0];
        		int *q = &b[3];
        		printf("%d", q - p);
        		return 0;
        }
        ```
        
    
    **Increment and Decrement**
    
    post increment
    
    ```c
    #include <stdio.h>
    
    int main(){
        int a[] = {5, 16, 7, 89, 45, 32, 23, 10};
        int *p = &a[0];
        printf("%d ", *(p++)); //5
        printf("%d", *p); //16
        return 0;
    }
    ```
    
    pre increment
    
    ```c
    int main(){
        int a[] = {5, 16, 7, 89, 45, 32, 23, 10};
        int *p = &a[0];
        printf("%d ", *(++p)); //16
        return 0;
    }
    ```
    
    post&pre decrement
    
    ```c
    #include <stdio.h>
    
    int main(){
        int a[] = {5, 16, 7, 89, 45, 32, 23, 10};
        int *p = &a[2];
        printf("%d ", *(--p));//16
        printf("%d ", *(p--));//16
        printf("%d", *p);//5
        return 0;
    }
    ```
    
- comparing pointers
    - use relational operators(<, >, ≤, ≥) and equality operators (==, !=) to compare pointers.
    - only possible when both pointers point to some array.
    - output depends on the relative positions of both the pointers.
    
    ```c
    #include <stdio.h>
    
    int main(){
        int a[] = {1, 2, 3,4 ,5, 6};
        int *p = &a[3];
        int *q = &a[5];
        printf("%d\n", p<=q);
        printf("%d\n", p>=q);
        q = &a[3];
        printf("%d", p==q);
        return 0;
    }
    ```
    
- sum of array elements using pointers
    
    ```c
    #include <stdio.h>
    
    int main(){
        int a[] = {11, 22, 36, 5, 2};
        int sum=0, *p;
    
        for(p = &a[0]; p <= &a[4]; p++){
            sum += *p;
        }
    
        printf("Sum is %d", sum);
    }
    
    //THE SAME functionality
    //you can see why in the next toggle
    
    #include <stdio.h>
    
    int main(){
        int a[] = {11, 22, 36, 5, 2};
        int sum=0, *p;
    
        for(p = a; p <= a + 4; p++){
            sum += *p;
        }
    
        printf("Sum is %d", sum);
    }
    ```
    
- using array name as pointer
    
    FACT: name of an array can be used as a pointer to the first element of an array.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2072.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2073.png)
    
    now it is clear that
    
    `*(a + i) = a[i];`
    
    a word of caution:
    
    although  we can call the name of an array as a pointer to the first element of the existing array, it is not possible to assign a new address to it. For example,
    
    ```c
    int main() {
    		int a[] = {11, 22, 36, 5, 2};
    	
    		printf("%p", a++);
    		return 0;
    }
    ```
    
    a++ actually means a = a + 1.
    
    this means we want to assign the address of the next integer value in array which is impossible.
    
- Reverse a Series of Numbers using Pointers
    
    ```c
    #include <stdio.h>
    
    #define N 5
    
    int main(){
        int a[N], *p;
        printf("Enter %d elements in the array: ", N);
        for(p=a;p < a + N; p++){
            scanf("%d", p);
        }
        printf("Elements in reverse order:\n");
        for(p = a+N-1; p >= a; p--){
            printf("%d ", *p);
        }
        return 0;
    }
    ```
    
- Passing Array as an Argument to a Function
    
    an array names is always treated as a pointer.
    
    ```c
    #include <stdio.h>
    // add(int b[], int len) -> same thing
    //just know that b[] here is just a pointer
    int add(int* b, int len){ 
        int sum = 0, i;
        for(i=0; i<len; i++){
            sum += b[i];
        }
        return sum;
    }
    
    int main(){
        int a[] = {1, 2, 3, 4};
        int len = sizeof(a)/sizeof(a[0]);
    		//here by passing the name of an array,
    		//we are passing the base address of the array
        printf("%d", add(a, len));
        return 0
    }
    ```
    
    **int b[] == int* b
    
    C specifies that when processing the types of the arguments for functions, arrays are converted into pointers to the contained type.
    
- using pointers to print 2D arrays
    
    we already know that internally, the computer will store the n-dimensional array in a sequential manner only.
    
    **difference between row major and column major order**
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2074.png)
    
    **FACT: C stores multidimensional arrays in row major order!**
    
    to print the two dimensional array, we would traditionally do,
    
    ```c
    for(i = 0; i<row; i++){
    	for(j = 0; j<column; j++){
    			printf("%d ",a[i][j]);
    	}
    }
    ```
    
    we do the nested for loops to print our the elements of the multi-dimensional array. Using pointers, however, we can write the logic in one line. this is a printing method using the data structure.
    
    ```c
    for(p = &a[0][0]; p <= &a[row-1][col-1]; p++){
    		printf("%d ", *p);
    }
    ```
    
- Processing the multidimensional array elements (or) address Arithmetic of multidimensional arrays
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2075.png)
    
    1D array → a means the pointer to the first element of the array
    
    2D array → a means the pointer to the first 1D array
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2076.png)
    
    In 2D array,
    
    a + 1 ⇒ 1008(pointer to 2nd 1D array)
    
    *a ⇒ pointer to the first element of first 1D array ⇒ &a[0][0] here) 1000
    
    **a ⇒  *(*a) ⇒ the actual value of the first element of first 1D array here) 1
    
    *(a+1)+1 ⇒ pointer to the second element of the second 1D array here) 1012
    
    In 3D array,
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2077.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2078.png)
    
    a = pointer to 1st 2D array = 1000
    
    a+1 = pointer to 2nd 2D array = 1016
    
    *(a+1) = pointer to 1st 1D array of 2nd 2D array
    
    *(*(a+1)) = pointer to 1st element of 1st 1D array of 2nd 2D array
    
    **(*(a+1))) = 5 = a[1][0][0]
    
    Q. I want to access 2nd element of the below array
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2079.png)
    
    *(**a + 1)
    
- Pointer Pointing to an Entire Array
    
    ```c
    int main() {
    		int a[5] = {1, 2, 3, 4, 5};
    		int (*p)[5] = &a;
    		pritnf("%d", *p);
    		return 0;
    }
    ```
    
    *p → pointer to the whole array of 5 elements
    
    ***(asterisk) moves us one step inside, &moves us one step outside**
    
    here, if you put *(asterisk) in front of a, it gives the address of the whole one dimensional array which has 5 elements.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2080.png)
    
    *p here is a pointer to the whole one dimensional array. to have the whole address of the entire one dimensional array, you need to assign it as above. (*p)[5]!!!*
    
    p → address of the entire array
    
    *p → address of the first element
    
    **p → value of the first element
    

### Strings in C

```c
int main(){
    char* ptr = "String";
    printf("%s\n", ptr); //String
    printf("%c\n", *ptr); //S
    printf("%s\n", ptr+1); //tring
    printf("%c\n", ptr[0]); //S
    return 0;
}
```

- String Literals
    
    String Literal(or String Constant) is a sqeuence of characters enclosed within double quotes.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2081.png)
    
    when printing string literals, it won’t allow the user to tab enter in the middle.
    
    There are two ways to prevent this.
    
    1. using \ → gives extra indentation.
    2. using multiple double quotes → no indentation
    
    ```jsx
    int main(){
        printf("%s", "I am just writing something \ I am just writing something2");
        printf("\n");
        printf("%s", "I am just writing something "
                     "I am just writing something2");
    }
    ```
    
- Storing the String Literals
    
    printf(”hello”); 
    
    Whatever go inside the printf and scanf functions are String Literals.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2082.png)
    
    In C, Compiler treats a string literal as a **pointer to the first character.**
    
    So to the printf and scanf, we are passing a pointer to the first character of a string literal.
    
    printf(”Earth”); 
    
    Passing ‘Earth” is equivalent to passing the pointer to letter ‘E’
    
- Performing Operations on String Literals
    - Assigning String Literal to a Pointer
        
        `char *ptr = “Hello World!”`
        
        - writing string literal is equivalent to writing the pointer to the first character of the string literal.
        - ptr contains the address of the first character of the string literal.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2083.png)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2084.png)
        
    
- String Literal v. Character Constant
    
    “H” ≠ ‘H’
    
    “H” is represented by a pointer to a character ‘H’ 
    
    ‘H’ is represented by an integer(ASCII Code: 72)
    
    - printf expects a pointer to a character not the integer. That is why
        
        printf(”\n”); doesn’t matter at all while printf(’\n’); matters. 
        
- Declaring and Initializing a String Variables
    
    A string variable is a one dimensional array of characters that is capable of holding a string at a time.
    
    ex) char s[6]
    
    - Always make the array one character longer than the string. If length of the string is 5 characters long then don’t forget to make extra room for Null character.
    - Failing to do so may cause unpredictable results when program is executed as some C libraries assume the strings are Null terminated.
    - initializing a string variable
        
        ```c
        int main(){
            //initializing a string variable
            char s[6] = "Hello";
        }
        ```
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2085.png)
        
        Although, it seems like “Hello” in the above example is a string literal but it is not.
        
        When a string is assigned to a character array, then this character array is treated like other types of arrays. We can modify its characters.
        
        - recall that we cannot modify a string literal
        - but we can modify a char array.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2086.png)
        
        **short length initializer**
        
        ```c
        char s[7] = "Hello";
        ```
        
        what is does is that the 7 spaces are secured and the 6th and 7th space will be filled with null characters(\0).
        
        **long length initializer**
        
        ```c
        char s[4] = "Hello"
        printf("%s", s);
        //OUTPUT: hell�|��
        ```
        
        rest of part, here o, will be truncated.
        
        **equal length initializer**
        
        ```c
        #include <stdio.h>
        
        int main(){
            char s[5] = "hello";
            char c[5];
        
            for(int i = 0; i<5; i++){
                c[i] = s[i];
            }
        
            printf("%s", c);
        }
        //OUTPUT: hellohello
        ```
        
        considering the output, this is definitely unpredicted situation. We would normally expect the output of just hello. To prevent this, we need to take the following strategy instead.
        
        ```c
        #include <stdio.h>
        
        int main(){
            char s[6] = "hello";
            char c[6];
        
            int i;
            for(i = 0; i<5; i++){
                c[i] = s[i];
            }
            c[i] = '\0';
            
            printf("%s", c);
        }
        //OUTPUT: hello
        ```
        
        first, since we need the room for the null character, we initialize array ‘s length as 6. and after the value allocation is done, since the value of the variable i is automatically 5, we can allocate the null character at the end of the array to prevent an unexpected outcome.
        
        **Omitting the length**
        
        ```c
        char s[] = "Hello";
        ```
        
        Automatically, the compiler sets aside 6 characters for s which is enough to store the string “Hello” with null character.
        
- writing Strings using printf and puts Functions
    
    ```c
    #include <stdio.h>
    
    int main(){
        char *ptr = "Hello World";
        printf("%s", ptr); //Hello World
        printf("%.5s", ptr);//Hello
        printf("%6.5s", ptr);// Hello
        return 0;
    }
    ```
    
    - “%m.ns” is used to printf just a part of the string where n is the number of characters to be displayed and m denotes the size of the field within which the string will be displayed.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2087.png)
        
    
    **using puts**
    
    puts()  function is a function declared in <stdio.h> library and is used to write strings to the output screen.
    
    Also, puts() function automatically writes a newline character after writing the string to the output screen.
    
    ** char argument in puts() function won’t work.
    
    ```c
    int main(){
        char *s = "Hello";
        puts(s);
        puts(s);
        /**
         Hello
         Hello
         */
    }
    ```
    
- Reading Strings using scanf and gets Functions
    
    ```c
    #include <stdio.h>
    
    int main(){
        char a[10];
        printf("Enter the string:\n");
        scanf("%s", a);
        printf("%s", a);
    }
    ```
    
    - Like any array name, a is treated as a pointer to the fist element of the array. Therefore, there is no need to put & in front of a.
    - scanf() doesn’t store the white space characters in the string variable. It only reads characters other than white spaces and store them in the specified character array until it encounters a white-space character.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2088.png)
        
    
    **reading string using gets() function**
    
    In order to read an entire line of input, gets() function can be used.
    
    ```c
    char a[10];
    printf("Enter the string:\n");
    gets(a);
    printf("%s", a);
    
    //but when our input exceed the limit length, the program may crash
    ```
    
    - Both gets() and scanf() functions have no way to detect when the character array is full. Both never checks the mazimum limit of input characters. Hence, they may cause undefined behavior and probably lead to buffer overflow error which eventually causes the program to crash.
    
    scanf has the way to set the limit for the number of characters to bestored in the character array. By using %ns, where n indicates the number of characters allowed to store in the character array.
    
    ```c
    char a[10];
    printf("Enter the string:\n");
    scanf("%9s", a);
    printf("%s", a); 
    /*
    Input: Youaremostwelcome
    Output: Youaremos
    */
    ```
    
    However, gets() is still unsafe. It will try to write the characters beyond the memory allocated to the character array which is unsafe because it will simply overwrite the memory beyond the memory allocated to the character array. Therefore, it is not safe to use gets() in any case.
    
- Designing The Input Function using getchar()
    
    as scanf and gets functions are risky to use, it is advisable to design our own input function.
    
    say we want our input function to have following functionalities.
    
    1. It must continue to read the string even after seeing white space characters
    2. It must stop reading the string after seeing the newline character
    3. it must discard extra characters
    4. it must return the number of characters it stores in the character array
    
    getchar() function is used to read one character at a time from the user input. It returns an integer equivalent to the ASCII code of the character.
    
    ```c
    #include <stdio.h>
    
    int input(char str[], int n){
        int ch, i=0;
        while((ch = getchar()) != '\n'){
            if(i < n){
                str[i++] = ch;
            }
        }
        str[i] = '\0';
        return i;
    }
    
    int main(){
        char str[100];
        int n = input(str, 5);
        printf("%d %s", n, str);
        return 0;
    }
    ```
    
- putchar()
    
    `putchar()` accepts an integer argument(which represents a character it wants to display) and returns an integer representing the character written on the screen.
    
    prototype: int putchar(int ch)
    
    ```c
    #include <stdio.h>
    
    int main(){
        int ch;
        for(ch = 'A'; ch<='Z'; ch++){
            putchar(ch);
        }
        return 0;
    }
    ```
    
    - putchar(80); //P
    - putchar(’P’); //P
    
- strcpy()
    
    `#inlcude <string.h>` → contains all the required functions for performing string operations.
    
    prototype: char* strcpy(char* destination, const char* source)
    
    - strcpy is used to copy a string pointer by source (including NULL character) to the destination (character array)
    - strcpy returns the pointer to the first character of the string which is copied in the destination. Hence if we use %s, then whole string will be printed on the screen.
    
    ```c
    #include <stdio.h>
    #include <string.h>
    
    int main(){
        char str1[10] = "Hello";
        char str2[10];
    
        printf("%s\n", strcpy(str2, str1));
        printf("%s", str2);
        return 0;
    }
    /*
    Hello
    Hello
    */
    ```
    
    - a word of caution
        
        in the call to strcpt(str1, str2), there is no way the strcpy will check whether the string pointed by str2 will fit in str1. If the length of the string pointed by str2 is greater than the length of the character array str1 then it will be an undefined behavior.
        
        to avoid this, use strncpy()
        
    
- strncpy()
    
    strncpy(destination, source, sizeof(destination));
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2089.png)
    
    strincpy will leave the string in str2(destination) without a terminating NULL character, If the size of str1(source) is equal to or greater than the size of str2(destination).
    
    ```c
    #inlcude <stdio.h>
    #include <string.h>
    
    int main(){
    		char str1[6] = "Hello";
    		char str2[6];
    		strncpy(str2, str1, sizeof(str2));
    		str2[sizeof(str2) - 1] = '\0';
    		printf("%s", str2);
    		return 0; 
    }
    ```
    
    then we should add the null terminating character at the end of the char arr.
    
- strlen()
    
    strlen() function is used to determine the length of the given string.
    
    `size_t strlen(const char* str);`
    
    - it doesn’t count Null character.
        
        ```c
        #include <stdio.h>
        #include <string.h>
        
        int main(){
            char *str = "Hello World";
            printf("%d", strlen(str)); //11
            r
        ```
        
    - it calculates the length of the string, not the length of the array.
        
        → even if we did 
        
        str[100] = “Hello world”
        
        pritnf(”%d”, strlen(str));
        
        it will print 11.
        
- strcat()
    
    strcat() function appends the content of string str2 at the end of the string str1.
    
    - it is important to note that str2 is getting added to str1. This is going to change the content of the str1.
    
    prototype: char* strcat(char* str1, const char* str2);
    
    ```c
    #include <stdio.h>
    #include <string.h>
    
    int main(){
        char str1[100], str2[100];
        strcpy(str1, "Welcome to ");
        strcpy(str2, "my house." );
        strcat(str1, str2);
        printf("%s", str1); //Welcome to my house.
        return 0;
    }
    ```
    
    - an undefined behavior can be observed if size of str1 isn’t long enough to accommodate the additional characters of str2.
    - to avoid this, use strncat()
    
- strncat()
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2090.png)
    
- strcmp()
    
    prototype: int strcmp(const char* s1, const char* s2);
    
    - compares two strings s1 ans s2
    - returns value
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2091.png)
        
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2092.png)
    
    when s1<s2
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2093.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2094.png)
    
- Array of Strings
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2095.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2096.png)
    
    reference: [w3w school](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e.md)
    

### Function Pointers

- function pointer basics
    
    Function pointers are like normal pointers but they have the a capability to point to a function.
    
    ```c
    int fun(int a, int b){
    		return a+b;
    }
    ```
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2097.png)
    
    take the following example.
    
    HOW to declare a pointer to an array?
    
    ```c
    int main() {
    		int *ptr[10];
    		return 0;
    }
    ```
    
    To avoid this, we have to put the parenthesis around the *ptr.
    
    now ptr is a pointer pointing to an array of 10 integers.
    
    *ptr[10] does NOT the way of declaring a pointer to an array.
    
    Since [] operator is in precedence to * operator, meaning it’s stronger, the *ptr[10] will be an ARRAY that contains 10 pointers pointing to integers. 
    
    ```c
    int main(){
    		int (*ptr)[10];
    		return 0;
    }
    ```
    
    now the question is, HOW to declare a pointer to a function?
    
    ```c
    int add(int a, int b)
    {
    		return a + b;
    }
    ```
    
    **prototype**
    
    ```c
    int main()
    {
    		int (*ptr)(int, int);
    }
    ```
    
    **assigning the address of a function to a function pointer.**
    
    ```c
    int main()
    {
    		int (*ptr)(int, int) = &add; //add is a function identifier
    }
    ```
    
    **using the function pointer**
    
    ```c
    int main()
    {
    		int result;
    		int (*ptr)(int, int) = &add;
    		result = *ptr(10, 20);
    		printf("%d", result);
    }
    ```
    
    OR
    
    ```c
    int main()
    {
    		int result;
    		int (*ptr)(int, int) = add;
    		result = *ptr(10, 20);
    		printf("%d", result);
    }
    ```
    
    You basically don’t have to put the & in front of the function identifier since the function identifier naturally means address of the function/the initial address of the function.
    
- applications
    
    there are some situations in which user has to decide which function has to be called at a particular point in time.
    
    Let’s sat, we want to design a calculator which has the capability to perform addition, subtraction, multiplication and division.
    
    Here, the user will decide which operation he/she wats to perform.
    
    Suppose, we have decided to create separate functions for these operations.
    
    Now we want user to decide which function has to be called at runtime.
    
    1. first way is to use if-switch cases
    2. another way is to use function pointers.
    
    ```c
    #include <stdio.h>
    # define ops 4
    
    float sum(float a, float b) {return (a+b);}
    float sub(float a, float b) {return (a-b);}
    float mult(float a, float b) {return (a*b);}
    float divi(float a, float b) {return (a/b);}
    
    int main() {
        float (*ptr2func[ops]) (float, float) = {sum, sub, mult, divi};
        int choice;
        float a, b;
        printf("Enter your choice: 0 for sum, 1 for sub, 2 for mult, 3 for divi.");
        scanf("%d", &choice);
        printf("Enter the two numbers:\n");
        scanf("%f %f", &a, &b);
        printf("%f", ptr2func[choice](a, b));
        return 0;
    }
    ```
    

### Structures

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2098.png)

A structure is a user defined data type that can be used to group elements of different types into a single type.

```c
struct {
		char *engine;
		char *fuel_type;
		int fuel_tank_cap;
		int seating_cap;
		float city_mileage;
} car1, car2;
```

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%2099.png)

- Structure Types (Using Structure tag)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20100.png)
    
    ```c
    #include <stdio.h>
    
    struct employee{
        char *name;
        int age;
        int salary;
    };
    
    int manager() {
        struct employee manager;
    
        manager.age = 27;
    
        if(manager.age > 30) {manager.salary = 65000;}
        else{manager.salary = 55000;}
        return manager.salary;
    }
    
    int main(){
        struct employee emp1;
        struct employee emp2;
    
        printf("Enter the salary of employee1: ");
        scanf("%d", &emp1.salary);
        printf("Enter the salary of employee2: ");
        scanf("%d", &emp2.salary);
        printf("Employee 1 salary is: %d\n", emp1.salary);
        printf("Employee 2 salary is: %d\n", emp2.salary);
        printf("Manager's salary is %d", manager());
        return 0;
    }
    ```
    
- Structure Types (Using typedef)
    
    Syntax: `typedef existing_data_type new_data_type`
    
    typedef gives freedom to the suer by allowing them to create their own types.
    
    ex) 
    
    ```c
    typedef int INTEGER;
    
    int main() {
    		INTEGER var = 100;
    		printf("%d", var);
    		return 0;
    }
    ```
    
    use of typedef in structures
    
    ```c
    typedef struct car {
    		char engine[50];
    		char fuel_type[10];
    		int fuel_tank_cap;
    		int seating_cap;
    		float city_mileage;
    }car; //car becomes a new data type
    
    int main() {
    		car c1;
    }
    ```
    
- Initializing and Accessing the Structure Members
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20101.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20102.png)
    
    - Designated Initialization
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20103.png)
        
        OUTPUT: 10 20 30
        
- Declaring an Array of Structure
    
    Instead of declaring multiple variable, we can also declare an array of structure in which each element of the array will represent a structure variable.
    
    ```c
    #include <stdio.h>
    
    struct car {
        int fuel_tank_cap;
        int seating_cap;
        float city_mileage;
    };
    
    int main() {
        struct car c[2];
        int i;
        for(i=0; i<2; i++){
            printf("Enter the car %d fuel tank capacity: ", i+1);
            scanf("%d", &c[i].fuel_tank_cap);
            printf("Enter the car %d fuel seat capacity: ", i+1);
            scanf("%d", &c[i].seating_cap);
            printf("Enter the car %d fuel city mileage: ", i+1);
            scanf("%f", &c[i].city_mileage);
        }
        printf("\n");
        for(i=0; i<2; i++){
            printf("\nCar %d details: \n", i+1);
            printf("fuel tank capacity: %d\n", c[i].fuel_tank_cap);
            printf("fuel seat capacity: %d\n", c[i].seating_cap);
            printf("fuel city mileage: %f\n", c[i].city_mileage);
        }
    }
    ```
    
- Accessing members of structure using structure pointer
    
    
    - pointer below is a pointer to some variable of type struct abc.
    
    ```c
    struct abs {
    		int x;
    		int y;
    }
    
    int main() {
    		struct abc a = {0, 1};
    		struct abc *ptr = &a;
    		printf("%d %d", ptr -> x, ptr -> y); //0 1
    		return 0;
    }
    ```
    
    - ptr → x is equivalent to (*ptr).x
    
- structure padding in C
    
    Processor doesn’t read 1 byte at a time from memory.
    
    **It reads 1 word at a time.**
    
    ex) If we have a 32 bit processor then it means it can access 4 bytes at a time which means word size is 4 bytes.
    
    ex) If we have a 64 bit processor then it means it can access 8 bytes at a time which means word size is 4 bytes.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20104.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20105.png)
    
    This is an unnecessary usage of CPU cycles.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20106.png)
    
    once you do this, even though the memory is wasted, variable c can be accessed at one CPU cycle.
    
    The sequence of the member variables of the struct affects the size of the struct.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20107.png)
    
    - try to imagine the memory allocation of the code above.
    
- structure packing
    
    because of structure padding, size of the structure becomes more than the size of the actual structure. Due to this some memory will get wasted.
    
    **Structure packing**
    
    - we can avoid the wastage of memory by simply writing #pragma pack(1)
    - #pragma is a special purpose directive used to turn on or off certain features
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20108.png)
    
    - we have to remember that if we use pragma, the memory will not get wasted, but the CPU cycle will be wasted.
- Calculating the Area of Rectangle using Structures
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20109.png)
    
    ```c
    #include <stdio.h>
    
    struct point {
        int x;
        int y;
    };
    
    struct rectangle {
            struct point upper_left;
            struct point lower_right;
    };
    
    int area(struct rectangle r) {
        int length, breath;
        length = r.lower_right.x - r.upper_left.x;
        breath = r.upper_left.y - r.lower_right.y;
    
        return length*breath;
    }
    
    int main() {
        struct rectangle r;
        printf("Enter the upper left coordinates of the rectangle: \n");
        scanf("%d %d", &r.upper_left.x, &r.upper_left.y);
        printf("Enter the lower right coordinates of the rectangle: \n");
        scanf("%d %d", &r.lower_right.x, &r.lower_right.y);
        printf("Area of the rectangle: %d", area(r));
        return 0;
    }
    ```
    
- array vs structures
    
    int case of passing an array of structures
    
    ```c
    #include <stdio.h>
    
    struct point {
        int x;
        int y;
    };
    
    void edit(struct point arr[]) {
        for(int i=0; i<2; i++){
            arr[i].x++;
            arr[i].y++;
        }
    }
    
    int main() {
        struct point point1 = {1, 2};
        struct point point2 = {2, 3};
        struct point arr[2] = {point1, point2};
        edit(arr);
    
        for(int i=0; i<2; i++){
            printf("%d %d\n", arr[i].x, arr[i].y);
        }
        return 0;
    }
    
    /*
    2 3
    3 4
    */
    ```
    
    in case of passing structure
    
    ```c
    #include <stdio.h>
    
    struct point {
        int x;
        int y;
    };
    
    void edit(struct point pt) {
        pt.x++;
        pt.y++;
    }
    
    int main() {
        struct point point1 = {1, 2};
        struct point point2 = {2, 3};
        edit(point1);
        edit(point2);
    
        printf("%d %d\n", point1.x, point1.y);
        printf("%d %d\n", point2.x, point2.y);
    
        return 0;
    }
    /*
    1 2
    2 3
    */
    ```
    
- pointers & structures … LinkedList
    - adding in the middle
        
        ```c
        //
        //  main.c
        //  CPlayground
        //
        //  Created by Jewook Park on 12/26/23.
        //
        
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node {
            int value;
            struct node *link;
        };
        
        //function declarations
        struct node* add_at_end(struct node *ptr, int value);
        void add_at_pos(struct node* head, int value, int pos);
        
        struct node* add_at_end(struct node *ptr, int value){
            struct node* temp = malloc(sizeof(struct node));
            temp -> value = value;
            temp -> link = NULL;
            
            ptr->link = temp;
            return temp;
        }
        
        void add_at_pos(struct node* head, int value, int pos){
            struct node* ptr2 = malloc(sizeof(struct node));
            struct node *ptr = head;
            ptr2 -> value = value;
            ptr2 -> link = NULL;
            
            pos--;
            while(pos != 1){
                ptr = ptr-> link;
                pos--;
            }
            
            ptr2->link = ptr->link;
            ptr->link = ptr2;
        }
        
        int main(int argc, char*argv[]) {
            struct node *head = malloc(sizeof(struct node));
            head -> value = 20;
            head -> link = NULL;
            
            struct node *ptr = head;
            ptr = add_at_end(ptr, 30);
            ptr = add_at_end(ptr, 40);
            
            add_at_pos(head, 59, 3);
            add_at_pos(head, 61, 4);
            
            ptr = head;
            while(ptr != NULL){
                printf("%d ", ptr->value);
                ptr = ptr -> link;
            }
            
            return 0;
        }
        ```
        
    - deleting the last
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
          int data;
          struct node *link;
        };
        
        void del_last(struct node *head){
          if(head == NULL){
            printf("List is empty");
          }else if(head->link == NULL){
            free(head);
            head = NULL;
          }else{
            struct node *temp = head;
            while(temp -> link -> link != NULL){
              temp = temp -> link;
            }
            free(temp -> link);
            temp -> link = NULL;
          }
        }
        
        struct node *add_end(struct node *head, int data){
          struct node *temp = malloc(sizeof(struct node));
          temp -> data = data;
          temp -> link = NULL;
        
          head -> link = temp;
          return temp;
        }
        
        int main(void) {
          struct node *head = malloc(sizeof(struct node));
          head -> data = 45;
          head -> link = NULL;
          struct node *first = head;
          
          head = add_end(head, 98);
          head = add_end(head, 72);
          head = add_end(head, 35);
        
          del_last(first);
        
          struct node *temp = first;
          while(temp != NULL){
            printf("%d ", temp -> data);
            temp = temp -> link;
          }
          return 0;
        }
        ```
        
    - deleting the first
        
        TC: O(1)
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
          int data;
          struct node *link;
        };
        
        struct node* del_first(struct node *head){
          if(head == NULL){
            printf("List is empty");
          }else if(head -> link == NULL){
            free(head);
            head = NULL;
          } else {
            struct node *temp = head;
            head = head -> link;
            free(temp);
            temp = NULL;
          }
          return head;
        }
        
        struct node *add_end(struct node *head, int data){
          struct node *temp = malloc(sizeof(struct node));
          temp -> data = data;
          temp -> link = NULL;
        
          head -> link = temp;
          return temp;
        }
        
        int main(void) {
          struct node *head = malloc(sizeof(struct node));
          head -> data = 45;
          head -> link = NULL;
          struct node *first = head;
          
          head = add_end(head, 98);
          head = add_end(head, 72);
          head = add_end(head, 35);
        
          first = del_first(first);
        
          struct node *temp = first;
          while(temp != NULL){
            printf("%d ", temp -> data);
            temp = temp -> link;
          }
          return 0;
        }
        ```
        

### Unions

- Union basics
    
    Union is a user defined data type but unlike structure, union members share the same memory location.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20110.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20111.png)
    
    In union, members share the same memory location. If we make changes in one member then it will be reflected to other member as well.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20112.png)
    
    - size of the union is taken according to the size of the largest member of the union.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20113.png)
    
    - we can access members of union through pointers by using the arrow(→) operator.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20114.png)
    
- Applications of Unions
    - part 1
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20115.png)
        
        we can see that the price is a common property between Books and Shirts.
        
        if we were to attain this with struct,
        
        1. Books do not possess the properties of color, size, design
        2. Shirts do not possess the properties of title, author, num_pages
        
        Therefore, i’s a waste of memory. 
        
        the blow happens.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20116.png)
        
        we can save lots of space using unions
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20117.png)
        
        ```c
        #include <stdio.h>
        
        struct artGallery{
            union{
                struct artwork{
                    char* media;
                    char* title;
                    char* price;
                } painting1;
        
                struct sculpture{
                    char* material;
                    char* name;
                    char* price;
                } sculpture1;
            };
        };
        
        int main() {
            struct artGallery a;
            a.painting1.media = "water color";
            a.painting1.title = "put everything";
            a.painting1.price = "$2000";
        
            printf("%s\n", a.painting1.title);
            printf("%ld", sizeof(a));
            return 0;
        }
        ```
        
    - part 2
        
        ```c
        typedef union {
        		int a;
        		char b;
        		double c;
        } data;
        
        int main() {
        		data arr[10];
        		arr[0].a = 10;
        		arr[1].b = 'a';
        		arr[2].c = 10.178;
        		//and so on
        		return 0;	
        }
        ```
        
        why not structure
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20118.png)
        

### Enumeration in C

An enumerated type is a user defined type which is used to assign names to integral constants because names are easier to handle in program.

- if we do not assign values to enum names then, automatically compiler will assign values to them starting from 0. → in the example below, False → 1, True → 2

```c
enum Bool {False, True};

int main() {
		enum Bool var;
		var = True;
		printf("%d", var);
		return 0;
}
```

Q. we can also use %define to assign names to integral constants. Then, why do we even need enum?

1. Enums can be declared in the local scope so the num is not visible form outside of the function.
2. Enum names are automatically initialized by the compiler.
- Enum basics
    
    Fact1:
    
    - Two or more names can have same value.
    
    ```c
    int main() {
    		enum point {x=0, y=0, z=0};
    		printf("%d %d %d", x, y, z); // 0 0 0 
    		return 0;
    }
    ```
    
    - we can assign values in any order. All unassigned names will get value as value of previous name+1
    
    ```c
    int main(){
    		enum point {y=2, x=34, t, z=0};
    		printf("%d %d %d %d", x, y, z, t);// 34 2 0 35
    		return 0;
    }
    ```
    
    - only integral values are allowed
    
    ```c
    int main() {
    		enum point {x=34, y=2.5, z=0};
    		printf("%d %d %d", x, y, z);
    		return 0;
    }
    ```
    
    OUTPUT: integer constant expression must have integer type, not 'double'
    enum point {x=34, y=2.5, z=0};
    
    - All enum constant must be unique in their scope.
    
    ```c
    int main(){
    		enum point1 {x=34, y=2, z=0};
    		enum point2 {x=4, p=25, q=1};
    		printf("%d %d %d %d %d", x, y, z, p, q);
    		return 0;
    }
    ```
    
    OUPUT: 
    
    error: redefinition of enumerator 'x'
    enum point2 {x=4, p=25, q=1};
    

### LinkedList v. Array

|  | Linked List | Array |
| --- | --- | --- |
| Deletion in the beginning | O(1) | O(n) |
|  |  |  |
- deleting the Node at a Particular Position
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        int value;
        struct node* link;
    };
    
    struct node* add_at_end(struct node* ptr, int value){
        struct node* tmp = malloc(sizeof(struct node));
        tmp -> value = value;
        tmp -> link = NULL;
    
        ptr -> link = tmp;
        return tmp;
    }
    
    void del_pos(struct node **head, int position){
        struct node *current = *head;
        struct node *previous = *head;
        if(*head == NULL)
            printf("List is already empty");
        else if(position == 1){
            *head = current -> link;
            free(current);
            current = NULL;
        }else {
            while(position != 1){
                previous = current;
                current = current -> link;
                position--;
            }
            previous -> link = current -> link;
            free(current);
            current = NULL;
        }
    }
    
    int main(){
        struct node* head = malloc(sizeof(struct node));
        head -> value = 45;
        head -> link = NULL;
    
        struct node* ptr = head;
        ptr = add_at_end(ptr, 98);
        ptr = add_at_end(ptr, 3);
        del_pos(&head, 1);
        ptr = head;
    
        while(ptr != NULL){
            printf("%d ", ptr -> value);
            ptr = ptr -> link;
        }
    
        return 0;
    }
    ```
    
    [reason why we need to use the double pointer here](https://chanywa.com/343)
    
    if we want to directly mutate something (that is inside the main()) at the helper function, we need the address of that thing. Here, we want to mutate the pointer to the integer value. Then, we need to have the pointer to that pointer(address of that pointer) as a parameter.
    
- deleting the entire Linked List
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        int value;
        struct node* link;
    };
    
    struct node* add_at_end(struct node* ptr, int value){
        struct node* tmp = malloc(sizeof(struct node));
        tmp -> value = value;
        tmp -> link = NULL;
    
        ptr -> link = tmp;
        return tmp;
    }
    struct node* del_list(struct node* head){
        struct node* temp = head;
        while(temp != NULL){
            temp = temp -> link;
            free(head);
            head = temp;
        }
        return head;
    }
    
    int main(){
        struct node* head = malloc(sizeof(struct node));
        head -> value = 45;
        head -> link = NULL;
    
        struct node* ptr = head;
        ptr = add_at_end(ptr, 98);
        ptr = add_at_end(ptr, 3);
        head = del_list(head);
    
        if(head == NULL){
            printf("Linked List has been deleted successfully.");
        }
    
        return 0;
    }
    ```
    
    we need to store the address of the second node somewhere so that we can reach the second node even if the first node is deleted.
    
    key point:
    
    temp = temp → link;
    
    free(head);
    
    head = temp;
    
- reverse a single linked list
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20119.png)
    
    next = head → link;
    
    head → link = prev;
    
    prev = head;
    
    head = next;
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        int value;
        struct node* link;
    };
    
    struct node* add_at_end(struct node* ptr, int value){
        struct node* tmp = malloc(sizeof(struct node));
        tmp -> value = value;
        tmp -> link = NULL;
    
        ptr -> link = tmp;
        return tmp;
    }
    
    struct node* reverse(struct node *head){
        struct node *prev = NULL;
        struct node *next = NULL;
        while(head != NULL){
            next = head -> link;
            head -> link = prev;
            prev = head;
            head = next;
        }
        head = prev;
        return head;
    }
    
    int main(){
        struct node* head = malloc(sizeof(struct node));
        head -> value = 45;
        head -> link = NULL;
    
        struct node* ptr = head;
        ptr = add_at_end(ptr, 98);
        ptr = add_at_end(ptr, 3);
        head = reverse(head);
    
        ptr = head;
        while(ptr != NULL){
            printf("%d ", ptr ->value); 
            ptr = ptr -> link;
        }//3 98 45 
        return 0;
    }
    ```
    

### Sorted Singly Linked List

given a sorted singly linked list, we need to insert a new node at the right position.

- inserting a new element
    
    ```c
    struct node* insert(struct node* head, int data){
    		struct node* temp;
    		struct node*newP = malloc(sizeof(struct node));
    		newP->data = data;
    		newP->link = NULL;
    
    		int key = data;
    		if(head == NULL || key < head-> data){
    				newP->link = head;
    				head = newP;
    		}else{
    				temp = head;
    				while(temp -> link != NULL && temp -> link -> data < key)
    						temp = temp->link
    				newP->link = temp->link;
    				temp->link = newP;
    		}
    		return head; 
    }
    ```
    
    adding the node at first is the edge case
    

### Doubly Linked List

- inserting a node in an empty list
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        struct node* prev;
        int value;
        struct node* next;
    };
    
    struct node* addToEmpty(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        head = temp;
        return head;
    }
    
    int main() {
        struct node* head = NULL;
        head = addToEmpty(head, 45);
        printf("%d", head -> value);
        return 0;
    }
    ```
    
- insertion at the Beginning & insertion at the end
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        struct node* prev;
        int value;
        struct node* next;
    };
    
    struct node* add_at_start(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next =  head;
        head -> prev = temp;
        head = temp;
        return head;
    }
    
    struct node* add_at_end(struct node* head, int data){
        struct node* temp, *tp;
        temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        tp = head;
        while(tp->next != NULL){
            tp = tp->next;
        }
        tp->next = temp;
        temp->prev = tp;
        return head;
    }
    
    struct node* addToEmpty(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        head = temp;
        return head;
    }
    
    int main() {
        struct node* head = NULL;
        struct node* ptr;
        head = addToEmpty(head, 0);
        head = add_at_start(head, 1);
        head = add_at_end(head, 2);
        ptr = head;
        while(ptr != NULL){
            printf("%d ", ptr->value);
            ptr = ptr -> next;
        }
    
        return 0;
    }
    ```
    
- insertion between the nodes (add after pos)
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        struct node* prev;
        int value;
        struct node* next;
    };
    
    struct node* add_at_start(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next =  head;
        head -> prev = temp;
        head = temp;
        return head;
    }
    
    struct node* add_at_end(struct node* head, int data){
        struct node* temp, *tp;
        temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        tp = head;
        while(tp->next != NULL){
            tp = tp->next;
        }
        tp->next = temp;
        temp->prev = tp;
        return head;
    }
    
    struct node* addToEmpty(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        head = temp;
        return head;
    }
    
    struct node* addAfterPos (struct node* head, int data, int position){
        struct node* newP = NULL;
        struct node* temp = head;
        struct node* temp2 = NULL;
        newP = addToEmpty(newP, data);
    
        while(position != 1){
            temp = temp -> next;
            position--;
        }
    		
    		
    		//considering the case where we need to add a node at the last
        if(temp->next == NULL){
            temp -> next = newP;
            newP -> prev = temp;
        }
        else {
            temp2 = temp -> next;
            temp -> next = newP;
            temp2 -> prev = newP;
            newP -> prev = temp;
            newP -> next = temp2;
        }
        return head;
    }
    
    int main() {
        struct node* head = NULL;
        struct node* ptr;
        head = addToEmpty(head, 0);
        head = add_at_start(head, 1);
        head = add_at_end(head, 2);
        head = addAfterPos(head, 99, 2);
    
        ptr = head;
        while(ptr != NULL){
            printf("%d ", ptr->value);
            ptr = ptr -> next;
        }
    
        return 0;
    }
    ```
    
- insertion between the nodes (add before pos)
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        struct node* prev;
        int value;
        struct node* next;
    };
    
    struct node* add_at_start(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next =  head;
        head -> prev = temp;
        head = temp;
        return head;
    }
    
    struct node* add_at_end(struct node* head, int data){
        struct node* temp, *tp;
        temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        tp = head;
        while(tp->next != NULL){
            tp = tp->next;
        }
        tp->next = temp;
        temp->prev = tp;
        return head;
    }
    
    struct node* addToEmpty(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        head = temp;
        return head;
    }
    
    struct node* addAfterPos (struct node* head, int data, int position){
        struct node* newP = NULL;
        struct node* temp = head;
        struct node* temp2 = NULL;
        newP = addToEmpty(newP, data);
    
        while(position != 1){
            temp = temp -> next;
            position--;
        }
    
        if(temp->next == NULL){
            temp -> next = newP;
            newP -> prev = temp;
        }
        else {
            temp2 = temp -> next;
            temp -> next = newP;
            temp2 -> prev = newP;
            newP -> prev = temp;
            newP -> next = temp2;
        }
        return head;
    }
    
    struct node* addBeforePos (struct node* head, int data, int position){
        struct node* newP = NULL;
        struct node* temp = head;
        struct node* temp2 = NULL;
        newP = addToEmpty(newP, data);
    
        while(position>2){
            temp = temp -> next;
            position--;
        }
    		//considering add at the beggining
        if(position == 1){
            head = add_at_start(head, data);
        }
        else{
            temp2 = temp -> next;
            temp -> next = newP;
            temp2 -> prev = newP;
            newP -> prev = temp;
            newP -> next = temp2;
        }
        return head;
    }
    
    int main() {
        struct node* head = NULL;
        struct node* ptr;
        head = addToEmpty(head, 0);
        head = add_at_start(head, 1);
        head = add_at_end(head, 2);
        head = addBeforePos(head, 99, 1);
    
        ptr = head;
        while(ptr != NULL){
            printf("%d ", ptr->value);
            ptr = ptr -> next;
        }
    
        return 0;
    }
    ```
    
- deleting the first node
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    struct node{
        struct node* prev;
        int value;
        struct node* next;
    };
    
    struct node* add_at_start(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next =  head;
        head -> prev = temp;
        head = temp;
        return head;
    }
    
    struct node* add_at_end(struct node* head, int data){
        struct node* temp, *tp;
        temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        tp = head;
        while(tp->next != NULL){
            tp = tp->next;
        }
        tp->next = temp;
        temp->prev = tp;
        return head;
    }
    
    struct node* addToEmpty(struct node* head, int data){
        struct node* temp = malloc(sizeof(struct node));
        temp -> prev = NULL;
        temp -> value = data;
        temp -> next = NULL;
        head = temp;
        return head;
    }
    
    struct node* addAfterPos (struct node* head, int data, int position){
        struct node* newP = NULL;
        struct node* temp = head;
        struct node* temp2 = NULL;
        newP = addToEmpty(newP, data);
    
        while(position != 1){
            temp = temp -> next;
            position--;
        }
    
        if(temp->next == NULL){
            temp -> next = newP;
            newP -> prev = temp;
        }
        else {
            temp2 = temp -> next;
            temp -> next = newP;
            temp2 -> prev = newP;
            newP -> prev = temp;
            newP -> next = temp2;
        }
        return head;
    }
    
    struct node* addBeforePos (struct node* head, int data, int position){
        struct node* newP = NULL;
        struct node* temp = head;
        struct node* temp2 = NULL;
        newP = addToEmpty(newP, data);
    
        while(position>2){
            temp = temp -> next;
            position--;
        }
    
        if(position == 1){
            head = add_at_start(head, data);
        }
        else{
            temp2 = temp -> next;
            temp -> next = newP;
            temp2 -> prev = newP;
            newP -> prev = temp;
            newP -> next = temp2;
        }
        return head;
    }
    
    struct node* del_first(struct node* head) {
        head = head -> next;
        free(head -> prev);
        head -> prev = NULL;
    
        return head;
    }
    
    int main() {
        struct node* head = NULL;
        struct node* ptr;
        head = addToEmpty(head, 0);
        head = add_at_start(head, 1);
        head = add_at_end(head, 2);
        head = addBeforePos(head, 99, 1);
    
        ptr = head;
        printf("before deletion. \n");
        while(ptr != NULL){
            printf("%d ", ptr->value);
            ptr = ptr -> next;
        }
    
        head = del_first(head);
        printf("\nafter deletion. \n");
        ptr = head;
        while(ptr != NULL){
            printf("%d ", ptr->value);
            ptr = ptr -> next;
        }
        
        //before deletion. 
        //99 1 0 2 
        //after deletion. 
        //1 0 2 
        
        return 0;
    }
    ```
    
- deleting the last node
    
    ```c
    struct node* delLast(struct node* head) {
    		struct node* temp = head;
    		struct node* temp2;
    		while(temp -> next != NULL){
    				temp = temp -> next;
    		}
    		temp2 = temp -> prev;
    		free(temp2 -> next);
    		temp2 -> next = NULL;
    		free(temp);
    		reutrn head;
    }
    ```
    
- deleting the intermediate node
    
    ```c
    struct node* delInter(struct node* head, int position){
        struct node* temp = head;
        struct node* temp2 = NULL;
        if(position == 1){
            head = del_first(head);
            return head;
        }
        while(position > 1){
            temp = temp -> next;
            position--;
        }
        if(temp -> next == NULL){head = del_last(head);}
        else{
            temp2 = temp->prev;
            temp2->next = temp->next;
            temp->next->prev = temp2;
            free(temp);
            temp = NULL;
        }
        return head;
    }
    ```
    
- reversing doubly linked list
    
    
- why doubly linked list?
    
    a doubly linked list is a variation of a singly linked list where each node is also pointing to its previous node.
    
    - deletion operation is faster in doubly linked list, if the pointer to the node is given
        
        in case of singly linked list, it is important to keep one more pointer pointing to the node just before the node we want to delete. 
        
        imagine we have 5 nodes in the list and out target is to delete the third node, then it that case, temp has to move one step forward. This means traversal is required.
        
        However, in case of doubly linked list, deleting the intermediate node is very easy. There is no need to keep an extra pointer to delete the intermediate node because it is always possible to reach the previous node from the current node to be deleted.
        
    - inserting a new node before a given node is easier in doubly linked list
        
        in case of singly linked list, a pointer to the previous node is required → traversal is required.
        
        in case of doubly linked list, inserting a new node before the given node is very easy because we can always reach a node before the given node.
        

### Circular Linked List

Circular Singly Linked List

- similar to the singly linked list except that the last node of the circular singly linked list points to the first node.
- operations on circular singly linked list
    - insertion at the beginning
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20120.png)
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
            int value;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->value = data;
            temp->next=temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next=tail->next;
            tail->next = newP;
            return tail;
        }
        
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p=p->next;
            }while(p!=tail->next);
        }
        
        int main() {
            struct node* tail;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
        
            print(tail);
            return 0;
        }
        ```
        
        할 수 있다 화이팅!!
        
    - traversing the list
        
        to traverse a circular linked list, we have to take advantage of do while loop.
        
        because if we check p!=tail→next, the flow will escape the while loop right away. let’s see the code example.
        
        ```c
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p=p->next;
            }while(p!=tail->next);
        }
        ```
        
    - insertion at the end
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20121.png)
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
            int value;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->value = data;
            temp->next=temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next=tail->next;
            tail->next = newP;
            return tail;
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP -> value = data;
            newP -> next = NULL;
        
            newP->next = tail->next;
            tail->next = newP;
            tail = tail -> next;
            return tail;
        }
        
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p=p->next;
            }while(p!=tail->next);
        }
        
        int main() {
            struct node* tail;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
            tail = addAtEnd(tail, 6);
            tail = addAtEnd(tail, 66);
        
            print(tail);
            return 0;
        }
        ```
        
    - insertion between the nodes
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
            int value;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->value = data;
            temp->next=temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next=tail->next;
            tail->next = newP;
            return tail;
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP -> value = data;
            newP -> next = NULL;
        
            newP->next = tail->next;
            tail->next = newP;
            tail = tail -> next;
            return tail;
        }
        
        struct node* addAfterPos(struct node* tail, int data, int pos){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next = NULL;
            struct node* p = tail->next;
            while(pos > 1){
                p = p->next;
                pos--;
            }
            newP->next = p->next;
            p->next = newP;
            if(p == tail){
                tail=tail->next;
            }
            return tail;
        }
        
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p=p->next;
            }while(p!=tail->next);
        }
        
        int main() {
            struct node* tail;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
            tail = addAtEnd(tail, 6);
            tail = addAtEnd(tail, 66);
            tail = addAfterPos(tail, 77, 4);
        
            print(tail);
            return 0;
        }
        ```
        
        when adding after a certain position, we definitely have to take care of a situation where we add to the last. the reason why we set the p pointer at the first node of the list is so that we can differentiate a situation where we add at the first and at the end. later on the code, the if check plays a crucial role to update the tail in case of adding a new node at the end.
        
    - deleting the first node
        
        ```c
        struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next = NULL;
            struct node* p = tail->next;
            while(pos > 1){
                p = p->next;
                pos--;
            }
            newP->next = p->next;
            p->next = newP;
            if(p == tail){
                tail=tail->next;
            }
            return tail;
        }
        
        struct node* delFirst(struct node* tail){
            if(tail == NULL){
                return tail;
            }else if(tail->next == tail){
                free(tail);
                tail=NULL;
                return tail;
            }
            struct node* temp= tail -> next;
            tail -> next = temp -> next;
            free(temp);
            temp = NULL;
            return tail;
        }
        
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p=p->next;
            }while(p!=tail->next);
        }
        
        int main() {
            struct node* tail;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
            tail = addAtEnd(tail, 6);
            tail = addAtEnd(tail, 66);
            tail = addAfterPos(tail, 77, 4); //34 45 6 66 77
            tail = delFirst(tail); //45 6 66 77
        
            print(tail);
            return 0;
        }
        ```
        
    - deleting the last node
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
            int value;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->value = data;
            temp->next=temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next=tail->next;
            tail->next = newP;
            return tail;
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP -> value = data;
            newP -> next = NULL;
        
            newP->next = tail->next;
            tail->next = newP;
            tail = tail -> next;
            return tail;
        }
        
        struct node* addAfterPos(struct node* tail, int data, int pos){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next = NULL;
            struct node* p = tail->next;
            while(pos > 1){
                p = p->next;
                pos--;
            }
            newP->next = p->next;
            p->next = newP;
            if(p == tail){
                tail=tail->next;
            }
            return tail;
        }
        
        struct node* delFirst(struct node* tail){
            if(tail == NULL){
                return tail;
            }else if(tail->next == tail){
                free(tail);
                tail=NULL;
                return tail;
            }
            struct node* temp= tail -> next;
            tail -> next = temp -> next;
            free(temp);
            temp = NULL;
            return tail;
        }
        
        struct node* delLast(struct node* tail){
            struct node* temp = tail -> next;
            while(temp -> next != tail){
                temp = temp->next;
            }
            temp->next = tail->next;
            free(tail);
            tail = temp;
            return tail;
        }
        
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p=p->next;
            }while(p!=tail->next);
        }
        
        int main() {
            struct node* tail;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
            tail = addAtEnd(tail, 6);
            tail = addAtEnd(tail, 66);
            tail = addAfterPos(tail, 77, 4); //34 45 6 66 77
            tail = delFirst(tail); //45 6 66 77
            tail = delLast(tail); //45 6 66
        
            print(tail);
            return 0;
        }
        ```
        
    - deleting the intermediate node
        
        ```c
        struct node* delInter(struct node* tail, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail -> next;
            if(tail->next == tail){
                free(tail);
                tail = NULL;
                return tail;
            }
            if(pos == 1){
                tail->next = temp->next;
                free(temp);
                temp=NULL;
                return tail;
            }
            while(pos > 2){
                temp = temp->next;
                pos--;
            }
            struct node* temp2 = temp -> next;
            temp->next = temp2->next;
            if(temp2 == tail) {
                tail = temp;
                tail->next = temp2->next;
            }
            free(temp2);
            temp2 = NULL;
            return tail;
        }
        ```
        
    - counting the number of nodes
        
        ```c
        void countElements(struct node* tail){
            struct node* temp = tail->next;
            int count = tail==NULL?-1:0;
            while(temp != tail){
                temp = temp->next;
                count++;
            }
            count++;
            printf("There are %d elements in the list.\n", count);
        }
        ```
        
    - searching the index of an element
        
        ```c
        int searchIndexOf(struct node* tail, int element){
            if(tail == NULL){return -2;}
            int index = 0;
            struct node* temp = tail->next;
            do{
                if(temp->value == element){
                    return index;
                }
                temp = temp->next;
                index++;
            }while(temp != tail->next);
            return -1;
        }
        ```
        
    - entire code
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node{
            int value;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->value = data;
            temp->next=temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next=tail->next;
            tail->next = newP;
            return tail;
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = malloc(sizeof(struct node));
            newP -> value = data;
            newP -> next = NULL;
        
            newP->next = tail->next;
            tail->next = newP;
            tail = tail -> next;
            return tail;
        }
        
        struct node* addAfterPos(struct node* tail, int data, int pos){
            struct node* newP = malloc(sizeof(struct node));
            newP->value = data;
            newP->next = NULL;
            struct node* p = tail->next;
            while(pos > 1){
                p = p->next;
                pos--;
            }
            newP->next = p->next;
            p->next = newP;
            if(p == tail){
                tail=tail->next;
            }
            return tail;
        }
        
        struct node* delFirst(struct node* tail){
            if(tail == NULL){
                return tail;
            }else if(tail->next == tail){
                free(tail);
                tail=NULL;
                return tail;
            }
            struct node* temp= tail -> next;
            tail -> next = temp -> next;
            free(temp);
            temp = NULL;
            return tail;
        }
        
        struct node* delLast(struct node* tail){
            struct node* temp = tail -> next;
            while(temp -> next != tail){
                temp = temp->next;
            }
            temp->next = tail->next;
            free(tail);
            tail = temp;
            return tail;
        }
        
        struct node* delInter(struct node* tail, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail -> next;
            if(tail->next == tail){
                free(tail);
                tail = NULL;
                return tail;
            }
            if(pos == 1){
                tail->next = temp->next;
                free(temp);
                temp=NULL;
                return tail;
            }
            while(pos > 2){
                temp = temp->next;
                pos--;
            }
            struct node* temp2 = temp -> next;
            temp->next = temp2->next;
            if(temp2 == tail) {
                tail = temp;
                tail->next = temp2->next;
            }
            free(temp2);
            temp2 = NULL;
            return tail;
        }
        
        void print(struct node* tail){
            struct node* p = tail->next;
            do {
                printf("%d ", p->value);
                p = p->next;
            }while(p!=tail->next);
        }
        
        void countElements(struct node* tail){
            struct node* temp = tail->next;
            int count = tail==NULL?-1:0;
            while(temp != tail){
                temp = temp->next;
                count++;
            }
            count++;
            printf("There are %d elements in the list.\n", count);
        }
        
        int searchIndexOf(struct node* tail, int element){
            if(tail == NULL){return -2;}
            int index = 0;
            struct node* temp = tail->next;
            do{
                if(temp->value == element){
                    return index;
                }
                temp = temp->next;
                index++;
            }while(temp != tail->next);
            return -1;
        }
        
        int main() {
            struct node* tail;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
            tail = addAtEnd(tail, 6);
            tail = addAtEnd(tail, 66);
            tail = addAfterPos(tail, 77, 4); //34 45 6 66 77
            tail = delFirst(tail); //45 6 66 77
            printf("%d\n", searchIndexOf(tail, 6)); //1
            countElements(tail); //There are 4 elements in the list.
            tail = delLast(tail); //45 6 66
            tail = delInter(tail, 1); //6 66
            tail = delInter(tail, 2); //6
        
            print(tail);
            return 0;
        }
        ```
        

Circular Doubly Linked List

- similar to the doubly linked list except that the last node of the circular doubly linked list points to the first node and the first node of the circular doubly linked list points to the last node.
- operations on circular doubly linked list
    - insertion at the beginning
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        struct node {
            struct node* prev;
            int data;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->prev = temp;
            temp->data = data;
            temp->next = temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail == NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                return tail;
            }
        }
        
        void print(struct node* tail){
            if(tail == NULL){
                printf("No element in the List");
            }else{
                struct node* temp = tail -> next;
                do{
                    printf("%d ", temp->data);
                    temp=temp->next;
                }while(temp != tail->next);
            }
            printf("\n");
        }
        
        int main() {
            struct node* tail = NULL;
            tail = addToEmpty(45);
            tail = addAtBeg(tail, 34);
            print(tail);
            return 0;
        }
        ```
        
    - insertion at the end
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        struct node {
            struct node* prev;
            int data;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->prev = temp;
            temp->data = data;
            temp->next = temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail == NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                return tail;
            }
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail==NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                tail = tail->next;
                return tail;
            }
        }
        
        void print(struct node* tail){
            if(tail == NULL){
                printf("No element in the List");
            }else{
                struct node* temp = tail -> next;
                do{
                    printf("%d ", temp->data);
                    temp=temp->next;
                }while(temp != tail->next);
            }
            printf("\n");
        }
        
        int main() {
            struct node* tail = NULL;
            tail = addToEmpty(45); //35
            tail = addAtBeg(tail, 34); //34 35
            tail = addAtEnd(tail, 17); //34 35 17
            print(tail);
            return 0;
        }
        ```
        
    - insertion between the nodes
        
        ```python
        #include <stdio.h>
        #include <stdlib.h>
        struct node {
            struct node* prev;
            int data;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->prev = temp;
            temp->data = data;
            temp->next = temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail == NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                return tail;
            }
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail==NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                tail = tail->next;
                return tail;
            }
        }
        
        struct node* addInter(struct node* tail, int data, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail -> next;
            struct node* newP = addToEmpty(data);
            newP->data = data;
            newP->prev=NULL;
            newP->next=NULL;
        
            while(pos>1){
                temp = temp->next;
                pos--;
            }
        
            newP->prev = temp;
            newP->next = temp->next;
            temp->next->prev=newP;
            temp->next=newP;
        
            if(tail == temp)
                tail = tail->next;
            return tail;
        }
        
        void print(struct node* tail){
            if(tail == NULL){
                printf("No element in the List");
            }else{
                struct node* temp = tail -> next;
                do{
                    printf("%d ", temp->data);
                    temp=temp->next;
                }while(temp != tail->next);
            }
            printf("\n");
        }
        
        int main() {
            struct node* tail = NULL;
            tail = addToEmpty(45); //45
            tail = addAtBeg(tail, 34); //34 45
            tail = addAtEnd(tail, 17); //34 45 17
            tail = addInter(tail, 20, 2); //34 45 20 17
            tail = addInter(tail, 11, 4); //34 45 20 17
            print(tail);
            return 0;
        }
        ```
        
        we need to check if we want to add the node at the end and update the tail.
        
    - deleting the first node
        
        ```python
        #include <stdio.h>
        #include <stdlib.h>
        struct node {
            struct node* prev;
            int data;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->prev = temp;
            temp->data = data;
            temp->next = temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail == NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                return tail;
            }
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail==NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                tail = tail->next;
                return tail;
            }
        }
        
        struct node* addInter(struct node* tail, int data, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail -> next;
            struct node* newP = addToEmpty(data);
            newP->data = data;
            newP->prev=NULL;
            newP->next=NULL;
        
            while(pos>1){
                temp = temp->next;
                pos--;
            }
        
            newP->prev = temp;
            newP->next = temp->next;
            temp->next->prev=newP;
            temp->next=newP;
        
            if(tail == temp)
                tail = tail->next;
            return tail;
        }
        
        struct node* delFirst(struct node* tail){
            if(tail == NULL)
                return tail;
            struct node* temp = tail->next;
            if(temp == tail){
                free(tail);
                tail=NULL;
                return tail;
            }
            tail->next = temp->next;
            temp->next->prev = tail;
            free(temp);
            temp=NULL;
            return tail;
        }
        
        void print(struct node* tail){
            if(tail == NULL){
                printf("No element in the List");
            }else{
                struct node* temp = tail -> next;
                do{
                    printf("%d ", temp->data);
                    temp=temp->next;
                }while(temp != tail->next);
            }
            printf("\n");
        }
        
        int main() {
            struct node* tail = NULL;
            tail = addToEmpty(45); //45
            tail = addAtBeg(tail, 34); //34 45
            tail = addAtEnd(tail, 17); //34 45 17
            tail = addInter(tail, 20, 2); //34 45 20 17
            tail = addInter(tail, 11, 4); //34 45 20 17 11
            tail = delFirst(tail);//45 20 17 11
        
            print(tail);
            return 0;
        }
        ```
        
        we need to check when there is zero or one node.
        
    - deleting the last node
        
        ```python
        #include <stdio.h>
        #include <stdlib.h>
        struct node {
            struct node* prev;
            int data;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->prev = temp;
            temp->data = data;
            temp->next = temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail == NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                return tail;
            }
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail==NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                tail = tail->next;
                return tail;
            }
        }
        
        struct node* addInter(struct node* tail, int data, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail -> next;
            struct node* newP = addToEmpty(data);
            newP->data = data;
            newP->prev=NULL;
            newP->next=NULL;
        
            while(pos>1){
                temp = temp->next;
                pos--;
            }
        
            newP->prev = temp;
            newP->next = temp->next;
            temp->next->prev=newP;
            temp->next=newP;
        
            if(tail == temp)
                tail = tail->next;
            return tail;
        }
        
        struct node* delFirst(struct node* tail){
            if(tail == NULL)
                return tail;
            struct node* temp = tail->next;
            if(temp == tail){
                free(tail);
                tail=NULL;
                return tail;
            }
            tail->next = temp->next;
            temp->next->prev = tail;
            free(temp);
            temp=NULL;
            return tail;
        }
        
        struct node* delLast(struct node* tail){
            if(tail==NULL)
                return tail;
            struct node* temp = tail->prev;
            if(tail == temp){
                free(temp);
                temp = NULL;
                return tail;
            }
            temp->next = tail->next;
            tail->next->prev= temp;
            free(tail);
            tail = temp;
            return tail;
        }
        
        void print(struct node* tail){
            if(tail == NULL){
                printf("No element in the List");
            }else{
                struct node* temp = tail -> next;
                do{
                    printf("%d ", temp->data);
                    temp=temp->next;
                }while(temp != tail->next);
            }
            printf("\n");
        }
        
        int main() {
            struct node* tail = NULL;
            tail = addToEmpty(45); //45
            tail = addAtBeg(tail, 34); //34 45
            tail = addAtEnd(tail, 17); //34 45 17
            tail = addInter(tail, 20, 2); //34 45 20 17
            tail = addInter(tail, 11, 4); //34 45 20 17 11
            tail = delFirst(tail);//45 20 17 11
            tail = delLast(tail);//45 20 17
        
            print(tail);
            return 0;
        }
        ```
        
    - deleting the intermediate node
        
        ```python
        #include <stdio.h>
        #include <stdlib.h>
        struct node {
            struct node* prev;
            int data;
            struct node* next;
        };
        
        struct node* addToEmpty(int data){
            struct node* temp = malloc(sizeof(struct node));
            temp->prev = temp;
            temp->data = data;
            temp->next = temp;
            return temp;
        }
        
        struct node* addAtBeg(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail == NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                return tail;
            }
        }
        
        struct node* addAtEnd(struct node* tail, int data){
            struct node* newP = addToEmpty(data);
            if(tail==NULL){
                return newP;
            }else{
                struct node* temp = tail->next;
                newP->prev = tail;
                newP->next = temp;
                temp->prev = newP;
                tail->next = newP;
                tail = tail->next;
                return tail;
            }
        }
        
        struct node* addInter(struct node* tail, int data, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail -> next;
            struct node* newP = addToEmpty(data);
            newP->data = data;
            newP->prev=NULL;
            newP->next=NULL;
        
            while(pos>1){
                temp = temp->next;
                pos--;
            }
        
            newP->prev = temp;
            newP->next = temp->next;
            temp->next->prev=newP;
            temp->next=newP;
        
            if(tail == temp)
                tail = tail->next;
            return tail;
        }
        
        struct node* delFirst(struct node* tail){
            if(tail == NULL)
                return tail;
            struct node* temp = tail->next;
            if(temp == tail){
                free(tail);
                tail=NULL;
                return tail;
            }
            tail->next = temp->next;
            temp->next->prev = tail;
            free(temp);
            temp=NULL;
            return tail;
        }
        
        struct node* delLast(struct node* tail){
            if(tail==NULL)
                return tail;
            struct node* temp = tail->prev;
            if(tail == temp){
                free(temp);
                temp = NULL;
                return tail;
            }
            temp->next = tail->next;
            tail->next->prev= temp;
            free(tail);
            tail = temp;
            return tail;
        }
        
        struct node* delInter(struct node* tail, int pos){
            if(tail == NULL)
                return tail;
            struct node* temp = tail->next;
            if(temp->next == tail){
                free(temp); temp = NULL;
                return tail;
            }
            while(pos>1){
                temp = temp->next;
                pos--;
            }
            if(temp == tail){
                tail = tail->prev;
            }
            temp->prev->next = temp->next;
            temp->next->prev = temp->prev;
            free(temp);temp=NULL;
            return tail;
        }
        
        void print(struct node* tail){
            if(tail == NULL){
                printf("No element in the List");
            }else{
                struct node* temp = tail -> next;
                do{
                    printf("%d ", temp->data);
                    temp=temp->next;
                }while(temp != tail->next);
            }
            printf("\n");
        }
        
        int main() {
            struct node* tail = NULL;
            tail = addToEmpty(45); //45
            tail = addAtBeg(tail, 34); //34 45
            tail = addAtEnd(tail, 17); //34 45 17
            tail = addInter(tail, 20, 2); //34 45 20 17
            tail = addInter(tail, 11, 4); //34 45 20 17 11
            tail = delFirst(tail);//45 20 17 11
            tail = delLast(tail);//45 20 17
            tail = delInter(tail, 1); //20 17
            print(tail);
            return 0;
        }
        ```
        

Node appearance

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20122.png)

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20123.png)

### Stacks

A stack is a linear data structure in which insertions and deletions are allowed only at the end, called the top of the stack.

1. any object can be accessed only from the top.
2. any object can be added only at the top.
- As a stack is a linear data structure, we can implement it using an array or a linked list

**user point of view**

`push(data)`: Inserts data onto stack

`pop()`: Deletes the last inserted data from stack

`top()`: returns the last inserted element without removing it

`size()`: returns the size of the number of elements in the stack

`isEmpty()`: returns TRUE if the stack is empty, else returns FALSE

`isFull()`: returns TRUE if the stack is full, else returns FALSE

- array implementation of stacks
    
    when using array, we know that stack_arr[] is an array and insertion and deletion operations can be performed at any place but we want the stack_arr[] to behave like a stack. Hence, the insertions and deletions must be performed at the end.
    
    we will keep a variable **top** which will keep track of the last inserted element or the topmost element in an array.
    
    to indicate that the stack is empty, we will put -1 in the variable top.
    
    - top = 0 indicates that the topmost element is at index 0 and this means there is only one element in the stack.
    - operations
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20124.png)
        
        **For push operation:**
        
        - top is incremented by 1.
        - New element is pushed at the position top.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20125.png)
        
        here, push(12) is impossible. There is not enough space in the stack. This state is called the overflow state and the new element cannot be pushed.
        
        **For pop operation:**
        
        - the element at the position of top is deleted.
        - top is decremented by 1.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20126.png)
        
    - push
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20127.png)
        
        Almost every operation function requires the stack_arr[] array.
        
        Instead of passing it to every function, the better option is to declare the stack_arr globally.
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 4
        
        int stack_arr[MAX];
        int top = -1;
        
        void push(int data){
            if(top == MAX - 1){
                printf("Stack Overflow\n");
                return;
            }
            top++;
            stack_arr[top] = data;
        }
        
        int main(){
            push(1);
            push(2);
            push(3);
            push(4);
            push(5); //Stack Overflow
            return 0;
        }
        ```
        
    - pop
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20128.png)
        
        Q. How to delete the element at index n?
        
        We cannot simply remove the array element. Still, we can give the user an **illusion** that the array element is deleted by decrementing the top variable.
        
        top variable always keeps track of the topmost element of the stack. If the top is decremented by 1 then the user will perceive that the topmost element is deleted.
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 4
        
        int stack_arr[MAX];
        int top = -1;
        
        void push(int data){
            if(top == MAX - 1){
                printf("Stack Overflow\n");
                return;
            }
            top++;
            stack_arr[top] = data;
        }
        
        int pop(){
            if(top == -1){
                printf("Stack underflow");
                exit(1);
            }
            int value;
            value = stack_arr[top];
            top--;
            return value;
        }
        
        void print(){
            int i;
            if(top == -1){
                printf("Stack underflow\n");
                return;
            }
            for(i=top; i>=0; i--)
                printf("%d ", stack_arr[i]);
            printf("\n");
        }
        
        int main(){
            int data;
            push(1);
            push(2);
            push(3);
            push(4);
            print(); //4 3 2 1
            data = pop();
            data = pop();
            printf("%d\n", data);//3
            print(); // 2 1
            return 0;
            data = pop();
        }
        ```
        
    - isFull & isEmpty
        
        In the push() function, we were checking whether a stack is full or not. That’s main part of the isFull() function.
        
        **isFull**
        
        ```c
        int isFull(){
        		if(top == MAX - 1)
        				return 1;
        		else
        				return 0;
        }
        ```
        
        Similarly, checking whether a stack is empty was used in the pop function.
        
        **isEmpty**
        
        ```c
        int isEmpty(){
        		if(top == -1)
        				return 1;
        		else
        				return 0;
        }
        ```
        
    - simple stack program
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 4
        
        int stack_arr[MAX];
        int top = -1;
        
        void push(int data){
            if(top == MAX - 1){
                printf("Stack Overflow\n");
                return;
            }
            top++;
            stack_arr[top] = data;
        }
        
        int pop(){
            if(top == -1){
                printf("Stack underflow");
                exit(1);
            }
            int value;
            value = stack_arr[top];
            top--;
            return value;
        }
        
        void print(){
            int i;
            if(top == -1){
                printf("Stack underflow\n");
                return;
            }
            for(i=top; i>=0; i--)
                printf("%d ", stack_arr[i]);
            printf("\n");
        }
        
        int isFull(){
            if(top == MAX-1){
                return 1;
            }else{
                return 0;
            }
        }
        
        int isEmpty(){
            if(top == -1){
                return 1;
            }else{
                return 0;
            }
        }
        
        int main(){
            int data;
            int choice;
        
            while(choice != 5)
            {
                printf("\n1. Push\n2. Pop\n3. Print the top element\n4. Print all the elements of the stack\n5. Quit");
                printf("\n");
                printf("Please enter your choice: ");
                scanf("%d", &choice);
                printf("\n");
        
                switch(choice) {
                    case 1:
                        printf("Enter the element to be pushed: ");
                        scanf( "%d", &data);
                        push(data);
                        printf("\nentered element is %d\n", data);
                        break;
                    case 2:
                        printf("\ndeleted element is %d\n",pop());
                        break;
                    case 3:
                        printf("\nthe top element is %d\n",top);
                        break;
                    case 4:
                        print();
                        break;
                }
            }
        
            return 0;
        }
        ```
        
    
    [a program arr[0] being the top](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/a%20program%20arr%5B0%5D%20being%20the%20top%20200785e06f6c43f2a5ef19df106153e7.md)
    
    - a program to print prime factors of a number
        
        Objective: write a program to print all the prime factors of a number in descending order using a stack.
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 6
        
        int stack_arr[MAX];
        int second_top = -1;
        
        void push(int data){
            second_top++;
            if(second_top != 0){
                stack_arr[second_top] = data;
                int temp = stack_arr[second_top];
                stack_arr[second_top] = stack_arr[0];
                stack_arr[0] = temp;
            }else{stack_arr[0] = data;}
            printf("data added: %d\n", data);
        }
        
        int pop(){
            int value;
            if(second_top == -1){
                printf("Stack underflow\n");
                exit(1);
            }
            value = stack_arr[0];
            stack_arr[0] = 0;
            int tmp = stack_arr[second_top];
            stack_arr[second_top] = stack_arr[0];
            stack_arr[0] = tmp;
            second_top--;
            return value;
        }
        
        int isFull(){
            if(second_top == MAX-1)
                return 1;
            else
                return 0;
        }
        
        int isEmpty(){
            if(second_top == -1)
                return 1;
            else
                return 0;
        }
        
        int peek(){
            if(isEmpty()){
                printf("Stack Underflow\n");
                exit(1);
            }
            return stack_arr[0];
        }
        
        void prime_fact(int num) {
            int i = 2;
            //Push all the prime factors of a number onto stack
            while(num != 1){
                while(num%i == 0){
                    push(i);
                    num = num/i;
                }
                i++;
            }
            //Pop all the prime factors from the stack and print
            printf("Prime factors of the number in descending order are as follows: ");
            while (second_top != -1) {
                printf("%d ", pop());
            }
        }
        
        void print() {
            if (second_top == -1) {
                printf("Stack underflow\n");
                exit(1);
            }
            printf("%d ", stack_arr[0]);
            for (int i = second_top; i > 0; i--) {
                printf("%d ", stack_arr[i]);
            }
        }
        
        int main(){
            int number;
            printf("Please enter a positive number: ");
            scanf("%d", &number);
        
            prime_fact(number);
            /*
             * data added: 2
             * data added: 3
             * data added: 7
             * Prime factors of the number in descending order are as follows: 7 3 2
             * */
            return 0;
        }
        ```
        
    - decimal to binary using stack
        
        steps:
        
        1. Divide the number by 2.
        2. Store the remainder somewhere.
        3. Repeat step 1 and 2 until quotient becomes 0.
        4. Print all the remainders in reverse order.
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 6
        
        int stack_arr[MAX];
        int second_top = -1;
        
        void push(int data){
            second_top++;
            if(second_top != 0){
                stack_arr[second_top] = data;
                int temp = stack_arr[second_top];
                stack_arr[second_top] = stack_arr[0];
                stack_arr[0] = temp;
            }else{stack_arr[0] = data;}
            printf("data added: %d\n", data);
        }
        
        int pop(){
            int value;
            if(second_top == -1){
                printf("Stack underflow\n");
                exit(1);
            }
            value = stack_arr[0];
            stack_arr[0] = 0;
            int tmp = stack_arr[second_top];
            stack_arr[second_top] = stack_arr[0];
            stack_arr[0] = tmp;
            second_top--;
            return value;
        }
        
        int isFull(){
            if(second_top == MAX-1)
                return 1;
            else
                return 0;
        }
        
        int isEmpty(){
            if(second_top == -1)
                return 1;
            else
                return 0;
        }
        
        int peek(){
            if(isEmpty()){
                printf("Stack Underflow\n");
                exit(1);
            }
            return stack_arr[0];
        }
        
        void dec2bin(int n){
            while(n != 0) {
                push(n%2);
                n /= 2;
            }
        }
        
        void print() {
            if(isEmpty()){
                printf("Stack Underflow.");
                exit(1);
            }
            while(!isEmpty()){
                printf("%d", pop());
            }
        }
        
        int main(){
            int number;
            printf("Please enter a positive number: ");
            scanf("%d", &number);
        
            dec2bin(number);
            print(); //10100
            return 0;
        }
        ```
        
    
- Linked List implementation of stacks
    
    Why Linked List?
    
    - use linked list when the size of the stack is not known in advance.
    
    Why should we prefer the beginning of the linked list as the top of the stack?
    
    - time complexity of adding a node at the beginning: O(1)
    - time complexity of removing the first node: O(1)
    
    while…
    
    - time complexity of adding a node at the end: O(1)
    - time complexity of removing a node at the end: O(n)
    
    → the code of push() and pop() functions should be similar to the code of inserting and deleting the node at the beginning.
    
    - Stack overflow occurs when there is no space left to dynamically allocate the memory. In that case, malloc() function will return NULL.
    - Stack underflow occurs when top is equal to NULL.
    
    Declaring the top pointer globally in the code.
    
    ```c
    struct node {
    		int data;
    		struct node* link;
    } *top = NULL;
    ```
    
    - `push()`
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node {
            int data;
            struct node* link;
        } *top = NULL;
        
        void push(int data){
            struct node* newNode = malloc(sizeof(struct node));
            //checking for stack overflow
            if(newNode == NULL){
                printf("Stack Overflow");
                exit(1);
            }
            newNode->data= data;
            newNode->link = NULL;
        
            newNode->link = top;
            top = newNode;
        }
        
        void print(){
            struct node* ptr = top;
            printf("The stack elements are: ");
            while(ptr != NULL){
                printf("%d ", ptr->data);
                ptr = ptr->link;
            }
            printf("\n");
        }
        
        int main(){
            int choice, data;
            while(1){
                printf("1. Push\n");
                printf("2. Print\n");
                printf("3. Quit\n");
                printf("Enter your choice: ");
                scanf("%d", &choice);
        
                switch(choice){
                    case 1:
                        printf("Enter the element to be pushed: ");
                        scanf("%d", &data);
                        push(data);
                        break;
                    case 2: print(); break;
                    case 3: exit(1);
                    default:
                        printf("Wrong Choice\n");
                        break;
                }
            }
            return 0;
        }
        ```
        
    - `pop()` && `isEmpty` && `peek`
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        int isEmpty();
        void push(int data);
        int pop();
        int peek();
        
        struct node {
            int data;
            struct node* link;
        } *top = NULL;
        
        void push(int data){
            struct node* newNode = malloc(sizeof(struct node));
            //checking for stack overflow
            if(newNode == NULL){
                printf("Stack Overflow");
                exit(1);
            }
            newNode->data= data;
            newNode->link = NULL;
        
            newNode->link = top;
            top = newNode;
        }
        
        int pop(){
            if(isEmpty()) {
                printf("Stack Underflow");
                exit(1);
            }
            int value = top->data;
            struct node* temp = top;
            top = top->link;
            free(temp);
            temp = NULL;
            return value;
        }
        
        int isEmpty(){
            if(top == NULL)
                return 1;
            else
                return 0;
        }
        
        void print(){
            struct node* ptr = top;
            if(isEmpty()){
                printf("Stack Underflow.");
                exit(1);
            }
            printf("The stack elements are: ");
            while(ptr != NULL){
                printf("%d ", ptr->data);
                ptr = ptr->link;
            }
            printf("\n");
        }
        
        int peek(){
            if(isEmpty()){
                printf("Stack Underflow");
                exit(1);
            } return top->data;
        }
        
        int main(){
            int choice, data;
            while(1){
                printf("1. Push\n");
                printf("2. Pop\n");
                printf("3. Print the top element\n");
                printf("4. Print all the elements of the stack\n");
                printf("5. Quit\n");
                printf("Enter your choice: ");
                scanf("%d", &choice);
        
                switch(choice){
                    case 1:
                        printf("Enter the element to be pushed: ");
                        scanf("%d", &data);
                        push(data);
                        break;
                    case 2:
                        data = pop();
                        printf("Deleted element is %d\n", data);
                        break;
                    case 3:
                        printf("the topmost element of the stack is %d\n" ,peek());
                        break;
                    case 4:
                        print();
                        break;
                    case 5: exit(1);
                    default:
                        printf("Wrong Choice\n");
                        break;
                }
            }
            return 0;
        }
        ```
        
    
- programs
    - reverse the elements of the sack by using 2 different temporary stacks
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node;
        struct node* push(int data, struct node* top);
        int isEmpty(struct node* top);
        struct node* pop(struct node* top);
        int peek(struct node* top);
        
        struct node {
            int data;
            struct node* link;
        };
        
        struct node* push(int data, struct node* top){
            struct node* newNode = malloc(sizeof(struct node));
            //checking for stack overflow
            if(newNode == NULL){
                printf("Stack Overflow");
                exit(1);
            }
            newNode->data= data;
            newNode->link = NULL;
        
            newNode->link = top;
            top = newNode;
            return top;
        }
        
        struct node* pop(struct node* top){
            struct node* temp;
            if (isEmpty(top)){
                printf("Stack Underflow.");
                exit(1);
            }
            temp = top;
            top = top->link;
            return temp;
        }
        
        int isEmpty(struct node* top){
            if(top == NULL)
                return 1;
            else
                return 0;
        }
        
        void print(struct node* top){
            struct node* ptr = top;
            if(isEmpty(top)){
                printf("Stack Underflow.");
                exit(1);
            }
            printf("The stack elements are: ");
            while(ptr != NULL){
                printf("%d ", ptr->data);
                ptr = ptr->link;
            }
            printf("\n");
        }
        
        int peek(struct node* top){
            if(isEmpty(top)){
                printf("Stack Underflow");
                exit(1);
            } return top->data;
        }
        
        int count(struct node* top){
            if(top == NULL)
                return 0;
            int count = 0;
            struct node* temp = top;
            while(temp!=NULL){
                count++;
                temp = temp -> link;
            }
            return count;
        }
        
        int main(){
            struct node* top = NULL;
            struct node* top1 = NULL;
            struct node* top2 = NULL;
            struct node* temp;
        
            top = push(1, top); //you can either do this or return top from the push function
            top = push(2, top);
            top = push(3, top);
            int originalLength = count(top);
            print(top);
            for(int i = 0; i<originalLength; i++)
            {
                temp = pop(top);
                top = temp->link;
                top1 = push(temp->data, top1);
            }
            print(top1);
        
            for(int i=0; i<originalLength; i++){
                temp = pop(top1);
                top1 = temp->link;
                top2 = push(temp->data, top2);
            }
        
            print(top2);
            return 0;
        }
        ```
        
    - palindrome
        
        Let’s say someone has provided a string of characters formed with all a’s and b’s.
        
        The string is marked with a special character X which represents the middle of the string. (For example: aaaXbbb, ababaXabab..)
        
        With all this information, write a program to check whether the given string is a palindrome or not.
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        
        struct node;
        void push(int data);
        int isEmpty();
        int pop();
        int peek();
        
        struct node {
            int data;
            struct node* link;
        } *top = NULL;
        
        void push(int data){
            struct node* newNode = malloc(sizeof(struct node));
            //checking for stack overflow
            if(newNode == NULL){
                printf("Stack Overflow");
                exit(1);
            }
            newNode->data= data;
            newNode->link = NULL;
        
            newNode->link = top;
            top = newNode;
        }
        
        int pop(){
            struct node* temp;
            int val;
            if (isEmpty(top)){
                printf("Stack Underflow.");
                exit(1);
            }
            temp = top;
            val = temp->data;
            top = top->link;
            free(temp);
            temp = NULL;
            return val;
        }
        
        int isEmpty(){
            if(top == NULL)
                return 1;
            else
                return 0;
        }
        
        void print(struct node* top){
            struct node* ptr = top;
            if(isEmpty(top)){
                printf("Stack Underflow.");
                exit(1);
            }
            printf("The stack elements are: ");
            while(ptr != NULL){
                printf("%d ", ptr->data);
                ptr = ptr->link;
            }
            printf("\n");
        }
        
        int peek(){
            if(isEmpty()){
                printf("Stack Underflow");
                exit(1);
            } return top->data;
        }
        
        int count(struct node* top){
            if(top == NULL)
                return 0;
            int count = 0;
            struct node* temp = top;
            while(temp!=NULL){
                count++;
                temp = temp -> link;
            }
            return count;
        }
        
        void palindrome_check(char *s){
            int i = 0;
            char val;
            while(s[i] != 'X'){
                push(s[i]);
                i++;
            }
            i++;
            while(s[i] != NULL){
                if(isEmpty() || s[i] != pop()){
                    printf("The string is not a palindrome");
                    exit(1);
                }
                i++;
            }
            if(isEmpty()){
                printf("The string is a palindrome");
            }else{
                printf("The string is not a palindrome");
            }
        }
        
        int main(){
            char s[100];
            printf("Please enter the string: ");
            scanf("%s", s);
        
            palindrome_check(s);
            return 0;
        }
        ```
        
    - nested brackets
        1. create an empty stack.
        2. scan the symbols of the expressions from left to right.
        3. if the symbol is a left bracket, then push that symbol onto the stack.
        4. if the symbol is a right bracket, do the following
            1. if the stack is empty,
                
                print “Invalid expression: Right brackets are more than the left brackets.”
                
            2. else
                
                pop an element from the stack.
                
                if the popped bracket does not match with right bracket
                
                printf “Invalid expression: Mismatched brackets.”
                
        5. after scanning all the symbols of expression
            1. if stack is empty
                
                print “Valid expression: brackets are well balanced.”
                
            2. else
                
                print “invalid expression: left brackets are more than right brackets.”
                
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #include <string.h>
        
        int isEmpty();
        void push(char);
        char pop();
        int isMatching(char, char);
        
        struct node {
            char c;
            struct node* link;
        }* top = NULL;
        
        int main(){
            char* str = "((a, b))}}}}}}";
            for(int i=0; i<strlen(str); i++){
                if(str[i] == '(' || str[i] == '{' || str[i] == '['){
                    push(str[i]);
                }
                if(str[i] == ')' || str[i] == '}' || str[i] ==']'){
                    if(isEmpty()){
                        printf("Invalid expression: Right brackets are more than the left brackets");
                        exit(1);
                    }
                    if(!isMatching(pop(), str[i])){
                        printf("invalid expression: Mismatched brackets");
                    }
                }
            }
            if(isEmpty()){
                printf("Valid expression: brackets are well balanced.");
            }else{
                printf("Invalid expression: left brackets are more than right brackets.");
            }
        }
        
        void push(char data){
            struct node* newNode = malloc(sizeof(struct node));
            if(newNode == NULL){
                printf("Stack Overflow");
                exit(1);
            }
            newNode->c = data;
            newNode->link = NULL;
        
            newNode->link = top;
            top = newNode;
        }
        
        char pop(){
            if(isEmpty()){
                printf("Stack Underflow");
                exit(1);
            }
            char value = top->c;
            struct node* temp = top;
            top = top->link;
            free(temp);
            temp = NULL;
            return value;
        }
        
        int isEmpty(){
            if(top == NULL)
                return 1;
            else
                return 0;
        }
        
        int isMatching(char a, char b){
            if(a=='(' && b==')'){
                return 1;
            }
            if(a=='{' && b=='}'){
                return 1;
            }
            if(a=='[' && b==']'){
                return 1;
            }
            return 0;
        }
        ```
        
    - Infix to Postfix
        - examples of Infix operations
            
            ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20129.png)
            
        - examples of Postfix operations
            
            infix operation: A+B/C*D-E/(F+G)
            
            to …
            
            postfix operation: ABC/D*+EFG+/-
            
        - converting infix to postfix
            
            ```c
            #include <stdio.h>
            #include <stdlib.h>
            #include <string.h>
            #define MAX 100
            
            //Scan the symbols of the given postfix expression from left to right
            /*
            and for each symbol, do the following:
            1. If symbol is an operand
                    push it on the stack
            2. If symbol is an operator
                    Pop two symbols out of the stack and apply the operator on these symbols.
                    Push the result on the stack
            3. After scanning all the symbols of the postfix expression, pop the remaining 
               symbol out of the stack and print it on the screen. The remaining symbol 
               is the result obtained after evaluating the postfix expression.
            */
            
            //if met the operator,
            /*
            if the precedence of operators in the stack are greater than or equal to the
            current operator, then pop the operators out of the stack and store all the operators
            in the postfix array else simply push the current operator onto the stack.
            */
            char stack[MAX];
            char infix[MAX], postfix[MAX];
            int top = -1;
            
            void push(char);
            char pop();
            int isEmpty();
            void inToPost();
            int space(char);
            void print();
            int precedence(char);
            
            int main()
            {
                printf("Enter the infix expression: ");
                gets(infix);
                
                inToPost();
                print();
                return 0;
            }
            
            void inToPost(){
                int i, j=0;
                char symbol, next;
                for(i=0; i<strlen(infix); i++){
                    symbol = infix[i];
                    if(!space(symbol)){switch(symbol){
                        case '(': 
                            push(symbol);
                            break;
                        case ')':
                            while((next=pop()) != '(')
                                postfix[j++] = next;
                            break;
                        case '+':
                        case '-':
                        case '*':
                        case '/':
                        case '^':
                            while(!isEmpty() && precedence(stack[top]) >= precedence(symbol))
                                postfix[j++] = pop();
                            push(symbol);break;
                        default:
                            postfix[j++] = symbol;
                    }}
                }
                while(!isEmpty()){
                    postfix[j++] = pop();
                }
                postfix[j] = '\0';
            }
            
            int space(char c){
                if(c == ' ' || c == '\t')
                    return 1;
                else
                    return 0;
            }
            
            int precedence(char symbol){
                switch(symbol){
                    case '^':
                        return 3;
                    case '/':
                    case '*':
                        return 2;
                    case '+':
                    case '-':
                        return 1;
                    default:
                        return 0;
                }
            }
            
            void print(){
                int i=0;
                printf("The equivalent postfix expression is: ");
                while(postfix[i]){
                    printf("%c", postfix[i++]);
                }
                printf("\n");
            }
            
            void push(char c){
                if(top == MAX - 1){
                    printf("Stack Overflow\n");
                    return;
                }
                top++;
                stack[top] = c;
            }
            
            char pop(){
                char c;
                if(top == -1){
                    printf("Stack underflow\n");
                    exit(1);
                }
                c = stack[top];
                top = top - 1;
                return c;
            }
            
            int isEmpty(){
                if(top == -1)
                    return 1;
                else
                    return 0;
            }
            ```
            
        - evaluate the postfix expression
            
            Scan the symbols of the given postfix expression from left to right and for each symbol, do the following:
            
            1. If symbol is an operand
                
                Push it on the stack.
                
            2. If symbol is an operator
                
                Pop two symbols out of the stack and apply the operator on these symbols.
                
                Push the result on the stack 
                
            3. After scanning all the symbols of the postfix expression, pop the remaining symbol out of the stack and print it on the screen. The remaining symbol is the result obtained after evaluating expression.
                
                ```c
                #include <stdio.h>
                #include <stdlib.h>
                #include <string.h>
                #include <math.h>
                #define MAX 100
                
                int stack[MAX];
                char infix[MAX], postfix[MAX];
                int top = -1;
                
                void push(char);
                char pop();
                int isEmpty();
                void inToPost();
                int space(char);
                void print();
                int post_eval();
                int precedence(char);
                
                int main()
                {
                    int result;
                    printf("Enter the infix expression: ");
                    gets(infix);
                
                    inToPost();
                    result = post_eval();
                    print();
                    printf("result is %d", result);
                    return 0;
                }
                
                int post_eval(){
                    int i, a, b;
                    for(i=0; i<strlen(postfix); i++){
                        if(postfix[i] >= '0' && postfix[i]<= '9')
                            push(postfix[i] - '0');
                        else {
                            a = pop();
                            b = pop();
                            switch(postfix[i]) {
                                case '+':
                                    push(b+a);break;
                                case '-':
                                    push(b-a);break;
                                case '*':
                                    push(b*a);break;
                                case '/':
                                    push(b/a);break;
                                case '^':
                                    push(pow(b, a)); break;
                            }
                        }
                    }
                    return pop();
                }
                
                void inToPost(){
                    int i, j=0;
                    char symbol, next;
                    for(i=0; i<strlen(infix); i++){
                        symbol = infix[i];
                        if(!space(symbol)){switch(symbol){
                                case '(':
                                    push(symbol);
                                    break;
                                case ')':
                                    while((next=pop()) != '(')
                                        postfix[j++] = next;
                                    break;
                                case '+':
                                case '-':
                                case '*':
                                case '/':
                                case '^':
                                    while(!isEmpty() && precedence(stack[top]) >= precedence(symbol))
                                        postfix[j++] = pop();
                                    push(symbol);break;
                                default:
                                    postfix[j++] = symbol;
                            }}
                    }
                    while(!isEmpty()){
                        postfix[j++] = pop();
                    }
                    postfix[j] = '\0';
                }
                
                int space(char c){
                    if(c == ' ' || c == '\t')
                        return 1;
                    else
                        return 0;
                }
                
                int precedence(char symbol){
                    switch(symbol){
                        case '^':
                            return 3;
                        case '/':
                        case '*':
                            return 2;
                        case '+':
                        case '-':
                            return 1;
                        default:
                            return 0;
                    }
                }
                
                void print(){
                    int i=0;
                    printf("The equivalent postfix expression is: ");
                    while(postfix[i]){
                        printf("%c", postfix[i++]);
                    }
                    printf("\n");
                }
                
                void push(char c){
                    if(top == MAX - 1){
                        printf("Stack Overflow\n");
                        return;
                    }
                    top++;
                    stack[top] = c;
                }
                
                char pop(){
                    char c;
                    if(top == -1){
                        printf("Stack underflow\n");
                        exit(1);
                    }
                    c = stack[top];
                    top = top - 1;
                    return c;
                }
                
                int isEmpty(){
                    if(top == -1)
                        return 1;
                    else
                        return 0;
                }
                ```
                
        

### Queues

First In First Out (or Last In Last Out)

- operations:
    - insertion at tail/rear → `enqueue(param a)`
    - deletion at head/front → `dequeue()`
    - front()/peek()
    - isFull()
    - isEmpty()
- things to consider (implemented by array)
    - whatever between front and rear pointer is the span of a queue.
    - overflow condition: when enqueue to the full-width array
    - underflow condition: when dequeue to the empty array
    
- linear queue implementation (using array)
    
    ```c
    #include <stdlib.h>
    #include <stdio.h>
    
    # define N 5
    int queue[N];
    
    void enqueue(int);
    void display();
    void peek();
    void dequeue();
    
    int front, rear = -1;
    
    int main(){
        enqueue(2);
        enqueue(5);
        enqueue(-1);
        display();
        peek();
        dequeue();
        peek();
        display();
        return 0;
    }
    
    void enqueue(int num){
        if(front == -1 && rear == -1){
            front++;
            rear++;
            queue[front] = num;
            printf("enqueued element: %d\n", queue[rear]);
        }else if(rear == N - 1){
            printf("queue overflow\n");
            return;
        }else{
            rear++;
            queue[rear] = num;
            printf("enqueued element: %d\n", queue[rear]);
        }
    }
    
    void dequeue(){
        if(rear == -1){
            printf("queue underflow\n");
        }else if(rear == front){
            printf("dequeued element: %d\n",queue[front]);
            front = rear = -1;
        }else{
            printf("dequeued element: %d\n",queue[front]);
            front++;
        }
    }
    
    void display(){
        if(front == -1 && rear == -1){
            printf("nothing is in the queue.\n");
        }else{
            printf("current queue is: ");
            for(int i = front; i<rear+1; i++){
                printf("%d ", queue[i]);
            }
            printf("\n");
        }
    }
    
    void peek(){
        if(front == -1 && rear == -1){
            printf("noting is in the queue.\n");
        }else{
            printf("the peek is %d\n", queue[front]);
        }
    }
    ```
    
    drawback: 
    
    when did enqueue(int num) 5 times and dequeued couple times, even though there are some spaces left, we cannot enqueue more because the rear = N - 1 
    
    → need of the circular queue.
    
- queue implementation (using LinkedList)
    
    you could either enqueue from the rear and dequeue from the the front or enqueue from the front and dequeue from the rear.
    
    - it is essential to maintain the front and rear pointers for the sake of the time complexity.
    - OUPUT:
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20130.png)
    
    ```c
    #include <stdlib.h>
    #include <stdio.h>
    
    void enqueue(int);
    void display();
    void peek();
    void dequeue();
    
    struct node {
        int data;
        struct node* link;
    };
    struct node* front = NULL;
    struct node* rear = NULL;
    
    int main(){
        enqueue(5);
        enqueue(0);
        enqueue(-3);
        display();
        dequeue();
        peek();
    }
    
    void enqueue(int data){
        struct node* newNode = malloc(sizeof(struct node));
        newNode->data = data;
        newNode->link = NULL;
        if(front == NULL && rear==NULL){
            front = rear = newNode;
        }else{
            rear->link = newNode;
            rear = rear->link;
        }
    }
    
    void dequeue(){
        if(front==NULL && rear==NULL){
            printf("queue underflow\n");
            exit(1);
        }else if(front == rear){
            free(front);
            front = NULL;
            rear = NULL;
        }else{
            struct node* temp = front;
            printf("dequeued %d.\n", temp->data);
            front = temp->link;
            free(temp);
            temp = NULL;
        }
    }
    
    void display(){
        if(front == NULL && rear == NULL){
            printf("There is no node to display in the queue.\n");
        }else{
            struct node* temp = front;
            while(temp != NULL){
                printf("%d ", temp->data);
                temp = temp->link;
            }
            printf("\n");
        }
    }
    
    void peek(){
        if(front == NULL && rear == NULL){
            printf("There is no node to peek in the queue.\n");
        }else{
            printf("the top node in the queue is %d\n", front->data);
        }
    }
    ```
    
- circular queue implementation (using array)
    
    the identified drawback of the linear queue was that when rear reaches the end of the array, even though there are some spaces left since we dequeued a little bit, we cannot enqueue more in that condition.
    
    ```c
    #include <stdlib.h>
    #include <stdio.h>
    
    void enqueue(int);
    void display();
    void peek();
    void dequeue();
    
    #define N 5
    int queue[N];
    int front = -1;
    int rear = - 1;
    
    int main(){
        enqueue(2);
        enqueue(-1);
        enqueue(5);
        enqueue(6);
        enqueue(7);
        display();
        dequeue();
        dequeue();
        dequeue();
        display();
        enqueue(0);
        display();
        peek();
    
        return 0;
    }
    
    void enqueue(int data){
        if(front == -1 && rear == -1){
            front = rear = 0;
            queue[rear] = data;
        }
        else if((rear+1)%N == front){
            printf("queue is full, can't enqueue more.\n");
            exit(1);
        }else{
            queue[(rear+1)%N] = data;
            rear = (rear+1)%N;
            printf("enqueued %d.\n", data);
        }
    }
    
    void dequeue(){
        if(front == -1 && rear == -1){
            printf("queue is empty, can't dequeue more.\n");
            exit(1);
        }else if(front == rear){
            printf("dequeued %d.\n", queue[front]);
            front = rear = -1;
        }else{
            printf("dequeued %d.\n", queue[front]);
            front = (front+1)%5;
        }
    }
    
    void display(){
        int i = front;
        if(front==-1 && rear==-1){
            printf("queue is empty.\n");
        }else{
            printf("queue is: ");
            while(i != rear){
                printf("%d ", queue[i]);
                i = (i+1)%N;
            }
            printf("%d\n", queue[rear]);
        }
        printf("\n");
    }
    
    void peek(){
        if(front==-1 && rear==-1){
            printf("queue is empty\n");
        }else{
            printf("result of the peek: %d\n", queue[front]);
        }
    
    }
    ```
    
- circular queue implementation (using Linked List)
    
    ```c
    #include <stdlib.h>
    #include <stdio.h>
    
    void enqueue(int);
    void display();
    void peek();
    void dequeue();
    
    struct node{
        int data;
        struct node* link;
    };
    
    struct node* front = NULL;
    struct node* rear  = NULL;
    
    int main() {
        enqueue(2);
        enqueue(-1);
        enqueue(5);
        display(); //2 1 5
        dequeue();
        peek();//result of the peek -1
    }
    
    void enqueue(int data){
        struct node* newNode = malloc(sizeof(struct node));
        newNode->data = data;
        newNode->link = NULL;
        if(rear == NULL){
            front = rear = newNode;
            rear->link = newNode;
        }else{
            rear->link = newNode;
            rear = rear -> link;
            rear->link = front;
        }
    }
    
    void dequeue(){
        struct node* temp = front;
        if(front == NULL && rear == NULL){
            printf("there is no node to dequeue.\n");
        }else if( front == rear){
            free(temp);
            temp = front = rear = NULL;
        }else{
            front = temp->link;
            rear = temp->link;
            free(temp);
            temp = NULL;
        }
    }
    
    void peek(){
        if(front == NULL && rear == NULL){
            printf("there is no node to peek\n");
        }else{
            printf("result of the peek: %d\n", front->data);
        }
    }
    
    void display(){
        if(front == NULL & rear == NULL){
            printf("there is no node to display.\n");
        }else{
            struct node* temp = front;
            while(temp->link != front){
                printf("%d ", temp->data);
                temp = temp->link;
            }
            printf("%d \n", temp->data);
        }
    }
    ```
    
- Implementation of queue using stacks
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20131.png)
    
    when enqueued, from push to stack A. when dequeued, pop all the elements in stack A to the stack B and  pop one from stack B and pop to A one by one.
    
    given that stack A is filled, 
    
    time complexity of enqueue: O(1)
    
    time complexity of dequeue: O(n)
    
    ```c
    #include <stdlib.h>
    #include <stdio.h>
    
    void enqueue(int);
    void display();
    void peek();
    void dequeue();
    void push1(int);
    void push2(int);
    int pop1();
    int pop2();
    
    #define N 5
    int S1[N], S2[N];
    int top1 = -1, top2 = -1;
    int count=0;
    
    int main() {
        enqueue(2);
        enqueue(-1);
        enqueue(5);
        display();
        dequeue();
        enqueue(7);
        display();
    }
    
    void enqueue(int data){
        push1(data);
        count++;
    }
    
    void dequeue(){
        if(top1 == -1 && top2 == -1){
            printf("queue is empty.\n");
        }
        for(int i=0; i<count;i++){
            push2(pop1());
        }
        printf("dequeued %d\n", pop2());
        count--;
        for(int i=0; i<count; i++){
            push1(pop2());
        }
    }
    
    void push1(int data){
        if(top1 == N-1){
            printf("stack overflow.\n");
        }else{
            top1++;
            S1[top1] = data;
        }
    }
    
    int pop1(){
        if(top1 == -1){
            printf("stack underflow.\n");
            exit(1);
        }else{
            top1--;
            return S1[top1+1];
        }
    }
    
    void push2(int data){
        if(top2 == N-1){
            printf("stack overflow.\n");
        }else{
            S2[top2+1] = data;
            top2++;
        }
    }
    
    int pop2(){
        if(top2 == -1){
            printf("stack underflow.\n");
            exit(1);
        }else{
            top2--;
            return S2[top2+1];
        }
    }
    
    void display(){
        if(top1 == -1){
            printf("there is nothing to display.\n");
        }else{
            for(int i=count-1; i>-1; i--){
                printf("%d ", S1[i]);
            }
            printf("\n");
        }
    }
    ```
    
- DEQUE (Double Ended Queue)
    
    insertion and deletion are allowed in both ends.
    
    it has both LIFO and FIFO properties.
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20132.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20133.png)
    
    - deque implementation (circular array)
        
        ```c
        #include <stdlib.h>
        #include <stdio.h>
        
        #define N 5
        int deque[N];
        int f=-1, r=-1;
        void enqueueFront(int);
        void enqueueRear(int);
        void dequeueFront();
        void dequeueRear();
        void display();
        void getFront();
        
        int main(){
            enqueueFront(2);
            enqueueFront(5);
            enqueueRear(-1);
            enqueueRear(0);
            enqueueFront(7);
            enqueueFront(4);
            display();
        
            return 0;
        }
        
        void enqueueFront(int x){
            if((f==0 && r==N-1) || f==r+1){
                printf("deque is full\n");
            }else if(f==-1 && r==-1){
                f=r=0;
                deque[f] = x;
            }else if(f==0){
                f=N-1;
                deque[f] = x;
            }else{
                f--;
                deque[f] = x;
            }
        }
        
        void enqueueRear(int x){
            if((f==0 && r==N-1) || f==r+1){
                printf("deque is full\n");
            }else if(f==-1 && r==-1){
                f=r=0;
                deque[f] = x;
            }else if(r==N-1){
                r=0;
                deque[r] = x;
            }else{
                r++;
                deque[r] = x;
            }
        }
        
        void display(){
            int i = f;
            if(f==-1 && r==-1){
                printf("queue is empty.\n");
            }else{
                printf("queue is: ");
                while(i != r){
                    printf("%d ", deque[i]);
                    i = (i+1)%N;
                }
                printf("%d\n", deque[r]);
            }
            printf("\n");
        }
        
        void getFront(){
            if((f==0 && r==N-1) || f==r+1){
                printf("deque is full\n");
            }else{
                printf("%d\n", deque[f]);
            }
        }
        
        void dequeueFront(){
            if(f==-1 && r==-1){
                printf("deque is empty.\n");
            }else if(f==r){
                f=r=-1;
            }else{
                f=(f+1)%N;
            }
        }
        
        void dequeueRear(){
            if(f==-1 && r==-1){
                printf("deque is empty.\n");
            }else if(f==r){
                f=r=-1;
            }else if(r==0){
                r = N-1;
            }else{
                r= (r-1)%N;
            }
        }
        ```
        

---

### Trees

![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20134.png)

```c
/*
- **nodes**=> A, B, C, D, E, F, G, H, I, G, K
- **root**: A
- **parent node**: F is a parent of J and K
- **child node**: J&K are children of F
- **leaf node:** I, J, K
- **non-leaf node**: A, B, C, D, E, F, G, H
- **path:** sequence of consecutive edges from source node to destination node
- **ancestor:** any predecessor node on the path from the root to that node
- **descendant:** any successor node on the path from that node to the leaf node.
- **sub-tree:** a group of all the nodes from the root and all its descendants.
sibling: nodes that share the same parent.
degree: the number of the children of that node ex) degree of F = 2. If we were asked the degree of the whole tree, we say the largest degree of a node. here, 2.
- **depth of node:** length of the path from the root to that node. depth of A: 0,B: 1,  J:3.
- **height of node:** no. of edges in the longest path from that node to a leaf.
- **height of A:**3
- level of tree = height of tree
level of node != height of node
*/
```

- Binary tree
    
    each node can have at most 2 children
    
    possible binary trees
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20135.png)
    
    **maximum nodes per level: 
    
    $$
    2^n, where\ n\ is\ level
    $$
    
    **maximum nodes up to level: $2^{h+1}-1$, where h is height
    
    → which means,
    
    $$
    n: {maximum\ nodes\ up\ to\ height} \newline n = 2^{h+1}-1 \newline n+1=2^{h+1}\newline log_2(n+1)=log_2(2^{h+1})\newline h+1=log_2(n+1) \newline h=log_2(n+1)-1
    $$
    
    **types of binary tree
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20136.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20137.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20138.png)
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20139.png)
    
    full binary tree: binary tree in which every parent node/internal node has either two or no children.
    
    complete binary tree: completely filled (except possibly the last level) and the last level has nodes as to the left as possible. 
    
    perfect binary tree: all internal nodes have 2 children and all leaves are at the same level
    
    |  | max nodes | min nodes | traits |
    | --- | --- | --- | --- |
    | full binary tree | 2^(h+1)-1 | 2h+1 | no. of leaf = no. of internal nodes + 1 |
    | binary tree | 2^(h+1)-1 | h+1 |  |
    | complete binary tree | 2^(h+1) - 1 | 2^h |  |
    | perfect binary tree | 2^(h+1) - 1 | 2^(h+1) - 1 |  |
    
    |  | min height | max height | traits |
    | --- | --- | --- | --- |
    | full binary tree | log_2(n+1)-1 | (n-1)/2 | no. of leaf = no. of internal nodes + 1 |
    | binary tree | log_2(n+1)-1 | n-1 |  |
    | complete binary tree | log_2(n+1)-1 | log_2(n) |  |
    | perfect binary tree | log_2(n+1)-1 | log_2(n+1)-1 |  |
    - binary tree implementation using recursion
        
        ```c
        #include <stdlib.h>
        #include <stdio.h>
        
        struct node{
            int data;
            struct node *left, *right;
        };
        
        struct node* create();
        
        int main(){
            struct node* root = create();
            return 0;
        }
        
        struct node* create(){
            int x;
            struct node* newNode= malloc(sizeof(struct node));
            printf("enter the data.\n");
            scanf("%d", &x);
            if(x==-1){
                return 0;
            }
            newNode->data = x;
            printf("enter the left child of %d", x);
            newNode->left = create();
            printf("enter the right child of %d", x);
            newNode->right = create();
            return newNode;
        }
        ```
        
        Depth First.
        
    - binary tree traversals(inorder, preorder and postorder)
        
        inorder = Left Root Right
        
        preorder= Root Left Right
        
        postorder= Left Right Root
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20140.png)
        
        Inorder - B D A G E C H F I
        
        Preorder - A B D C E G F H I
        
        Postorder - D B G E H I F C A 
        
    - array representation of binary tree (sequential representation)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20141.png)
        
        case1
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20142.png)
        
        $$
        if\ a\ node\ is\ at\ i^{th}\ index, \newline left\ child\ would\ be\ at:\ [(2*i)+1] \newline right\ child\ would\ be\ at:\ [(2*i)+2] \newline parent\ would\ be\ at:\ [(i-1)/2]
        $$
        
        case2
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20143.png)
        
        $$
        if\ a\ node\ is\ at\ i^{th}\ index, \newline left\ child\ would\ be\ at:\ [(2*i)] \newline right\ child\ would\ be\ at:\ [(2*i)+1] \newline parent\ would\ be\ at:\ [i/2]
        $$
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20144.png)
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20145.png)
        
        when blue was given, red is empty node
        
        given an incomplete tree, you have to make it complete tree by adding empty nodes for the formulas to work properly.
        
        ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20146.png)
        
    - inorder, preorder, postorder implementation
        
        as discussed, 
        
        inorder: left root right
        
        preorder: root left right
        
        post order: left right root
        
        ```c
        #include <stdlib.h>
        #include <stdio.h>
        
        struct node{
            int data;
            struct node *left, *right;
        };
        
        struct node* create();
        void preorder(struct node* root);
        void inorder(struct node* root);
        void postorder(struct node* root);
        
        int main(){
            struct node* root = create();
            printf("Pre-order\n");
            return 0;
        }
        
        void preorder(struct node *root){
            if(root == NULL){
                return;
            }
            printf("%d", root->data);
            preorder(root->left);
            preorder(root->right);
        }
        
        void inorder(struct node *root){
            if(root == NULL){
                return;
            }
            inorder(root->left);
            printf("%d", root->data);
            inorder(root->right);
        }
        
        void postorder(struct node *root){
            if(root == NULL){
                return;
            }
            postorder(root->left);
            postorder(root->right);
            printf("%d", root->data);
        }
        
        struct node* create(){
            int x;
            struct node* newNode= malloc(sizeof(struct node));
            printf("enter the data.\n");
            scanf("%d", &x);
            if(x==-1){
                return 0;
            }
            newNode->data = x;
            printf("enter the left child of %d", x);
            newNode->left = create();
            printf("enter the right child of %d", x);
            newNode->right = create();
            return newNode;
        }
        ```
        
    
- Binary Search Tree
    
    In [computer science](https://en.wikipedia.org/wiki/Computer_science), a **binary search tree** (**BST**), also called an **ordered** or **sorted binary tree**, is a [rooted](https://en.wikipedia.org/wiki/Rooted_tree) [binary tree](https://en.wikipedia.org/wiki/Binary_tree) [data structure](https://en.wikipedia.org/wiki/Data_structure) with the key of each internal node being greater than all the keys in the respective node's left subtree and less than the ones in its right subtree. The time complexity of operations on the binary search tree is linear with respect to the height of the tree. duplicates are not allowed in BST.
    
    - insertion and deletion
        
        for deletion, you will mostly likely to have three situations
        
        1. deleting a node with no child
            1. you can just delete it.
        2. deleting a node with one child
            1. you link the node’s child and the parent 
            2. you delete the node
            
            1. replace the node with the child node.
            2. delete the child node(leaf)
        3. deleting a node with two children
            1. make sure you replace the inorder preceder OR inorder successor with the node you want to delete
            2. delete the node
        
    
    When something grows exponentially, it’s being multiplied. When something grows logarithmically, it is being divided. 
    
    Access/Search: $worst\ case: O( n) \ best\ case: O(log_2n)$
    
    When trying to access or search for a particular node of a tree, you have to start a the top, or the root. Say we’re trying to get to the node with the value of 4. say we must access from 5. We know the value we’re searching for is less than 5 so that means the value can be found somewhere in the left/right branches. → this effectively get rid of our choices, allowing use to rule of the nodes with higher values. 
    
    Insert/Delete: $worst\ case: O( n) \ best\ case: O(log_2n)$
    
    Exactly the same as access/search, in order to insert an element or delete an element of any given value, at most we need to search one branch from each node from the time. 
    
- AVL Tree
    
    As introduced in the BST section, to guarantee the time complexity of $O(log_2(n))$ for insertoin/deletion/search, the tree has to be balanced. To obtain the balanced tree, not left or right skewed, we can use the AVL tree.
    
    the AVL tree a is binary tree where the absolute value of the height of left sub tree - the height of right sub tree is either 0 or 1. set of {-1, 0, 1} are called the balanced factor. you calculate the **balance factor** for each  node and balance the tree on the factor is out of range.
    
    Insertion in AVL Tree
    
    ![Untitled](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Untitled%20147.png)
    
    - simple trick for left rotation → right rotation / right rotation → left rotation/ left rotation/ right rotation
        
        always the median value of the three will be the root of the updated tree.
        
    
    Deletion in AVL Tree
    
    Since AVL Tree is essentially a BST, the basic deletion process is the same as that of BST. After the deletion, we additionally have to check the balance factor for each node again and apply corresponding changes.
    

[Red-Black Tree](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/Red-Black%20Tree%2049d98c5c7a5d4d0aa133f1e7e0b686fc.md)

- Splay Tree
    
    another variance of binary search tree.
    
    splay tree는 삽입, 삭제, 검색의 연산을 수행한 뒤, splay를 통해 최근에 접근한 노드를 루트에위치시켜 트리를 재구성 합니다. 즉, 자주 탐색하는 키를 가진 노드를 루트에 가깝게 위치하도록 구성하여 연산의 효율성을 높입니다.
    
    - roughly balanced tree
    - insertion
        
        the basic insertion process is the same as the binary search tree, but the splaying part is added at the end of each insertion.
        
    - deletion
        
        the basic deletion process is te same as the binary search tree, but the splaying part is added at the end of each deletion.
        

[B-Tree](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/B-Tree%20ba0d691dfbe34ef4bb568bd2ae8039d0.md)

- B+ Tree
    
    B+ tree is a variation of the B-tree data structure. In a B+ tree, data pointers are stored only at the leaf nodes of the tree. In a B+ tree, the structure of a leaf node differs from that of internal nodes.
    
    - always grows towards root
    - all the data should be presented in the leaf nodes
    - searching is very easy when stored in B+ tree
    
    order ($m$) = 4
    
    max children = $m$ = 4
    
    min children = $[\frac{m}{2}]$ = 2
    
    max keys = $(m-1)$ = 3
    
    min keys = $[\frac{m}{2}]-1$ = 1
    

[C++](C%20C++%20fb024cca155a4cd482d5fe57c5fdb39e/C++%20662ee454b48547d8a663ad0510b65469.md)