# Cpp的一些知识杂碎

## Cpp类的定义
Cpp类的构造函数中，可以采用这样的定义方式
```cpp
class test{
public:
    int x;
    int y;
    test(int a,int b):x(a),y(b){
        cout<<"finished"<<endl;
    }
};
```
## Cpp关于类的指针
对于类来说，new返回的是一个新元素的指针，这里会调用构造函数，而声明指针只是初始化一个指针，不会调用构造函数，所以新建一个指针不会新建一个对象，只有new才会新建一个对象并返回指针，直接声明对象不返回结果。

例如：ListNode L(0),新建一个对象而不返回任何结果，而ListNode * ptr; ptr=new ListNode(0); new返回一个指针，将其赋给ptr，当然ptr作为指针后面也可以更新到其他地方，但像前一个声明对象的方式，L就只能代表这个对象了，不利于循环的实现以及链表的实现，注意日常使用

## memset函数
void *memset(void *s, int ch, size_t n);

函数解释：将s中当前位置后面的n个字节 （typedef unsigned int size_t ）用 ch 替换并返回 s 。

memset：作用是在一段内存块中填充某个给定的值，它是对较大的结构体或数组进行清零操作的一种最快方法。

memset()函数原型是extern void *memset(void *buffer, int c, int count) 
- buffer：为指针或是数组
- c：是赋给buffer的值，函数在填充内存块时是使用该值的无符号字符形式，所以c的范围为0-255。
- count：是buffer的长度
- eg: memset(f,0,n); //f为指针