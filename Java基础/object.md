下面给出编写一个完美的equals方法的建议：  

1） 显式参数命名为otherObject， 稍后需要将它转换成另一个叫做other的变量。
2） 检测this与otherObject是否引用同一个对象：
这条语句只是一个优化。 实际上， 这是一种经常采用的形式。 因为计算这个等式要
比一个一个地比较类中的域所付出的代价小得多。
3） 检测otherObject是否为null， 如果为null， 返回false。 这项检测是很必要
的。
4） 比较this与otherObject是否属于同一个类。 如果equals的语义在每个子类中
有所改变， 就使用getClass检测：
如果所有的子类都拥有统一的语义， 就使用instanceof检测：
5） 将otherObject转换为相应的类类型变量：
6） 现在开始对所有需要比较的域进行比较了。 使用==比较基本类型域， 使用
equals比较对象域。 如果所有的域都匹配， 就返回true； 否则返回false。
如果在子类中重新定义equals， 就要在其中包含调用super.equals（ other） 。  

示例

![image-20200421124627044](D:\my\study\TyporaNote\Java基础\图片\image-20200421124627044.png)