## 一、什么是线索化二叉树？

> ==基本介绍==

1)n个结点的二叉链表中含有n+1 【公式 2n-(n-1)=n+1】 个空指针域。利用二叉链表中的空指针域，存放指向**该**[结点](https://baike.baidu.com/item/结点)在**某种遍历次序**下的前驱和后继结点的指

针（这种附加的指针称为"线索"）

2)这种加上了线索的二叉链表称为**线索链表**，相应的二叉树称为**线索二叉树**(Threaded **BinaryTree**)**。根据线索性质的不同，线索二叉树可分为**前序线索

二叉树、中序线索二叉树**和**后序线索二叉树三种

3)一个结点的前一个结点，称为**前驱**结点

4)一个结点的后一个结点，称为**后继**结点

> ==案例==

 ![image-20220124223600488](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220124223610.png)



## 二、代码实现线索二叉树（以中序为例）

### 1、如何创建线索二叉树（中序）

> ==思路==

 ![image-20220124223816970](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220124223817.png)

> ==代码==

```java
/**
     * 创建线索化二叉树（中序）
     * 思路:
     * 1、先处理左子树的前驱（左），在处理后继（右）
     *
     * @param node
     */
public void threadedBinaryTree(HeroNode node) {
    // 递归头（结束标志）
    if (node == null) {
        return;
    }
    // （一）先处理左子树(线索化)
    threadedBinaryTree(node.getLeft());
    // （二）处理当前节点的前驱节点
    // 以节点8为例子， 8 的left节点 = null, 8 的 leftType = 1
    if (node.getLeft() == null) {
        // 让当前指针的左指针指向前驱结点
        node.setLeft(pre);
        // 修改当前节点的左指针的类型，指向前驱结点
        node.setLeftType(1);
    }
    // 处理后继节点，由于二叉树是单向的，所以需要保留前驱节点，让其指向 node（上面的节点）
    // pre != null 的目的是为了保证第一个元素的前驱节点为null 也就是当前的元素 8
    if (pre != null && pre.getRight() == null) {
        pre.setRight(node);
        pre.setRightType(1);
    }
    // 给pre赋值，成为上一个递归（未结束）的前驱节点（下面的）
    pre = node;
    // （三）最后处理右子树（线索化）
    threadedBinaryTree(node.getRight());

}
```

### 2、如何遍历线索二叉树？

> ==思路==

 ![image-20220124224017975](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220124224018.png)

> ==代码实现==

```java
/**
     * 中序遍历线索二叉树（迭代法）
     */
public void infixThreaded() {
    HeroNode node = root;
    // 其实是一条线（链表）
    while (node != null) {
        // 先找寻最头部的元素
        while (node.getLeftType() == 0) {
            node = node.getLeft();
        }
        // leftType == 1
        System.out.println(node);
        // 如果右子树指向的是后继节点，则直接输出即可
        while (node.getRightType() == 1) {
            // 到下一节点（后继），并打印
            node = node.getRight();
            System.out.println(node);
        }
        // 这很重要，会跳到下一个后继节点
        node = node.getRight();
    }
}
```



### 3、完整代码

