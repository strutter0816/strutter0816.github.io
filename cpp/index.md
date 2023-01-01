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

