# C#-单例模式



## 简介

​	当我们在程序中执行某一些操作时，会执行创建对象的操作。但当我们将执行一个重复的操作多次时，就有可能创建多个无用的对象。

​	在使用单例模式时，我们就可以保证创建的对象永远只有一个。



## 实现方法

​	调用需要创建的对象所提供的特殊创建方法，该方法中将会判断是否已经创建过该对象，若是已经创建过，则直接返回已经创建的对象。代码如下：

~~~c#
class Class1
{
    public static Class1 class1 = null;//整个程序唯一的Class1对象
    
    private class1(){}
    
    public static Class1 Create()
    {
        if(class1==null)		//如果没有创建过对象，则创建
        {
            class1 = new Class1();
        }
        return class1;
    }
}

class class2
{
    newClass1 = Class1.Create(); //调用Class1类中提供的静态创建函数
}
~~~