```java
package com.fafa.tree.threadedbinarytree;

import lombok.Data;

/**
 * 线索化二叉树
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-23 21:34
 */
public class ThreadedBinaryTreeDemo {

    public static void main(String[] args) {
        HeroNode root = new HeroNode(1);
        HeroNode node2 = new HeroNode(3);
        HeroNode node3 = new HeroNode(6);
        HeroNode node4 = new HeroNode(8);
        HeroNode node5 = new HeroNode(10);
        HeroNode node6 = new HeroNode(14);
        // 创建二叉树（手动）
        root.setLeft(node2);
        root.setRight(node3);
        node2.setLeft(node4);
        node2.setRight(node5);
        node3.setLeft(node6);
        // 测试线索二叉树
        ThreadedBinaryTree threadedBinaryTree = new ThreadedBinaryTree(root);
        threadedBinaryTree.threadedBinaryTree(root);
        // 测试节点
        HeroNode test = node5;
        System.out.println("当前节点为：" + test);
        System.out.println("前驱节点为：" + test.getLeft());
        System.out.println("后继节点为：" + test.getRight());
        // 测试遍历中序的线索化二叉树
        threadedBinaryTree.infixThreaded();

    }
}

/**
 * 创建线索化二叉树
 */
class ThreadedBinaryTree {

    HeroNode root = null;

    /**
     * 前驱结点
     */
    HeroNode pre = null;

    public ThreadedBinaryTree(HeroNode root) {
        this.root = root;
    }

    /**
     * 中序遍历线索二叉树（迭代法）
     */
    public void infixThreaded() {
        HeroNode node = root;
        // 其实是一条线（链表）
        while (node != null) {
            // 先找寻最头部的元素
            while (node.getLeftType() == 0) {
                node = node.getLeft();
            }
            // leftType == 1
            System.out.println(node);
            // 如果右子树指向的是后继节点，则直接输出即可
            while (node.getRightType() == 1) {
                // 到下一节点（后继），并打印
                node = node.getRight();
                System.out.println(node);
            }
            // 这很重要，会跳到下一个后继节点
            node = node.getRight();
        }
    }

    /**
     * 创建线索化二叉树（中序）
     * 思路:
     * 1、先处理左子树的前驱（左），在处理后继（右）
     *
     * @param node
     */
    public void threadedBinaryTree(HeroNode node) {
        // 递归头
        if (node == null) {
            return;
        }
        // （一）先处理左子树(线索化)
        threadedBinaryTree(node.getLeft());
        // （二）处理当前节点的前驱节点
        // 以节点8为例子， 8 的left节点 = null, 8 的 leftType = 1
        if (node.getLeft() == null) {
            // 让当前指针的左指针指向前驱结点
            node.setLeft(pre);
            // 修改当前节点的左指针的类型，指向前驱结点
            node.setLeftType(1);
        }
        // 处理后继节点，由于二叉树是单向的，所以需要保留前驱节点，让其指向 node（上面的节点）
        // pre != null 的目的是为了保证第一个元素的前驱节点为null 也就是当前的元素 8
        if (pre != null && pre.getRight() == null) {
            pre.setRight(node);
            pre.setRightType(1);
        }
        // 给pre赋值，成为上一个递归（未结束）的前驱节点（下面的）
        pre = node;
        // （三）最后处理右子树（线索化）
        threadedBinaryTree(node.getRight());

    }

}

/**
 * 英雄节点
 */
@Data
class HeroNode {
    private int id;

    private HeroNode left;
    private HeroNode right;
    /**
     * 说明
     * 1、如果leftType == 0 表示指向的是左子树，如果是 1 表示指向的是前驱节点
     * 2、如果rightType == 0 表示指向的是右子树，如果是 1 表示指向的是后继节点
     */
    private int leftType;
    private int rightType;


    /**
     * 构造方法，默认做左右节点为空
     *
     * @param id
     */
    public HeroNode(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "HeroNode{" +
            "id=" + id +
            ", leftType=" + leftType +
            ", rightType=" + rightType +
            '}';
    }

    /**
     * 前序遍历
     * 思路：
     * 1、再打印父节点
     * 2、然后判断左子树是否为空，不为空的话，递归打印
     * 3、判断右子树是否为空，不为空的话，递归打印
     */
    public void preOrder() {
        // 为什么可以直接打印，不用判断根节点呢，因为传进来的肯定是一个有效的节点，所以不用判断（在上一调用层已经进行判断了）
        System.out.println(this);
        if (this.left != null) {
            this.left.preOrder();
        }
        if (this.right != null) {
            this.right.preOrder();
        }
    }

    /**
     * 中序遍历
     * 思路：
     * 1、先判断左子树是否为空，不为空的话，递归打印
     * 2、再打印父节点
     * 3、判断右子树是否为空，不为空的话，递归打印
     */
    public void infixOrder() {
        if (this.left != null) {
            this.left.infixOrder();
        }
        System.out.println(this);
        if (this.right != null) {
            this.right.infixOrder();
        }
    }

    /**
     * 后序遍历
     * 思路：
     * 1、先判断左子树是否为空，不为空的话，递归打印
     * 2、判断右子树是否为空，不为空的话，递归打印
     * 3、再打印父节点
     */
    public void postOrder() {
        if (this.left != null) {
            this.left.postOrder();
        }
        if (this.right != null) {
            this.right.postOrder();
        }
        System.out.println(this);
    }

    /**
     * 前序遍历查找
     *
     * @param no 编号
     * @return
     */
    public HeroNode preOrderSearch(int no) {
        System.out.println("get into preSearch~");
        // 比较当前节点是不是
        if (this.getId() == no) {
            return this;
        }
        // 结果节点
        HeroNode resNode = null;
        // 比较左子节点
        // 和遍历的思路大同小异
        // 1、判断当前的做自己额点是否为空，如不为空则继续遍历查找（递归）
        // 2、如左子节点找到结果，则直接返回
        if (this.left != null) {
            resNode = this.left.preOrderSearch(no);
        }
        // 如果不为空，说明在左子树找到了
        if (resNode != null) {
            return resNode;
        }
        // 同上，只不过最后直接返回resNode即可，因为无论找到没，都是resNode
        if (this.right != null) {
            resNode = this.right.preOrderSearch(no);
        }
        return resNode;
    }

    /**
     * 中序遍历查找
     *
     * @param no 编号
     * @return
     */
    public HeroNode infixOrderSearch(int no) {
        // 结果节点
        HeroNode resNode = null;
        // 比较左子节点
        // 和遍历的思路大同小异
        // 1、判断当前的做自己额点是否为空，如不为空则继续遍历查找（递归）
        // 2、如左子节点找到结果，则直接返回
        if (this.left != null) {
            resNode = this.left.infixOrderSearch(no);
        }
        // 如果不为空，说明在左子树找到了
        if (resNode != null) {
            return resNode;
        }
        // 要放在比较语句前面，不能单纯的写在最前面（因为统计的是比较次数）
        System.out.println("get into infixSearch~");
        // 比较当前节点是不是
        if (this.getId() == no) {
            return this;
        }
        // 同上，只不过最后直接返回resNode即可，因为无论找到没，都是resNode
        if (this.right != null) {
            resNode = this.right.infixOrderSearch(no);
        }
        return resNode;
    }

    /**
     * 后序遍历查找
     *
     * @param no 编号
     * @return
     */
    public HeroNode postOrderSearch(int no) {

        // 结果节点
        HeroNode resNode = null;
        // 比较左子节点
        // 和遍历的思路大同小异
        // 1、判断当前的做自己额点是否为空，如不为空则继续遍历查找（递归）
        // 2、如左子节点找到结果，则直接返回
        if (this.left != null) {
            resNode = this.left.postOrderSearch(no);
        }
        // 如果不为空，说明在左子树找到了
        if (resNode != null) {
            return resNode;
        }
        // 同上，只不过最后直接返回resNode即可，因为无论找到没，都是resNode
        if (this.right != null) {
            resNode = this.right.postOrderSearch(no);
        }
        if (resNode != null) {
            return resNode;
        }
        // 要放在比较语句前面，不能单纯的写在最前面（因为统计的是比较次数）
        System.out.println("get into postSearch~");
        // 如果左右子树都没找到
        if (this.getId() == no) {
            return this;
        }
        return null;
    }

    /**
     * 递归删除节点
     * 1、如果需要删除的节点是叶子结点的话，就直接删除该节点即可
     * 2、如果删除的节点是非叶子节点，则删除该子树
     */
    public void delNode(int no) {
        //思路
        /*
		 * 	1. 因为我们的二叉树是单向的，所以我们是判断当前结点的子结点是否需要删除结点，而不能去判断当前这个结点是不是需要删除结点.
			2. 如果当前结点的左子结点不为空，并且左子结点 就是要删除结点，就将this.left = null; 并且就返回(结束递归删除)
			3. 如果当前结点的右子结点不为空，并且右子结点 就是要删除结点，就将this.right= null ;并且就返回(结束递归删除)
			4. 如果第2和第3步没有删除结点，那么我们就需要向左子树进行递归删除
			5.  如果第4步也没有删除结点，则应当向右子树进行递归删除.

		 */
        if (this.left != null && this.left.getId() == no) {
            // 置为空
            this.setLeft(null);
            return;
        }
        if (this.right != null && this.right.getId() == no) {
            this.setRight(null);
            return;
        }
        if (this.left != null) {
            this.left.delNode(no);
        }
        if (this.right != null) {
            this.right.delNode(no);
        }
    }

}
```

