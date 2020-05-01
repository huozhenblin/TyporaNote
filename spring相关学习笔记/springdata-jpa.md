# 1.springdate-jpa概念

Spring数据存储库抽象中的中心接口是repository。它以domain class和domain class的ID类型作为类型参数来管理。此接口主要用作标记接口，用于捕获要使用的类型并帮助您发现扩展此接口的接口。CrudRepository为正在管理的实体类提供了复杂的CRUD功能。

`CrudRepository` **interface**

~~~java
public interface CrudRepository<T, ID> extends Repository<T, ID> {

  <S extends T> S save(S entity);      	Saves the given entity.

  Optional<T> findById(ID primaryKey); Returns the entity identified by the given ID.

  Iterable<T> findAll();           	Returns all entities.    

  long count();      	Returns the number of entities.                  

  void delete(T entity);         Deletes the given entity.      

  boolean existsById(ID primaryKey);   	Indicates whether an entity with the given ID exists.


  // … more functionality omitted.
}
~~~

我们还提供了特定于持久性技术的抽象，如JpaRepository或MongoRepository。这些接口扩展了CrudRepository并公开了底层持久性技术的功能，此外还公开了与持久性技术无关的通用接口，如CrudRepository。

在CrudRepository的顶部，有一个PagingAndSortingRepository抽象，它添加了额外的方法来简化对实体的分页访问:

**Example 4.** `PagingAndSortingRepository` **interface**

~~~java
public interface PagingAndSortingRepository<T, ID> extends CrudRepository<T, ID> {

  Iterable<T> findAll(Sort sort);

  Page<T> findAll(Pageable pageable);
}
~~~

To access the second page of `User` by a page size of 20, you could do something like the following

~~~java
PagingAndSortingRepository<User, Long> repository = // … get access to a bean
Page<User> users = repository.findAll(PageRequest.of(1, 20));
~~~

除了查询方法之外，还提供了count和delete查询的查询派生。下面的列表显示了一个派生count查询的接口定义:

~~~java
interface UserRepository extends CrudRepository<User, Long> {

  long countByLastname(String lastname);
}
//删除方法
interface UserRepository extends CrudRepository<User, Long> {

  long deleteByLastname(String lastname);

  List<User> removeByLastname(String lastname);
}
~~~

# 2.查询方法

标准的CRUD功能存储库通常对底层数据存储有查询。使用Spring Data，声明这些查询变成了一个四步过程:

## 建立查询的4个步骤

### 第一步 定义存储库接口

Declare an interface extending Repository or one of its subinterfaces and type it to the domain class and ID type that it should handle,

~~~java
interface PersonRepository extends Repository<Person, Long> { … }
~~~

首先，定义一个domain class-specif的存储库接口。接口必须扩展Repository，并将其类型转换为domain class和ID类型。如果您希望为该域类型公开CRUD方法，请扩展CrudRepository而不是Repository。通常，your repository 接口扩展了repository、CrudRepository或PagingAndSortingRepository。

#### 使用不同的Spring数据模块的存储库

如果存储库定义扩展了特定于模块的存储库，那么它就是特定Spring数据模块的有效候选。

下面的例子显示了一个使用模块特定接口(JPA)的存储库:

~~~java
interface MyRepository extends JpaRepository<User, Long> { }

@NoRepositoryBean
interface MyBaseRepository<T, ID> extends JpaRepository<T, ID> { … }

interface UserRepository extends MyBaseRepository<User, Long> { … }
~~~

MyRepository和UserRepository在它们的类型层次结构中扩展了JpaRepository。它们是Spring Data JPA模块的有效候选者。

The following example shows a repository that uses domain classes with annotations:

~~~java
interface PersonRepository extends Repository<Person, Long> { … }

@Entity
class Person { … }

interface UserRepository extends Repository<User, Long> { … }

@Document
class User { … }
~~~

PersonRepository引用Person，它是用JPA @Entity注释的，所以这个存储库显然属于Spring Data JPA。UserRepository引用User，它是用Spring Data MongoDB的@Document注释注释的。

### 第二步创建操作方法

Declare query methods on the interface.

~~~java
interface PersonRepository extends Repository<Person, Long> {
  List<Person> findByLastname(String lastname);
}
~~~

The repository proxy has two ways to derive a store-specific query from the method name:

- By deriving the query from the method name directly.
- By using a manually defined query.

构建在Spring数据存储库基础结构中的查询生成器机制对于在存储库实体上构建约束查询非常有用。该机制从方法中去除find…By、read…By、query…By、count…By和get…By前缀，并开始解析其余部分。引入子句可以包含进一步的表达式，例如使用Distinct来设置要创建的查询上的Distinct标志。但是，第一个通过充当分隔符来指示实际标准的开始。在非常基本的级别上，您可以定义实体属性上的条件，并将它们与and连接起来

