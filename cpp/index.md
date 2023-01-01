# C++ notes


<!--more-->

## Output

std::cout<<
you can add many **cout** objects as you want, but it does not insert a new line at the end of the output

\n will create a new line:

```cpp
#include <iostream>
// iostream is a header file library 
// lets us work with i/o  objects
int main(){
    
    std::cout<<"hello world!"<<"\n";
	return 0;
    //return 0 ends the main function.
}
    
```

you can use namespace std 
and you can directly use "cout" to print you contents
the code is below

```cpp
#include <iostream>
using namespace std;
int main(){
    cout<<"hello world";
    return 0;

}
    

```

## Variables

have the same types of variables with JAVA

1. int
2. double
3. char
4. string
5. bool

```cpp
#include <iostream>
using namespace std;
int main()
{
    int age = 20;
    string name = "zhouxingyu";
    cout << "i am" << name << '\n';
    cout << " i am " << age << " years old";

    return 0;
}

```

### Multiple Variables

```
int x,y,z;
```

**all cpp variables must be identified with unique names**
**Names cannot contain whitespaces or special characters like ! # %**

## Input

cout is pronounced "see  out" Used for output and uses the insertion operator(**<<**)
cin is pronounced "see in" use the extraction operator **>>**

## Data Types

int myNum = 5;        // Integer (whole number)
float myFloatNum = 5.99;   // Floating point number
double myDoubleNum = 9.98;  // Floating point number
char myLetter = 'D';     // Character
bool myBoolean = true;    // Boolean
string myText = "Hello";   // String

## Operators

the same with JAVA

## string

```cpp
    string a = "hello ";
    string b = "world";
    string c = a.append(b);
    string d = a + b;
    cout << c;
```

a+b is equal to append

## Conditions

the same with Java

- IF
- ELSE
- ELSE IF 
- SWITCH

variable = (condition)?expressionTrue:expresionFalse

## Structures

give a name to the structure ,and treat it a date type

```CPP
#include <iostream>
using namespace std;
int main()
{
   struct test
   {
      /* data */
      int NO;
      string name;
   } student1, student2;
   
   student1.name = "Leonard";
   student1.NO = 1;
   student2.name = "Stark";
   student2.NO = 2;
   cout<<student1.NO<<" "<<student1.name<<endl;
   cout<<student2.NO<< " "<<student2.name;
}

```

## References

we can use either the variable name "test" to refer to the name

```CPP
   string name = "Leo";
   string &test = name;
   cout<<test;
```

## Memory address

**&** was used to create a reference variable,But it can also be used to get the memory address of a variable which is the location of where the variable is stored on the computer.

```CPP
   string name = "Leo";
   cout<<&name;
```

memory address is very important ,references and pointers are two features that make c++ stand out from other programming languages just like Python and Java;

## Pointers

### create pointer

is a variable that stores the memory address as its value.

Even though we can declare ptr in three ways,**I prefer the first one**,it can make us more clear

```cpp
string* ptr;
string * ptr;
string *ptr;

```



```CPP
string food = "pizza";
   string* ptr = &food;
   cout<<ptr<<endl;
   cout<<&food;
```

ptr and &food have the same output

### Dereference 

Get Memory Address and Value

in the previous chapter we said we could use ***** to get the memory address of a variable.However, we can use this operator to get the value of the variable.

### Modify Pointers

we can change the pointer value.

```cpp
string food = "pizza";
   string* ptr = &food;
   cout<<food<<endl;
   cout<<*ptr<<endl;
   *ptr = "apple";
   cout<<*ptr<<endl;
```

## Function

```cpp
void test(){
   cout<<"test function";
}
int main()
{
   test();

}

```

if a user-defined function is declared after the main() function,an error will occur.

its feature makes cpp different from java/python

### Pass by Reference

when you need to change the value of arguments ,you can use reference,

directly control the address of variables whether or not inside the function

```CPP
void swapNums(int &x, int &y)
{
   int z = x;
   x = y;
   y = z;
   cout<<"X memory address"<<&x<<'\n';
   cout<<"Y memory address"<<&y<<'\n';

}
int main()
{  
   
   int x =10;
   int y =20;
   swapNums(x,y);

   cout<<&x<<endl;
   cout<<&y<<endl;
      
   
}

```

