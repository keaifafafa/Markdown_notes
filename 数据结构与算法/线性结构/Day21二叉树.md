## 一、为什么要使用树这种数据结构

1)数组存储方式的分析

 优点：通过下标方式访问元素，速度快。**对于有序数组**，还可使用二分查找提高检索速度。

 缺点：如果要检索具体某个值，或者插入值(按一定顺序)**会整体移动**，效率较低 [示意图]

2)链式存储方式的分析

 优点：在一定程度上对数组存储方式有优化(比如：插入一个数值节点，只需要将插入节点，链接到链表中即可， 删除效率也很好)。

 缺点：在进行检索时，效率仍然较低，比如(检索某个值，需要从头节点开始遍历) 【示意图】

3)**树**存储方式的分析

 能提高数据**存储，读取**的效率, 比如利用 **二叉排序树**(Binary Sort Tree)，既可以保证数据的检索速度，同时也可以保证数据的插入，删除，修改的速度。

【示意图,后面详讲】

 案例: [7, 3, 10, 1, 5, 9, 12]

## 二、什么是二叉树

> ==二叉树示意图==

 ![image-20220122232012082](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122232020.png)

> ==概念==

 ![image-20220122232110347](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122232110.png)

 ![image-20220122232432418](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122232432.png)

## 三、二叉树前中后序遍历

> ==遍历说明==

 ![image-20220122232623897](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122232623.png)

前序遍历: **先输出父节点**，再遍历左子树和右子树

中序遍历: 先遍历左子树，**再输出父节点**，再遍历右子树

后序遍历: 先遍历左子树，再遍历右子树，**最后输出父节点**

**小结**: 看输出父节点的顺序，就确定是前序，中序还是后序

> ==遍历要求==

 ![image-20220122232716077](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122232716.png)

> ==代码实现==

```java
package com.fafa.tree;

/**
 * 二叉树
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-22 16:51
 */
public class BinaryTreeDemo {
    public static void main(String[] args) {
        // 创建节点
        HeroNode root = new HeroNode(1, "宋江");
        HeroNode node2 = new HeroNode(2, "吴用");
        HeroNode node3 = new HeroNode(3, "卢俊义");
        HeroNode node4 = new HeroNode(4, "林冲");
        HeroNode node5 = new HeroNode(5, "吴胜");
        // 先手动生成二叉树（后面会用递归来生成，暂时先手动）
        root.setLeft(node2);
        root.setRight(node3);
        node3.setRight(node4);
        node3.setLeft(node5);
        // 创建二叉树
        BinaryTree tree = new BinaryTree(root);
        // 测试前序遍历
        System.out.println("前序遍历");
        tree.preOrder();
        // 测试中序遍历
        System.out.println("中序遍历");
        tree.infixOrder();
        // 测试后序遍历
        System.out.println("后序遍历");
        tree.postOrder();

    }

}

/**
 * 创建二叉树
 */
class BinaryTree {

    HeroNode root = null;

    public BinaryTree(HeroNode root) {
        this.root = root;
    }

    /**
     * 前序遍历
     */
    public void preOrder() {
        if (this.root != null) {
            this.root.preOrder();
        } else {
            System.out.println("这是一颗空树");
        }
    }

    /**
     * 中序遍历
     */
    public void infixOrder() {
        if (this.root != null) {
            this.root.infixOrder();
        } else {
            System.out.println("这是一颗空树");
        }
    }

    /**
     * 后序遍历
     */
    public void postOrder() {
        if (this.root != null) {
            this.root.postOrder();
        } else {
            System.out.println("这是一颗空树");
        }
    }


}

/**
 * 英雄节点
 */
class HeroNode {
    private int id;
    private String name;
    private HeroNode left;
    private HeroNode right;

    /**
     * 构造方法，默认做左右节点为空
     *
     * @param id
     * @param name
     */
    public HeroNode(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public HeroNode getLeft() {
        return left;
    }

    public void setLeft(HeroNode left) {
        this.left = left;
    }

    public HeroNode getRight() {
        return right;
    }

    public void setRight(HeroNode right) {
        this.right = right;
    }

    @Override
    public String toString() {
        return "HeroNode{" +
            "id=" + id +
            ", name='" + name + '\'' +
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
}

```

## 四、二叉树前中后序查找

> ==需求==

 ![image-20220122233549339](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122233549.png)

> ==代码实现==

添加到HeroNode类里

```java
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
```





## 五、二叉树删除节点

> ==要求==

 ![image-20220122233634014](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122233634.png)

> ==代码实现==

在HeroNode类里添加

```java
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
```

在BinaryTree类里添加

```java
/**
     * 删除节点
     * @param no
     */
public void delNode(int no) {
    if (root != null) {
        // 这要判断待删除节点是否为根节点
        if (root.getId() == no) {
            root = null;
        } else {
            root.delNode(no);
        }
    } else {
        System.out.println("空数，无法删除~");
    }
}
```

> ==课后思考==

 ![image-20220122234108368](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220122234108.png)
