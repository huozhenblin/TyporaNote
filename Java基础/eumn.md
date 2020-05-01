# 1.枚举的定义

~~~java
//枚举类型，使用关键字enum，内部枚举实例
enum Day {
    MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
~~~

相当简洁，在定义枚举类型时我们使用的关键字是enum，与class关键字类似，只不过前者是定义枚举类型，后者是定义类类型。枚举类型Day中分别定义了从周一到周日的值，这里要注意，值一般是大写的字母，多个值之间以逗号分隔。同时我们应该知道的是枚举类型可以像类(class)类型一样，定义为一个单独的文件，当然也可以定义在其他类内部，更重要的是枚举常量在类型安全性和便捷性都很有保证，如果出现类型问题编译器也会提示我们改进，但务必记住枚举表示的类型其取值是必须有限的，也就是说每个值都是可以枚举出来的，比如上述描述的一周共有七天。
使用 Day day =Day.MONDAY;  直接这样引用

## 反编译

~~~Java
//反编译Day.class
final class Day extends Enum
{
    //编译器为我们添加的静态的values()方法
    public static Day[] values()
    {
        return (Day[])$VALUES.clone();
    }
    //编译器为我们添加的静态的valueOf()方法，注意间接调用了Enum也类的valueOf方法
    public static Day valueOf(String s)
    {
        return (Day)Enum.valueOf(com/zejian/enumdemo/Day, s);
    }
    //私有构造函数
    private Day(String s, int i)
    {
        super(s, i);
    }
     //前面定义的7种枚举实例
    public static final Day MONDAY;
    public static final Day TUESDAY;
    public static final Day WEDNESDAY;
    public static final Day THURSDAY;
    public static final Day FRIDAY;
    public static final Day SATURDAY;
    public static final Day SUNDAY;
    private static final Day $VALUES[];

    static 
    {    
        //实例化枚举实例
        MONDAY = new Day("MONDAY", 0);
        TUESDAY = new Day("TUESDAY", 1);
        WEDNESDAY = new Day("WEDNESDAY", 2);
        THURSDAY = new Day("THURSDAY", 3);
        FRIDAY = new Day("FRIDAY", 4);
        SATURDAY = new Day("SATURDAY", 5);
        SUNDAY = new Day("SUNDAY", 6);
        $VALUES = (new Day[] {
            MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
        });
    }
}
~~~



# 2.枚举的常见方法

## Enum抽象类常见方法

Enum是所有 Java 语言枚举类型的公共基本类（注意Enum是抽象类），以下是它的常见方法

![image-20200423161337614](D:\my\study\TyporaNote\Java基础\图片\image-20200423161337614.png)

示例代码

~~~java
package com.zejian.enumdemo;

/**
 * Created by zejian on 2017/5/7.
 * Blog : http://blog.csdn.net/javazejian [原文地址,请尊重原创]
 */
public class EnumDemo {

