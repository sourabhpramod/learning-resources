### Custom Exceptions in Java
In Java, exceptions are events that disrupt the normal flow of the program's execution. When Java's built-in exceptions (like `IOException`, `NullPointerException`) aren't sufficient, you can create your own custom exceptions by extending the `Exception` class (checked exceptions) or `RuntimeException` class (unchecked exceptions).

#### Steps to create and use a custom exception:
1. **Define a custom exception class** by extending the `Exception` or `RuntimeException` class.
2. **Throw** this custom exception when a specific condition arises.
3. **Handle** the exception using a `try-catch` block.

#### Example:

```java
// Step 1: Creating a custom exception by extending Exception (checked exception)
class AgeNotValidException extends Exception {
    // Constructor to accept the custom error message
    public AgeNotValidException(String message) {
        super(message);
    }
}

public class CustomExceptionExample {
    // Step 2: Method to validate age and throw the custom exception
    public static void checkAge(int age) throws AgeNotValidException {
        if (age < 18) {
            throw new AgeNotValidException("Age is not valid. Must be 18 or older.");
        }
    }

    public static void main(String[] args) {
        try {
            // Step 3: Call the method that can throw the custom exception
            checkAge(16);
        } catch (AgeNotValidException e) {
            // Step 4: Handling the custom exception
            System.out.println("Caught the exception: " + e.getMessage());
        } finally {
            // The finally block executes whether or not an exception is caught
            System.out.println("Validation complete.");
        }
    }
}
```

#### Output:
```
Caught the exception: Age is not valid. Must be 18 or older.
Validation complete.
```

---

### Explanation of `try`, `throw`, `throws`, `catch`, `finally`

#### 1. **`try` Block**
The `try` block is used to write code that might throw an exception. If an exception occurs, the `try` block is exited, and control moves to the `catch` block if available.

#### Example:

```java
try {
    int result = 10 / 0;  // This will throw an ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Exception caught: " + e.getMessage());
}
```

#### 2. **`throw`**
The `throw` keyword is used to explicitly throw an exception, either Java's built-in exceptions or custom exceptions.

#### Example:

```java
public void validateNumber(int number) {
    if (number < 0) {
        throw new IllegalArgumentException("Number cannot be negative");
    }
}
```

#### 3. **`throws`**
The `throws` keyword is used in the method signature to indicate that the method might throw an exception. It passes responsibility for handling the exception to the method that calls it.

#### Example:

```java
public void someMethod() throws IOException {
    // Code that might throw an IOException
}
```

#### 4. **`catch` Block**
The `catch` block is used to handle the exception that is thrown in the `try` block. It "catches" the exception and prevents the program from crashing.

#### Example:

```java
try {
    int[] array = new int[5];
    System.out.println(array[10]);  // Will throw ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Caught the exception: " + e.getMessage());
}
```

#### 5. **`finally` Block**
The `finally` block always executes after the `try-catch` block, whether an exception is thrown or not. It's typically used for cleanup activities, like closing files or releasing resources.

#### Example:

```java
try {
    int num = 50 / 0;
} catch (ArithmeticException e) {
    System.out.println("Caught an exception: " + e.getMessage());
} finally {
    System.out.println("This will always be executed.");
}
```

#### Output:
```
Caught an exception: / by zero
This will always be executed.
```

---

### Detailed Example of All Components Together:

```java
class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}

class BankAccount {
    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }

    // Method that throws the custom exception if balance is insufficient
    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException("Insufficient balance to withdraw: " + amount);
        }
        balance -= amount;
        System.out.println("Withdrawn: " + amount + ". Remaining balance: " + balance);
    }
}

public class BankExample {
    public static void main(String[] args) {
        BankAccount account = new BankAccount(500);

        try {
            // Trying to withdraw an amount greater than the balance
            account.withdraw(600);
        } catch (InsufficientBalanceException e) {
            // Handling the custom exception
            System.out.println("Exception: " + e.getMessage());
        } finally {
            // This block will always execute, regardless of the exception
            System.out.println("Transaction completed.");
        }
    }
}
```

#### Output:
```
Exception: Insufficient balance to withdraw: 600.0
Transaction completed.
```

### Summary of Keywords:
- **`try`**: Block of code where exceptions might occur.
- **`throw`**: Used to explicitly throw an exception.
- **`throws`**: Declares that a method might throw certain exceptions.
- **`catch`**: Used to catch and handle exceptions thrown in the `try` block.
- **`finally`**: Block of code that always executes after `try-catch`, often used for cleanup actions.

