## Switch Case:

```
if(condtions){
  //block
  variable = x;
}


switch (variable) {
    case value1:
        // code block
        break;
    case value2:
        // code block
        break;
    // more cases...
    default:
        // default code block
}
```
## Converting types:

1. **Implicit Conversion (Widening)**
   ```java
   int num = 10;
   double d = num; // int to double
   ```

2. **Explicit Conversion (Narrowing)**
   ```java
   double d = 10.5;
   int num = (int) d; // double to int
   ```

3. **String to Integer/Double**
   ```java
   String str = "123";
   int num = Integer.parseInt(str); // String to int

   String str2 = "123.45";
   double d = Double.parseDouble(str2); // String to double
   ```

4. **Integer/Double to String**
   ```java
   int num = 123;
   String str = Integer.toString(num); // int to String

   double d = 123.45;
   String str2 = Double.toString(d); // double to String
   ```

## Rounding to decimal places

Here’s how you can round a `double` or `float` value to two decimal places using `String.format()`, `printf()`, and `Math.round()`:

1. **Using `String.format()`**
   ```java
   double value = 123.456789;
   String rounded = String.format("%.2f", value);
   System.out.println(rounded); // Output: 123.46
   ```

2. **Using `printf()`**
   ```java
   double value = 123.456789;
   System.out.printf("%.2f%n", value); // Output: 123.46
   ```

3. **Using `Math.round()`**
   ```java
   double value = 123.456789;
   double rounded = Math.round(value * 100.0) / 100.0;
   System.out.println(rounded); // Output: 123.46
   ```

## String Traversal:
```
String str = "example";
for (int i = 0; i < str.length(); i++) {
    char ch = str.charAt(i);
    System.out.println(ch);
}
```

## HashSets:

Here’s how you can use a `HashSet` in Java:

1. **Creating a `HashSet`**
   ```java
   import java.util.HashSet;

   HashSet<String> set = new HashSet<>();
   ```

2. **Adding Elements**
   ```java
   set.add("apple");
   set.add("banana");
   set.add("cherry");
   ```

3. **Removing Elements**
   ```java
   set.remove("banana");
   ```

4. **Checking if an Element Exists**
   ```java
   boolean exists = set.contains("apple");
   System.out.println(exists); // Output: true
   ```

5. **Iterating Through Elements**
   ```java
   for (String item : set) {
       System.out.println(item);
   }
   ```

6. **Size of the `HashSet`**
   ```java
   int size = set.size();
   System.out.println(size); // Output: 2
   ```

7. **Clearing All Elements**
   ```java
   set.clear();
   ```

8. **Checking if the `HashSet` is Empty**
   ```java
   boolean isEmpty = set.isEmpty();
   System.out.println(isEmpty); // Output: true
   ```
## bitwise operators 

Bitwise operators in Java are used to perform operations on the binary representations of integers. Here's a quick overview:

1. **AND (`&`)**: Performs a bitwise AND operation. Each bit of the result is 1 if the corresponding bits of both operands are 1; otherwise, it is 0.
   ```java
   int a = 5; // 0101 in binary
   int b = 3; // 0011 in binary
   int result = a & b; // 0001 in binary (1 in decimal)
   ```

2. **OR (`|`)**: Performs a bitwise OR operation. Each bit of the result is 1 if at least one of the corresponding bits of the operands is 1.
   ```java
   int result = a | b; // 0111 in binary (7 in decimal)
   ```

3. **XOR (`^`)**: Performs a bitwise XOR operation. Each bit of the result is 1 if the corresponding bits of the operands are different; otherwise, it is 0.
   ```java
   int result = a ^ b; // 0110 in binary (6 in decimal)
   ```

4. **Complement (`~`)**: Inverts all the bits of the operand.
   ```java
   int result = ~a; // 1010 in binary (in decimal, this is -6 due to sign bit)
   ```

