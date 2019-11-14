---
layout: post
title:  "Java Core Quiz - Entrance Level 1"
categories: Java Learning
tags:  Java Quiz
excerpt: null
mathjax: true
author: Bo Chen
---

* content
{:toc}

## 手写以下代码，请确保关键知识点正确

1. 一个Employee类，要求有constructor, instance fields and methods

``` java
class Employee{
  // instance fields
  private String name ;
  private double salary;
  private Local Date hireDay;
  // constructor
  public Employee(St ring n , double s, int year , int month , int day){
    name = n;
    salary = s;
    hireDay = Local Date.of (year , month, day) ;
    // a method
  public String getName(){
    return name;
  }
  // more methods
  // ...
}
```

2. 一个静态方法，并且调用它

``` java
class Util{
    public static int getCount(){
        return 100;
    }
}

class Test{
    public static void main(){
      System.out.println(util.getCount());
    }
}
```

3. 假设已有Employee类，创建一个继承Employee类的Manager类，

``` java
class Employee{
    //something here
}

class Manager extends Employee{
    //something here
}
```

4. 强制类型转换，强制将一个Employee对象，转换为Manager对象

``` java
if (employee instanceof Manager){
  Manager boss = (Manager) employee;
}
```

5. 一段try-catch-finally语句

``` java
try{
  System.out.println("hello world");
  } catch (Exception e){
    e.printStackTrace();
  } finally {
    System.out.println("finally");
}

```

6. 一个包含抽象方法的抽象类以及一个继承它的类

``` java
public abstract class AbstractEmployee {
    /**
     * This is for demo the abstract method
     * @return a string
     */
    public abstract String generateName();
}

public class Employee extends AbstractEmployee {
    @Override
    public String generateName() {
        return null;
    }
}

```

7. 一个interface以及一个实现它的类

``` java
public interface EmployeeInterface {
    /**
     * Show interface
     * @return
     */
    String generateName();
}

public class EmployeeImp implements EmployeeInterface {
    @Override
    public String generateName() {
        return null;
    }
}

```

8. 一个lambda来计算两个String的长度差

``` java
String[] players = {"Rafael Nadal", "Novak Djokovic", "Stanislas Wawrinka", "David Ferrer", "Roger Federer", "Andy Murray",
"Tomas Berdych", "Juan Martin Del Potro","Richard Gasquet", "John Isner"};
Arrays.sort(players,(String s1, String s2) -> s1.length() - s2.length() );
Arrays.stream(players).forEach(System.out::println);
```

9. 使用java命令来运行jar文件

`java -jar aaa.jar`

10.使用Hashmap用来保存Employee对象。并且实现1）将Employee和对应员工号（SN）放入map，并且2）使用SN来取得Employee

``` java
Map<String, Employee> employeeMap = new HashMap<String, Employee>(4);
Employee emp = new Employee("my name");
System.out.println(emp);
emp = new Employee("new name");
employeeMap.put("SN1", emp);
System.out.println(employeeMap.get("SN1"));
```

---------------------------------------------
手写是指不依赖IDE，使用纯文本编辑器或者传统纸笔来编写代码片段。不要求代码可以运行，但是关键知识点需要正确
