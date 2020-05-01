# 内部类

## 什么是内部类呢？

内部类（ Inner Class ）就是定义在另外一个类里面的类。与之对应，包含内部类的类被称为外部类。

## 内部类的主要作用如下：

1. 内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一个包中的其他类访问该类

2. 内部类的方法可以直接访问外部类的所有数据，包括私有的数据

3. 内部类所实现的功能使用外部类同样可以实现，只是有时使用内部类更方便

## 内部类有几种呢？

- 成员内部类
- 静态内部类
- 方法内部类
- 匿名内部类

示例

~~~java
//外部类HelloWorld
public class HelloWorld {
    
    // 内部类Inner，类Inner在类HelloWorld的内部
    public class Inner {
        
		// 内部类的方法
		public void show() {
			System.out.println("welcome to imooc!");
		}
	}
    
	public static void main(String[] args) {
        
        // 创建外部类对象
		HelloWorld hello = new HelloWorld();
        // 创建内部类对象
		Inner i = hello.new Inner();
        // 调用内部类对象的方法
		i.show();
	}
}
~~~

# 种类解析

## Java 中的成员内部类

内部类中最常见的就是成员内部类，也称为普通内部类。我们来看如下代码：

~~~java
public class InnerClass {
    //外部类的私有属性name
    private String name = "imooc";

    //外部类的成员属性
    int age = 20;

    //成员内部类Inner
    public class Inner {
        String name = "爱慕课";
        //内部类中的方法
        public void show() {
            System.out.println("外部类中的name：" +       InnerClass.this.name          );
            System.out.println("内部类中的name：" +       this.name           );
            System.out.println("外部类中的age：" + age);
        }
    }

    //测试成员内部类
    public static void main(String[] args) {

        //创建外部类的对象
        InnerClass o = new InnerClass ();

        //创建内部类的对象
        Inner inn =  o.new Inner()            ;

        //调用内部类对象的show方法
        inn.show();
    }
}
~~~

运行结果

![image-20200427095249432](D:\my\study\TyporaNote\Java基础\图片\image-20200427095249432.png)

### **成员内部类的使用方法**：

1、 Inner 类定义在 Outer 类的内部，相当于 Outer 类的一个成员变量的位置，Inner 类可以使用任意访问控制符，如 public 、 protected 、 private 等

2、 Inner 类中定义的 test() 方法可以直接访问 Outer 类中的数据，而不受访问控制符的影响，如直接访问 Outer 类中的私有属性a

3、 定义了成员内部类后，必须使用外部类对象来创建内部类对象，而不能直接去 new 一个内部类对象，即：内部类 对象名 = 外部类对象.new 内部类( );

4、 编译上面的程序后，会发现产生了两个 .class 文件

![img](D:\my\study\TyporaNote\Java基础\图片\53a004590001164004560040.jpg)

其中，第二个是外部类的 .class 文件，第一个是内部类的 .class 文件，即成员内部类的 .class 文件总是这样：外部类名$内部类名.class

注：

1、 外部类是不能直接使用内部类的成员和方法滴

可先创建内部类的对象，然后通过内部类的对象来访问其成员变量和方法。

2、 如果外部类和内部类具有相同的成员变量或方法，内部类默认访问自己的成员变量或方法，如果要访问外部类的成员变量，可以使用 this 关键字。如：

![img](D:\my\study\TyporaNote\Java基础\图片\539e638b0001ab1208200295.jpg)

## Java 中的静态内部类

静态内部类是 static 修饰的内部类，这种内部类的特点是：

1、 静态内部类不能直接访问外部类的非静态成员，但可以通过 **new 外部类().成员** 的方式访问 

2、 如果外部类的静态成员与内部类的成员名称相同，可通过“类名.静态成员”访问外部类的静态成员；如果外部类的静态成员与内部类的成员名称不相同，则可通过“成员名”直接调用外部类的静态成员

3、 创建静态内部类的对象时，不需要外部类的对象，可以直接创建 **内部类 对象名= new 内部类();**

![img](D:\my\study\TyporaNote\Java基础\图片\539e948a0001a71007630511.jpg)

结果

![img](D:\my\study\TyporaNote\Java基础\图片\539e94a500014f0101930052.jpg)

~~~java
public class SinnerClass {

    // 外部类中的静态变量score
    private static int score = 84;
    private int age = 11;

    // 创建静态内部类
    public   static  class SInner {
        // 内部类中的变量score
        int score = 91;

        public void show() {
            System.out.println("访问外部类中的score：" +      SinnerClass.score      );
            System.out.println("访问内部类中的score：" + score);
            System.out.println("访问外部类中的age：" + new SinnerClass().age);
        }
    }

    // 测试静态内部类
    public static void main(String[] args) {
        // 直接创建内部类的对象
        SInner si = new SInner();

        // 调用show方法
        si.show();
    }
}‘
    //结果
 访问外部类中的score：84
访问内部类中的score：91
访问外部类中的age：11
~~~

## Java 中的方法内部类

方法内部类就是内部类定义在外部类的方法中，方法内部类只在该方法的内部可见，即只在该方法内可以使用。

![img](D:\my\study\TyporaNote\Java基础\图片\539ea96700013ca708200621.jpg)

**一定要注意哦：**由于方法内部类不能在外部类的方法以外的地方使用，因此方法内部类不能使用访问控制符和 static 修饰符。

## 匿名内部类

- 匿名内部类是没有访问修饰符的。
- 匿名内部类必须继承一个抽象类或者实现一个接口
- 匿名内部类中不能存在任何静态成员或方法
- 匿名内部类是没有构造方法的，因为它没有类名。
- 与局部内部类相同匿名内部类也可以引用局部变量。此变量也必须声明为 final

~~~java
public class Button {
    public void click(final int params){
        //匿名内部类，实现的是ActionListener接口
        new ActionListener(){
            public void onAction(){
                System.out.println("click action..." + params);
            }
        }.onAction();
    }
    //匿名内部类必须继承或实现一个已有的接口
    public interface ActionListener{
        public void onAction();
    }

    public static void main(String[] args) {
        Button button=new Button();
        button.click();
    }
}

~~~

为什么局部变量需要final修饰呢

因为局部变量和匿名内部类的生命周期不同。

匿名内部类是创建后是存储在堆中的，而方法中的局部变量是存储在Java栈中，当方法执行完毕后，就进行退栈，同时局部变量也会消失。

那么此时匿名内部类还有可能在堆中存储着，那么匿名内部类要到哪里去找这个局部变量呢？

为了解决这个问题编译器为自动地帮我们在匿名内部类中创建了一个局部变量的备份，也就是说即使方法执结束，匿名内部类中还有一个备份，自然就不怕找不到了。

但是问题又来了。

如果局部变量中的a不停的在变化。
那么岂不是也要让备份的a变量无时无刻的变化。
为了保持局部变量与匿名内部类中备份域保持一致。
编译器不得不规定死这些局部域必须是常量，一旦赋值不能再发生变化了。

所以为什么匿名内部类应用外部方法的域必须是常量域的原因所在了。

特别注意
在Java8中已经去掉要对final的修饰限制，但其实只要在匿名内部类使用了，该变量还是会自动变为final类型（只能使用，不能赋值）
