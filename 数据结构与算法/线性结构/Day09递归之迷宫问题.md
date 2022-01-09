## 一、递归（Recursion）

### 1、递归简介

简单的说: 递归就是方法自己调用自己,每次调用时传入不同的变量**.****递归有助于编程者解决复杂的问题**,同时可以让代码变得简洁。

### 2、递归可以解决什么问题

1)各种数学问题如: 8皇后问题 , 汉诺塔, 阶乘问题, 迷宫问题, 球和篮子的问题(google编程大赛)

2)各种算法中也会使用到递归，比如快排，归并排序，二分查找，分治算法等.

3)将用栈解决的问题-->递归代码比较简洁

### 3、递归需要遵守的重要规则

1)执行一个方法时，就创建一个新的受保护的独立空间(栈空间)

2)方法的局部变量是独立的，不会相互影响, 比如n变量

3)如果方法中使用的是引用类型变量(比如数组，对象)，就会共享该引用类型的数据，引用变量在堆里.

4)递归必须向退出递归的条件逼近，否则就是无限递归,出现StackOverflowError，死归了:)

5)当一个方法执行完毕，或者遇到return，就会返回，遵守谁调用，就将结果返回给谁，同时当方法执行完毕或者返回时，该方法也就执行完毕。

> **如果还是很抽象的话，可以自己打断点，debug一遍**

### 4、递归机制图解

> ==案例代码==

```java
public class RecursionTest {
    public static void main(String[] args) {
        test(4);
    }

    /**
     * 测试递归打印数字
     *
     * @param n
     */
    public static void test(int n) {
        if (n > 2) {
            test(n - 1);
        }
        System.out.println("n = " + n);
    }
}
```

> ==图解==

递归调用规则：

1. 当程序执行到一个方法时，就会开辟一个独立的空间(栈)

2. 每个空间的数据(局部变量)，是独立的.

 ![image-20220108204735276](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220108204744.png)

 ![image-20220108204825937](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220108204826.png)

## 二、简单迷宫问题

### 1、问题描述

 ![image-20220108204955053](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220108204955.png)

### 2、代码实现

```java
package com.fafa.recurison;

/**
 * 迷宫问题
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-08 15:13
 */
public class MazeDemo {
    public static void main(String[] args) {
        // 创建二维数组，模拟迷宫
        // 地图
        int[][] map = new int[8][7];
        // 初始化迷宫
        initMap(map);
        // 显示迷宫
        System.out.println("    ====地图界面====");
        showMap(map);
        // 寻路
        findWay(map, 1, 1);
        System.out.println("    ====寻路路线====");
        showMap(map);
    }

    /**
     * 初始化迷宫
     *
     * @param map
     */
    public static void initMap(int[][] map) {
        // 将上下左右最外层置为1（表示墙）
        for (int i = 0; i < map.length; i++) {
            for (int j = 0; j < map[i].length; j++) {
                // 行
                if (i == 0 || i == 7) {
                    map[i][j] = 1;
                }
                // 列
                else if (j == 0 || j == 6) {
                    map[i][j] = 1;
                }
            }
        }
        // 挡板
        map[3][1] = 1;
        map[3][2] = 1;
        // 加上这两行，可以看到回溯效果
        /*map[1][2] = 1;
        map[2][2] = 1;*/
    }

    /**
     * 显示迷宫
     *
     * @param map
     */
    public static void showMap(int[][] map) {
        for (int[] row : map) {
            for (int data : row) {
                System.out.print(data + "\t");
            }
            System.out.println();
        }
    }

    /**
     * 迷宫寻路
     * 说明：
     * 1、map表示地图
     * 2、i，j 表示从那个地方开始出发（默认 1，1）
     * 3、如果小球能到map[6][5]位置，则说明通路找到
     * 4、约定：0表示为未走过，1表示墙，2表示路可以走通，3表示该点已走过但是行不通
     * 5、走迷宫的策略：下->右->上->左，如果该点走不通，再回溯
     * @param map 地图
     * @param i
     * @param j
     * @return 如果找到返回true，否则，返回false
     */
    public static boolean findWay(int[][] map, int i, int j) {
        // 递归头，结束标志,通路已经找到
        if (map[6][5] == 2) {
            return true;
        } else {
            // 如果没走过
            if (map[i][j] == 0) {
                // 假设可以走通
                map[i][j] = 2;
                // 然后依次试探：下->右->上->左
                if (findWay(map, i + 1, j)) {
                    return true;
                } else if (findWay(map, i, j + 1)) {
                    return true;
                } else if (findWay(map, i - 1, j)) {
                    return true;
                } else if (findWay(map, i, j - 1)) {
                    return true;
                } else {
                    // 死路
                    map[i][j] = 3;
                    return false;
                }
            } else {
                // 也就是map[i][j] == 1 || map[i][j] == 2 || map[i][j] == 3
                return false;
            }
        }
    }
}

```

> ==结果图==

可以打断点，用debug查看调用全过程

 ![image-20220108205208077](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220108205208.png)

### 3、最短路径思路

可以不断的改变寻路策略，比如第一次是：上->下->右->左，第二次可以是：右->下->上->左

然后用一个List集合记录每个策略的2的个数，数量最少者即为最短路径！

