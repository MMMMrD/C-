# C#-事件（event）



## 为什么要使用事件

​	根据之前在委托中的所学知识，我们可以了解到委托中可以存入一个或多个相同返回值与参数的函数，这样在调用委托的使用就会将委托中存入的所有函数都调用一遍，用不着在一个一个的调用各个函数，很好的实现了程序的封装。

​	但是这又出现了另一些问题——委托是可以被赋值的，且委托被赋值之后，从前保存的函数将不再存在。针对这一问题，先辈们提出了事件的解决方法。



## 事件是什么？

​	为了防止各种参数被修改，于是拥有了参数的属性。同样的，为了防止委托被修改，于是出现了事件。事件不允许被直接赋值，只可以用 “+=” 和 “-=” 对其中保存的函数进行修改，提高了程序的安全型。

​	事件在类中声明且生成，且通过使用同一个类或其他类中的委托与事件处理程序关联。包含事件的类用于发布事件。这被称为 **发布器（publisher）** 类。其他接受该事件的类被称为 **订阅器（subscriber）** 类。事件使用 **发布-订阅（publisher-subscriber）** 模型。

​	**发布器（publisher）** 是一个包含事件和委托定义的对象。事件和委托之间的联系也定义在这个对象中。发布器（publisher）类的对象调用这个事件，并通知其他的对象。

​	**订阅器（subscriber）** 是一个接受事件并提供事件处理程序的对象。在发布器（publisher）类中的委托调用订阅器（subscriber）类中的方法（事件处理程序）。



## 声明事件（Event）

在类的内部声明事件，首先必须声明该事件的委托类型。例如：

```
public delegate void BoilerLogHandler(string status);
```

然后，声明事件本身，使用 **event** 关键字：

```
// 基于上面的委托定义事件
public event BoilerLogHandler BoilerEventLog;
```

上面的代码定义了一个名为 *BoilerLogHandler* 的委托和一个名为 *BoilerEventLog* 的事件，该事件在生成的时候会调用委托。



## 实例

~~~c#
using System;
namespace SimpleEvent
{
  using System;
  /***********发布器类***********/
  public class EventTest
  {
    private int value;

    public delegate void NumManipulationHandler();//声明委托

    public event NumManipulationHandler ChangeNum;//声明事件
    
    protected virtual void OnNumChanged()
    {
      if ( ChangeNum != null )
      {
        ChangeNum(); /* 事件被触发 */
      }
      else
      {
        Console.WriteLine( "event not fire" );
        Console.ReadKey(); /* 回车继续 */
      }
    }


    public EventTest() //构造函数，将变量value设置为初始值5
    {
      int n = 5;
      SetValue( n );
    }


    public void SetValue( int n )//设置变量value
    {
      if ( value != n )
      {
        value = n;
        OnNumChanged();
      }
    }
  }


  /***********订阅器类***********/

  public class subscribEvent
  {
    public void printf()
    {
      Console.WriteLine( "event fire" );
      Console.ReadKey(); /* 回车继续 */
    }
  }

  /***********触发***********/
  public class MainClass
  {
    public static void Main()
    {
      EventTest e = new EventTest(); /* 实例化对象,第一次没有触发事件 */
      
      subscribEvent v = new subscribEvent(); /* 实例化对象 */
      
      e.ChangeNum += new EventTest.NumManipulationHandler( v.printf ); 
        /* 注册 */
      
      e.SetValue( 7 );
      e.SetValue( 11 );
    }
  }
}
~~~