示例

~~~java
interface PersonRepository extends Repository<Person, Long> {

  List<Person> findByEmailAddressAndLastname(EmailAddress emailAddress, String lastname);

  // Enables the distinct flag for the query
  List<Person> findDistinctPeopleByLastnameOrFirstname(String lastname, String firstname);
  List<Person> findPeopleDistinctByLastnameOrFirstname(String lastname, String firstname);

  // Enabling ignoring case for an individual property
  List<Person> findByLastnameIgnoreCase(String lastname);
  // Enabling ignoring case for all suitable properties
  List<Person> findByLastnameAndFirstnameAllIgnoreCase(String lastname, String firstname);

  // Enabling static ORDER BY for a query
  List<Person> findByLastnameOrderByFirstnameAsc(String lastname);
  List<Person> findByLastnameOrderByFirstnameDesc(String lastname);
}
~~~

注 

1.属性表达式只能引用被管理实体的直接属性

假设一个人有一个带邮政编码的地址。在这种情况下，该方法创建属性遍历x.address.zipCode。

List<Person> findByAddressZipCode(ZipCode zipCode);

原理

解析算法首先将整个部分(AddressZipCode)解释为属性，然后检查域类中具有该名称的属性(未大写)。如果算法成功，它将使用该属性。如果没有，该算法将驼峰情况部分的源代码从右侧分割为一个头部和一个尾部，并尝试在我们的示例中找到相应的属性AddressZip和Code。如果算法找到一个头的属性，它就会取下尾，然后继续从那里构建树，按照刚才描述的方式将尾分割开来。如果第一个分割不匹配，则算法将分割点向左移动(地址、邮政编码)并继续。

虽然这在大多数情况下都是可行的，但是算法可能会选择错误的属性。假设Person类也有一个addressZip属性。该算法已经在第一轮拆分中匹配，选择了错误的属性，然后失败(因为addressZip类型可能没有code属性)。

#### 分页和排序查询创建

**Using** `Pageable`**,** `Slice`**, and** `Sort` **in query methods**

~~~java
Page<User> findByLastname(String lastname, Pageable pageable);

Slice<User> findByLastname(String lastname, Pageable pageable);

List<User> findByLastname(String lastname, Sort sort);

List<User> findByLastname(String lastname, Pageable pageable);
~~~

第一个方法允许您传递一个org.springframe .data.domain.Pageable实例，以便动态地将分页添加到静态定义的查询中。页面知道可用元素和页面的总数。它通过基础设施触发一个count查询来计算总数量。由于这可能很昂贵(取决于所使用的商店)，所以您可以返回一个切片。一个片只知道下一个片是否可用，这在遍历较大的结果集时可能就足够了

#### **Using Pageable as controller method argument**

~~~java
@Controller
@RequestMapping("/users")
class UserController {

  private final UserRepository repository;

  UserController(UserRepository repository) {
    this.repository = repository;
  }

  @RequestMapping
  String showUsers(Model model, Pageable pageable) {

    model.addAttribute("users", repository.findAll(pageable));
    return "users";
  }
}
~~~

The preceding method signature causes Spring MVC try to derive a `Pageable` instance from the request parameters by using the following default configuration:

| `page` | Page you want to retrieve. 0-indexed and defaults to 0.页数  |
| ------ | ------------------------------------------------------------ |
| `size` | Size of the page you want to retrieve. Defaults to 20.每页大小 |
| `sort` | Properties that should be sorted by in the format `property,property(,ASC|DESC)`. Default sort direction is ascending. Use multiple `sort` parameters if you want to switch directions — for example, `?sort=firstname&sort=lastname,asc`. 排序方式 |

要自定义此行为，请分别注册实现PageableHandlerMethodArgumentResolverCustomizer接口或SortHandlerMethodArgumentResolverCustomizer接口的bean。它的customize()方法被调用，允许您更改设置，如下面的示例所示:



#### 限制结果集记录数

查询方法的结果可以通过使用第一个或第一个关键字来限制，这两个关键字可以互换使用。可以将一个可选的数值追加到top或first，以指定要返回的最大结果大小。如果该数字被省略，则假设结果大小为1。下面的例子展示了如何限制查询大小:

~~~java
User findFirstByOrderByLastnameAsc();

User findTopByOrderByAgeDesc();

Page<User> queryFirst10ByLastname(String lastname, Pageable pageable);

Slice<User> findTop3ByLastname(String lastname, Pageable pageable);

List<User> findFirst10ByLastname(String lastname, Sort sort);

List<User> findTop10ByLastname(String lastname, Pageable pageable);
~~~



### 第三步

