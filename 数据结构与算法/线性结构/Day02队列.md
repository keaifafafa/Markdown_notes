队列

### 一、应用场景

**银行排队案例**

 ![image-20211229161321456](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211229161331.png)



### 二、队列介绍

- 队列是一个有序列表，可用 **数组** 或者 **链表** 来实现

- 遵循**先入先出**的原则，即：先存入队列的数据，要先取出。后存入的要后取出

- 示意图

   ![image-20211229161516939](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211229161517.png)

### 三、实现思路

> ==数组模拟队列==

- 队列本身是有序列表，若使用数组的结构来存储队列的数据，则队列数组的声明如下图, 其中 maxSize 是该队列的最大容量。

- 因为队列的输出、输入是分别从前后端来处理，因此需要两个变**量** **front**及 **rear**分别记录队列前后端**的下标，front 会随着数据输出而改变，而 rear则是随着数据输入而改变，如图所示:

 ![image-20211229161616956](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211229161617.png)

### 四、代码实现（Java）

> ==数组模拟队列 ArrayQueue.java==

```java
/**
 * 使用数组模拟队列-编写一个ArrayQueue类
 */
class ArrayQueue {
    /**
     * 表示数组的最大容量
     */
    private int maxSize;
    /**
     * 队列头
     */
    private int front;
    /**
     * 队列尾
     */
    private int rear;
    /**
     * 模拟队列
     */
    private int[] arr;

    /**
     * 创建队列的构造器
     */
    public ArrayQueue(int arrMaxSize) {
        this.maxSize = arrMaxSize;
        arr = new int[maxSize];
        // 指向队列头部，指向队列头的前一个位置
        front = -1;
        // 指向队列尾部，指向队列尾的位置（具体位置，包含队列尾部）
        rear = -1;
    }

    /**
     * 判断队列是否是满的
     */
    public boolean isFull() {
        // 自己写的判断逻辑
        /* if(rear == (maxSize - 1)){
            return true;
        }
        return false;*/
        // 韩老师写的判断逻辑
        return rear == (maxSize - 1);
    }

    /**
     * 判断队列是否为空
     */
    public boolean isEmpty() {
        return front == rear;
    }

    /**
     * 添加数据到队列（入队）
     * 1、先判断队列是否已经满了
     * 2、然后在确定是否进行添加
     */
    public void addQueue(int o) {
        // 先判断是否已经满了
        if (!isFull()) {
            ++rear;
            arr[rear] = o;
            System.out.println("成功加入！");
            return;
        }
        System.out.println("队列已经满，无法添加");
    }

    /**
     * 获取队列数据(出队)
     * 1、先判断队列是否为空
     * 2、然后在确定是否进行出队
     */
    public int getQueue() {
        if (!isEmpty()) {
            // 头部后移
            ++front;
            return arr[front];
        }
        // 抛出异常，不要写 return -1;这种 throw直接就结束了，所以不用再写 return 了
        throw new RuntimeException("队列为空，不能出队！！！");
    }

    /**
     * 展示队列所有数据
     */
    public void showQueue() {
        if (!isEmpty()) {
            for (int i = front + 1; i <= rear; i++){
                System.out.printf("arr[%d] = %d\t",i + 1,arr[i]);
            }
            return;
        }
        System.out.println("队列为空，无数据可展示！！！");
        return;

    }

    /**
     * 展示队头
     */
    public int headQueue(){
        if(!isEmpty()){
            return arr[front + 1];
        }
        throw new RuntimeException("队列为空，无队首元素！！！");
    }

}

```

> ==主方法==

