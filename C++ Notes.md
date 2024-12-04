# Object-Oriented Programming in C++

## 1. Introduction to OOPS
Object-Oriented Programming (OOP) is a programming paradigm based on the concept of **objects**, which can contain data and methods. OOP focuses on organizing code into reusable components.

### Key Features of OOP:
- **Encapsulation**
- **Abstraction**
- **Inheritance**
- **Polymorphism**

---

## 2. Class and Object

### Class:
A class is a blueprint for creating objects. It defines properties and behaviors (data members and member functions).

**Syntax:**
```cpp
class ClassName {
   private:
     // Data members
   public:
     // Member functions
};
```

### Object
An object is an instance of a class.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Car {
  public:
    string brand;
    string model;
    int year;

    void displayInfo() {
      cout << brand << " " << model << " " << year << endl;
    }
};

int main() {
  Car car1;
  car1.brand = "Toyota";
  car1.model = "Camry";
  car1.year = 2020;

  car1.displayInfo();  // Output: Toyota Camry 2020
  return 0;
}
```

### 3. Encapsulation
Encapsulation is the concept of bundling data (variables) and methods (functions) operating on the data into a single unit or class. It also involves restricting access to the details of the object.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Employee {
  private:
    int salary;

  public:
    void setSalary(int s) {
      salary = s;
    }

    int getSalary() {
      return salary;
    }
};

int main() {
  Employee emp;
  emp.setSalary(50000);
  cout << "Salary: " << emp.getSalary() << endl;  // Output: Salary: 50000
  return 0;
}
```
## 4. Abstraction
Abstraction is the concept of hiding the complex implementation details and showing only the essential features of an object.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Animal { //abstract class
  public:
    virtual void sound() = 0;  // Pure virtual function
};

class Dog : public Animal {
  public:
    void sound() override {
      cout << "Bark" << endl;
    }
};

int main() {
  Dog d;
  d.sound();  // Output: Bark
  return 0;
}
```

## 5. Inheritance
Inheritance is a mechanism by which one class can inherit properties and behaviors of another class. It promotes code reusability.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Animal {
  public:
    void eat() {
      cout << "Eating..." << endl;
    }
};

class Dog : public Animal {
  public:
    void bark() {
      cout << "Barking..." << endl;
    }
};

int main() {
  Dog d;
  d.eat();  // Inherited from Animal class
  d.bark(); // Specific to Dog class
  return 0;
}
```
## Levels of Inheritance
* ## Single Inheritance
Single inheritance is when a class inherits from one base class.
**Syntax:**
```cpp
class Animal {
  public:
    void eat() {
      cout << "Eating..." << endl;
    }
};

class Dog : public Animal {
  public:
    void bark() {
      cout << "Barking..." << endl;
    }
};

int main() {
  Dog d;
  d.eat();  // Inherited from Animal class
  d.bark(); // Specific to Dog class
  return 0;
}
```
* ## Multilevel Inheritance
Multilevel inheritance is when a class inherits from another class, which itself inherits from another class.
**Syntax:**
```cpp
class Animal {
  public:
    void eat() {
      cout << "Eating..." << endl;
    }
};

class Mammal : public Animal {
  public:
    void walk() {
      cout << "Walking..." << endl;
    }
};

class Dog : public Mammal {
  public:
    void bark() {
      cout << "Barking..." << endl;
    }
};

```
* ## Hierarchical Inheritance
Hierarchical inheritance is when multiple classes inherit from the same base class.
**Syntax:**
```cpp
class Animal {
  public:
    void eat() {
      cout << "Eating..." << endl;
    }
};

class Dog : public Animal {
  public:
    void bark() {
      cout << "Barking..." << endl;
    }
};

class Cat : public Animal {
  public:
    void meow() {
      cout << "Meowing..." << endl;
    }
};
```
* ## Multiple Inheritance
Multiple inheritance is when a class inherits from more than one base class.
**Syntax:**
```cpp
class Animal {
  public:
    void eat() {
      cout << "Eating..." << endl;
    }
};

class Pet {
  public:
    void play() {
      cout << "Playing..." << endl;
    }
};

class Dog : public Animal, public Pet {
  public:
    void bark() {
      cout << "Barking..." << endl;
    }
};

```
* ## Hybrid Inheritance
Hybrid inheritance is a combination of two or more types of inheritance.
**Syntax:**
```cpp
class Animal {
  public:
    void eat() {
      cout << "Eating..." << endl;
    }
};

class Mammal : public Animal {
  public:
    void walk() {
      cout << "Walking..." << endl;
    }
};

class Pet {
  public:
    void play() {
      cout << "Playing..." << endl;
    }
};

class Dog : public Mammal, public Pet {
  public:
    void bark() {
      cout << "Barking..." << endl;
    }
};
```

