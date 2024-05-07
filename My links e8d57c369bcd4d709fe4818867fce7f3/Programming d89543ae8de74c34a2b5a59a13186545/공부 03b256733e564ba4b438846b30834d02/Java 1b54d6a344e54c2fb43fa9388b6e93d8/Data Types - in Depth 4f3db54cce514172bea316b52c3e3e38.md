# Data Types - in Depth

Primitive Data Types

- Integer
    - byte, short, int, long
    - some examples using integers
        
        ```java
        public class Main {
          public static void main(String[] args) {
            BiNumber numbers = new BiNumber(2, 3);
            System.out.println(numbers.add());//5
            System.out.println(numbers.multiply());//6
            numbers.doubleNum();
            System.out.println(numbers.getNumber1());//4
            System.out.println(numbers.getNumber2());//6
          }
        }
        
        public class BiNumber {
        
          private int x;
          private int y;
        
          public BiNumber(int x, int y) {
            this.x = x;
            this.y = y;
          }
        
          public int add() {
            return this.x + this.y;
          }
        
          public int multiply(){
            return this.x * this.y;
          }
        
          public void doubleNum() {
            this.x *= 2;
            this.y *= 2;
          }
        
          public int getNumber1() {
            return this.x;
          }
        
          public int getNumber2() {
            return this.y;
          }
        }
        ```
        
- Floating Point
    - float, double
    - floats and doubles aren’t that accurate.
        - ex) 34.56789876 + 34.2234 ⇒ 68.79129875999999
    - so, you should use **BigDecimal class** when dealing with some important businesses
- BigDecimal class
    - BigDecimal is the only way to get the accurate calculation in Java.
    - BigDecimal objects are immutable once they are created.
    
    if you really want the accurate representation, use string as a parameter. When you use double, you will get an inaccurate value, such as 34.2234 → 34.223399999999999999840…
    
    ```java
    import java.math.BigDecimal;
    
    public class Main {
      public static void main(String[] args) {
        BigDecimal number1 = new BigDecimal("34.56789876");
        BigDecimal number2 = new BigDecimal("34.2234");
        BigDecimal number3 = number1.add(number2);
        System.out.println(number3); //68.79129876
      }
    }
    
    //you can do the addition to a BigDecimal object only with
    //another BigDecimal object.
    BigDecimal number = new BigDecimal("11.5");
    BigDecimal number2 = new BigDecimal("23.45678");
    number.add(number2); // 34.95679
    
    //therefore you cannot do this
    int i = 5;
    //number.add(i);
    /*
    Error:
    incompatible types: int cannot be converted to java.math.BigDecimal
    number.add(i)
    */
    
    //you can do this though
    number.add(new BigDecimal(i));
    ```
    
    ![Untitled](Data%20Types%20-%20in%20Depth%204f3db54cce514172bea316b52c3e3e38/Untitled.png)
    
    BigDecimal Exercise
    
    goal of this program is to get the total value, which is
    
    principal + principal*interest
    
    - My  code
    
    ```java
    //MAIN CLASS
    
    import java.math.BigDecimal;
    
    /*
    Simple Interest Formula
    Total amount = principal + principal*interest*noOfYears;
    */
    public class Main {
      public static void main(String[] args) {
        SimpleInterestCalculator calculator = new SimpleInterestCalculator("4500.00", "7.5");
        BigDecimal totalValue = calculator.calculateTotalValue(5);// 5years
    
        System.out.println(totalValue.toString());
      }
    }
    ```
    
    ```java
    import java.math.BigDecimal;
    
    public class SimpleInterestCalculator extends SuperCalculator {
      private String principal;
      private String interest;
    
      public SimpleInterestCalculator(String principal, String interest) {
        this.principal = principal;
        this.interest = interest;
      }
      @Override
      public BigDecimal converter(String str) {
        BigDecimal bd = new BigDecimal(str);
        return bd;
      }
    
      @Override
      public BigDecimal converter(int i) {
        BigDecimal bd = new BigDecimal(i);
        return bd;
      }
    
      public BigDecimal calculateTotalValue(int i) {
        return converter(this.principal)
            .add((converter(this.principal).multiply(converter(this.interest)).multiply(converter(i))));
      }
    }
    ```
    
    ```java
    import java.math.BigDecimal;
    
    abstract class SuperCalculator{
      public abstract BigDecimal converter(String str);
      public abstract BigDecimal converter(int i);
    }
    ```
    
    **retrospection:** what I did was I straight up created the SimpleInterestCaculator class and created the two variables that could go into the constructor. And automatically I did this.principal = principal; & this.interest = interest; by doing so, the variables’ types were fixed as String, forcing me to make functions that convert String values to BigDecimal values. To make two different convert() methods: one takes String value, and the other takes int value as a parameter, I had to create an abstract class, SuperCalculator,  which contains two different types of methods to be overridden in the child class, SimpleInterestCalculator class in this case.
    
    - Instructor’s code
    
    ```java
    //MAIN CLASS
    import java.math.BigDecimal;
    
    /*
    Simple Interest Formula
    Total amount = principal + principal*interest*noOfYears;
    */
    public class Main {
      public static void main(String[] args) {
        SimpleInterestCalculator calculator = new SimpleInterestCalculator("4500.00", "7.5");
        BigDecimal totalValue = calculator.calculateTotalValue(5);// 5years
    
        System.out.println(totalValue.toString());
      }
    }
    ```
    
    ```java
    import java.math.BigDecimal;
    
    BigDecimal principal;
    BigDecimal interest;
    
    public class SimpleInterestCalculator {
        public SimpleInterestCalculator(String principal, String interest){
        this.principal = new BigDecimal(principal);
        this.interest = new BigDecimal(interest);
      }
      
      public BigDecimal calculateTotalValue(int noOfYears){
        //total value = p+p*i*ny
        return principal.add(principal.multiply(interest).multiply(new BigDecimal(noOfYears)));
      }
    }
    ```
    
    **retrospection:** what the instructor of this course did was to set the principal and interest field as BigDecimal values first. Then he went on to create a constructor whose parameters are in String. Most importantly, however, the conversion, which happened in the individual methods in my case, happened in the constructor. As he set the field as BigDecimal values, when he called those fields by utilizing **this.** keyword, BigDecimal values were called and he was able to convert the String that’s inside the constructor into BigDecimal using **new** keywords.
    
    **Result:** this way the code became much faster and easier, as it didn’t use the unnecessary abstractions, nor the complicated methods.
    