```java
package com.fafa.queue;

import java.util.Scanner;

/**
 * 使用数组模拟实现队列
 *
 * @author Sire
 * @version 1.0
 * @date 2021-12-29 16:17
 */
public class ArrayQueueDemo {

    public static void main(String[] args) {
        // 创建一个队列
        ArrayQueue arrayQueue = new ArrayQueue(3);
        // 用户选择键
        char key = ' ';
        // 循环判断
        boolean loop = true;
        Scanner sc = new Scanner(System.in);
        menu();
        while(loop){
            key = sc.next().charAt(0);

            switch (key){
                    // 入队
                case 'a':
                    System.out.println("请输入队元素");
                    int a = sc.nextInt();
                    arrayQueue.addQueue(a);
                    break;
                    // 出队
                case 'g':
                    try {
                        int g = arrayQueue.getQueue();
                        System.out.println("出队元素为" + g);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                    // 显示全部
                case 's':
                    arrayQueue.showQueue();
                    break;
                    // 显示头部
                case 'h':
                    try {
                        int h = arrayQueue.headQueue();
                        System.out.println("队首元素为：" + h);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                    // 退出程序
                case 'e':
                    sc.close();
                    loop = false;
                    break;
                default:
                    break;
            }
        }
        System.out.println("程序退出");
    }

    public static void menu(){
        System.out.println("a:入队");
        System.out.println("g:出队");
        System.out.println("s:显示全部");
        System.out.println("h:显示队首");
        System.out.println("e:退出程序");
    }

}
```

> ==上述代码存在的问题==

问题就是，数组空间无法实现复用，没有形成一个环状（ 取 模 ），就是已经入队的位置，即使出队后，也无法继续利用其位置添加新的元素了

 ![image-20211229192142199](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211229192144.png)

### 五、代码优化

#### 1、优化思路

对前面的数组模拟队列的优化，充分利用数组. 
 因此将数组看做是一个环形的。(通过取模的方
 式来实现即可)

思路如下:

1. front 变量的含义做一个调整： front 就指向队列的第一个元素, 也就是说 arr[front] 就是队列的第一个元素

front 的初始值 = 0

2. rear 变量的含义做一个调整：rear 指向队列的最后一个元素的后一个位置. 因为希望空出一个空间做为约定.

rear 的初始值 = 0

3. 当队列满时，条件是 ==(rear + 1) % maxSize == front== 【满】

4. 对队列为空的条件， rear == front 空

5. 当我们这样分析， 队列中有效的数据的个数  ==(rear + maxSize - front) % maxSize==      // rear = 1 front = 0 

   其实本质上就是rear - front 的绝对值，加maxSize就是为了避免负数的情况        

6.  将 rear 后移，这里必须要考虑取模（防止数组下标越界）
   ==rear = (rear + 1) % maxSize==;

   front同理；

7.  我们就可以在原来的队列上修改得到，一个环形队列

#### 2、实现代码

> ==CircleArrayQueue.java==

