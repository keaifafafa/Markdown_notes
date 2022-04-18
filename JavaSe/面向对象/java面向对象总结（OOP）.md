# java面向对象总结（OOP）

## 1.定义：

面向[对象](https://baike.baidu.com/item/对象)(Object Oriented)是[软件开发方法](https://baike.baidu.com/item/软件开发方法/971447)，一种编程范式。面向对象是一种对现实世界理解和抽象的方法，是计算机编程技术发展到一定阶段后的产物。

面向对象是相对于面向过程来讲的，[面向对象方法](https://baike.baidu.com/item/面向对象方法/216078)，把相关的数据和方法组织为一个整体来看待，从更高的层次来进行系统建模，更贴近事物的自然运行模式。

## 2.三大特性：

- ### 封装（ [encapsulation](http://www.youdao.com/w/encapsulation/#keyfrom=E2Ctranslation)  ）：

  1. 该露的露，该藏的藏（**高内聚，低耦合**）
  2. 隐藏 ***<u>对象</u>***  的属性和实现细节，仅对外提供公共访问方式，将变化 **隔离**，便于使用，提高 **复用性** 和 **安全性**。 

- ### 继承（  **[inherit](http://www.youdao.com/w/inherit/#keyfrom=E2Ctranslation)** ）：

  1.  提高代码复用性；继承是多态的前提。 (**extends , super关键字 , 方法的重写**)
  2. **super注意点：**
     - super 调用父类构造器，**必须**在构造器**第一个**位置 
     - super 必须只能出现在 **子类** 的 **方法** 或者 **构造方法** 里
     - super 与 this 不能同时调用**构造方法**
  3. **super 与 this 的区别：**
     - this 本身调用者的对象  super 代表父类对象的应用
     - this 没有继承也可以用  super 只能在继承条件下使用
     - 构造方法： this 表示本类的构造器  super 表示的是父类的构造器
  4. **方法的重写（ override ）：**
     - 非（静态方法或者有final,private修饰的方法 ） 可以重写
     - 需要有继承关系，子类重写父类方法
     - 参数列表必须相同

- ### 多态（ [polymorphism](http://www.youdao.com/w/polymorphism/#keyfrom=E2Ctranslation) ）：

  1.  即同一方法可以根据发送对象的不同而采取多种不同的行为方式。父类或接口定义的引用变量可以指向子类或具体实现类的实例对象。提高了程序的拓展性。

  2.  注意点：

     - 多态是方法的多态，属性没有

     - 父类与子类有联系  ，类型转换异常 Class Cast Exception！

     - 存在关系：继承关系方法需要重写，父类引用指向子类

       ``` java
       father f1 = new son();
       ```

       

  

## 3.五大基本原则：

**1、单一职责原则SRP(Single Responsibility Principle)**
​	 类的功能要单一，不能包罗万象，跟杂货铺似的。
​	 **2、开放封闭原则OCP(Open－Close Principle)**
​	 一个模块对于拓展是开放的，对于修改是封闭的，想要增加功能热烈欢迎，想要修改，哼，一万个不乐意。
​	 **3、里式替换原则LSP(the Liskov Substitution Principle LSP)**
 	子类可以替换父类出现在父类能够出现的任何地方。比如你能代表你爸去你姥姥家干活。哈哈~~
​	 **4、依赖倒置原则DIP(the Dependency Inversion Principle DIP)**
​	 高层次的模块不应该依赖于低层次的模块，他们都应该依赖于抽象。抽象不应该依赖于具体实现，具体实现应	该依赖于抽象。就是你出国要说你是中国人，而不能说你是哪个村子的。比如说中国人是抽象的，下面有具体	的xx省，xx市，xx县。你要依赖的是抽象的中国人，而不是你是xx村的。
​	 **5、接口分离原则ISP(the Interface Segregation Principle ISP)**
 	设计时采用多个与特定客户类有关的接口比采用一个通用的接口要好。就比如一个手机拥有打电话，看视频，	玩游戏等功能，把这几个功能拆分成不同的接口，比在一个接口里要好的多。

##  4.接口和抽象类

### 1.抽象类(abstract)

- 就是约束，有人会帮我们去实现
- 抽象类的所有抽象方法只能由子类去实现
- 不能new，只能子类去实现
- 抽象类里可以写普通方法，抽象方法必须在抽象类中

###  2.接口(interface)

- 只有规范，自己无法写任何普通方法 
- 可以多继承
- 实现了接口的类 ，需要重写接口里的方法