5. **Left Shift (`<<`)**: Shifts the bits of the number to the left by a specified number of positions. This operation fills the vacated bits on the right with 0s.
   ```java
   int result = a << 1; // 1010 in binary (10 in decimal)
   ```

6. **Right Shift (`>>`)**: Shifts the bits of the number to the right by a specified number of positions. The sign bit is used to fill the vacated bits on the left.
   ```java
   int result = a >> 1; // 0010 in binary (2 in decimal)
   ```

7. **Unsigned Right Shift (`>>>`)**: Shifts the bits of the number to the right by a specified number of positions, filling the vacated bits on the left with 0s, regardless of the sign bit.
   ```java
   int result = a >>> 1; // 0010 in binary (2 in decimal)
   ```

These operators can be useful for low-level programming, such as in systems programming, graphics, or performance optimization tasks.

## String Function:
To capitalize an entire word (all characters in uppercase) in Java, use:

```java
String capitalizedWord = yourString.toUpperCase();
```

This will convert the entire string to uppercase. For example:

```java
String word = "hello";
String capitalizedWord = word.toUpperCase(); // Output: "HELLO"
```

```
str.toLowerCase();
```
for lower casing 


### to get the end of an array with bigger size but lower number of elements:

```java
for(int i=0; c[i]!='\0'; i++)
```

## TO TAKE CHAR AS INPUT 

To take a character as input in Java, you can use the `Scanner` class and its `next().charAt(0)` method. This method reads a `String` from the user and extracts the first character of that `String`.

Here's an example:

```java
import java.util.Scanner;

public class CharacterInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a character: ");
        char input = scanner.next().charAt(0);

        System.out.println("You entered: " + input);

        scanner.close();
    }
}
```

### Explanation:
- `Scanner scanner = new Scanner(System.in);` creates a `Scanner` object to read input from the console.
- `scanner.next().charAt(0);` reads the input as a `String` and then `charAt(0)` extracts the first character of that `String`.
- The character is then stored in the variable `input` and can be used as needed.

This method ensures you capture a single character from the user's input.


## To find number of digits in a number

```
int numDigits = String.valueOf(number).length();
```


# JAVA STUFF ENTHOKKEYOOO:

Here's how you can write single-function programs for the following tasks in Java: **Harmonic Sum**, **LCM and HCF**, and **Disarium Number**.

### 1. Harmonic Sum in Java

```java
public class HarmonicSum {
    public static double harmonicSum(int n) {
        double sum = 0.0;
        for (int i = 1; i <= n; i++) {
            sum += 1.0 / i;
        }
        return sum;
    }

    public static void main(String[] args) {
        int n = 5;  // Calculate harmonic sum of first n numbers
        double result = harmonicSum(n);
        System.out.println("Harmonic Sum of " + n + " is: " + result);
    }
}
```

### 2. LCM and HCF in Java

```java
public class LCMandHCF {
    // Function to calculate GCD using Euclidean algorithm
    public static int gcd(int a, int b) {
        if (b == 0) {
            return a;
        }
        return gcd(b, a % b);
    }

    // Function to calculate LCM
    public static int lcm(int a, int b) {
        return (a * b) / gcd(a, b);
    }

    public static void main(String[] args) {
        int a = 12, b = 18;
        int hcf = gcd(a, b);
        int lcm = lcm(a, b);
        System.out.println("HCF of " + a + " and " + b + " is: " + hcf);
        System.out.println("LCM of " + a + " and " + b + " is: " + lcm);
    }
}
```

### 3. Disarium Number in Java

A **Disarium Number** is a number where the sum of its digits powered with their respective positions is equal to the number itself (e.g., 89: \(8^1 + 9^2 = 89\)).

