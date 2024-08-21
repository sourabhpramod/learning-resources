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