Set up Spring to create proxy instances for those interfaces, either with [JavaConfig](https://docs.spring.io/spring-data/jpa/docs/2.2.6.RELEASE/reference/html/#repositories.create-instances.java-config) or with [XML configuration](https://docs.spring.io/spring-data/jpa/docs/2.2.6.RELEASE/reference/html/#repositories.create-instances).

java配置，在springboot中不用配置自动配置

~~~java
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;

@EnableJpaRepositories
class Config { … }
~~~

### 第四步

Inject the repository instance and use it, as shown in the following example:

~~~java
class SomeClient {

  private final PersonRepository repository;

  SomeClient(PersonRepository repository) {
    this.repository = repository;
  }

  void doSomething() {
    List<Person> persons = repository.findByLastname("Matthews");
  }
}
~~~



## 查询查找策略

JPA模块支持将查询手动定义为字符串或从方法名派生查询

虽然从方法名获得查询非常方便，但是可能会遇到这样的情况:方法名解析器不支持希望使用的关键字，或者方法名会变得非常难看。因此，您可以通过命名约定使用JPA命名查询(有关更多信息，请参阅使用JPA命名查询)，或者使用@Query注释您的查询方法(有关详细信息，请参阅使用@Query)。

## 创建查询

示例

~~~java
public interface UserRepository extends Repository<User, Long> {

  List<User> findByEmailAddressAndLastname(String emailAddress, String lastname);
}
~~~

我们从这里使用JPA criteria API创建一个查询，但是，本质上，它转换成以下查询:

select u from User u where u.emailAddress = ?1 and u.lastname = ?2。

Spring Data JPA执行属性检查并遍历嵌套属性，如“属性表达式”中所述。

下表描述了JPA支持的关键字以及包含该关键字的方法:

| Keyword                | Sample                                                       | JPQL snippet                                                 |
| :--------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `And`                  | `findByLastnameAndFirstname`                                 | `… where x.lastname = ?1 and x.firstname = ?2`               |
| `Or`                   | `findByLastnameOrFirstname`                                  | `… where x.lastname = ?1 or x.firstname = ?2`                |
| `Is`, `Equals`         | `findByFirstname`,`findByFirstnameIs`,`findByFirstnameEquals` | `… where x.firstname = ?1`                                   |
| `Between`              | `findByStartDateBetween`                                     | `… where x.startDate between ?1 and ?2`                      |
| `LessThan`             | `findByAgeLessThan`                                          | `… where x.age < ?1`                                         |
| `LessThanEqual`        | `findByAgeLessThanEqual`                                     | `… where x.age <= ?1`                                        |
| `GreaterThan`          | `findByAgeGreaterThan`                                       | `… where x.age > ?1`                                         |
| `GreaterThanEqual`     | `findByAgeGreaterThanEqual`                                  | `… where x.age >= ?1`                                        |
| `After`                | `findByStartDateAfter`                                       | `… where x.startDate > ?1`                                   |
| `Before`               | `findByStartDateBefore`                                      | `… where x.startDate < ?1`                                   |
| `IsNull`, `Null`       | `findByAge(Is)Null`                                          | `… where x.age is null`                                      |
| `IsNotNull`, `NotNull` | `findByAge(Is)NotNull`                                       | `… where x.age not null`                                     |
| `Like`                 | `findByFirstnameLike`                                        | `… where x.firstname like ?1`                                |
| `NotLike`              | `findByFirstnameNotLike`                                     | `… where x.firstname not like ?1`                            |
| `StartingWith`         | `findByFirstnameStartingWith`                                | `… where x.firstname like ?1` (parameter bound with appended `%`) |
| `EndingWith`           | `findByFirstnameEndingWith`                                  | `… where x.firstname like ?1` (parameter bound with prepended `%`) |
| `Containing`           | `findByFirstnameContaining`                                  | `… where x.firstname like ?1` (parameter bound wrapped in `%`) |
| `OrderBy`              | `findByAgeOrderByLastnameDesc`                               | `… where x.age = ?1 order by x.lastname desc`                |
| `Not`                  | `findByLastnameNot`                                          | `… where x.lastname <> ?1`                                   |
| `In`                   | `findByAgeIn(Collection ages)`                               | `… where x.age in ?1`                                        |
| `NotIn`                | `findByAgeNotIn(Collection ages)`                            | `… where x.age not in ?1`                                    |
| `True`                 | `findByActiveTrue()`                                         | `… where x.active = true`                                    |
| `False`                | `findByActiveFalse()`                                        | `… where x.active = false`                                   |
| `IgnoreCase`           | `findByFirstnameIgnoreCase`                                  | `… where UPPER(x.firstame) = UPPER(?1)`                      |

# JpaRepository库

![image-20200423112544997](D:\my\study\TyporaNote\spring相关学习笔记\images\image-20200423112544997.png)

