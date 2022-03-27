# C#-委托类型（delegate）



## 为什么要使用委托

​	由前面所学可知，我们可以将操作相同、参数不同的几个方法写成同名方法的重载，以减少代码量。可是，当参数相同时，我们就不能使用重载实现类似的操作。委托就帮我们解决了这类问题。



## 委托概念

​	在某些特定情况下，需要把方法（函数）作为参数传给另一个方法。当一个方法作为参数传递给另一个方法时，这个参数就是委托类型。

​	注意，只有当函数的形参类型与委托的形参类型相同，才能将函数传递给委托。

​	下面是实例代码：

~~~c#
public delegate void DelSayHellow(string name);//创建委托

public SayHellow
{
    static void Main(string[] args)
    {
        Test("张三",ChineseSayHellow);//将函数赋值给委托，传给另一个函数
        Test("lisi",EnglishSayHellow);
        
        //DeleSayHellow dele = ChineseSayHellow;
        //DeleSayHellow dele = new DelSayHellow(ChineseSayHellow);
        //以上两种方法都可以创建委托对象 并将委托对象传给方法
        
        Test("张三"，dele);
    }

    public void Test(string name,DelSayHellow del)//通用打招呼调用
    {
        del(name);
    }

    public void ChineseSayHellow(string name)//中文打招呼
    {
        Console.WriteLine("吃了吗？"+name);
    }

    public void EnglishSayHellow(string name)//英文打招呼
    {
        Console.WriteLine("Nice to meet you"+name);
    }

}
~~~



## 匿名函数

​	由上述代码可知，使用委托可以将函数传给另一个函数，但却没有让代码量减少，甚至不如直接使用原函数，于是出现了匿名函数。

​	由委托可知，可以将一个函数当作参数传给另一个函数。如果作为参数的函数在程序运行周期中只使用一次，那么这个定义过的函数既会占内存空间，又有可能使函数名混淆。入不定义该函数，而是直接将该函数写在形参位置，则可以避免这些问题。

~~~c#
public delegate void DelSayHi(string name);

class Test
{
    static coid Main(string[] args)
    {
        String[] names = {"abcdeFG","HiJkLmN"};
		ProStr(names,delegate(string name)
        {
        	return "\""+ name +"\""; //写一个函数作为参数传给另一个函数   
        });
    }
    
    public static void ProStr(string[] name,DelSayHi del)
    {
        for(int i=0;i<name.Length;i++)
        {
            name[i] = del(name[i]);
        }
    }
}
~~~

​	由上述代码看到，我们直接将一个函数赋值给了一个定义过的委托，就可以通过直接调用这个委托来调用这个函数，从而极大的减少了代码量，也提升了代码可读性。这在开发大型程序的时候是十分重要的



## 泛型委托

​	在定义一个函数时，我们可以先假设期参数类型为T，等到使用该函数时，再声明具体的参数类型。这样就可以让一个相同的方法对不同的参数类型使用。

~~~c#
public delegate int DelMax<T>(T num1,T num2);
    class Program
    {
        static void Main(string[] args)
        {
            int[] array = { 1, 2, 3, 4, 5 };
            int result = GetMax<int>(array, (int num1, int num2) =>
             {
                 return num1 - num2;
             });//lamda表达式创建委托
            
            string[] strs = {"abcd","efg"};
            string str = GetMax(strs,(string str1,string str2) =>
            {
                return str1.Lenth - str2.Lenth;
            });

            Console.WriteLine(result);
        }

        public static T GetMax<T>(T[] nums,DelMax<T> del)
            //建立一个参数类型为T的、获得数组中的最大值的函数
        {
            T max = nums[0];
            
            for(int i=1;i<nums.Length;i++)
            {
                if(del(max,nums[i])<0)//使用委托判断大小
                {
                    max = nums[i];
                }
            }

            return max;
        }
    }
~~~

​	由上述代码可以看出，我们对 **相同的函数** 传入了两个 **不同的参数类型**



## lamda表达式

​	**lamda表达式** 可以看作是匿名函数的缩写，可以有效的简写代码。

~~~c#
public delegate int test(int num);

class Test
{
    test t = (int n) => { return n };//将int型参数n，传给方法体
}
~~~

​	在集合中，lamda表达式还可以直接写成如下代码

~~~c#
using System;
using System.Collections.Generic;

	class Program
    {
        static void Main(string[] args)
        {
            List<int> intList = new List<int> { 1, 2, 3, 4, 5 };
            intList.RemoveAll(n => n > 4);
			//利用lamda表达式将一个函数传给另一个函数
            
            Console.WriteLine(intList);
        } 
    }
~~~