```java
public class DisariumNumber {
    public static boolean isDisarium(int num) {
        int sum = 0, temp = num;
        int digits = Integer.toString(num).length();

        while (temp > 0) {
            int digit = temp % 10;
            sum += Math.pow(digit, digits);
            digits--;
            temp /= 10;
        }

        return sum == num;
    }

    public static void main(String[] args) {
        int number = 89;  // Test with any number
        if (isDisarium(number)) {
            System.out.println(number + " is a Disarium Number.");
        } else {
            System.out.println(number + " is not a Disarium Number.");
        }
    }
}
```

### Explanation:

1. **Harmonic Sum**:
   - The `harmonicSum(int n)` function calculates the sum of reciprocals of the first `n` natural numbers.

2. **LCM and HCF**:
   - `gcd(int a, int b)` computes the greatest common divisor (HCF).
   - `lcm(int a, int b)` uses the relationship between LCM and GCD to compute the least common multiple.

3. **Disarium Number**:
   - The `isDisarium(int num)` function checks if a given number is a Disarium number by summing the digits raised to the power of their positions and comparing the result with the original number.

You can run each of these functions individually in the same Java file by placing them in the `main` method of their respective classes.


You can convert a binary number to a decimal number in Java using either of the following methods:

### 1. Using `Integer.parseInt()` Method
Java provides a built-in function `Integer.parseInt()` which can convert a binary string to a decimal integer.

```java
public class BinaryToDecimal {
    public static void main(String[] args) {
        String binary = "1101";  // Example binary number as a string
        int decimal = Integer.parseInt(binary, 2);  // Convert binary to decimal
        System.out.println("Binary: " + binary + " to Decimal: " + decimal);
    }
}
```

### Explanation:
- The `parseInt()` method takes two arguments: 
  - The first argument is the binary number as a `String`.
  - The second argument `2` specifies the base of the input number (binary = base 2).
- This method converts the binary string into its decimal equivalent.

### Output:
```
Binary: 1101 to Decimal: 13
```

### 2. Manual Conversion (Without Built-in Methods)
You can manually convert a binary number to decimal using a loop by iterating over each digit and applying the formula for binary-to-decimal conversion:

\[
\text{Decimal} = \sum (\text{binary digit} \times 2^{\text{position}})
\]

```java
public class BinaryToDecimalManual {
    public static int binaryToDecimal(int binary) {
        int decimal = 0;
        int base = 1;  // 2^0
        while (binary > 0) {
            int lastDigit = binary % 10;
            decimal += lastDigit * base;
            base = base * 2;
            binary = binary / 10;
        }
        return decimal;
    }

    public static void main(String[] args) {
        int binary = 1101;  // Example binary number
        int decimal = binaryToDecimal(binary);
        System.out.println("Binary: " + binary + " to Decimal: " + decimal);
    }
}
```

### Explanation:
- The `binaryToDecimal()` function converts a binary number (provided as an integer) to decimal by processing each binary digit from right to left.
- It multiplies each digit by powers of 2, accumulating the result into the `decimal` variable.

### Output:
```
Binary: 1101 to Decimal: 13
```

Both methods effectively convert binary to decimal, with the first method being more concise using Java’s built-in function, and the second method offering a step-by-step manual approach.

To convert a **decimal number back to binary** in Java, you can use either of the following methods:

### 1. Using `Integer.toBinaryString()` Method
Java provides a built-in function `Integer.toBinaryString()` that can convert a decimal number to a binary string.

```java
public class DecimalToBinary {
    public static void main(String[] args) {
        int decimal = 13;  // Example decimal number
        String binary = Integer.toBinaryString(decimal);  // Convert decimal to binary
        System.out.println("Decimal: " + decimal + " to Binary: " + binary);
    }
}
```

### Explanation:
- The `toBinaryString()` method takes a decimal integer as input and returns its binary equivalent as a string.

### Output:
```
Decimal: 13 to Binary: 1101
```

### 2. Manual Conversion (Without Built-in Methods)
You can manually convert a decimal number to binary by repeatedly dividing the number by 2 and collecting the remainders.

