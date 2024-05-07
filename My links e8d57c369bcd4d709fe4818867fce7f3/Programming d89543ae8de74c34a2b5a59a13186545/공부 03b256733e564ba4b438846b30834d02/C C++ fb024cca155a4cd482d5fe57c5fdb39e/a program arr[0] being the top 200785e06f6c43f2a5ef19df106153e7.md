# a program arr[0] being the top

author: Jewook Park

the benefits of keeping the top element at arr[0]

- we don’t need a variable named “top” to keep track of the topmost element. But we have to keep track of the first element, the course says.

```c
void push(int data){
		int i;
		first += 1;
		for(i = first; i>0; i--)
				//switching values
				stack_arr[i]  = stack_arr[i-1];
		stack_arr[0] = data;
}
```

this is what I got for my course code. However, I personally think if the array size get bigger, this code inherently costs lots of calculations, memory spaces, etc. In this code, `stack_arr[i-1]` is allocated to the `stack_arr[i]`. This allocation part of the code is inside the for loop as well. 

In such code, when i’th value gets pushed into the stack, the allocation happens i-1 times. This also could raise a situation where 100000th element cause (100000 - 1) times of value allocation. I considered this very calculation-costly, therefore I tried to come up with a better solution.

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX 6

/*
author: Jewook Park
*/
int stack_arr[MAX];
int second_top = -1;

void push(int data){
    second_top++;
    if(second_top != 0){
				//swtching the first and the last element.
        stack_arr[second_top] = data;
        int temp = stack_arr[second_top];
        stack_arr[second_top] = stack_arr[0];
        stack_arr[0] = temp;
    }else{stack_arr[0] = data;}
    printf("data added: %d\n", data);
}

void print(){
    if(second_top == - 1){
        printf("Stack underflow\n");
        exit(1);
    }
    printf("%d ", stack_arr[0]);
    for(int i = second_top; i>0; i--){
        printf("%d ", stack_arr[i]);
    }
}

int main(){
    push(20);
    push(30);
    push(40);
    push(50);
    push(60);
    print(); //60 50 40 30 20
		return 0;
}
```

In this code example, the principle of keeping the **top element** at `stack_arr[0]` is the same. However, the push() function and print() function got a bit tweaked. 

Rather than switching values for every element of the stack, it switches (in the array implementation wise) the first and the last element of the updated array, which ends up switching only 1 time even for the aforementioned 100000th value’s insertion. Of course, the print() function has to change to a function that prints `stack_arr[0]` first and prints the rest of the elements in a separate for loop.

I believe this method reduces the value allocation (which is true), thus reducing a little bit of time cost as well. Let me know if you have better alternatives.

- `pop()` function
    
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
    
    void print(){
        if(second_top == - 1){
            printf("Stack underflow\n");
            exit(1);
        }
        printf("%d ", stack_arr[0]);
        for(int i = second_top; i>0; i--){
            printf("%d ", stack_arr[i]);
        }
    }
    
    int main(){
        push(20);
        push(30);
        push(40);
        push(50);
        push(60);
        printf("%d \n",pop()); //60
        print(); // 50 40 30 20
        return 0;
    }
    ```
    
- `isEmpty()` & `isFull()` & `peek()` function
    
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
    
    void print(){
        if(second_top == - 1){
            printf("Stack underflow\n");
            exit(1);
        }
        printf("%d ", stack_arr[0]);
        for(int i = second_top; i>0; i--){
            printf("%d ", stack_arr[i]);
        }
    }
    
    int main(){
        push(20);
        push(30);
        push(40);
        push(50);
        push(60);
    		push(70);
    		printf("current peek is %d\n", peek()); //70
        if(isFull()){
            printf("the stack is full\n");
        } //the stack is full
        printf("%d \n",pop()); //70
        printf("%d \n",pop()); //60
        printf("%d \n",pop()); //50
        printf("%d \n",pop()); //40
        printf("%d \n",pop()); //30
        printf("%d \n",pop()); //20
        if(isEmpty()){
            printf("the stack is empty");
        } // the stack is empty
        return 0;
    }
    ```