    public static void main(String[] args){

        //创建枚举数组
        Day[] days=new Day[]{Day.MONDAY, Day.TUESDAY, Day.WEDNESDAY,
                Day.THURSDAY, Day.FRIDAY, Day.SATURDAY, Day.SUNDAY};

        for (int i = 0; i <days.length ; i++) {
            System.out.println("day["+i+"].ordinal():"+days[i].ordinal());
        }

        System.out.println("-------------------------------------");
        //通过compareTo方法比较,实际上其内部是通过ordinal()值比较的
        System.out.println("days[0].compareTo(days[1]):"+days[0].compareTo(days[1]));
        System.out.println("days[0].compareTo(days[1]):"+days[0].compareTo(days[2]));

        //获取该枚举对象的Class对象引用,当然也可以通过getClass方法
        Class<?> clazz = days[0].getDeclaringClass();
        System.out.println("clazz:"+clazz);

        System.out.println("-------------------------------------");

        //name()
        System.out.println("days[0].name():"+days[0].name());
        System.out.println("days[1].name():"+days[1].name());
        System.out.println("days[2].name():"+days[2].name());
        System.out.println("days[3].name():"+days[3].name());

        System.out.println("-------------------------------------");

        System.out.println("days[0].toString():"+days[0].toString());
        System.out.println("days[1].toString():"+days[1].toString());
        System.out.println("days[2].toString():"+days[2].toString());
        System.out.println("days[3].toString():"+days[3].toString());

        System.out.println("-------------------------------------");

        Day d=Enum.valueOf(Day.class,days[0].name());
        Day d2=Day.valueOf(Day.class,days[0].name());
        System.out.println("d:"+d);
        System.out.println("d2:"+d2);
    }
 /**
 执行结果:
   day[0].ordinal():0
   day[1].ordinal():1
   day[2].ordinal():2
   day[3].ordinal():3
   day[4].ordinal():4
   day[5].ordinal():5
   day[6].ordinal():6
   -------------------------------------
   days[0].compareTo(days[1]):-1
   days[0].compareTo(days[1]):-2
   clazz:class com.zejian.enumdemo.Day
   -------------------------------------
   days[0].name():MONDAY
   days[1].name():TUESDAY
   days[2].name():WEDNESDAY
   days[3].name():THURSDAY
   -------------------------------------
   days[0].toString():MONDAY
   days[1].toString():TUESDAY
   days[2].toString():WEDNESDAY
   days[3].toString():THURSDAY
   -------------------------------------
   d:MONDAY
   d2:MONDAY
   */

}
enum Day {
    MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

~~~

# 3.枚举与Class对象

上述我们提到当枚举实例向上转型为Enum类型后，values()方法将会失效，也就无法一次性获取所有枚举实例变量，但是由于Class对象的存在，即使不使用values()方法，还是有可能一次获取到所有枚举实例变量的，在Class对象中存在如下方法：

![image-20200423162028248](D:\my\study\TyporaNote\Java基础\图片\image-20200423162028248.png)

因此通过getEnumConstants()方法，同样可以轻而易举地获取所有枚举实例变量下面通过代码来演示这个功能：

~~~java
//正常使用
Day[] ds=Day.values();
//向上转型Enum
Enum e = Day.MONDAY;
//无法调用,没有此方法
//e.values();
//获取class对象引用
Class<?> clasz = e.getDeclaringClass();
if(clasz.isEnum()) {
    Day[] dsz = (Day[]) clasz.getEnumConstants();
    System.out.println("dsz:"+Arrays.toString(dsz));
}

/**
   输出结果:
   dsz:[MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY]
 */
~~~

# 4.枚举的进阶用法

在前面的分析中，我们都是基于简单枚举类型的定义，也就是在定义枚举时只定义了枚举实例类型，并没定义方法或者成员变量，实际上使用关键字enum定义的枚举类，除了不能使用继承(因为编译器会自动为我们继承Enum抽象类而Java只支持单继承，因此枚举类是无法手动实现继承的)，可以把enum类当成常规类，也就是说我们可以向enum类中添加方法和变量，甚至是mian方法，下面就来感受一把。

## 向enum类添加方法与自定义构造函数

重新定义一个日期枚举类，带有desc成员变量描述该日期的对于中文描述，同时定义一个getDesc方法，返回中文描述内容，自定义私有构造函数，在声明枚举实例时传入对应的中文描述，代码如下

~~~java
package com.zejian.enumdemo;

/**
 * Created by zejian on 2017/5/8.
 * Blog : http://blog.csdn.net/javazejian [原文地址,请尊重原创]
 */
public enum Day2 {
    MONDAY("星期一"),
    TUESDAY("星期二"),
    WEDNESDAY("星期三"),
    THURSDAY("星期四"),
    FRIDAY("星期五"),
    SATURDAY("星期六"),
    SUNDAY("星期日");//记住要用分号结束

    private String desc;//中文描述

    /**
     * 私有构造,防止被外部调用
     * @param desc
     */
    private Day2(String desc){
        this.desc=desc;
    }

    /**
     * 定义方法,返回描述,跟常规类的定义没区别
     * @return
     */
    public String getDesc(){
        return desc;
    }

    public static void main(String[] args){
        for (Day2 day:Day2.values()) {
            System.out.println("name:"+day.name()+
                    ",desc:"+day.getDesc());
        }
    }

    /**
     输出结果:
     name:MONDAY,desc:星期一
     name:TUESDAY,desc:星期二
     name:WEDNESDAY,desc:星期三
     name:THURSDAY,desc:星期四
     name:FRIDAY,desc:星期五
     name:SATURDAY,desc:星期六
     name:SUNDAY,desc:星期日
     */
}
~~~

从上述代码可知，在enum类中确实可以像定义常规类一样声明变量或者成员方法。但是我们必须注意到，如果打算在enum类中定义方法，务必在声明完枚举实例后使用分号分开，倘若在枚举实例前定义任何方法，编译器都将会报错，无法编译通过，同时即使自定义了构造函数且enum的定义结束，我们也永远无法手动调用构造函数创建枚举实例，毕竟这事只能由编译器执行。