```java
public class DecimalToBinaryManual {
    public static String decimalToBinary(int decimal) {
        StringBuilder binary = new StringBuilder();
        while (decimal > 0) {
            int remainder = decimal % 2;
            binary.append(remainder);
            decimal = decimal / 2;
        }
        return binary.reverse().toString();  // Reverse the string as binary digits are calculated in reverse order
    }

    public static void main(String[] args) {
        int decimal = 13;  // Example decimal number
        String binary = decimalToBinary(decimal);
        System.out.println("Decimal: " + decimal + " to Binary: " + binary);
    }
}
```

### Explanation:
- The `decimalToBinary()` function calculates the binary digits (remainders) by continuously dividing the decimal number by 2.
- It appends each remainder to a `StringBuilder`, and finally, the binary string is reversed since the binary number is formed from least significant bit to most significant bit.

### Output:
```
Decimal: 13 to Binary: 1101
```

Both methods will convert a decimal number to binary. The first method uses Java’s built-in functionality, while the second one demonstrates the step-by-step manual conversion process.


To **convert a decimal number to hexadecimal** and **vice versa** in Java, you can use the following methods:

### 1. Decimal to Hexadecimal

#### Using `Integer.toHexString()` (Built-in Method)

```java
public class DecimalToHex {
    public static void main(String[] args) {
        int decimal = 255;  // Example decimal number
        String hex = Integer.toHexString(decimal);  // Convert decimal to hexadecimal
        System.out.println("Decimal: " + decimal + " to Hexadecimal: " + hex.toUpperCase());
    }
}
```

### Explanation:
- `Integer.toHexString(decimal)` converts a decimal integer to a hexadecimal string.
- `.toUpperCase()` is used to print the hexadecimal in uppercase format (optional).

### Output:
```
Decimal: 255 to Hexadecimal: FF
```

#### Manual Conversion (Without Built-in Method)

```java
public class DecimalToHexManual {
    public static String decimalToHex(int decimal) {
        StringBuilder hex = new StringBuilder();
        char[] hexChars = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'};

        while (decimal > 0) {
            int remainder = decimal % 16;
            hex.append(hexChars[remainder]);
            decimal = decimal / 16;
        }

        return hex.reverse().toString();  // Reverse to correct the order
    }

    public static void main(String[] args) {
        int decimal = 255;  // Example decimal number
        String hex = decimalToHex(decimal);
        System.out.println("Decimal: " + decimal + " to Hexadecimal: " + hex);
    }
}
```

### Explanation:
- The manual method continuously divides the decimal by 16, appends the corresponding hexadecimal character (using a lookup array), and reverses the result to get the correct hexadecimal representation.

### Output:
```
Decimal: 255 to Hexadecimal: FF
```

### 2. Hexadecimal to Decimal

#### Using `Integer.parseInt()` (Built-in Method)

```java
public class HexToDecimal {
    public static void main(String[] args) {
        String hex = "FF";  // Example hexadecimal number
        int decimal = Integer.parseInt(hex, 16);  // Convert hexadecimal to decimal
        System.out.println("Hexadecimal: " + hex + " to Decimal: " + decimal);
    }
}
```

### Explanation:
- `Integer.parseInt(hex, 16)` converts a hexadecimal string to a decimal integer. The second argument `16` specifies that the input is in base 16.

### Output:
```
Hexadecimal: FF to Decimal: 255
```

#### Manual Conversion (Without Built-in Method)

```java
public class HexToDecimalManual {
    public static int hexToDecimal(String hex) {
        int decimal = 0;
        int base = 1;  // 16^0

        for (int i = hex.length() - 1; i >= 0; i--) {
            char hexChar = hex.charAt(i);
            if (hexChar >= '0' && hexChar <= '9') {
                decimal += (hexChar - '0') * base;
            } else if (hexChar >= 'A' && hexChar <= 'F') {
                decimal += (hexChar - 'A' + 10) * base;
            }
            base = base * 16;
        }
        return decimal;
    }

    public static void main(String[] args) {
        String hex = "FF";  // Example hexadecimal number
        int decimal = hexToDecimal(hex);
        System.out.println("Hexadecimal: " + hex + " to Decimal: " + decimal);
    }
}
```

