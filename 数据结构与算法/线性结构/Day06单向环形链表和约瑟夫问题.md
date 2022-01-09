## 一、单向环形链表

### 1、单向环形链表的应用场景

 ![image-20220104181727639](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220104181729.png)

**Josephu**(约瑟夫、约瑟夫环)**问题**

Josephu 问题为：设编号为1，2，… n的n个人围坐一圈，约定编号为k（1<=k<=n）的人从1开始报数，数到m 的那个人出列，它的下一位又从1开始报数，数到m的那个人又出列，依次类推，直到所有人出列为止，由此产生一个出队编号的序列。

**提示**：用一个不带头结点的循环链表来处理Josephu 问题：先构成一个有n个结点的单循环链表，然后由k结点起从1开始计数，计到m时，对应结点从链表中删除，然后再从被删除结点的下一个结点又从1开始计数，直到最后一个结点从链表中删除算法结束。

### 2、单向环形链表的示意图

 ![image-20220104181823571](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220104181823.png)

## 二、实现约瑟夫问题

### 1、思路解析

 ![image-20220105145942395](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220105145949.png)

**构建**一个单向的环形链表思路

1. 先创建第一个节点, 让 first 指向该节点，并形成环形

2. 后面当我们每创建一个新的节点，就把该节点，加入到已有的环形链表中即可.

**遍历**环形链表

1. 先让一个辅助指针(变量) cur，指向first节点

2. 然后通过一个while循环遍历 该环形链表即可 cur.next == first 结束

### 2、代码实现

```java
package com.fafa.linkedlist;

/**
 * 约瑟夫问题
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-04 18:26
 */
public class Joseph {
    public static void main(String[] args) {
        CircleSingleLinkedList list = new CircleSingleLinkedList();
        // 添加
        list.addNodeToCircle(5);
        // 遍历
        //list.getAllNode();
        // 测试约瑟夫问题
        list.countBoy(1,2,5);
    }
}

/**
 * 创建单向环形链表
 */
class CircleSingleLinkedList {
    /**
     * 创建头结点
     */
    private Boy first = null;

    /**
     * 初始化
     */
    public CircleSingleLinkedList() {
    }

    /**
     * 将节点添加到环形单向链表中
     *
     * @param nums 需要添加的数量
     */
    public void addNodeToCircle(int nums) {
        // 首先检测数字是否合法
        if (nums < 1) {
            System.out.println("nums应该大于等于1");
            return;
        }
        Boy curBoy = null;
        for (int i = 1; i <= nums; i++) {
            // 创建节点
            Boy boy = new Boy(i);
            // 如果序号是1
            if (i == 1) {
                // 将头结点变成boy，并将boy的next指向first，
                first = boy;
                boy.setNext(first);
                // 便于下一个节点的添加
                curBoy = first;
            } else {
                curBoy.setNext(boy);
                boy.setNext(first);
                // 相当于后移
                curBoy = boy;
            }
        }
    }

    /**
     * 遍历所有节点
     */
    public void getAllNode() {
        // 判断是否为空
        if(first == null){
            System.out.println("链表为空！");
            return;
        }
        // 遍历节点
        Boy temp = first;
        while (true) {
            if (temp.getNext() == first) {
                System.out.println(temp.toString());
                break;
            }
            System.out.println(temp.toString());
            // 后移
            temp = temp.getNext();
        }
    }

    /**
     * 小朋友出圈
     * @param startNo 开始的位置
     * @param countNum 出圈的数字
     * @param nums 小朋友的总数
     */
    public void countBoy(int startNo,int countNum,int nums){
        // 先对传入数字进行校验
        if(startNo < 1 || countNum > nums || nums < 1){
            System.out.println("传入参数不合法！");
            return;
        }
        // 先把 cur 放到first位置
        Boy cur = first;
        Boy helper = first;
        // helper 放到 first的前一个位置
        while(helper.getNext() != first){
            // 后移
            helper = helper.getNext();
        }
        // 将 cur 和 helper 移动到 规定位置（startNo），因为本身就是位置1，所以只需要移动startNo - 1次
        for (int i = 0; i < startNo - 1; i++){
            cur = cur.getNext();
            helper = helper.getNext();
        }
        // 开始让孩子出圈
        while(true){
            // 游戏结束，幸运儿产生（未出圈的孩子）
            if (cur == helper){
                break;
            }
            // 移动countNum - 1次，相当于数数
            for (int i = 0; i < countNum - 1; i++){
                // 后移
                cur = cur.getNext();
                helper = helper.getNext();
            }
            // 出圈
            System.out.printf("第%d号小朋友出圈\n",cur.getNo());
            cur = cur.getNext();
            helper.setNext(cur);
        }
        System.out.printf("幸运儿是第%d号小朋友\n",cur.getNo());
    }
}

/**
 * Boy类
 */
class Boy {
    /**
     * 编号
     */
    private int no;
    /**
     * 指针域
     */
    private Boy next;

    /**
     * 构造方法
     *
     * @param no
     */
    public Boy(int no) {
        this.no = no;
    }

    public int getNo() {
        return no;
    }

    public void setNo(int no) {
        this.no = no;
    }

    public Boy getNext() {
        return next;
    }

    public void setNext(Boy next) {
        this.next = next;
    }

    @Override
    public String toString() {
        return "Boy{" +
            "no=" + no +
            '}';
    }
}

```



