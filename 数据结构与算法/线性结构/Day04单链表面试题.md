## 单链表常见面试题（新浪、百度、腾讯）

### 1、求单链表中有效节点的个数(很简单)

> ==实现代码==

```java
/**
     * 常见面试题1：获取单链表的有效元素个数
     * 思路:直接遍历（但是要排除头结点）
     */
public static int getValidNode(HeroNode head){
    int num = 0;
    // 链表为空
    if (head.next == null){
        return num;
    }
    // 排除头结点
    HeroNode temp = head.next;
    while (temp != null){
        // 有效节点数+1
        num++;
        // 后移
        temp = temp.next;
    }
    return num;
}
```

> ==测试代码==

```java
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
    linkedList.addByOrder(node4);
    linkedList.addByOrder(node3);
    linkedList.addByOrder(node3);
    linkedList.addByOrder(node2);
    // 打印
    linkedList.findAllLink();
    // 统计节点有效个数
    System.out.println("有效的英雄节点数为：" + getValidNode(linkedList.getHead()));
}
```

> ==结果==

 ![image-20211231135807628](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211231135815.png)

### 2、查找单链表中的倒数第k个结点 【新浪面试题】

> ==实现代码==

```java
/**
     * 常见面试题2：查找单链表中的 倒数 第k个结点 【新浪面试题】
     * 思路：
     * 1、首先获取有效的节点数，并将 倒数 第几位转换成 正数 第几位
     * 2、利用循环遍历，设置一个哨兵来计数，然后和正数的进行比对，相等即为找到目标！
     */
public static HeroNode findInverseNode(HeroNode head, int n) {
    if (head.next == null) {
        return null;
    }
    // 排除头结点
    HeroNode cur = head.next;
    int validNum = getValidNode(head);
    boolean flag = false;
    // 对于 请求参数的合法性校验
    if (n > validNum || n < 0) {
        return null;
    }
    // 转换成 正数 的
    n = validNum - n;
    // 计数用的哨兵
    int count = 0;
    // 当然这里也可以用for循环
    while (true) {
        if (cur == null) {
            break;
        }
        if (n == count) {
            // 找到目标
            flag = true;
            break;
        }
        count++;
        // 后移
        cur = cur.next;
    }
    if (flag) {
        return cur;
    }
    return null;
}
```

> ==测试代码==

```java
// 查找单链表中的 倒数 第k个结点
int k = 4;
System.out.println("英雄信息为：" + findInverseNode(linkedList.getHead(), k));
```

> ==效果图==

 ![image-20211231160449194](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211231160449.png)

### 3、单链表的反转【腾讯面试题，有点难度】

 ![image-20211231222138790](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211231222139.png)

> ==实现代码==

```java
/**
     * 常见面试题3：单链表的反转【腾讯面试题，有点难度】
     * 思路：
     * 1、首先定义一个新的节点（cur）
     * 2、然后遍历原来的head节点，没遍历一个节点，就将其添加到cur中，只不过要用头插法！！！
     */
public static HeroNode reverseLink(HeroNode head) {
    // 当只有一个节点，或者一个节点都没有时
    if (head.next == null || head.next.next == null) {
        System.out.println("无需反转");
        return head;
    }
    // 遍历正向链表的（原来的链表）
    HeroNode temp = head.next;
    // 存储临时的temp变量（注意事项是地址传递）
    HeroNode copy = null;
    // 存储反向链表的
    HeroNode reverseHead = new HeroNode(0, "", "");
    while (temp != null) {
        // 赋值 （注意这里是地址传递，并非值传递）
        copy = temp;
        // 后移
        temp = temp.next;
        // 头插法
        copy.next = reverseHead.next;
        reverseHead.next = copy;
    }
    return reverseHead;
}

/**
     * 查询全部节点
     * @param head
     */
public static void queryAll(HeroNode head) {
    HeroNode temp = head.next;
    int i = 1;
    if (head.next == null) {
        System.out.println("当前链表为空，无数据可以打印！");
        return;
    }
    while (temp != null) {
        System.out.println("第" + i + "个英雄信息如下:" + temp.toString());
        // 后移
        temp = temp.next;
        i++;
    }
}
```

> ==测试代码==

```java
// 反向链表
System.out.println("反向链表");
HeroNode reverseLink = reverseLink(linkedList.getHead());
queryAll(reverseLink);
```

> ==效果图==

 ![image-20211231173444089](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211231173446.png)

### 4、从尾到头打印单链表 【百度，要求方式1：反向遍历 。 方式2：Stack栈】

方式1：反向遍历：其实就是**反转链表**（就是第三道面试题的方法），不建议使用，因为那样会破坏原有的链表结构！万一后续需要在打印正向链表呢，所以只改变打印顺序即可。

方式2：Stack栈

 ![image-20211231222200865](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211231222200.png)

> ==实现代码==

```java
/**
     * 常见面试题4：从尾到头打印单链表 【百度，要求方式1：反向遍历 。 方式2：Stack栈】
     */
public static Stack<HeroNode> reservePrintLink(HeroNode head) {
    Stack<HeroNode> stack = new Stack<>();
    HeroNode temp = head.next;
    if (head.next == null) {
        System.out.println("当前链表为空，无数据可以打印！");
        return null;
    }
    while (temp != null) {
        // 入栈
        stack.push(temp);
        // 后移
        temp = temp.next;
    }
    return stack;
}

/**
     * 循环遍历Stack
     */
public static void getAllStack(Stack stack){
    while(stack.size() > 0){
        System.out.println(stack.pop() + "出栈");
    }
}
```

> ==测试代码==

```java
// 方向打印链表
System.out.println("测试反向链表打印");
Stack<HeroNode> nodeStack = reservePrintLink(linkedList.getHead());
getAllStack(nodeStack);
```

> ==运行结果==

 ![image-20211231220101192](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20211231220101.png)



