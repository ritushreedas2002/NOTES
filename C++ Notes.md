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

class Animal {
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

## 6. Polymorphism
Polymorphism allows methods to do different things based on the object it is acting upon. There are two types:
* Compile-time (Method Overloading)
* Run-time (Method Overriding)

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

## Method Overriding Example:
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

## 7. Constructors and Destructors
## Constructor:
A constructor is a special member function that initializes objects of a class. It is automatically called when an object is created.
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

