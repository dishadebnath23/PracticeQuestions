# Practice Questions – Day 1 (OOPS)

This document contains my practice answers for Day 1, focusing on core Object-Oriented Programming concepts in Java. Each question is explained with practical reasoning and simple code examples, keeping interview expectations in mind.



 Q1. BankAccount Class Design

Should `balance` be public? Justify  
No, the `balance` field should not be public.  
Balance represents sensitive financial information and allowing direct access can lead to invalid states such as negative balance or unauthorized modification. To protect data integrity, it should be declared as `private`.

 How would you control deposits and withdrawals using methods?  
Deposits and withdrawals should be performed through public methods that validate the input and enforce business rules. This ensures that balance changes happen only in a controlled manner.

How does encapsulation help enforce banking rules?  
Encapsulation hides internal data and exposes only required operations. By restricting direct access to balance and allowing updates only through validated methods, rules such as no negative balance and valid transaction amounts can be enforced.

```java
class BankAccount {
    private String accountNumber;
    private double balance;
    private String accountHolderName;

    public BankAccount(String accountNumber, String name, double balance) {
        this.accountNumber = accountNumber;
        this.accountHolderName = name;
        this.balance = balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Insufficient balance");
        }
    }

    public double getBalance() {
        return balance;
    }
}
Q2. Withdrawal Failure Due to Insufficient Balance
Checked or unchecked exception?
An unchecked exception is more suitable because insufficient balance is a business rule violation rather than a system failure.

Why is exception handling critical?
Exception handling prevents application crashes, provides meaningful error messages, and separates normal execution logic from error-handling logic.

How would a custom exception improve code clarity?
A custom exception clearly represents the domain-specific problem, making the code easier to understand and maintain.

java
Copy code
class InsufficientBalanceException extends RuntimeException {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}
java
Copy code
public void withdraw(double amount) {
    if (amount > balance) {
        throw new InsufficientBalanceException("Insufficient balance");
    }
    balance -= amount;
}
Q3. PhysicalProduct and DigitalProduct
What common behaviors would you abstract?
Common behaviors include retrieving price and purchasing the product.

Abstract class or interface?
An interface is preferred because both product types share behavior but do not require shared state, and interfaces support multiple inheritance.

java
Copy code
interface Product {
    double getPrice();
    void purchase();
}
java
Copy code
class PhysicalProduct implements Product {
    public double getPrice() {
        return 500;
    }

    public void purchase() {
        System.out.println("Product will be shipped");
    }
}
java
Copy code
class DigitalProduct implements Product {
    public double getPrice() {
        return 200;
    }

    public void purchase() {
        System.out.println("Download link will be sent");
    }
}
Q4. Polymorphism in Java
Polymorphism allows a parent class reference to point to a child class object and execute the child class implementation at runtime.

Compile-time vs Runtime Polymorphism
Compile-time polymorphism is achieved using method overloading.

Runtime polymorphism is achieved using method overriding.

Which one uses method overriding?
Runtime polymorphism uses method overriding.

Why is runtime polymorphism important?
It enables flexibility, loose coupling, and dynamic behavior, which are essential in real-world applications and frameworks.

java
Copy code
class Employee {
    double calculateSalary() {
        return 30000;
    }
}

class FullTimeEmployee extends Employee {
    @Override
    double calculateSalary() {
        return 50000;
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new FullTimeEmployee();
        System.out.println(emp.calculateSalary());
    }
}
