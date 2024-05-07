# Email Application

Senario: You are an IT support Administrator Specialist and are charged with the task of creating email accounts for new hires.

Your application should  do the following:

- Generate an email with the following syntax: *firstname.lastname@department.company.com*
- Determine the department(sales, development, accounting), if none leave blank
- Generate a random String for a password
- Have set methods to change the password, set the mailbox capacity, and define an alternate email address
- Have get methods to display the name, email, and mailbox capacity.
- knowledge used
    - String (constructor)
        
        ```
        public String(char[] value)
        ```
        
        Allocates a new `String` so that it represents the sequence of characters currently contained in the character array argument. The contents of the character array are copied; subsequent modification of the character array does not affect the newly created string.
        
        **Parameters:**`value` - The initial value of the string
        

```java
import java.util.Scanner;
import java.lang.Math;

public class Email {
  private String firstName;
  private String lastName;
  private String department;
  private String company;
  private String password;
  private final int passwordLength = 10;//setting passwordlength as default.
  private int mailBoxCapacity = 500;//default mailbox capacity is 500.
  private String alternateAddy;
  private String email;
  private String companySuffix = ".anycompany.com";

  //constructor to receive the first name and last name.
  public Email(String firstName, String lastName){
    this.firstName = firstName;
    this.lastName = lastName;
    //print out name when the email is created.
    System.out.println("Email created: " + firstName + " " + lastName);

    //as soon as the email is created, call  a method asking for the department - return the department.
    this.department = setDepartment();
    System.out.println("Department: " + this.department);

    //call a method that returns a random password.
    this.password = getRandPassword(passwordLength);
    System.out.println("Your password is " + this.password);

    //combine elements to generate the email.
    email = firstName.toLowerCase() + "." + lastName.toLowerCase() + "@" + department + companySuffix;
    System.out.println("your email is " + email);
  }
  //we don't want other people to directly access the variables, therefore we uise the encapsulation technique by getters and setters.

  //ask for the department
  private String setDepartment(){
    System.out.println("Hello, new worker: " + firstName + "\nDEPARTMENT CODES:\n1 for Sales\n2 for development\n3 for accounting.\nEnter the department codes:");
    Scanner in = new Scanner(System.in);
    int depChoice = in.nextInt();
    String department;
    switch(depChoice){
      case 1: department = "sales"; break;
      case 2: department = "development"; break;
      case 3: department = "accounting"; break;
      default: department = "";
    }
    return department;
  }
  //Generate a ramdom password
  //MAX length here is 44;
  public String getRandPassword(int length){
    String passwordSet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*";
    char[] password = new char[length];
    for(int i = 0; i < length; i++){
      int rand = (int)(Math.random()*passwordSet.length());//a random number(index) to determine a random char in passwordSet.
      //assigning each index of password a random character;
      password[i] = passwordSet.charAt(rand);
    }
    return new String(password);
  }
  //setters
  //Set the mailbox capacity
  public void setMailBoxCapacity(int mailBoxCapacity){
    this.mailBoxCapacity = mailBoxCapacity;
  }
  //Set the alternate email
  public void setAlternateAddy(String alternateAddy){
    this.alternateAddy = alternateAddy;
  }
  //Change the password
  public void setPassword(String password){
   this.password = password; 
  }
  //getters
  public int getMailBoxCapacity(){ return this.mailBoxCapacity; }
  public String getAlternateAddy(){ return this.alternateAddy; }
  public String getPassword(){ return this.password; }

  public String showInfo(){
    System.out.println("--------YOUR INFORMATION--------");
    return "DISPLAY NAME: " + firstName + " " + lastName + "\n" +
           "COMPANY EMAIL: " + email + "\n" +
           "MAILBOX CAPACITY: " + mailBoxCapacity + "mb";
  }
  //override toString() to generate a deafault form for Email.
  public String toString(){
    return  firstName.toLowerCase() + "." + lastName.toLowerCase() + "@" + department + companySuffix;
  }
}
```

```java
public class Main {
  public static void main(String[] args){
    Email em1 = new Email("Lukas", "Park");
    char i = em1.toString().charAt(5);
    System.out.println(i);
  }
}
```