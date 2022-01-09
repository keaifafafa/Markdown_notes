## 单链表

### 一、链表介绍

链表是有序的列表，但是它在内存中是存储如下

 ![image-20211230190347193](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230190407.png)

小结:

1)链表是以节点的方式来存储,是链式存储

2)每个节点包含 data 域， next 域：指向下一个节点.

3)如图：发现链表的**各个节点不一定是连续存储**.

4)链表分带头节点的链表和没有头节点的链表，根据实际的需求来确定

### 二、单链表

#### 2.1、单链表介绍

单链表(带头结点) **逻辑结构**示意图如下

 ![image-20211230190525691](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230190525.png)

#### 2.2、单链表的应用实例

使用带head头的**单向链表**实现 –水浒英雄排行榜管理

1)完成对英雄人物的**增删改查**操作， 注: **删除和修改,查找
		** **可以考虑学员独立完成，也可带学员完成**

2)第一种方法在添加英雄时，直接添加到链表的尾部

3)**第二种方式在添加英雄时**，根据排名将英雄插入到指定位置
		(如果有这个排名，则添加失败，并给出提示)

 ![image-20211230190736889](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230190736.png)

#### 2.3、添加节点代码实现

 ![image-20211230222102586](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230222109.png)

> ==未优化版本（即第一种添加方式)==

```java
package com.fafa.linkedlist;

/**
 * 单链表
 * @author Sire
 * @version 1.0
 * @date 2021-12-30 14:55
 */
public class SingleLinkedListDemo {

    public static void main(String[] args) {
        HeroNode node1 = new HeroNode(1, "李逵", "黑旋风");
        HeroNode node2 = new HeroNode(2, "宋江", "及时雨");
        HeroNode node3 = new HeroNode(3, "吴用", "智多星");
        HeroNode node4 = new HeroNode(4, "林冲", "豹子头");
        // 初始化链表
        SingleLinkedList linkedList = new SingleLinkedList();
        // 添加英雄
        linkedList.addLink(node1);
        linkedList.addLink(node4);
        linkedList.addLink(node3);
        linkedList.addLink(node2);
        // 遍历
        linkedList.findAllLink();
    }
}

/**
 * 创建链表
 */
class SingleLinkedList{

    private HeroNode head = null;

    public SingleLinkedList() {

        // 头结点
        head = new HeroNode(0,"","");
    }

    /**
     *  插入元素
     */
    public void addLink(HeroNode heroNode){
        // 临时变量，用来寻找尾节点
        HeroNode temp = head;
        while(true){
            // 如果当前为尾结点
            if (temp.next == null){
                heroNode.next = null;
                temp.next = heroNode;
                break;
            }else {
                // 后移搜索
                temp = temp.next;
            }
        }
    }

    /**
     * 遍历全部元素
     */
    public void findAllLink(){
        HeroNode temp = head.next;
        int i = 1;
        if (isEmpty()){
            System.out.println("当前链表为空，无数据可以打印！");
            return;
        }
        while(temp != null){
            System.out.println("第"+ i +"个英雄信息如下:" + temp.toString());
            // 后移
            temp = temp.next;
            i++;
        }
    }

    /**
     * 判断链表是否为空
     */
    public boolean isEmpty(){
        return head.next == null;
    }

}

/**
 * 定义HeroNode，每一个 HeroNode 对象就是一个节点
 */
class HeroNode{
    /**
     * 编号
     */
    public int no;
    /**
     * 英雄名字
     */
    public String name;
    /**
     * 英雄昵称
     */
    public String nickname;
    /**
     * 指针域，指向下一个节点
     */
    public HeroNode next;

    /**
     * 构造器
     * @param no
     * @param name
     * @param nickname
     */
    public HeroNode(int no, String name, String nickname) {
        this.no = no;
        this.name = name;
        this.nickname = nickname;

    }

    public HeroNode() {

    }

    @Override
    public String toString() {
        return "HeroNode{" +
            "no=" + no +
            ", name='" + name + '\'' +
            ", nickname='" + nickname + '\'' +
            '}';
    }
}


```

 ![image-20211230191404889](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230191405.png)

