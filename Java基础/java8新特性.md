# 1.lambda表达式

方法比较

~~~java
public class java8test {
    @Test
    public void say(){
        System.out.println("hello");
    }
//    原匿名内部类
    @Test
    public void test1(){
        Comparator<Integer> com = new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return Integer.compare(o1, o2);
            }
        };
        TreeSet<Integer> ts = new TreeSet<>(com);

    }
//    lambda表达式
    @Test
    public void  test2(){
        Comparator<Integer> com =(x,y) ->Integer.compare(x, y);
        TreeSet<Integer> ts = new TreeSet<>(com);
    }
}

~~~

## Lambda 表达式语法  

Lambda 表达式在Java 语言中引入了一个新的语法元
素和操作符。这个操作符为 “ ->” ， 该操作符被称
为 Lambda 操作符或剪头操作符。它将 Lambda 分为
两个部分：  

左侧： 指定了 Lambda 表达式需要的所有参数，这个参数就对应就是要实现的接口的方法的参数列表
右侧： 指定了 Lambda 体，即 Lambda 表达式要执行
的功能  ，对抽象方法的具体实现

语法格式一： 无参，无返回值， Lambda 体只需一条语句  

![image-20200427111257928](D:\my\study\TyporaNote\Java基础\图片\image-20200427111257928.png)

语法格式二： Lambda 需要一个参数  

![image-20200427111312452](D:\my\study\TyporaNote\Java基础\图片\image-20200427111312452.png)

语法格式三： Lambda 只需要一个参数时，参数的小括号可以省略  

![image-20200427111329811](D:\my\study\TyporaNote\Java基础\图片\image-20200427111329811.png)

语法格式四： Lambda 需要两个参数，并且有返回值  

![image-20200427112734130](D:\my\study\TyporaNote\Java基础\图片\image-20200427112734130.png)

语法格式五： 当 Lambda 体只有一条语句时， return 与大括号可以省略  

![image-20200427112748874](D:\my\study\TyporaNote\Java基础\图片\image-20200427112748874.png)

语法格式六：  

![image-20200427112815858](D:\my\study\TyporaNote\Java基础\图片\image-20200427112815858.png)

类型推断

上述 Lambda 表达式中的参数类型都是由编译器推断
得出的。 Lambda 表达式中无需指定类型，程序依然可
以编译，这是因为 javac 根据程序的上下文，在后台
推断出了参数的类型。 Lambda 表达式的类型依赖于上
下文环境，是由编译器推断出来的。这就是所谓的
“类型推断”  

# 2-函数式接口  

只包含一个抽象方法的接口，称为函数式接口  

你可以通过 Lambda 表达式来创建该接口的对象。（若 Lambda
表达式抛出一个受检异常，那么该异常需要在目标接口的抽象方
法上进行声明）。  

我们可以在任意函数式接口上使用 @FunctionalInterface 注解，
这样做可以检查它是否是一个函数式接口，同时 javadoc 也会包
含一条声明，说明这个接口是一个函数式接口。  

# 3Java 内置四大核心函数式接口  

四大核心接口

| 函数式接口                | 参数类型 | 返回类型 | 用途                                                         |
| ------------------------- | -------- | -------- | ------------------------------------------------------------ |
| Consumer<T> 消费型接口    | T        | void     | 对类型为T的对象应用操 作，包含方法： void accept(T t)        |
| Supplier<T> 供给型接口    | 无       | T        | 返回类型为T的对象，包 含方法： T get();                      |
| Function<T, R> 函数型接口 | T        | R        | 对类型为T的对象应用操 作，并返回结果。结果 是R类型的对象。包含方 法： R apply(T t); |
| Predicate<T> 断定型接口   | T        | boolean  | 确定类型为T的对象是否 满足某约束，并返回 boolean 值。包含方法 boolean test(T t); |

其他接口

| BiFunction<T, U, R>                                    | T, U            | R               | 对类型为 T, U 参数应用 操作， 返回 R 类型的结 果。 包含方法为 R apply(T t, U u); |
| ------------------------------------------------------ | --------------- | --------------- | ------------------------------------------------------------ |
| UnaryOperator<T> (Function子接口)                      | T               | T               | 对类型为T的对象进行一 元运算， 并返回T类型的 结果。 包含方法为 T apply(T t); |
| BinaryOperator<T> (BiFunction 子接口)                  | T, T            | T               | 对类型为T的对象进行二 元运算， 并返回T类型的 结果。 包含方法为 T apply(T t1, T t2); |
| BiConsumer<T, U>                                       | T, U            | void            | 对类型为T, U 参数应用 操作。 包含方法为 void accept(T t, U u) |
| ToIntFunction<T> ToLongFunction<T> ToDoubleFunction<T> | T               | int long double | 分 别 计 算 int 、 long 、 double、 值的函数                 |
| IntFunction<R> LongFunction<R> DoubleFunction<R>       | int long double | R               | 参数分别为int、 long、 double 类型的函数                     |

