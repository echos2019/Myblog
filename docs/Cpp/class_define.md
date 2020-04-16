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