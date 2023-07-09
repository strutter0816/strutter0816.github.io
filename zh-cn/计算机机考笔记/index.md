# 机考笔记

<!--more-->
## CPP万能头
```cpp
#include<bits/stdc++.h>
using namespace std;
int main(){
  
  return 0 ;
}
```
## C/C++ %s %d %u 基本用法
%d              十进制有符号整数 
%u              十进制
%f              浮点数 
%s              字符串 
%c              单个字符 
%p              指针的值 
%e              指数形式的浮点数 
%x, %X          无符号以十六进制表示的整数 
%0              无符号以八进制表示的整数 
%g              自动选择合适的表示法 


可以在"%"和字母之间加小写字母l, 表示输出的是长型数。 
       %ld   表示输出long整数 
       %lf   表示输出double浮点数

可以在"%"和字母之间插进数字表示最大场宽。 
       例如:  %3d   表示输出3位整型数, 不够3位右对齐。 
                 %9.2f 表示输出场宽为9的浮点数, 其中小数位为2, 整数位为6, 
                  小数点占一位, 不够9位右对齐。 
                  %8s   表示输出8个字符的字符串, 不够8个字符右对齐。 
       如果字符串的长度、或整型数位数超过说明的场宽, 将按其实际长度输出。 
但对浮点数, 若整数部分位数超过了说明的整数位宽度, 将按实际整数位输出; 
若小数部分位数超过了说明的小数位宽度, 则按说明的宽度以四舍五入输出。 
       另外, 若想在输出值前加一些0, 就应在场宽项前加个0。 
       例如:   %04d  表示在输出一个小于4位的数值时, 将在前面补0使其总宽度为4位。 
       如果用浮点数表示字符或整型量的输出格式, 小数点后的数字代表最大宽度, 小数点前的数字代表最小宽度。
       例如: %6.9s 表示显示一个长度不小于6且不大于9的字符串。若大于9,  则第9个字符以后的内容将被删除。

  可以控制输出左对齐或右对齐, 即在"%"和字母之间加入一个"-" 号可说明输出为左对齐, 否则为右对齐。 
    例如:   %-7d  表示输出7位整数左对齐 
               %-10s 表示输出10个字符左对齐

## 迭代器对容器进行遍历
迭代器是一种检查容器内元素并遍历元素的数据类型，通常用于对**C++中各种容器内元素的访问**，但不同的容器有不同的迭代器，初学者可以将迭代器理解为*指针* 因为也是使用*进行访问。
### vector迭代器
```cpp
#include<bits/stdc++.h>
using namespace std;
// 万能头
int main(){
 vector<int> vtr;
 vtr.push_back(1);
 vtr.push_back(2);
 vtr.push_back(4);
 vtr.push_back(6);
 vector<int>:: iterator it;
 for ( it = vtr.begin(); it !=vtr.end(); it++)
 {
    cout<<*it<<" ";
 }
 
return 0;
}
```
输出
```
1 2 4 6
```
## 字符串常用函数
1. String
- string.find(string a ,pos),a 是子字符串，pos是查找开始的位置
- string.length()
- string.strsub(int start,int length) start 是字符串开始的位置，length是子字符串的长度
### set 使用迭代器进行遍历输出
```cpp
 set<string> country;
 country.insert("China");
 country.insert("America");
 country.insert("Canada");
 country.insert("Canada");
 for (set<string>:: iterator it = begin(country) ; it!= country.end(); it++)
 {
    cout<<*it<<" ";
 }
 cout<<endl;
 country.erase("American");
 if(!country.count("American")){
    cout<<"Can't find American"<<endl;

 }
```
## 多组输入
### C
```c
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b;
    while (scanf("%d%d", &a, &b) != EOF) {
        printf("%d\n", a+b);
    }
    return 0;
}
```

一个多组输入的例子
```c
 double a;
    while (scanf("%lf", &a) != EOF)
    {
        if (a < 1000)
        {
          // 使用%g可以除去小数点后面多余的0 如果是整数的话 显示整数
            printf("discount=1,pay=%g\n", a);
        }
        if (a >= 1000 && a < 2000)
        {
            printf("discount=0.95,pay=%g\n", a * 0.95);
        }
        if (a >= 2000 && a < 3000)
        {
            printf("discount=0.9,pay=%g\n", a * 0.9);
        }
        if (a >= 3000 && a < 5000)
        {
            printf("discount=0.85,pay=%g\n", a * 0.85);
        }
        if (a >= 5000)
        {
            printf("discount=0.8,pay=%g\n", a * 0.8);
        }
    }
```
### CPP
```cpp
#include <bits/stdc++.h>  
using namespace std;  
  
int main() {  
    int a, b;  
    while (cin >> a >> b) {  
        cout << a + b << endl;  
    }  
    return 0;  
}  
```
### Java
```java
Scanner stdin = new Scanner(System.in);  
while (stdin.hasNext()) {  
    String s = stdin.next();  
    int n = stdin.nextInt();  
    double b = stdin.nextDouble();  
}  
```
### Python
```python
while True:  
    try:  
        a, b = map(int, input().split())  
        c = a+b  
        print(c)  
    except: #读到文件末尾抛出异常结束循环  
        break  
```