![image-20230101141217725](https://raw.githubusercontent.com/strutter0816/githubPngImags/main/img/202301011412837.png)

### Arrays

pass arrays to a function

```cpp
void myFunction(int myNumbers[5]) {
  for (int i = 0; i < 5; i++) {
    cout << myNumbers[i] << "\n";
  }
}

int main() {
  int myNumbers[5] = {10, 20, 30, 40, 50};
  myFunction(myNumbers);
  return 0;
}
```

### Recursion

```cpp
int sum(int k)
{
   if (k > 0)
   {
      /* code */
      return k + sum(k - 1);
   }
   else
   {
      return 0;
   }
}
int main()
{

   int result = sum(100);
   cout << result;
}
```

the program follows these steps

10 + sum(9)
10 + ( 9 + sum(8) )
10 + ( 9 + ( 8 + sum(7) ) )
...
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + sum(0)
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + 0

## Classes

```cpp
class myClass
{
public:
   int no;
   string name;
};

int main()
{

   myClass myclass;
   myclass.name = "Leonard Chow";
   myclass.no = 20;
}

```

### Constructor Parameter

```cpp
class Car {        // The class
  public:          // Access specifier
    string brand;  // Attribute
    string model;  // Attribute
    int year;      // Attribute
    Car(string x, string y, int z) { // Constructor with parameters
      brand = x;
      model = y;
      year = z;
    }
};

int main() {
  // Create Car objects and call the constructor with different values
  Car carObj1("BMW", "X5", 1999);
  Car carObj2("Ford", "Mustang", 1969);

  // Print values
  cout << carObj1.brand << " " << carObj1.model << " " << carObj1.year << "\n";
  cout << carObj2.brand << " " << carObj2.model << " " << carObj2.year << "\n";
  return 0;
}
```

### Access Specifiers

- public --members are accessible from outside the class
- private --members cannot be accessed from outside the class
- protected  --member cannot be accessed from outside the class, however, they can be accessed in inherited classes. You will learn more about Inheritance later.

```cpp
class MyClass {
  public:    // Public access specifier
    int x;   // Public attribute
  private:   // Private access specifier
    int y;   // Private attribute
};

int main() {
  MyClass myObj;
  myObj.x = 25;  // Allowed (public)
  myObj.y = 50;  // Not allowed (private)
  return 0;
}
```

if you try to access to private member ,an erroe occurs

```
error: y is private
```

### Encapsulation

we should make sure that "sensitive " data is hidden from users, To achieve this ,we must declare class variables/attributes as private(cannot be accessed from the outside class).Then we should provide getter and setter methods

```cpp
class Employee {
  private:
    // Private attribute
    int salary;

  public:
    // Setter
    void setSalary(int s) {
      salary = s;
    }
    // Getter
    int getSalary() {
      return salary;
    }
};
```

### Inheritance

To inherit from a class,use the **:** symbol

```CPP
// Base class
class Vehicle {
  public:
    string brand = "Ford";
    void honk() {
      cout << "Tuut, tuut! \n" ;
    }
};

// Derived class
class Car: public Vehicle {
  public:
    string model = "Mustang";
};

int main() {
  Car myCar;
  myCar.honk();
  cout << myCar.brand + " " + myCar.model;
  return 0;
}
```

#### Multilevel Inheritance

```cpp
// Base class (parent)
class MyClass {
  public:
    void myFunction() {
      cout << "Some content in parent class." ;
    }
};

// Derived class (child)
class MyChild: public MyClass {
};

// Derived class (grandchild)
class MyGrandChild: public MyChild {
};

int main() {
  MyGrandChild myObj;
  myObj.myFunction();
  return 0;
}
```

OR

```cpp
// Base class
class MyClass {
  public:
    void myFunction() {
      cout << "Some content in parent class." ;
    }
};

// Another base class
class MyOtherClass {
  public:
    void myOtherFunction() {
      cout << "Some content in another class." ;
    }
};

// Derived class
class MyChildClass: public MyClass, public MyOtherClass {
};

int main() {
  MyChildClass myObj;
  myObj.myFunction();
  myObj.myOtherFunction();
  return 0;
}
```

#### Access Specifiers

used protected which is similar to private, but it can be accessed in the inherited class.

```cpp
// Base class
class Employee {
  protected: // Protected access specifier
    int salary;
};

// Derived class
class Programmer: public Employee {
  public:
    int bonus;
    void setSalary(int s) {
      salary = s;
    }
    int getSalary() {
      return salary;
    }
};

int main() {
  Programmer myObj;
  myObj.setSalary(50000);
  myObj.bonus = 15000;
  cout << "Salary: " << myObj.getSalary() << "\n";
  cout << "Bonus: " << myObj.bonus << "\n";
  return 0;
}
```

### Files

```cpp
#include<iostream>
#include<fstream>
```

- ofstream --- create and write to files
- ifstream -- Reads from files
- fstream -- A combination of ofstream and ifstream: create read write to files

Create and write to a file

```CPP
#include<iostream>
#include<fstream>
using namespace std;
int main(){
   ofstream Myfile("test.txt");
   Myfile <<"stay hungery and stay foolish!";
   Myfile.close();
   return 0;

}
```

Read a file

```cpp
int main(){
   string myText;
   ifstream MyreadFile("test.txt");
   while (getline(MyreadFile,myText))
   {
      /* code */
      cout<<myText<<endl;
   }
   MyreadFile.close();
   

}
```

### Exceptions

three keyword  :**try**  **throw** **catch**

we use try block to test code if we throw the exception 

**throw** keyword to output a reference number



```cpp
  try
   {
      int age = 5;
      if (age >= 18)
      {
         cout << "Access granted - you are old enough.";
      }
      else
      {
         throw(age);
      }
   }
   catch (int myNum)
   {
      cout << "Access denied - You must be at least 18 years old.\n";
      cout << "Age is: " << myNum;
   }
```

in catch block we can use a reference number we throwed;if we don't know what type we use ,we can use the "three dots" inside the catch block

just like this 

```cpp
catch (...){
  // code
}
```


