## 一、什么是顺序存储二叉树

> ==基本说明==

 ![image-20220123211356300](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220123211358.png)



> ==特点==

 ![image-20220123211433258](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220123211433.png)



> 其实说白了就是把数组里的数据以二叉树的形式遍历出来（前序、中序、后序）

## 二、代码实现顺序存储二叉树

> ==要求==

 ![image-20220123211741256](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220123211741.png)

> ==代码实现==

```java
package com.fafa.tree;

/**
 * 顺序存储二叉树(数组转成二叉树)
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-23 20:37
 */
public class ArrBinaryTreeDemo {

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        ArrBinaryTree arrBinaryTree = new ArrBinaryTree(arr);
        // 测试前序遍历
        System.out.println("前序遍历结果：");
        arrBinaryTree.preOrder();
        // 测试中序遍历
        System.out.println("中序遍历结果：");
        arrBinaryTree.infixOrder();
        // 测试后序遍历
        System.out.println("后序遍历结果：");
        arrBinaryTree.postOrder();
    }

}

/**
 * 顺序存储二叉树
 */
class ArrBinaryTree{
    /**
     * 待遍历数组
     */
    int[] arr;

    public ArrBinaryTree(int[] arr) {
        this.arr = arr;
    }

    /**
     * 前序遍历重载方法
     */
    public void preOrder(){
        if (arr != null && arr.length != 0){
            preOrder(0);
        }else{
            System.out.println("数组不存在或者为空，无法遍历！");
        }
    }

    /**
     * 前序遍历
     * 实现思路：
     * 1、第N个元素的左子节点为 （2 * n + 1）
     * 2、第N个元素的右子节点为 （2 * n + 2）
     * 3、第N个元素的父节点为    (n - 1) / 2
     * @param index
     */
    public void preOrder(int index){
        System.out.println(arr[index]);
        // 向左递归遍历(必须要保证下标不越界得情况下)
        if ((index * 2 + 1) < arr.length){
            preOrder(2 * index + 1);
        }
        if ((index * 2 + 2) < arr.length){
            preOrder(2 * index + 2);
        }
    }

    /**
     * 中序遍历重载方法
     */
    public void infixOrder(){
        if (arr != null && arr.length != 0){
            infixOrder(0);
        }else{
            System.out.println("数组不存在或者为空，无法遍历！");
        }
    }

    /**
     * 中序遍历
     * 实现思路：
     * 1、先左子树
     * 2、在父节点
     * 3、最后是右子树
     * @param index
     */
    public void infixOrder(int index){
        // 向左递归遍历(必须要保证下标不越界得情况下)
        if ((index * 2 + 1) < arr.length){
            infixOrder(2 * index + 1);
        }
        System.out.println(arr[index]);
        if ((index * 2 + 2) < arr.length){
            infixOrder(2 * index + 2);
        }
    }

    /**
     * 后序遍历重载方法
     */
    public void postOrder(){
        if (arr != null && arr.length != 0){
            postOrder(0);
        }else{
            System.out.println("数组不存在或者为空，无法遍历！");
        }
    }

    /**
     * 后序遍历
     * 实现思路：
     * 1、先左子树
     * 2、在右子树
     * 3、最后是父节点
     * @param index
     */
    public void postOrder(int index){
        // 向左递归遍历(必须要保证下标不越界得情况下)
        if ((index * 2 + 1) < arr.length){
            postOrder(2 * index + 1);
        }
        if ((index * 2 + 2) < arr.length){
            postOrder(2 * index + 2);
        }
        System.out.println(arr[index]);
    }
}

```

