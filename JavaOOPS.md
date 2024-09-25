Java OOPS:

## Array of Objects:
```java
class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student[] students = new Student[3];
        students[0] = new Student("Alice", 20);
        students[1] = new Student("Bob", 22);
        students[2] = new Student("Charlie", 21);

        for (Student student : students) {
            student.display();
        }
    }
}
```

### 1. **Inheritance**
   - **Usage in `main()`**:
     ```java
     class Parent {
         void display() {
             System.out.println("Parent class method");
         }
     }
     class Child extends Parent {
         // Inherits the display() method
     }

     public class Main {
         public static void main(String[] args) {
             Child child = new Child();
             child.display();  // Calls Parent's display() method
         }
     }
     ```

---

### 2. **Polymorphism - Method Overloading**
   - **Usage in `main()`**:
     ```java
     class MathOperations {
         int add(int a, int b) {
             return a + b;
         }
         int add(int a, int b, int c) {
             return a + b + c;
         }
     }

     public class Main {
         public static void main(String[] args) {
             MathOperations mo = new MathOperations();
             System.out.println(mo.add(10, 20));  // Calls the method with 2 arguments
             System.out.println(mo.add(10, 20, 30));  // Calls the method with 3 arguments
         }
     }
     ```

---

### 3. **Multi-level Inheritance**
   - **Usage in `main()`**:
     ```java
     class A {
         void displayA() { System.out.println("A class method"); }
     }
     class B extends A {
         void displayB() { System.out.println("B class method"); }
     }
     class C extends B {
         void displayC() { System.out.println("C class method"); }
     }

     public class Main {
         public static void main(String[] args) {
             C c = new C();
             c.displayA();  // Calls A's method
             c.displayB();  // Calls B's method
             c.displayC();  // Calls C's method
         }
     }
     ```

---

### 4. **Polymorphism - Method Overriding**
   - **Usage in `main()`**:
     ```java
     class Parent {
         void display() {
             System.out.println("Parent method");
         }
     }
     class Child extends Parent {
         @Override
         void display() {
             System.out.println("Child method");
         }
     }

     public class Main {
         public static void main(String[] args) {
             Parent p = new Child();  // Polymorphism
             p.display();  // Calls Child's display() method (overridden version)
         }
     }
     ```

---

### 5. **Abstract Class and Methods**
   - **Usage in `main()`**:
     ```java
     abstract class Animal {
         abstract void sound();
     }
     class Dog extends Animal {
         void sound() {
             System.out.println("Dog barks");
         }
     }

     public class Main {
         public static void main(String[] args) {
             Animal dog = new Dog();  // Cannot instantiate Animal directly
             dog.sound();  // Calls Dog's sound() method
         }
     }
     ```

---

### 6. **Interfaces**
   - **Usage in `main()`**:
     ```java
     interface Animal {
         void sound();
     }
     class Dog implements Animal {
         public void sound() {
             System.out.println("Dog barks");
         }
     }

     public class Main {
         public static void main(String[] args) {
             Animal dog = new Dog();  // Interface reference
             dog.sound();  // Calls Dog's sound() method
         }
     }
     ```

---

### 7. **Use of `super`**
   - **Usage in `main()`**:
     ```java
     class Parent {
         Parent() {
             System.out.println("Parent Constructor");
         }
         void display() {
             System.out.println("Parent display");
         }
     }
     class Child extends Parent {
         Child() {
             super();  // Calls Parent constructor
             System.out.println("Child Constructor");
         }
         @Override
         void display() {
             super.display();  // Calls Parent's display method
             System.out.println("Child display");
         }
     }

     public class Main {
         public static void main(String[] args) {
             Child child = new Child();  // Calls both Parent and Child constructors
             child.display();  // Calls Child's display() method
         }
     }
     ```

---

### 8. **Multiple Inheritance (with Interfaces)**
   - **Usage in `main()`**:
     ```java
     interface A {
         void methodA();
     }
     interface B {
         void methodB();
     }
     class C implements A, B {
         public void methodA() {
             System.out.println("Method A");
         }
         public void methodB() {
             System.out.println("Method B");
         }
     }

     public class Main {
         public static void main(String[] args) {
             C obj = new C();
             obj.methodA();  // Calls method from Interface A
             obj.methodB();  // Calls method from Interface B
         }
     }
     ```

---

### 9. **Single Inheritance**
   - **Usage in `main()`**:
     ```java
     class A {
         void methodA() {
             System.out.println("Method A");
         }
     }
     class B extends A {
         // Single inheritance from A
     }

     public class Main {
         public static void main(String[] args) {
             B obj = new B();
             obj.methodA();  // Calls method from class A
         }
     }
     ```

---

Each of these examples demonstrates how to instantiate classes and use inheritance, polymorphism, abstract classes, interfaces, and the `super` keyword in the `main()` method to leverage Java's object-oriented programming features.
