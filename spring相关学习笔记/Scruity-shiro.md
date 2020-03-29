# springboot-scruity

## 相关的依赖

```xml
 <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-web</artifactId>
        </dependency>
```

## **需要继承的类**

```java
@EnableWebSecurity//注解用于启动标识 权限类
public class MyScruityConfig extends WebSecurityConfigurerAdapter {
}
```

## 设置权限和首页定制

继承父类的方法

```java
 @Override
    protected void configure(HttpSecurity http) throws Exception {
        //首页所有人你可以进
        // 用于认证权限的设置
        http.authorizeRequests()
                .antMatchers("/").permitAll()
                .antMatchers("/login1").permitAll()
                .antMatchers("/level1/**").hasRole("vip1")
                .antMatchers("/level2/**").hasRole("vip2");

           //没有权限默认会到哪一个页面
        //login页面
        //loginPage自定义登陆页
//        loginProcessingUrl("/login");表单提交到那个httprequest
//        passwordParameter().usernameParameter() 配置login1 页面提交的参数名的匹配固定的账号密码名字 
          http.formLogin().loginPage("/login1").passwordParameter().usernameParameter().loginProcessingUrl("/login");
        //开启注销功能
//        logoutsuccessUrl退出后跳转到那个页面，比如首页
        //开启注销功能，默认是（"/logout"）页面
//      自定义的话使用  logoutsuccessUrl退出后跳转到那个页面，比如首页
        
        http.logout().logoutSuccessUrl("/");
        //记住我功能,自定义前端参数
        http.rememberMe().rememberMeParameter("这个一般是前端自定义的一个按钮名字");
    }
```

## 授予权限

注意版本的差距 ，以及密码的保护需要硬解码

```java
//上面认证，下面授权
    //认证，springboot 2.1.x 可以直接使用
    //密码编码：passwordencoder
    //在springsecurity 5.0+中增加了许多加密方法
    //
    @Override
    //这些数据从数据库中加载
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                .withUser("shilin").password(new BCryptPasswordEncoder().encode("123456")).roles("vip1")
                .and().withUser("zhenglin").password(new BCryptPasswordEncoder().encode("123456")).roles("vip1","vip2");
    }
```



# shiro