# 4-方法引用与构造器引用  

## 方法引用

当要传递给Lambda体的操作，已经有实现的方法了，可以使用方法引用！（ 实现抽象方法的参数列表，必须与方法引用方法的参数列表保持一致！ ）方法引用：使用操作符 “ ::” 将方法名和对象或类的名字分隔开来。如下三种主要使用情况：  

 对象::实例方法

直接调用流中的实例的方式: 注意下面的Emp::getJob 就相当于集合中每一个emp对象都调用自己的getJob方法.

这个例子是讲将集合转换为流,map()方法可以理解为对集合的每一个元素进行相应的操作,这里就是对每一个emp实例调用getJob方法.最后.collect(Collectors.toList())将流转换为新的list集合(关于流,笔者后面会继续更新相关的博客).

```
listEmp.stream().map(Emp::getJob).collect(Collectors.toList());
```

 类::静态方法
 类::实例方法  



![image-20200427160727070](D:\my\study\TyporaNote\Java基础\图片\image-20200427160727070.png)

![image-20200427160737043](D:\my\study\TyporaNote\Java基础\图片\image-20200427160737043.png)

![image-20200427160749469](D:\my\study\TyporaNote\Java基础\图片\image-20200427160749469.png)

![image-20200427161002343](D:\my\study\TyporaNote\Java基础\图片\image-20200427161002343.png)

![image-20200427161158521](D:\my\study\TyporaNote\Java基础\图片\image-20200427161158521.png)



注意： 当需要引用方法的第一个参数是实例方法的调用者，而第二个参数是实例方法的参数是： ClassName::methodName  

![image-20200427162036811](D:\my\study\TyporaNote\Java基础\图片\image-20200427162036811.png)

## 构造器引用  

格式： ClassName::new  

与函数式接口相结合，自动与函数式接口中方法兼容。可以把构造器引用赋值给定义的方法，与构造器参数
列表要与接口中抽象方法的参数列表一致！  

![image-20200427162426775](D:\my\study\TyporaNote\Java基础\图片\image-20200427162426775.png)

## 数组引用  

格式： type[] :: new  

![image-20200427162852468](D:\my\study\TyporaNote\Java基础\图片\image-20200427162852468.png)

![image-20200427163010864](D:\my\study\TyporaNote\Java基础\图片\image-20200427163010864.png)

# 5.Stream

Java8中有两大最为重要的改变。第一个是 Lambda 表达式；另外一个则是 StreamAPI(java.util.stream.*)

Stream 是 Java8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。使用Stream API 对集合数据进行操作，就类似于使用 SQL 执行的数据库查询。也可以使用 Stream API 来并行执行操作。简而言之，Stream API 提供了一种高效且易于使用的处理数据的方式。  

图例

![image-20200427163744079](D:\my\study\TyporaNote\Java基础\图片\image-20200427163744079.png)

## 流(Stream) 到底是什么呢？

是数据渠道，用于操作数据源（集合、数组等）所生成的元素序列。
“集合讲的是数据，流讲的是计算！ ”  

注意：  

①Stream 自己不会存储元素。
②Stream 不会改变源对象。相反，他们会返回一个持有结果的新Stream。
③Stream 操作是延迟执行的。这意味着他们会等到需要结果的时候才执行。  

## Stream 的操作三个步骤  

创建 Stream  

一个数据源（如： 集合、数组）， 获取一个流  

中间操作  

一个中间操作链，对数据源的数据进行处理  

终止操作(终端操作)  

一个终止操作，执行中间操作链，并产生结果  

![image-20200427163934695](D:\my\study\TyporaNote\Java基础\图片\image-20200427163934695.png)

## 创建 Stream  

示例

![image-20200427164856111](D:\my\study\TyporaNote\Java基础\图片\image-20200427164856111.png)

Java8 中的 Collection 接口被扩展，提供了两个获取流的方法：  

- default Stream<E> stream() : 返回一个顺序流

- default Stream<E> parallelStream() : 返回一个并行流  

由数组创建流  

Java8 中的 Arrays 的静态方法 stream() 可以获取数组流：  

static <T> Stream<T> stream(T[] array): 返回一个流  

重载形式，能够处理对应基本类型的数组：
 public static IntStream stream(int[] array)
 public static LongStream stream(long[] array)
 public static DoubleStream stream(double[] array)  

由值创建流  

可以使用静态方法 Stream.of(), 通过显示值
创建一个流。它可以接收任意数量的参数。  