## 6. Polymorphism
Polymorphism allows methods to do different things based on the object it is acting upon. There are two types:
* Compile-time (Method Overloading)
* Run-time (1. Method Overriding  2. Virtual Function)

 ## Method Overloading Example:
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Calculator {
  public:
    int add(int a, int b) {
      return a + b;
    }

    int add(int a, int b, int c) {
      return a + b + c;
    }
};

int main() {
  Calculator calc;
  cout << calc.add(10, 20) << endl;       // Output: 30
  cout << calc.add(10, 20, 30) << endl;   // Output: 60
  return 0;
}
```
## Constructor Overloading
Constructor overloading allows a class to have multiple constructors with different parameter lists. The appropriate constructor is called based on the number or type of arguments passed.
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Box {
  private:
    int length, width, height;

  public:
    // Constructor with no arguments
    Box() {
      length = width = height = 0;
    }

    // Constructor with one argument
    Box(int side) {
      length = width = height = side;
    }

    // Constructor with three arguments
    Box(int l, int w, int h) {
      length = l;
      width = w;
      height = h;
    }

    int volume() {
      return length * width * height;
    }
};

int main() {
  Box box1;             // Calls the no-argument constructor
  Box box2(5);          // Calls the one-argument constructor
  Box box3(2, 3, 4);    // Calls the three-argument constructor

  cout << "Volume of box1: " << box1.volume() << endl;  // Output: 0
  cout << "Volume of box2: " << box2.volume() << endl;  // Output: 125
  cout << "Volume of box3: " << box3.volume() << endl;  // Output: 24

  return 0;
}

```
## Operator Overloading
Operator overloading allows you to redefine the way operators work for user-defined types. For example, you can redefine the + operator to add two objects of a custom class.
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Complex {
  private:
    int real, imag;

  public:
    // Constructor
    Complex(int r, int i) : real(r), imag(i) {}

    // Overload the + operator
    Complex operator+(const Complex& obj) {
        Complex temp(0, 0);
        temp.real = real + obj.real;
        temp.imag = imag + obj.imag;
        return temp;
    }

    void display() {
      cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
  Complex c1(3, 4), c2(1, 2);

  Complex c3 = c1 + c2;  // Uses the overloaded + operator

  c3.display();          // Output: 4 + 6i

  return 0;
}

```
## Method Overriding Example:
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Base {
  public:
     void show() {
      cout << "Base class" << endl;
    }
};

class Derived : public Base {
  public:
    void show() {
      cout << "Derived class" << endl;
    }
};
int main() {
    // Write C++ code here
    std::cout << "Try programiz.pro";
    Derived d;
    d.show();
}
```

## Method Overriding using virtual Function Example:
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Base {
  public:
    virtual void show() {
      cout << "Base class" << endl;
    }
};

class Derived : public Base {
  public:
    void show() override {
      cout << "Derived class" << endl;
    }
};

int main() {
  Base *basePtr;
  Derived d;
  basePtr = &d;
  basePtr->show();  // Output: Derived class
  return 0;
}
```

## Diff between virtual func and pure virtual func
In C++, the main difference between a virtual function and a pure virtual function is that a pure virtual function must be overridden in a derived class, while a virtual function does not need to be:

Virtual Function:-
A virtual function is a member function that can be overridden by derived classes. When a virtual function is called through a base class pointer or reference, the actual function called is determined at runtime, based on the type of the object being pointed to.

Pure virtual function:-
A special type of virtual function that is declared in a base class but does not have a definition in the base class. It is intended to be overridden and implemented by derived classes. 
To declare a function as pure virtual, you use the syntax =0. For example, virtual void f3() = 0; is a pure virtual function. 
Classes that contain pure virtual functions are called "abstract" and cannot be instantiated directly. Instead, they can be used as a blueprint for creating concrete derived classes.

## 7. Constructors and Destructors
## Constructor:
A constructor is a special member function that initializes objects of a class. It is automatically called when an object is created.

Constructor overloading is a feature in C++ where a class can have more than one constructor with different parameter lists. Each constructor performs a different task based on the arguments passed.


**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Rectangle {
  private:
    int width, height;

  public:
    // Default constructor
    Rectangle() {
      width = 0;
      height = 0;
      cout << "Default constructor called" << endl;
    }

    // Parameterized constructor
    Rectangle(int w, int h) {
      width = w;
      height = h;
      cout << "Parameterized constructor called" << endl;
    }

    // Copy constructor
    Rectangle(const Rectangle &rect) {
      width = rect.width;
      height = rect.height;
      cout << "Copy constructor called" << endl;
    }

    // Method to calculate area
    int area() {
      return width * height;
    }
};

int main() {
  Rectangle rect1;               // Calls default constructor
  Rectangle rect2(10, 20);        // Calls parameterized constructor
  Rectangle rect3(rect2);         // Calls copy constructor

  cout << "Area of rect2: " << rect2.area() << endl;   // Output: 200
  cout << "Area of rect3: " << rect3.area() << endl;   // Output: 200

  return 0;
}
```


## initializer List
In C++, you can call a parent class's constructor from a derived class constructor by using an initializer list. Here's how you can pass arguments to the parent class constructor from the child class:

**Syntax:**
```cpp
#include <iostream>
using namespace std;

// Parent class
class Parent {
  public:
    Parent(int x) {
      cout << "Parent class constructor called with value: " << x << endl;
    }
};

// Child class
class Child : public Parent {
  public:
    Child(int x, int y) : Parent(x) {  // Call to Parent class constructor with x
      cout << "Child class constructor called with value: " << y << endl;
    }
};

int main() {
  Child c(10, 20);  // Pass arguments to both Parent and Child constructors
  return 0;
}
```

## Explanation:
* In the Child class constructor, : Parent(x) calls the Parent class constructor and passes the argument x to it.
* This ensures that the parent class is properly initialized before the child class constructor runs.
* The Child constructor still receives its own arguments (y), and it can handle them independently after calling the parent constructor.

  
## Destructor:
A destructor is a special member function that is executed when the object goes out of scope. It is used to release resources.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class MyClass {
  public:
    MyClass() {
      cout << "Constructor called!" << endl;
    }

    ~MyClass() {
      cout << "Destructor called!" << endl;
    }
};

int main() {
  MyClass obj;  // Constructor called
  return 0;     // Destructor called
}
```
## Constructor calling and Destructor Calling Mechanism
**Syntax:**
```cpp
#include <iostream>
using namespace std;

// Parent class
class Parent {
  public:
    // Constructor of Parent class
    Parent() {
        cout << "Parent class constructor called" << endl;
    }
    
    // Destructor of Parent class
    ~Parent() {
        cout << "Parent class destructor called" << endl;
    }
};

// Child class
class Child : public Parent {
  public:
    // Constructor of Child class
    Child() {
        cout << "Child class constructor called" << endl;
    }
    
    // Destructor of Child class
    ~Child() {
        cout << "Child class destructor called" << endl;
    }
};

int main() {
    // Creating an object of Child class
    Child c;
    
    return 0;
}

```
## Output
**Syntax:**
```cpp
Parent class constructor called
Child class constructor called
Child class destructor called
Parent class destructor called
```


## Shallow Copy vs Deep Copy

## 1. Shallow Copy
A shallow copy is a bitwise copy of an object. The copied object will share the same memory addresses for any pointers, meaning changes made to the data members pointed to by the original object will also affect the copied object, and vice versa.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Student {
  public:
    string name;
    double* cgpaPtr;

    // Constructor
    Student(string name, double cgpa) {
        this->name = name;
        cgpaPtr = new double;  // Dynamically allocate memory
        *cgpaPtr = cgpa;       // Assign the value to the pointer
    }

    // Shallow Copy Constructor
    Student(const Student& obj) {
        this->name = obj.name;
        this->cgpaPtr = obj.cgpaPtr;  // Shallow copy of pointer (both share the same memory)
    }

    // Destructor
    ~Student() {
        delete cgpaPtr;  // Free dynamically allocated memory
        cout << "Destructor called for " << name << endl;
    }

    // Display information
    void getInfo() {
        cout << "Name: " << name << endl;
        cout << "CGPA: " << *cgpaPtr << endl;
    }
};

int main() {
    Student student1("Alice", 3.9);
    student1.getInfo();

    // Shallow copy of student1 to student2
    Student student2 = student1;  
    student2.getInfo();

    // Modifying the CGPA of student2 (which will also affect student1 due to shallow copy)
    *student2.cgpaPtr = 4.0;
    cout << "After modifying student2's CGPA:" << endl;
    student1.getInfo();  // This will also show the modified CGPA
    student2.getInfo();  // Shows the same modified CGPA

    return 0;
}

```

## Deep Copy
A deep copy involves creating a completely new copy of an object, including separate memory for any dynamically allocated resources. This ensures that the original and the copied object do not share the same memory for pointer-type data members.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Student {
  public:
    string name;
    double* cgpaPtr;

    // Constructor
    Student(string name, double cgpa) {
        this->name = name;
        cgpaPtr = new double;  // Dynamically allocate memory
        *cgpaPtr = cgpa;       // Assign the value to the pointer
    }

    // Deep Copy Constructor
    Student(const Student& obj) {
        this->name = obj.name;
        this->cgpaPtr = new double;   // Allocate new memory for the pointer
        *this->cgpaPtr = *obj.cgpaPtr; // Copy the value from the original object
    }

    // Destructor
    ~Student() {
        delete cgpaPtr;  // Free dynamically allocated memory
        cout << "Destructor called for " << name << endl;
    }

    // Display information
    void getInfo() {
        cout << "Name: " << name << endl;
        cout << "CGPA: " << *cgpaPtr << endl;
    }
};

int main() {
    Student student1("Alice", 3.9);
    student1.getInfo();

    // Deep copy of student1 to student2
    Student student2 = student1;  
    student2.getInfo();

    // Modifying the CGPA of student2 (which will not affect student1 due to deep copy)
    *student2.cgpaPtr = 4.0;
    cout << "After modifying student2's CGPA:" << endl;
    student1.getInfo();  // This will show the original CGPA
    student2.getInfo();  // Shows the modified CGPA

    return 0;
}

```

## 8. Access Modifiers
* Public: Accessible from outside the class.
* Private: Accessible only within the class.
* Protected: Accessible within the class and its derived classes.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Parent {
  protected:
    int id_protected;
  
  public:
    int id_public;
};

class Child : public Parent {
  public:
    void setId(int id) {
      id_protected = id;
    }

    void displayId() {
      cout << "Protected ID: " << id_protected << endl;
    }
};

int main() {
  Child c;
  c.setId(100);
  c.displayId();  // Output: Protected ID: 100
  return 0;
}
```
## this Keyword
The this keyword is a pointer that refers to the current object of the class. It is often used to resolve conflicts between class attributes and parameters with the same name.

this is a pointer , *this indidicates the current object by deferencing so *(this).name thens to current object's name so instead we can write this->name

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Person {
  private:
    string name;

  public:
    Person(string name) {
      this->name = name;  // 'this' refers to the current object
    }

    void display() {
      cout << "Name: " << this->name << endl;
    }
};

int main() {
  Person p("John");
  p.display();  // Output: Name: John
  return 0;
}
```
## Static Keyword
Static Variables
* A static variable inside a function retains its value between function calls. It is initialized only once and exists for the entire program.
* A static data member in a class is shared by all objects of the class. All objects access the same memory for this variable.
  
**Syntax:**
```cpp
#include <iostream>
using namespace std;

void countCalls() {
    static int count = 0;  // Static variable is initialized only once
    count++;
    cout << "Function called " << count << " times" << endl;
}

int main() {
    countCalls();  // Function called 1 times
    countCalls();  // Function called 2 times
    countCalls();  // Function called 3 times
    return 0;
}

```
## Output

**Syntax:**
```cpp
Function called 1 times
Function called 2 times
Function called 3 times

```
## Static Data Members in Classes
* A static data member of a class is shared among all objects of the class. There is only one copy of the static member, and it is not tied to any specific object. It can be accessed using the class name, and its value is shared across all instances.
* A static member function can only access static data members of the class and does not depend on any particular instance of the class.
  
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Student {
  public:
    string name;
    static int totalStudents;  // Static data member

    // Constructor
    Student(string n) {
        name = n;
        totalStudents++;  // Increment static member
    }

    // Static member function
    static int getTotalStudents() {
        return totalStudents;
    }
};

// Initialize static data member
int Student::totalStudents = 0;

int main() {
    Student s1("Alice");
    Student s2("Bob");
    Student s3("Charlie");

    // Access static member using the class name
    cout << "Total students: " << Student::getTotalStudents() << endl;  // Output: 3

    return 0;
}
```

## Static Objects
Static objects, much like static variables, have a lifetime that extends until the end of the program. They are created only once and persist throughout the program's execution.
A static object is initialized only once and retains its state across function calls.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class ABC {
public:
    ABC() {
        cout << "constructor\n";
    }

    ~ABC() {
        cout << "destructor\n";
    }
};

int main() {
    if (true) {
        ABC obj;
    }

    cout << "end of main fnx\n";
    return 0;
}
```
**Output:**
```cpp
constructor
destructor
end of main fnx

```
## with static 
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class ABC {
public:
    ABC() {
        cout << "constructor\n";
    }

    ~ABC() {
        cout << "destructor\n";
    }
};

int main() {
    if (true) {
        static ABC obj;
    }

    cout << "end of main fnx\n";
    return 0;
}
```
**Output:**
```cpp
constructor
end of main fnx
destructor
```
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Example {
  public:
    Example() {
        cout << "Constructor called!" << endl;
    }
    ~Example() {
        cout << "Destructor called!" << endl;
    }

    void display() {
        cout << "Display function called!" << endl;
    }
};

void createStaticObject() {
    static Example obj;  // Static object
    obj.display();
}

int main() {
    createStaticObject();  // Constructor called, Display function called
    createStaticObject();  // Only Display function called, constructor is not called again
    return 0;
}
```

## Modes of Inheritance

Modes provides restriction to how the child class treats its parent class variables and functions

| Access in Base Class | Public Inheritance | Protected Inheritance | Private Inheritance |
|----------------------|--------------------|-----------------------|---------------------|
| `public`             | `public`           | `protected`           | `private`           |
| `protected`          | `protected`        | `protected`           | `private`           |
| `private`            | Not accessible     | Not accessible        | Not accessible      |


## 1.Public 
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Base {
  public:
    int publicVar = 1;
  protected:
    int protectedVar = 2;
  private:
    int privateVar = 3;
};

class Derived : public Base {
  public:
    void display() {
        cout << "Public Var: " << publicVar << endl;        // Accessible
        cout << "Protected Var: " << protectedVar << endl;  // Accessible
        // cout << privateVar << endl;  // Error: Not accessible
    }
};

int main() {
    Derived obj;
    obj.display();
    cout << "Public Var accessed from main: " << obj.publicVar << endl;  // Accessible
    // cout << obj.protectedVar;  // Error: Not accessible
    return 0;
}
```

## 2.Protected Inheritance
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Base {
  public:
    int publicVar = 1;
  protected:
    int protectedVar = 2;
  private:
    int privateVar = 3;
};

class Derived : protected Base {
  public:
    void display() {
        cout << "Public Var: " << publicVar << endl;        // Accessible
        cout << "Protected Var: " << protectedVar << endl;  // Accessible
        // cout << privateVar << endl;  // Error: Not accessible
    }
};

int main() {
    Derived obj;
    obj.display();
    // cout << obj.publicVar;  // Error: Not accessible outside the class
    // cout << obj.protectedVar;  // Error: Not accessible
    return 0;
}
```

## Private Inheritance
**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Base {
  public:
    int publicVar = 1;
  protected:
    int protectedVar = 2;
  private:
    int privateVar = 3;
};

class Derived : private Base {
  public:
    void display() {
        cout << "Public Var: " << publicVar << endl;        // Accessible within the class
        cout << "Protected Var: " << protectedVar << endl;  // Accessible within the class
        // cout << privateVar << endl;  // Error: Not accessible
    }
};

int main() {
    Derived obj;
    obj.display();
    // cout << obj.publicVar;  // Error: Not accessible outside the class
    // cout << obj.protectedVar;  // Error: Not accessible
    return 0;
}
```

## Friend Function
A friend function in C++ is a function that is not a member of a class but has access to the class's private and protected members. By declaring a function as a friend of a class, that function can access the private and protected data of the class, which is normally hidden from non-member functions.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Rectangle {
  private:
    int width, height;

  public:
    // Constructor
    Rectangle(int w, int h) : width(w), height(h) {}

    // Declare the friend function
    friend int area(Rectangle& rect);  // Friend function declaration //friend int area(Rectangle); -> this is also correct
};