### Explanation:
- The manual method works by iterating through the hexadecimal string, converting each character to its decimal equivalent, and summing them based on their positional values (multiplied by powers of 16).

### Output:
```
Hexadecimal: FF to Decimal: 255
```

### Summary:
- **Decimal to Hexadecimal**: Use `Integer.toHexString(decimal)` for a built-in method or divide the decimal by 16 manually.
- **Hexadecimal to Decimal**: Use `Integer.parseInt(hex, 16)` for a built-in method or manually calculate each hexadecimal digit’s value using powers of 16.


To convert between **binary and hexadecimal** in Java, you can use both **built-in methods** and a **manual approach**.

### 1. Binary to Hexadecimal

#### Using Built-in Methods
First, convert the binary string to a decimal using `Integer.parseInt()`, and then convert the decimal to hexadecimal using `Integer.toHexString()`.

```java
public class BinaryToHex {
    public static String binaryToHex(String binary) {
        int decimal = Integer.parseInt(binary, 2);  // Convert binary to decimal
        return Integer.toHexString(decimal).toUpperCase();  // Convert decimal to hexadecimal
    }

    public static void main(String[] args) {
        String binary = "110111";  // Example binary number
        String hex = binaryToHex(binary);
        System.out.println("Binary: " + binary + " to Hexadecimal: " + hex);
    }
}
```

### Explanation:
- `Integer.parseInt(binary, 2)` converts the binary string to a decimal.
- `Integer.toHexString(decimal)` converts the decimal to hexadecimal.

### Output:
```
Binary: 110111 to Hexadecimal: 37
```

#### Manual Conversion (Without Built-in Methods)

You can break the binary number into groups of 4 bits (starting from the right) and convert each group directly to its hexadecimal equivalent.

```java
public class BinaryToHexManual {
    public static String binaryToHex(String binary) {
        StringBuilder hex = new StringBuilder();
        int len = binary.length();
        
        // Pad binary with leading zeros to make it a multiple of 4
        if (len % 4 != 0) {
            binary = "0".repeat(4 - len % 4) + binary;
        }

        // Create a lookup array for binary to hex conversion
        String[] hexLookup = {"0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", "C", "D", "E", "F"};

        // Process every group of 4 bits
        for (int i = 0; i < binary.length(); i += 4) {
            String chunk = binary.substring(i, i + 4);
            int decimalValue = Integer.parseInt(chunk, 2);  // Convert each 4-bit chunk to decimal
            hex.append(hexLookup[decimalValue]);  // Convert decimal to hex and append
        }
        
        return hex.toString();
    }

    public static void main(String[] args) {
        String binary = "110111";  // Example binary number
        String hex = binaryToHex(binary);
        System.out.println("Binary: " + binary + " to Hexadecimal: " + hex);
    }
}
```

### Explanation:
- The binary string is padded to ensure its length is a multiple of 4.
- Each 4-bit group is converted to decimal and then to hexadecimal using a lookup table.

### Output:
```
Binary: 110111 to Hexadecimal: 37
```

### 2. Hexadecimal to Binary

#### Using Built-in Methods
First, convert the hexadecimal string to a decimal using `Integer.parseInt()`, and then convert the decimal to binary using `Integer.toBinaryString()`.

```java
public class HexToBinary {
    public static String hexToBinary(String hex) {
        int decimal = Integer.parseInt(hex, 16);  // Convert hex to decimal
        return Integer.toBinaryString(decimal);  // Convert decimal to binary
    }

    public static void main(String[] args) {
        String hex = "37";  // Example hexadecimal number
        String binary = hexToBinary(hex);
        System.out.println("Hexadecimal: " + hex + " to Binary: " + binary);
    }
}
```