- Boolean
    - boolean
    - true/false
    - &&(and), ||(or), ^(xor), !(not)
    - xor returns true only when the two values being compared are different. **true^false** ⇒ true | **false^true** ⇒ true | **false^false** ⇒ false | **true^true** ⇒ false
    - main difference between && and & ( || and | )
        
        in &&’s case, it checks the value to the left and if it’s false, it doesn’t even consider going through the right side of it. &, however, does consider it. example is below.
        
        ```java
        public class Main {
          public static void main(String[] args) {
            int j = 15;
            int i = 10;
            boolean b = (j > 15) && (i++ > 5);
            System.out.println(b); //false 
            System.out.println(i); //10
            
            boolean b1 = (j > 15) & (i++ > 5);
            System.out.println(b1); //false 
            System.out.println(i); //11
          }
        }
        ```
        
        the same logic applies to || and |
        
        ```java
        public class Main {
          public static void main(String[] args) {
            int j = 15;
            int i = 10;
            boolean b = (j == 15) || (i++ > 5);
            System.out.println(b); //true
            System.out.println(i); //10
            
            boolean b1 = (j == 15) | (i++ > 5);
            System.out.println(b1); //true
            System.out.println(i); //11
          }
        }
        ```
        
- Character
    - char
    - Defining Character Literals
        - Unicode Representation also can be used. Prefix with \u. Example: char letterA = ‘\u0041’;
        - A number value can also be assigned to character. Example: char letterB = 66; Numeric value can be from 0 to 65535;
        - Escape code can be used to represent a character that cannot be typed as literal. Example: char newLine = ‘\n’;
        - when  doing operations with int and char, the result would be int.
    - How are characters stored?
        - Unicode
        - Same as integer types
    - Same operators as Integer Data Types
        
        ```java
        char ch = a;
        char a = 97;
        char ch1 = 66000;//Compiler error
        ```
        
        ```java
        MyChar myChar = new MyChar('c');
        System.out.println(myChar.isVowel());//'a', 'e', 'i', 'u' and Capitals
        System.out.println(myChar.isNumber());
        System.out.println(myChar.isAlphabet());
        MyChar.printLowerCaseAlphabets();
        MyChar.printUpperCaseAlphabets();
        ```
        
    - some practices and playing with characters
- how to find the size, max value, etc. of the data types?
    
    USE THE WRAPPER CLASSES OF EACH DATA TYPE
    
    just for example, I used the Integer class to indicate how
    
    ```java
    public class Main{
      public static void main(String[] args){
        System.out.println(Integer.SIZE); //32
        System.out.println(Integer.BYTES); //4
        System.out.println(Integer.MAX_VALUE); //2147483647
        System.out.println(Integer.MIN_VALUE); //-2147483647
      }
    }
    ```
    
- pre increment, post increment (that of decrement)
    
    ```java
    int i = 10;
    //before the increment happens, assignment happens.
    j = i++; //at this point, j is 10, and i becomes 11.
    
    int i = 10;
    //before the assignment happens, the increment happens
    j = ++i; //at this point, both j and i are 11.
    
    int i = 10;
    //before the decrement happens, assignment happens.
    j = i--;//at this point, j is 10, and i becomes 9.
    
    int i = 10;
    //before the assignment happens, the decrement happens.
    j = --i;//at this point, both j and i are 9.
    ```
    

In-Depth

- Literals
- Operators
- Conversion (Casting)