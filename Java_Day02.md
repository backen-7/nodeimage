# Java基础

## 1. 注释、标识符、关键字

1. 注释：提高代码可读性，不会被编译和执行。

   注释分类：

- 单行注释://
- 多行注释:/*..... */
- 文档注释(JavaDoc):/**    */

2. 标识符：由字母和数字，下划线，$组成，且只能由字母,$和下划线开头。严格区分大小写。
3. 关键字：java保留字，常用有50个。

## 2. 数据类型

1. 强类型语言：要求变量的使用要严格符合规定，变量先定义后使用（Java，C，C++）；安全性高但速度慢

2. 弱类型语言：变量的使用可以不符合规定（VB，JavaScript）

3. Java数据类型分为基本类型和引用类型

   基本数据类型： String(字符串)是一个类，不是基本数据类型的关键字

   - 整型：int，byte，short，long；long后要加L，用于区分

   - 浮点型：float，double；float要加F区分，否则默认为double型

   - 字符型：char；由‘ ’引起，只能包含一个字符

   - 布尔类型：boolean；代表是非（仅取值false和true）

   - ![Java数据类型](https://gitee.com/bbh7/node/raw/master/image-20220730171225109.png)

     

4. 什么是字节：

- 位(bit)：是计算机内部数据储存的最小单位，1000 0111八位二进制
- 字节(byte)：是计算机种数据处理的基本单位，习惯上用大写的B表示
- 1个字节表示八位（1B=8bit）。
- 字符：是指计算机中使用的字母、数字、符号、字。

5. 拓展：

- 整数在java里的进制表示：

  二进制：前缀0b

  八进制：无前缀

  十进制：前缀0

  十六进制：前缀0x

- 浮点数：

  ```java
  // float 特点：有限 离散 舍入误差 大约值 接近但不等于
  //最好避免用浮点数进行比较
  //银行业务常用BigDecimal  数学工具类 表示
  //float 失误举例：
          float f=0.1f;//0.1
          double d=0.1;//0.1
          System.out.println(f==d);//false
  
          float f1=234457799f;
          float f2=f1+1;
          System.out.println(f1==f2);//true
  ```



- 字符型：

  ```java
  /*
  字符串拓展
  字符型本质也是整型
  字符编码 Unicode表中（97=a,65=A）,范围：U0000~UFFFF
  转移字符：\
   */
  char c1='a';
  char c2='家';
  System.out.println(c1);
  System.out.println(c2);
  System.out.println((int)c1);//强制类型转换为int型  a=>97
  System.out.println((int)c2);//强制类型转换
  char c3='\u0061';
  System.out.println(c3);//a
  ```

- boolean类型：

  ```java
  /*
  boolean类型
   */
  boolean flag=true;
  if(flag){
      //等价于flag==true;  less is more代码要精简易读
      //空语句,可以用于占位
  }
  ```

## 3. 类型转换

1. 系统自动类型转换：由精度低的转向精度高的（byte,short,char,int,long,float,double）

2. 强制类型转换：由精度高的转向精度低的，用()运算符

3. 运算过程中，不同类型的数据先转化为同一类型再进行运算。

4. 注意：

   - 布尔类型不能进行强制类型转换
   - 不能把对象类型转换为不相干类型
   - 转换时注意溢出问题

5. ```java
   public static void main(String[] args) {
       //JDK7，数字之间可以用_ 分割
       int money=10_0000_0000;
       int years=20;
       int total=money*years;//money和years都是int型,运算结果仍是int型,超出int范围造成溢出
       System.out.println(total);//输出-1474836480
       long total2=money*years;//total2是long类型,由于运算优先级,先做*运算再赋值,所以total2先被赋值再转化为long型
       System.out.println(total2);//输出仍是-1474836480
       long total3=(long)money*years;//先将任意一个变量强制类型转换转化，运算时结果会自动转化为高精度的类型
       System.out.println(total3);//输出20000000000,成功
   }
   ```

## 4.变量

1. 变量即可以改变的量，变量必须先定义后使用。

2. 变量是程序中最基础的储存单位，包括变量类型，变量名和作用域。

3. 注意：变量类型可以是基本类型或引用类型（String）；变量名必须是合法的标识符

4. 变量的作用域：

   - 类变量：用**static**修饰的变量，从属于类。
   - 实例变量：从属于对象，定义位置在类里，方法外。基本类型未初始化默认为0；布尔类型默认为false，其余默认值null。
   - 局部变量：在方法内定义的变量，作用域为定义开始到方法结束

5. ```java
   public class Demo03 {
       static double salary=2500;//类变量
       int age;//实例变量
       String name;//实例变量
       public static void main(String[] args) {
           int i=25;//局部变量，仅在本定义方法内有效
           System.out.println(i);//输出i
           //实例变量的使用,从属于对象
           Demo03 demo03=new Demo03();
           System.out.println(demo03.age);//没有初始化和赋值默认为0（int类型）
           System.out.println(demo03.name);//没有初始化和赋值默认为null（String类型）
           //类变量的使用
           System.out.println(salary);//可以直接使用从属与类
       }
       public void add(){
           //System.out.println(i);报错,超出局部变量i的作用域
       }
   }
   ```

## 5.常量

1. 含义：不能被改变的量，称为常量

2. 由**final**修饰符定义：final修饰符与存储类型名static不分先后顺序

   ```java
   static final double PI=3.14;
   ```

## 6.规范

1. 所有的变量名，方法名，类名要见名知意
2. 类成员变量名：首字母小写和驼峰原则：monthSalary
3. 局部变量：首字母小写和驼峰原则
4. 常量：大写字母和下划线：MAX_VALUE
5. 类名：首字母大写和驼峰原则：Man，GoodMan
6. 方法名：首字母小写和驼峰原则：run()，runRun()

## 7.运算符

1. 算术运算符：+，-，*，/，%，++，--

2. 关系运算符：>，<，>=，<=，==，!=，

3. 逻辑运算符：&&，||，！ （短路性）

4. 位运算符：&，|，^，~，>>，<<，>>>

5. 条件运算符：？：

6. 赋值运算符：=，+=，-=，*=，/=，%=

7. 注意：

   - 不同类型变量进行运算，结果为最高精度类型
   - 关系运算符返回为布尔值（false和true）

8. ```java
   public static void main(String[] args) {
       int a=10;
       byte b=2;
       int c=3;
       double d=5;
       System.out.println(a/c);//输出2，整型除整型结果为整型
       System.out.println((double)a/c);//强制类型转换后再运输输出3.3
       System.out.println(b>a);//关系运算符返回值为boolean类型
       System.out.println(c<=d);//true
   }
   ```

9. ```java
   /*位运算 效率极高！
   A=0011 1100
   B=0000 1101
   ========================
   A&B=0000 1100   两1为1 按位与
   A|B=0011 1101   有1即1 按位或
   A^B=0011 0001   相同为0不同为1  按位异或
   ~B=1111 0010    按位取反
   ========================
   2*8=16  =>2*2*2*2
   <<   左移   代表*2
   >>   右移   代表/2
   0000 0000   0
   0000 0001   1
   0000 0010   2
   0000 0011   3
   0000 0100   4
   0000 1000   8
   0001 0000   16
    */
   System.out.println(2<<3);//输出16,左移三位代表乘,右移代表除
   ```

   10. 字符串连接字符 ：+

       ```java
       //字符串连接符  +
       int num=10;
       int num2=20;
       System.out.println(""+num+num2);//输出1020 ""代表空字符串,""+ 表示结果为String类型
       System.out.println(num+num2+"");//输出30 num+num2运算结果为int型,再加空字符串
       System.out.println("num="+num);//输出num=10 
       ```

## 8.包机制

1. 目的：为了更好的组织类，java提供了包机制，用于区分类名的命名空间（本质为文件夹）
2. 一般将公司域名倒置作为包名
3. 包名.*   表示包下所有的类（*为通配符）

## 9.JavaDoc

1. javadoc命令是用来生成自己的API文档的。

2. 参数信息：在类上加载或在方法上加载

   @author    作者名

   @version    版本号

   @since        使用的jdk版本

   @param     参数名

   @return      返回值情况

   @throws     异常抛出情况

3. 通过命令行 产生JavaDoc文件 ：javadoc -encoding UTF-8 -charset UTF-8 Doc.java *（-encoding UTF-8 -charset UTF-8便于文件规范展示）*

4. 通过IDEA 产生JavaDoc文件 ：Tools->Generate JavaDoc...

   ​                                                   ->Output directory

   ​                                                   ->Other command..:-encoding UTF-8 -charset UTF-8