#### 2.4、添加节点代码优化

 ![image-20211230222042782](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230222042.png)

> ==优化后的方法==

可以直接在内存中就将数据排好，大大提升效率

```java
/**
     * 优化后的添加方法
     */
public void addByOrder(HeroNode heroNode) {
    // 因为头结点不能动，所以需要辅助变量temp来找到添加位置
    // 因为是单链表，所以我们找的 temp 是位于 添加位置的前一个节点，否则添加不了
    HeroNode temp = head;
    // 用于判断是否有重复排名英雄
    boolean flag = false;
    /*优化后的*/
    // 1、要按排名进行添加，不分先来后到
    // 2、排名不得重复
    // 3、while循环里只有查找遍历，并无添加操作
    while (true) {
        // 防止空指针,说明temp已经在链表最后了
        if (temp.next == null) {
            break;
        }
        // 和 当前位置的后一个比大小，如果小于后面的那个英雄的编号，那么就在此处添加即可
        if (temp.next.no > heroNode.no) {
            break;
        } else if (temp.next.no == heroNode.no) {
            // 排名重复
            flag = true;
            break;
        }
        // 指针后移
        temp = temp.next;
    }

    if (flag) {
        System.out.println("排名已经重复，无法再次添加编号：" + heroNode.no);
        return;
    } else {
        // 添加操作
        heroNode.next = temp.next;
        temp.next = heroNode;
        System.out.println("添加成功！");
        return;
    }
}
```

> ==测试代码==

```java
public class SingleLinkedListDemo {

    public static void main(String[] args) {
        HeroNode node1 = new HeroNode(1, "李逵", "黑旋风");
        HeroNode node2 = new HeroNode(2, "宋江", "及时雨");
        HeroNode node3 = new HeroNode(3, "吴用", "智多星");
        HeroNode node4 = new HeroNode(4, "林冲", "豹子头");
        // 初始化链表
        SingleLinkedList linkedList = new SingleLinkedList();
        // 添加英雄
        linkedList.addByOrder(node1);
        linkedList.addByOrder(node4);
        linkedList.addByOrder(node3);
        linkedList.addByOrder(node4);
        linkedList.addByOrder(node2);

        // 遍历
        linkedList.findAllLink();
    }
}
```

> ==效果图==

 ![image-20211230210142356](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230210142.png)

#### 2.5、修改节点代码的实现

```java
/**
     * 修改节点信息
     * 1、编号(no)不能更改
     */
public void updateLink(HeroNode heroNode) {
    if (isEmpty()) {
        System.out.println("链表为空,没有可以更改的元素！");
        return;
    }
    HeroNode temp = head;
    // 作为一个哨兵，判断是否找到要修改的目标
    boolean flag = false;
    while (true) {
        // 到了链表的最后了，也就是都遍历完毕了
        if (temp == null) {
            break;
        }
        if (temp.no == heroNode.no) {
            flag = true;
            break;
        }
        // 后移
        temp = temp.next;
    }

    if (flag) {
        temp.name = heroNode.name;
        temp.nickname = heroNode.nickname;
        return;
    } else {
        System.out.println("不好意思，没有定位到该元素，编号：" + heroNode.no);
        return;
    }
}
```

#### 2.6、删除节点

 ![image-20211230221958246](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211230222000.png)

```java
/**
* 删除节点
*/
public void deleteLink(int no) {
    if (isEmpty()) {
        System.out.println("对不起，链表为空，无可删除对象！！！");
        return;
    }
    HeroNode temp = head;
    // 保留 temp 的值
    HeroNode front = temp;
    // 是否找到带删除节点的前一个节点
    boolean flag = false;
    while (true) {
        // 已经到链表的最后
        if (temp == null) {
            break;
        }
        if (temp.no == no) {
            flag = true;
            break;
        }
        front = temp;
        temp = temp.next;
    }

    if (flag) {
        front.next = temp.next;
        System.out.println("删除成功，编号：" + temp.no);
        return;
    } else {
        System.out.println("不好意思，没有找到编号：" + no + "的节点");
    }
}
```

