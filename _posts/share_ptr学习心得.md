## 为什么需要用到智能指针
> 主要是对于应用接口而言,比如`void fun1(char **str)`（`str`在函数中分配了空间）或者`char* fun2(...)`
> 这些分配的空间必须要等到调用函数使用完后去释放，但是对于不小心忘记去释放的，就会造成内存泄漏。所以采用智能指针`share_ptr`  

## 如何使用`share_ptr`
1. 智能指针值的内存分配  
> 智能指针与二级指针是有差异的，准去来说智能指针是一个对象
> `shared_ptr<char*> buf = make_shared<char*>(new char[FileSize]);`  

2. 智能指针内存的释放
> 明白
3.


## 什么时候需要写析构函数
1. 会作为某个类的基类的时候，这个时候需要将其写成虚析构函数  
2. 类中有成员变量需要分配空间的时候，需要在析构函数中释放掉这些分配的空间  
```c++
class MyClass
{
    char * content;
    MyClass()
    {
        content = new char[5];
    }

    ~MyClass()
    {
        //防止重复释放
        if (content)
        {
            delete(content);
            content = NULL;
        }
    }
}
```
