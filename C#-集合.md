# C#-集合



## 1.ArrayList集合

### 1)特点

​	集合相比于数组，没有长度，可以往里面加入各种类型的值。



### 2)相关代码

~~~c#
class Person
{
    static void Main(string[] args)
    {
        ArrayList al = new ArrayList();//创建一个集合对象
        
        al.Add('China');//Add表示将数据添加进集合之中
        
        al.AddRange(new int[]{1,2,3,4,5,6,7});//AddRange表示添加一个集合
        
        int len=al.Count;//集合不能使用Lenth语句获得长度，只能用Count语句获得存储对象数量
    }
}
~~~



### 3)局限

​	储存在集合中的数据，将会很难取出



## 2.Hashtable集合

### 1)特点

​	Hashtable集合又叫**键值对集合**，可以根据 **键** 去找 **值**；

​	键值对集合中，**键**必须是唯一的，但**值**可以是重复的。



### 2)相关代码

>1. 创建代码
>
>   ~~~c#
>   Hashtable ht = new Hashtable();
>   ~~~
>
> 
>
>2. 添加对象代码
>
>   ~~~c#
>   ht.Add(1,"张三");		 //Add(Key,Object)
>   ht.Add(2,"true");	  //如果在集合中已经存在该键，Add语句不会覆盖原来的键值对
>   
>   ht[3] = "新添加的";		//像这样写，也可以添加一个键值对，键为3，值为“新添加的”
>   
>   ht[1] = "替换张三";		/*这样写，如果集合里面没有，就会新增一个键值对，
>   						如果有，就会替换对应键的值*/
>   ~~~
>
>    
>
>3. foreach循环代码
>
>   ~~~c#
>   foreach(var item in collection)
>   {
>       //collection代表集合，也可以填入集合的Keys，item为集合中的每一个对象
>       //var为一个特殊的变量类型，根据对象所存入的值来判断变量类型
>   }
>   ~~~
>
>    
>
>4. 判断集合中是否有想要添加的键
>
>   ~~~c#
>   if(ht.ContainsKey(1))
>   {
>       ht.Add(1,"test");
>   }
>   else
>   {
>       Console.WriteLine("已经包含该键");
>   }
>   ~~~
>
>    
>
>5. 移除集合中的对象
>
>   ~~~c#
>   ht.Remove(key);//根据键移除集合中的元素
>   
>   ht.Clear();//移除集合中所有的元素
>   ~~~







