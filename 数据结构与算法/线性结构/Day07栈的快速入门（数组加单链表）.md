##  一、栈的简介

![image-20220105172357671](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220105172400.png)

1、栈的英文为(stack)

2、栈是一个**先入后出**(FILO-First In Last Out)的有序列表。

3、栈(stack)是限制线性表中元素的插入和删除**只能在线性表的同一端**进行的一种特殊线性表。允许插入和删除的一端，为变化的一端，称为**栈顶**(Top)，另一端为固定的一端，称为**栈底**(Bottom)。

4、根据栈的定义可知，最先放入栈中元素在栈底，最后放入的元素在栈顶，而删除元素刚好相反，最后放入的元素最先删除，最先放入的元素最后删除

5、出栈(pop)和入栈(push)的概念(如图所示)

 ![image-20220105172537102](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220105172537.png)

> ==栈的应用简介==

1)子程序的调用：在跳往子程序前，会先将下个指令的地址存到堆栈中，直到子程序执行完后再将地址取出，以回到原来的程序中。  

2)处理递归调用：和子程序的调用类似，只是除了储存下一个指令的地址外，也将参数、区域变量等数据存入堆栈中。

3)表达式的转换[中缀表达式转后缀表达式]与求值(实际解决)。

4)二叉树的遍历。

5)图形的深度优先(depth一first)搜索法。

## 二、栈的快速入门

### 1、数组模拟栈

1)用**数组模拟栈**的使用，由于栈是一种有序列表，
		 当然可以使用数组的结构来储存栈的数据内容，
 		下面我们就用数组模拟栈的**出栈**，**入栈**等操作。

 2)实现思路分析,并画出示意图![image-20220105172708905](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220105172708.png)

> ==代码实现==

```java
package com.fafa.stack;

import java.util.Scanner;

/**
 * 数组模拟栈
 * @author Sire
 * @version 1.0
 * @date 2022-01-05 15:49
 */
public class ArrayStackDemo {
    public static void main(String[] args) {
        ArrayStack arrayStack = new ArrayStack(5);
        // 是否一直循环
        boolean loop = true;
        // 用户交互键
        String key = "";
        Scanner sc = new Scanner(System.in);
        while(loop){
            menu();
            key = sc.next();
            switch (key){
                case "show":
                    arrayStack.getAll();
                    break;
                case "push":
                    System.out.println("请输入需要入栈的数据：");
                    int value = sc.nextInt();
                    arrayStack.push(value);
                    break;
                case "pop":
                    arrayStack.pop();
                    break;
                case "exit":
                    loop = false;
                    System.out.println("程序成功退出！");
                    break;
                default:
                    break;
            }
        }
    }
    /**
     * 菜单
     */
    public static void menu(){
        System.out.println("show：显示数据");
        System.out.println("push：数据入栈");
        System.out.println("pop：数据出栈");
        System.out.println("exit：退出程序");
        System.out.println("请输入您的选择：");
    }
}

/**
 * 数组栈
 */
class ArrayStack{
    /**
     * 栈的最大容量
     */
    private int maxSize;
    /**
     * 数组
     */
    private int[] stack;
    /**
     * 栈顶,初始化为-1，表示栈为空
     */
    private int top = -1;

    /**
     * 初始化
     */
    public ArrayStack(int maxSize) {
        this.maxSize = maxSize;
        stack = new int[this.maxSize];
    }

    /**
     * 判断栈满
     * @return
     */
    public boolean isFull(){
        return top == maxSize - 1;
    }
    /**
     * 栈空
     */
    public boolean isEmpty(){
        return top == -1;
    }
    /**
     * 入栈
     */
    public void push(int value){
        // 判断栈是否已满
        if (isFull()){
            System.out.println("栈满，无法入栈");
            return;
        }
        top++;
        // 添加到数组
        stack[top] = value;
        System.out.println(value + "成功入栈");
    }
    /**
     * 出栈
     */
    public void pop(){
        // 判断栈是否为空
        if (isEmpty()){
            System.out.println("栈空，无法出栈");
            return;
        }
        System.out.println(stack[top] + "成功出栈");
        top--;
    }
    /**
     * 遍历数组内元素
     */
    public void getAll(){
        if (isEmpty()){
            System.out.println("空栈，无数据！");
            return;
        }
        for (int i = top; i >= 0; i--) {
            System.out.print(stack[i] + "\t");
        }
        System.out.println();
    }
}
```

### 2、单链表模拟栈

> ==思路==

**可以参考链表反转的思路**

​	1、使用头插法，进行入栈操作

​	2、出栈，就是把头结点后面的一个元素移除即可

> ==代码实现==

```java
package com.fafa.stack;

import java.util.Scanner;

/**
 * 使用单链表来模拟栈
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-05 16:34
 */
public class SingleLinkedStackDemo {
    public static void main(String[] args) {
        SingleLinkedStack stack = new SingleLinkedStack();
        // 是否一直循环
        boolean loop = true;
        // 用户交互键
        String key = "";
        Scanner sc = new Scanner(System.in);
        while (loop) {
            menu();
            key = sc.next();
            switch (key) {
                case "show":
                    stack.show();
                    break;
                case "push":
                    System.out.println("请输入需要入栈的数据：");
                    int value = sc.nextInt();
                    stack.push(value);
                    break;
                case "pop":
                    try {
                        int pop = stack.pop();
                        System.out.println(pop + "出栈成功");
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                case "exit":
                    loop = false;
                    System.out.println("程序成功退出！");
                    break;
                default:
                    break;
            }
        }
    }

    /**
     * 菜单
     */
    public static void menu() {
        System.out.println("show：显示数据");
        System.out.println("push：数据入栈");
        System.out.println("pop：数据出栈");
        System.out.println("exit：退出程序");
        System.out.println("请输入您的选择：");
    }
}

/**
 * 创建单链表栈
 * 思路：
 * 1、使用头插法，进行入栈操作
 * 2、出栈，就是把头结点后面的一个元素移除即可
 */
class SingleLinkedStack {
    /**
     * 头结点（哑结点）
     */
    private LinkStack head = new LinkStack(0);

    /**
     * 判断栈是否为空（链式栈不会有满的情况）
     */
    public boolean isEmpty() {
        return head.getNext() == null;
    }

    /**
     * 入栈（链式栈不会有满的情况）
     * 头插法入栈
     */
    public void push(int value) {
        LinkStack stack = new LinkStack(value);
        // 入栈
        stack.setNext(head.getNext());
        head.setNext(stack);
        System.out.println(value + "成功入栈");
    }

    /**
     * 出栈
     */
    public int pop() {
        // 栈为空
        if (isEmpty()) {
            throw new RuntimeException("栈为空！");
        }
        // 栈不为空
        LinkStack temp = head.getNext();
        int value = temp.getValue();
        // 删除
        head.setNext(temp.getNext());
        return value;
    }

    /**
     * 遍历栈
     */
    public void show() {
        // 栈为空
        if (isEmpty()) {
            System.out.println("栈为空！");
            return;
        }
        // 栈不为空
        LinkStack temp = head.getNext();
        while (temp != null) {
            System.out.print(temp.getValue() + "\t");
            // 后移
            temp = temp.getNext();
        }
        // 换行
        System.out.println();
    }
}

/**
 * 链式栈
 */
class LinkStack {
    private int value;
    private LinkStack next;

    public LinkStack(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }

    public LinkStack getNext() {
        return next;
    }

    public void setNext(LinkStack next) {
        this.next = next;
    }

    @Override
    public String toString() {
        return "LinkStack{" +
            "value=" + value +
            '}';
    }
}

```