public static<T> Stream<T> of(T... values) : 返回一个流  

由函数创建流：创建无限流  

可以使用静态方法 Stream.iterate() 和Stream.generate(), 创建无限流。  

 迭代
public static<T> Stream<T> iterate(final T seed, final
UnaryOperator<T> f)
 生成
public static<T> Stream<T> generate(Supplier<T> s) :  

## Stream 的中间操作  

多个中间操作可以连接起来形成一个流水线，除非流水线上触发终止操作，否则中间操作不会执行任何的处理！
而在终止操作时一次性全部处理，称为“惰性求值” 。  

### 筛选与切片  

![image-20200427165740023](D:\my\study\TyporaNote\Java基础\图片\image-20200427165740023.png)

### 映射  

![image-20200427165908875](D:\my\study\TyporaNote\Java基础\图片\image-20200427165908875.png)

### 排序  

![image-20200427165930186](D:\my\study\TyporaNote\Java基础\图片\image-20200427165930186.png)

## Stream 的终止操作  

终端操作会从流的流水线生成结果。其结果可以是任何不是流的值，例如： List、 Integer，甚至是 void 。 

###  查找与匹配  

![image-20200427171347830](D:\my\study\TyporaNote\Java基础\图片\image-20200427171347830.png)

![image-20200427170420476](D:\my\study\TyporaNote\Java基础\图片\image-20200427170420476.png)

### 归约  

![image-20200427170455241](D:\my\study\TyporaNote\Java基础\图片\image-20200427170455241.png)

![image-20200428105406629](D:\my\study\TyporaNote\Java基础\图片\image-20200428105406629.png)



### 收集  

![image-20200427171426389](D:\my\study\TyporaNote\Java基础\图片\image-20200427171426389.png)

Collector 接口中方法的实现决定了如何对流执行收集操作(如收集到 List、 Set、 Map)。但是 Collectors 实用类提供了很多静态方法，可以方便地创建常见收集器实例， 具体方法与实例如下表：  

![image-20200427171521311](D:\my\study\TyporaNote\Java基础\图片\image-20200427171521311.png)

![image-20200427171547896](D:\my\study\TyporaNote\Java基础\图片\image-20200427171547896.png)

## 示例代码

~~~java
public void test2(){
        List<employee> employees = Arrays.asList(
                new employee(),
                new employee(),
                new employee(),
                new employee()

        );
        employees.stream().map(new Function<employee, Object>() {
            @Override
            public Object apply(employee employee) {
                return employee.getName();
            }
        });
        employees.stream().map(employee -> employee.getAge());
        employees.stream().map(employee::getAge);

    }
~~~



## 并行流与串行流  

并行流就是把一个内容分成多个数据块，并用不同的线程分别处理每个数据块的流。

Java 8 中将并行进行了优化，我们可以很容易的对数据进行并行操作。 Stream API 可以声明性地通过 parallel() 与sequential() 在并行流与顺序流之间进行切换。  

### 了解 Fork/Join 框架  

![image-20200428163548029](D:\my\study\TyporaNote\Java基础\图片\image-20200428163548029.png)

### Fork/Join 框架与传统线程池的区别  

采用 “工作窃取”模式（ work-stealing）：
当执行新的任务时它可以将其拆分分成更小的任务执行，并将小任务加到线程队列中，然后再从一个随机线程的队列中偷一个并把它放在自己的队列中。相对于一般的线程池实现,fork/join框架的优势体现在对其中包含的任务的
处理方式上.在一般的线程池中,如果一个线程正在执行的任务由于某些原因无法继续运行,那么该线程会处于等待状态.而在fork/join框架实现中,如果某个子问题由于等待另外一个子问题的完成而无法继续运行.那么处理该子问题的线程会主动寻找其他尚未运行的子问题来执行.这种方式减少了线程的等待时间,提高了性能  

## Optional 类  

Optional<T> 类(java.util.Optional) 是一个容器类，代表一个值存在或不存在，原来用 null 表示一个值不存在，现在 Optional 可以更好的表达这个概念。并且可以避免空指针异常  

常用方法：  

- Optional.of(T t) : 创建一个 Optional 实例

- Optional.empty() : 创建一个空的 Optional 实例

- Optional.ofNullable(T t):若 t 不为 null,创建 Optional 实例,否则创建空实例
- isPresent() : 判断是否包含值
- orElse(T t) : 如果调用对象包含值，返回该值，否则返回t
- orElseGet(Supplier s) :如果调用对象包含值，返回该值，否则返回 s 获取的值
- map(Function f): 如果有值对其处理，并返回处理后的Optional，否则返回 Optional.empty()
- flatMap(Function mapper):与 map 类似，要求返回值必须是Optional  



