# object对象

## equals方法  

Object类中的equals方法用于检测一个对象是否等于另外一个对象。 在Object类中， 这个方法将判断两个对象是否具有相同的引用。 如果两个对象具有相同的引用， 它们一定是相等的。 从这点上看， 将其作为默认操作也是合乎情理的。 然而，对于多数类来说， 这种判断并没有什么意义。 例如， 采用这种方式比较两个
PrintStream对象是否相等就完全没有意义。 然而， 经常需要检测两个对象状态的相等性， 如果两个对象的状态相等， 就认为这两个对象是相等的。  

例如， 如果两个雇员对象的姓名、 薪水和雇佣日期都一样， 就认为它们是相等的（ 在实际的雇员数据库中， 比较ID更有意义。 利用下面这个示例演示equals方法的实现机制） 。  

![image-20200426154610256](D:\my\study\TyporaNote\Java基础\图片\image-20200426154610256.png)

为了防备name或hireDay可能为null的情况， 需要使用Objects.equals方法。 如果两个参数都为null， Objects.equals（ a， b） 调用将返回true； 如果其中一个参数为null， 则返回false； 否则， 如果两个参数都不为null， 则调用a.equals（ b） 。 利用这个方法， Employee.equals方法的最后一条语句要改写为  

![image-20200426155629783](D:\my\study\TyporaNote\Java基础\图片\image-20200426155629783.png)

在子类中定义equals方法时， 首先调用超类的equals。 如果检测失败， 对象就不可
能相等。 如果超类中的域都相等， 就需要比较子类中的实例域  

![image-20200426155813166](D:\my\study\TyporaNote\Java基础\图片\image-20200426155813166.png)

Java语言规范要求equals方法具有下面的特性  

1） 自反性： 对于任何非空引用x， x.equals（ x） 应该返回true。
2） 对称性： 对于任何引用x和y， 当且仅当y.equals（ x） 返回true，
x.equals（ y） 也应该返回true。
3） 传递性： 对于任何引用x、 y和z， 如果x.equals（ y） 返回true，
y.equals（ z） 返回true， x.equals（ z） 也应该返回true。
4） 一致性： 如果x和y引用的对象没有发生变化， 反复调用x.equals（ y） 应该返回
同样的结果。
5） 对于任意非空引用x， x.equals（ null） 应该返回false。  

下面给出编写一个完美的equals方法的建议：  

1） 显式参数命名为otherObject， 稍后需要将它转换成另一个叫做other的变量。  

2） 检测this与otherObject是否引用同一个对象：  

![image-20200426160202748](D:\my\study\TyporaNote\Java基础\图片\image-20200426160202748.png)

这条语句只是一个优化。 实际上， 这是一种经常采用的形式。 因为计算这个等式要
比一个一个地比较类中的域所付出的代价小得多  

3） 检测otherObject是否为null， 如果为null， 返回false。 这项检测是很必要
的  

![image-20200426160312860](D:\my\study\TyporaNote\Java基础\图片\image-20200426160312860.png)

4） 比较this与otherObject是否属于同一个类。 如果equals的语义在每个子类中
有所改变， 就使用getClass检测：  

![image-20200426160330859](D:\my\study\TyporaNote\Java基础\图片\image-20200426160330859.png)

5） 将otherObject转换为相应的类类型变量：  

![image-20200426160413348](D:\my\study\TyporaNote\Java基础\图片\image-20200426160413348.png)

6） 现在开始对所有需要比较的域进行比较了。 使用==比较基本类型域， 使用
equals比较对象域。 如果所有的域都匹配， 就返回true； 否则返回false。  

![image-20200426160439595](D:\my\study\TyporaNote\Java基础\图片\image-20200426160439595.png)

如果在子类中重新定义equals， 就要在其中包含调用super.equals（ other） 。  

## hashCode方法  

散列码（ hash code） 是由对象导出的一个整型值。 散列码是没有规律的。 如果x和
y是两个不同的对象， x.hashCode（ ） 与y.hashCode（ ） 基本上不会相同。 在表5-
1中列出了几个通过调用String类的hashCode方法得到的散列码。  

String类使用下列算法计算散列码：  

![image-20200426160757385](D:\my\study\TyporaNote\Java基础\图片\image-20200426160757385.png)

由于hashCode方法定义在Object类中， 因此每个对象都有一个默认的散列码， 其值
为对象的存储地址。  

![image-20200426160924605](D:\my\study\TyporaNote\Java基础\图片\image-20200426160924605.png)

![image-20200426160934371](D:\my\study\TyporaNote\Java基础\图片\image-20200426160934371.png)

String和String Builder的散列码  

![image-20200426160951757](D:\my\study\TyporaNote\Java基础\图片\image-20200426160951757.png)

请注意， 字符串s与t拥有相同的散列码， 这是因为字符串的散列码是由内容导出
的。 而字符串缓冲sb与tb却有着不同的散列码， 这是因为在StringBuffer类中没有
定义hashCode方法， 它的散列码是由Object类的默认hashCode方法导出的对象存
储地址。  

如果重新定义equals方法， 就必须重新定义hashCode方法， 以便用户可以将对象插入到散列表中（ 有关散列表的内容将在第9章中讨论） 。hashCode方法应该返回一个整型数值（ 也可以是负数） ， 并合理地组合实例域的散列码， 以便能够让各个不同的对象产生的散列码更加均匀  

例如， 下面是Employee类的hashCode方法  

![image-20200426161558486](D:\my\study\TyporaNote\Java基础\图片\image-20200426161558486.png)

不过， 还可以做得更好。 首先， 最好使用null安全的方法Objects.hashCode。 如果其参数为null， 这个方法会返回0， 否则返回对参数调用hashCode的结果。另外， 使用静态方法Double.hashCode来避免创建Double对象  

![image-20200426161706725](D:\my\study\TyporaNote\Java基础\图片\image-20200426161706725.png)