// Definition of the friend function
int area(Rectangle& rect) {
    // The friend function has access to the private members of the class
    return rect.width * rect.height;
}

int main() {
    // Create an object of the Rectangle class
    Rectangle rect(10, 5);

    // Call the friend function to calculate the area
    cout << "Area of rectangle: " << area(rect) << endl;  // Output: 50

    return 0;
}

```

## Friend Class
A friend class in C++ is a class that is given access to the private and protected members of another class. By declaring a class as a friend, all member functions of the friend class can access the private and protected data of the class that declares the friendship.
Remember, friendship in C++ is not mutual, i.e., if class A is friend class of class B, this does not mean class B is friend class of class A.

**Syntax:**
```cpp
#include <iostream>
using namespace std;

class Rectangle {
  private:
    int width;
    int height;

  public:
    // Constructor
    Rectangle(int w, int h) : width(w), height(h) {}

    // Declare the class 'Calculator' as a friend of 'Rectangle'
    friend class Calculator;
};

// Friend class
class Calculator {
  public:
    // Member function of Calculator that calculates the area of Rectangle
    int area(Rectangle& rect) {
        // Access private members of Rectangle
        return rect.width * rect.height;
    }

    // Member function of Calculator that calculates the perimeter of Rectangle
    int perimeter(Rectangle& rect) {
        // Access private members of Rectangle
        return 2 * (rect.width + rect.height);
    }
};

int main() {
    // Create a Rectangle object
    Rectangle rect(10, 5);

    // Create a Calculator object
    Calculator calc;

    // Use the Calculator object to calculate area and perimeter
    cout << "Area of Rectangle: " << calc.area(rect) << endl;        // Output: 50
    cout << "Perimeter of Rectangle: " << calc.perimeter(rect) << endl;  // Output: 30

    return 0;
}

```