### Explanation:
- `Integer.parseInt(hex, 16)` converts the hexadecimal string to a decimal.
- `Integer.toBinaryString(decimal)` converts the decimal to binary.

### Output:
```
Hexadecimal: 37 to Binary: 110111
```

#### Manual Conversion (Without Built-in Methods)

You can convert each hexadecimal digit to its 4-bit binary equivalent using a lookup table.

```java
public class HexToBinaryManual {
    public static String hexToBinary(String hex) {
        StringBuilder binary = new StringBuilder();
        String[] binaryLookup = {
            "0000", "0001", "0010", "0011", "0100", "0101", "0110", "0111", 
            "1000", "1001", "1010", "1011", "1100", "1101", "1110", "1111"
        };

        for (int i = 0; i < hex.length(); i++) {
            char hexChar = hex.charAt(i);
            int decimalValue;

            if (hexChar >= '0' && hexChar <= '9') {
                decimalValue = hexChar - '0';
            } else {
                decimalValue = hexChar - 'A' + 10;
            }

            binary.append(binaryLookup[decimalValue]);  // Append the corresponding binary value
        }
        
        return binary.toString();
    }

    public static void main(String[] args) {
        String hex = "37";  // Example hexadecimal number
        String binary = hexToBinary(hex);
        System.out.println("Hexadecimal: " + hex + " to Binary: " + binary);
    }
}
```

### Explanation:
- Each hexadecimal digit is converted to its corresponding 4-bit binary representation using a lookup table.
- The result is appended to the `StringBuilder` to form the complete binary string.

### Output:
```
Hexadecimal: 37 to Binary: 110111
```

### Summary:
- **Binary to Hexadecimal**:
  - Use `Integer.parseInt(binary, 2)` to convert binary to decimal, then `Integer.toHexString(decimal)` to convert decimal to hexadecimal.
  - Alternatively, break the binary into 4-bit groups and map them directly to their hexadecimal values.
  
- **Hexadecimal to Binary**:
  - Use `Integer.parseInt(hex, 16)` to convert hexadecimal to decimal, then `Integer.toBinaryString(decimal)` to convert decimal to binary.
  - Alternatively, convert each hexadecimal digit to its 4-bit binary representation using a lookup table.


### Permutations of a given string
```java
public class Permutations {

    // Function to print all permutations of a given string
    public static void printPermutations(String str) {
        // Convert the string to a character array
        char[] chars = str.toCharArray();
        // Call the recursive function to generate permutations
        generatePermutations(chars, 0);
    }

    // Recursive function to generate permutations
    private static void generatePermutations(char[] chars, int index) {
        if (index == chars.length - 1) {
            // If the index is at the end of the array, print the permutation
            System.out.println(new String(chars));
        } else {
            for (int i = index; i < chars.length; i++) {
                // Swap the current index with the loop index
                swap(chars, index, i);
                // Recurse for the next index
                generatePermutations(chars, index + 1);
                // Swap back to the original configuration
                swap(chars, index, i);
            }
        }
    }

    // Helper method to swap characters in the array
    private static void swap(char[] chars, int i, int j) {
        char temp = chars[i];
        chars[i] = chars[j];
        chars[j] = temp;
    }

    public static void main(String[] args) {
        String str = "ABC";
        printPermutations(str);
    }
}
```


Here's how Vimal can implement the `calculateSubnets` method in Java to calculate the number of possible subnets based on the given IP address and subnet mask in CIDR notation:

```java
import java.util.Scanner;

public class SubnetCalculator {

    public static void calculateSubnets(String ipAddress, String cidrNotation) {
        // Extract the number after the '/' from the CIDR notation
        int subnetBits = Integer.parseInt(cidrNotation.split("/")[1]);
        
        // Total number of bits in an IPv4 address is 32
        int totalBits = 32;
        
        // The number of host bits is the difference between total bits and subnet bits
        int hostBits = totalBits - subnetBits;
        
        // Number of subnets is 2 raised to the power of hostBits
        int numberOfSubnets = (int) Math.pow(2, hostBits);
        
        // Print the result
        System.out.println("Number of Subnets: " + numberOfSubnets);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Input IP address
        String ipAddress = scanner.nextLine();
        
        // Input CIDR notation
        String cidrNotation = scanner.nextLine();
        
        // Call the method to calculate subnets
        calculateSubnets(ipAddress, cidrNotation);
        
        scanner.close();
    }
}
```

### Explanation:
1. **Input Handling**: The program reads the IP address and CIDR notation from user input.
2. **Subnet Calculation**:
   - The subnet bits are extracted from the CIDR notation by splitting the string on `/` and converting the second part to an integer.
   - The number of host bits is calculated by subtracting the subnet bits from 32 (total number of bits in an IPv4 address).
   - The number of subnets is calculated as \(2^{\text{hostBits}}\).
3. **Output**: The number of possible subnets is printed.

### Sample Output:
```
Input:
192.168.1.0
/24

Output:
Number of Subnets: 256
```


In Java, classes and objects form the foundation of Object-Oriented Programming (OOP). Here's a breakdown of the syntax, including constructors, with important details to remember:

### 1. **Class Syntax**
A class is a blueprint for objects, defining properties (fields) and behaviors (methods).

```java
class ClassName {
    // Fields (attributes)
    int field1;
    String field2;

    // Methods (behaviors)
    void method1() {
        // method implementation
    }
}
```

### Example:
```java
class Car {
    String model;
    int year;

    void displayDetails() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}
```

### 2. **Object Creation**
To create an object from a class, use the `new` keyword.

```java
ClassName objectName = new ClassName();
```

### Example:
```java
Car myCar = new Car();
```

### 3. **Constructor Syntax**
A constructor is a special method used to initialize objects. It has the same name as the class and **no return type**.

- **Default constructor**: Provided by Java if no constructor is defined.
- **Parameterized constructor**: Used to initialize fields with specific values.

```java
class ClassName {
    // Constructor
    ClassName() {
        // constructor implementation
    }

    // Parameterized Constructor
    ClassName(int param1, String param2) {
        // Initialize fields
    }
}
```

### Example:
```java
class Car {
    String model;
    int year;

    // Default constructor
    Car() {
        model = "Unknown";
        year = 2020;
    }

    // Parameterized constructor
    Car(String modelName, int yearOfManufacture) {
        model = modelName;
        year = yearOfManufacture;
    }

    void displayDetails() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}

// Creating objects
Car defaultCar = new Car();  // Calls default constructor
Car customCar = new Car("Toyota", 2021);  // Calls parameterized constructor
```

### 4. **Important Details for a Test**

- **Constructor rules**: 
  - No return type.
  - Same name as the class.
  - If no constructor is written, Java provides a default constructor.
  - If you define any constructor, Java will not provide the default constructor automatically.

- **Constructor overloading**: 
  - You can have multiple constructors in a class, each with different parameter lists.

- **Object instantiation**: 
  - Objects are instances of classes.
  - Object reference variables store the memory address of the object.
  
- **Access modifiers**: 
  - Constructors and fields can have access modifiers like `public`, `private`, `protected`, or no modifier (default/package-private).

### 5. **Memory allocation**
- **Heap memory**: Objects are stored in heap memory.
- **Stack memory**: Local variables, including object references, are stored in the stack.

### Testing Notes:
- Ensure constructors are properly defined for class instantiation.
- Test if objects are initialized with expected values (especially with parameterized constructors).
- When testing multiple constructors, verify that each initializes fields correctly.
- Handle cases where constructors might throw exceptions (like when working with invalid input parameters).

