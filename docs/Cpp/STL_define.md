# STL库的杂碎知识
## 优先队列的使用
优先队列是按照重载的小于规则，按照从大到小的顺序排列的
### 声明方式：
1、普通方法：
```cpp
priority_queue<int> q;   　　　　　　　　　　　　  //通过操作，按照元素从大到小的顺序出队

priority_queue<int,vector<int>, greater<int> > q;  　　//通过操作，按照元素从小到大的顺序出队
```
2、自定义优先级：
```cpp
struct cmp {     
　　operator bool ()(int x, int y)     
　　{        
　　　　 return　x > y;　　 // x小的优先级高       //也可以写成其他方式，如： return p[x] > p[y];表示p[i]小的优先级高
　　}
};
priority_queue<int, vector<int>, cmp> q;    //定义方法
//其中，第二个参数为容器类型。第三个参数为比较函数。
```
3、结构体声明方式：
```cpp
struct node {     
　　int x, y;     
　　friend bool operator < (node a, node b)     
　　{         
　　　　return a.x > b.x;    //结构体中，x小的优先级高     
　　}
};
priority_queue<node>q;   //定义方法
//在该结构中，y为值, x为优先级。
//通过自定义operator<操作符来比较元素中的优先级。
//在重载”<”时，最好不要重载”>”，可能会发生编译错误
```

## unordered_map使用

基于哈希表，便于进行字典操作，可以直接用[]运算符来直接取key的value
### 遍历判断是否在里面有该键值
```cpp
unordered_map<int,int> test;
if(test.find()==test.end()){
    .......
}
```

## set使用

set是基于红黑树的天然有序结构，所以在任何时候都是有序的
### 基本方法
begin()     　　 ,返回set容器的第一个元素

end() 　　　　 ,返回set容器的最后一个元素

clear()   　　     ,删除set容器中的所有的元素

empty() 　　　,判断set容器是否为空

max_size() 　 ,返回set容器可能包含的元素最大个数

size() 　　　　 ,返回当前set容器中的元素个数

rbegin　　　　 ,返回的值和end()相同

rend()　　　　 ,返回的值和rbegin()相同

count() ，     用来查找set中某个某个键值出现的次数。一个键值在set只可能出现0或1次

find()  ，     返回给定值值得定位器(iterator)，如果没找到则返回end()
### erase方法
erase(iterator)  ,删除定位器iterator指向的值

erase(first,second),删除定位器first和second之间的值

erase(key_value),删除键值key_value的值
### 搜寻某值
```cpp
set<int> test;
if(test.find()==test.end()){
    ......
}
```
## unordered_set使用

无序，易于删除等操作，基于哈希表，不允许重复字符出现，所以可以用来排重

搜寻值同样可以类似于set的find方法去调用

如果键值存在于unordered_set里面，可以使用erase方法将元素删除,方法类似于set的erase方法

## vector使用

### erase方法的使用
与set不同，由于set独特的不重复的机制，使得在调用erase方法时可以直接erase(value),对于vector就只能使用定位器去删除，要删除特定值就得先定位再删除，可以配合find和erase

函数原型：
> iterator erase(iterator position);
>
> iterator erase(iterator first, iterator last);
>
> 返回一个iterator ，指向删除元素的下一个元素。
>
所以在用for循环删除元素时，迭代器不用++指向下一个元素，erase()执行后，自动返回一个迭代器指向下一个元素。
```cpp
for(vector<int>::iterator iter=veci.begin(); iter!=veci.end(); )
{
     if( *iter == 3)
          iter = veci.erase(iter);
      else
            iter ++ ;
}
```
注意删除的时候，如果删除的是iter，而没有将erase的返回值存储或者利用其他手段，删除的那个地方的指针将会变为野指针，一定要注意

## algorithm库使用

### sort函数
> void sort(begin,end);
> 
> void sort(begin,end,compare);

begin和end在排序数组的时候，用数组指针即可，排序vector等的话可以使用begin()和end()方法来得到迭代器，当然，排序的时候包含begin不包含end，也可以编辑compare函数进行自定义排序。

下为示例：
```cpp
bool myfunction (int i,int j) { return (i<j); }

struct myclass {
  bool operator() (int i,int j) { return (i<j);}
} myobject;

int main () {
  int myints[] = {32,71,12,45,26,80,53,33};
  std::vector<int> myvector (myints, myints+8);               // 32 71 12 45 26 80 53 33

  // using default comparison (operator <):
  std::sort (myvector.begin(), myvector.begin()+4);           //(12 32 45 71)26 80 53 33

  // using function as comp
  std::sort (myvector.begin()+4, myvector.end(), myfunction); // 12 32 45 71(26 33 53 80)

  // using object as comp
  std::sort (myvector.begin(), myvector.end(), myobject);     //(12 26 32 33 45 53 71 80)

  return 0;
}
```