```java
/**
 * 使用数组模拟环形队列-CircleArrayQueue类
 */
class CircleArrayQueue {
    /**
     * 表示数组的最大容量
     */
    private int maxSize;
    /**
     * front 队列的第一个元素
     */
    private int front;
    /**
     * rear 指向队列的最后一个元素的后一个位置. 因为希望空出一个空间做为约定.
     */
    private int rear;
    /**
     * 模拟队列
     */
    private int[] arr;

    /**
     * 创建队列的构造器
     */
    public CircleArrayQueue(int arrMaxSize) {
        this.maxSize = arrMaxSize;
        arr = new int[maxSize];
        // front 队列的第一个元素
        front = 0;
        // rear 指向队列的最后一个元素的后一个位置. 因为希望空出一个空间做为约定.
        rear = 0;
    }

    /**
     * 判断队列是否是满的
     */
    public boolean isFull() {
        return (rear + 1) % maxSize == front;
    }

    /**
     * 判断队列是否为空
     */
    public boolean isEmpty() {
        return front == rear;
    }

    /**
     * 添加数据到队列（入队）
     * 1、先判断队列是否已经满了
     * 2、然后在确定是否进行添加
     */
    public void addQueue(int o) {
        // 先判断是否已经满了
        if (!isFull()) {
            arr[rear] = o;
            // 将 rear 后移，这里必须要考虑取模（防止数组下标越界）
            rear = (rear + 1) % maxSize;
            System.out.println("成功加入！");
            return;
        }
        System.out.println("队列已经满，无法添加");
    }

    /**
     * 获取队列数据(出队)
     * 1、先判断队列是否为空
     * 2、然后在确定是否进行出队
     */
    public int getQueue() {
        if (!isEmpty()) {
            // 这里需要分析出 front 是队列首个元素（并非数组第一个）
            // 1、temp用来存储arr[front] 的值，便于将front进行增加操作
            int temp = arr[front];
            // 2、front也要进行相加和取模操作（环形）
            front = (front + 1) % maxSize;
            // 3、返回 temp 保存的 arr[front] 的值
            return temp;
        }
        // 抛出异常，不要写 return -1;这种 throw直接就结束了，所以不用再写 return 了
        throw new RuntimeException("队列为空，不能出队！！！");
    }

    /**
     * 展示队列所有数据
     */
    public void showQueue() {
        if (!isEmpty()) {
            //思路: 从front开始遍历，遍历多少个元素(也就是有效的元素个数)
            // 其实有效个数就是 rear - front的绝对值，这里加maxSize是为了抵消负数
            /** 自己写的 **/
            /* int n = (rear + maxSize - front) % maxSize;
            int count = 0;
            int i = front;
            while (count < n) {
                System.out.printf("arr[%d] = %d\t", i % maxSize , arr[i % maxSize]);
                i++;
                count++;
            }*/
            /** 韩老师写的 **/
            for (int i = front; i < front + getValidSize(); i++) {
                System.out.printf("arr[%d] = %d\t", i % maxSize, arr[i % maxSize]);
            }
            System.out.println();
            return;
        }
        System.out.println("队列为空，无数据可展示！！！");
        return;

    }

    /**
     * 计算数组的有效个数
     */
    public int getValidSize() {
        // 其实有效个数就是 rear - front的绝对值，这里加maxSize是为了抵消负数
        return (rear + maxSize - front) % maxSize;
    }

    /**
     * 展示队头
     */
    public int headQueue() {
        if (!isEmpty()) {
            return arr[front];
        }
        throw new RuntimeException("队列为空，无队首元素！！！");
    }

}
```

> ==主方法（测试）==

```java
public class CircleArrayQueueDemo {
    public static void main(String[] args) {
        // 测试环形数组
        // 创建一个队列 这里实际可用参数只有 4 个，因为最后一个空间要作为约定
        CircleArrayQueue circleArrayQueue = new CircleArrayQueue(5);
        // 用户选择键
        char key = ' ';
        // 循环判断
        boolean loop = true;
        Scanner sc = new Scanner(System.in);
        menu();
        while (loop) {
            key = sc.next().charAt(0);

            switch (key) {
                    // 入队
                case 'a':
                    System.out.println("请输入队元素");
                    int a = sc.nextInt();
                    circleArrayQueue.addQueue(a);
                    break;
                    // 出队
                case 'g':
                    try {
                        int g = circleArrayQueue.getQueue();
                        System.out.println("出队元素为" + g);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                    // 显示全部
                case 's':
                    circleArrayQueue.showQueue();
                    break;
                    // 显示头部
                case 'h':
                    try {
                        int h = circleArrayQueue.headQueue();
                        System.out.println("队首元素为：" + h);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                    // 退出程序
                case 'e':
                    sc.close();
                    loop = false;
                    break;
                default:
                    break;
            }
        }
        System.out.println("程序退出");
    }

    /**
     * 菜单方法
     */
    public static void menu() {
        System.out.println("a:入队");
        System.out.println("g:出队");
        System.out.println("s:显示全部");
        System.out.println("h:显示队首");
        System.out.println("e:退出程序");
    }
}
```



