## 一、中缀表达式实现计算器

### 1、思路

1. 通过一个index值（索引），来遍历我们的表达式
2. 如果发现是数字，就直接进数栈
3. 如果是运算符，就直接进符号栈
4. 如果当前符号栈为空，则直接入栈
5. 如果符号栈里有操作符，需要进行判断，如果栈内操作符优先级**大于或者等于**当前操作符， 则pop出符号栈有一个元素，同时pop出数字栈内两个元素，三个元素进行运算，结果返回数字栈，**当前操作符**入字符栈，**反之**，当前操作符则直接进入符号栈
6. 表达式扫描完毕（index >= expression.length()），就按照顺序从数栈和符号栈中pop出相应的数和符号，并运算
7. 最后数栈内只有一个数的时候，则为结果。

**验证：** 3+2*6-2 = 13

### 2、图示

 ![image-20220106150547047](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220106150554.png)

### 3、代码实现

```java
package com.fafa.stack;

/**
 * 基于栈实现的计算器
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-05 18:14
 */
public class Calculator {
    public static void main(String[] args) {
        // 根据刚才的思路，完成表达式的运算
        String expression = "1000+2*6-205+8/4";
        // 创建两个栈，一个数字栈，一个符号栈
        ArrayStack2 numStack = new ArrayStack2(5);
        ArrayStack2 oprStack = new ArrayStack2(5);
        // 循环遍历的下标索引
        int index = 0;
        int nums1 = 0;
        int nums2 = 0;
        // 用于多位数拼接
        String keepNums = "";
        // 第一遍先把高优先级的运算完
        while (true) {
            // 截取字符串
            String s = expression.substring(index, index + 1);
            char ch = ' ';
            // 如果是操作字符（+、-、*、/）
            if (oprStack.isOperate(s.charAt(0))) {
                ch = s.charAt(0);
                // 如果符号栈为空
                if (oprStack.isEmpty()) {
                    oprStack.push(ch);
                }
                // 如果ch 大于等于 栈内运算符的优先级
                else if (oprStack.priority(ch) <= oprStack.priority((char) oprStack.peek())) {
                    nums1 = numStack.pop();
                    nums2 = numStack.pop();
                    char pop = (char) oprStack.pop();
                    int res = numStack.calResult(nums1, nums2, pop);
                    // 将结果 入栈（数字栈）
                    numStack.push(res);
                    oprStack.push(ch);
                } else {
                    oprStack.push(ch);
                }
            }
            // 如果是数字,直接进数栈
            else {
                /**
                 * 思路分析
                 * 1、 处理多位数，应观察其后面一位是不是为运算符，如果不是，则需要追加
                 * 2、 如果后面一位是运算符，则直接入栈，入完栈后，记得将keepNums设置为空
                 * 3、 需要特殊考虑下最后一个元素，因为他没有下一个，所以可以直接入栈
                 */
                // 拼接多位数
                keepNums += s;
                // 如果当前为最后一位
                if (index == expression.length() - 1) {
                    // 将字符转成整形（数字）
                    int num = Integer.parseInt(keepNums);
                    numStack.push(num);
                } else {
                    // 往下看一位，看是否为运算符
                    if (oprStack.isOperate(expression.substring(index + 1, index + 2).charAt(0))) {
                        // 将字符转成整形（数字）
                        int num = Integer.parseInt(keepNums);
                        numStack.push(num);
                        // 设为空
                        keepNums = "";
                    }
                }

            }
            // 后移
            index++;
            // 如果下标大于等于表达式的长度，则循环结束
            if (index >= expression.length()) {
                break;
            }

        }
        // 第二遍把剩余数字运算完，并获得结果
        while (true) {
            // 只要符号栈没空，那就可以继续运算
            if (!oprStack.isEmpty()) {
                nums1 = numStack.pop();
                nums2 = numStack.pop();
                char pop = (char) oprStack.pop();
                int res = numStack.calResult(nums1, nums2, pop);
                // 将结果入栈
                numStack.push(res);
            } else {
                break;
            }
        }
        System.out.printf("%s = %d", expression, numStack.peek());
    }
}

/**
 * 数组栈
 */
class ArrayStack2 {
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
    public ArrayStack2(int maxSize) {
        this.maxSize = maxSize;
        stack = new int[this.maxSize];
    }

    /**
     * 获取栈顶元素
     */
    public int peek() {
        return stack[top];
    }

    /**
     * 判断栈满
     *
     * @return
     */
    public boolean isFull() {
        return top == maxSize - 1;
    }

    /**
     * 栈空
     */
    public boolean isEmpty() {
        return top == -1;
    }

    /**
     * 入栈
     */
    public void push(int value) {
        // 判断栈是否已满
        if (isFull()) {
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
    public int pop() {
        // 判断栈是否为空
        if (isEmpty()) {
            throw new RuntimeException("栈空，无法出栈");
        }
        int value = stack[top];
        top--;
        return value;
    }

    /**
     * 遍历数组内元素
     */
    public void getAll() {
        if (isEmpty()) {
            System.out.println("空栈，无数据！");
            return;
        }
        for (int i = top; i >= 0; i--) {
            System.out.print(stack[i] + "\t");
        }
        System.out.println();
    }

    /**
     * 元素优先级判断
     * 使用数字大小作为比较
     */
    public int priority(char operate) {
        if (operate == '*' || operate == '/') {
            return 1;
        } else if (operate == '+' || operate == '-') {
            return 0;
        } else {
            // 目前只考虑 加减乘除
            return -1;
        }
    }

    /**
     * 判断是否为有效操作符
     */
    public boolean isOperate(char opr) {
        // 如果是加减乘除则为true
        if (opr == '*' || opr == '-' || opr == '/' || opr == '+') {
            return true;
        }
        return false;
    }

    /**
     * 计算结果
     *
     * @param num1
     * @param num2
     * @param operate 操作符
     * @return
     */
    public int calResult(int num1, int num2, char operate) {
        int res = 0;
        // 条件判断
        switch (operate) {
            case '*':
                res = num1 * num2;
                break;
            case '+':
                res = num1 + num2;
                break;
            case '/':
                res = num2 / num1;
                break;
            case '-':
                res = num2 - num1;
                break;
        }
        return res;
    }
}


```

## 二、各种表达式简介

### 1、前缀表达式

**前缀表达式的计算机求值**

从右至左扫描表达式，遇到数字时，将数字压入堆栈，遇到运算符时，弹出栈顶的两个数，用运算符对它们做相应的计算（栈顶元素 和 次顶元素），并将结果入栈；重复上述过程直到表达式最左端，最后运算得出的值即为表达式的结果

例如: (3+4)×5-6 对应的前缀表达式就是 **- × + 3 4 5 6 ,** **针对前缀表达式求值步骤如下**:

1)从**右至左扫描**，将6、5、4、3压入堆栈

2)遇到+运算符，因此弹出3和4（3为栈顶元素，4为次顶元素），计算出3+4的值，得7，再将7入栈

3)接下来是×运算符，因此弹出7和5，计算出7×5=35，将35入栈

4)最后是-运算符，计算出35-6的值，即29，由此得出最终结果

### 2、中缀表达式

1)中缀表达式就是**常见的运算表达式**，如(3+4)×5-6

2)中缀表达式的求值是我们人最熟悉的，但是对计算机来说却不好操作(前面我们讲的案例就能看的这个问题)，因此，在计算结果时，往往会将中缀表达式转成其它表达式来操作(一般转成后缀表达式.)

### 3、后缀表达式（逆波兰表达式）

1)后缀表达式又称**逆波兰表达式**,与前缀表达式相似，只是运算符位于操作数之后

2)中举例说明： (3+4)×5-6 对应的后缀表达式就是 **3 4 + 5 × 6 –**

3)**再比如**

 ![image-20220106201918161](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220106201921.png)

**后缀表达式的计算机求值**

**从左至右**扫描表达式，遇到数字时，将数字压入堆栈，遇到运算符时，弹出栈顶的两个数，用运算符对它们做相应的计算（次顶元素 和 栈顶元素），并将结果入栈；重复上述过程直到表达式最右端，最后运算得出的值即为表达式的结果

例如: (3+4)×5-6 对应的后缀表达式就是 **3 4 + 5 × 6 - ,** **针对后缀表达式求值步骤如下**

1)从左至右扫描，将3和4压入堆栈；

2)遇到+运算符，因此弹出4和3（4为栈顶元素，3为次顶元素），计算出3+4的值，得7，再将7入栈；

3)将5入栈；

4)接下来是×运算符，因此弹出5和7，计算出7×5=35，将35入栈；

5)将6入栈；

最后是-运算符，计算出35-6的值，即29，由此得出最终结果

## 三、逆波兰计算器（后缀表达式）

> ==任务要求==

1)**输入一个逆波兰表达式**(后缀表达式)，使用栈(Stack), **计算其结果**

2)**支持小括号和多位数整数，因为这里我们主要讲的是数据结构，因此计算器进行简化，只支持对整数的计算。**

3)**思路分析**

4)**代码完成**

> ==思路分析==

1. 首先认为将计算公式转为 后缀表达式（中间用空格隔开）
2. 然后将表达式分割，并将结果接存到List集合中（便于遍历筛选）。
3. 如果是数字，则进行入栈，如果是操作符，则进行相关的运算，并将结果存入栈。
4. 最后栈顶元素即为 结果。

> ==代码实现==

```java
package com.fafa.stack;

import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

/**
 * 逆波兰计算器（后缀表达式）
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-06 16:03
 */
public class PolandNotation {
    public static void main(String[] args) {
        // 先定义一个逆波兰表达式
        // (3+4)*5-6   => 3 4 + 5 * 6 -
        // (30+4)*5-6   => 3 4 + 5 * 6 -
        // 4 * 5 - 8 + 60 + 8 / 2   =>  4 5 * 8 - 60 + 8 2 / +
        String suffixExpression = "4 5 * 8 - 60 + 8 2 / +";
        List<String> list = getListString(suffixExpression);
        System.out.println("list = " + list);
        System.out.printf("%s = %d", suffixExpression, calculate(list));
    }

    /**
     * 将表达式分割存入List集合中
     */
    public static List<String> getListString(String suffixExpression) {
        List<String> list = new ArrayList<>();
        String[] s = suffixExpression.split(" ");
        for (String ele : s) {
            list.add(ele);
        }
        return list;
    }

    /**
     * 计算表达式的结果
     */
    public static int calculate(List<String> list) {
        Stack<Integer> stack = new Stack<Integer>();
        int num1 = 0, num2 = 0, res = 0;
        for (String ele : list) {
            // 如果数字，用正则表达式匹配  \d+ 表示是多位整数
            if (ele.matches("\\d+")) {
                stack.push(Integer.parseInt(ele));
            }
            // 如果为操作符
            else {
                num1 = stack.pop();
                num2 = stack.pop();
                res = calResult(num1, num2, ele);
                stack.push(res);
            }
        }
        return res;
    }

    /**
     * 计算结果
     *
     * @param num1
     * @param num2
     * @param operate 操作符
     * @return
     */
    public static int calResult(int num1, int num2, String operate) {
        int res = 0;
        // 条件判断
        switch (operate) {
            case "*":
                res = num1 * num2;
                break;
            case "+":
                res = num1 + num2;
                break;
            case "/":
                res = num2 / num1;
                break;
            case "-":
                res = num2 - num1;
                break;
            default:
                throw new RuntimeException("操作符有误");
        }
        return res;
    }
}
```

## 四、中缀表达式转后缀表达式

### 1、实现思路

 ![image-20220106203251168](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220106203251.png)

1. 初始化两个栈，运算符栈s1和储存中间结果的栈s2;
2. 从左至右扫描中缀表达式；
3. 遇到操作数是，将其压入s2；
4. 遇到运算符时，比较其余s1栈顶运算符的优先级；
   1. 如果s1为空，或者栈顶运算符为左括号“（ ”，则直接将此运算符入栈；
   2. 否则，若优先级比栈顶运算符的高，也将运算符压入s1；
   3. 否则，将s1栈顶的运算符弹出并压入到s2中，再次转到(4.1)与s1中新的栈顶运算符相比较
5. 遇到括号时：
   1. 如果是左括号“(”，则直接压入s1；
   2. 如果是右括号“)”，则依次弹出s1栈顶的运算符，并压入s2，直到遇到左括号为止，此时将这一对括号丢弃
6. 重复步骤2至5，直到表达式的最右边
7. 将s1中剩余的运算符依次弹出并压入s2
8. 依次弹出s2中的元素并输出，**结果的逆序即为中缀表达式对应的后缀表达式**

### 2、代码实现

```java
package com.fafa.stack;

import javax.naming.InsufficientResourcesException;
import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

/**
 * 中缀表达式转后缀表达式
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-06 16:03
 */
public class PolandNotation2 {
    public static void main(String[] args) {
        /**
         * 思路：
         * 1、将中缀表达式转成对应的list  即 1+((2+3)*4)-5   =>   [1,+,(,(,2,+,3,),*,4,-,5]
         * 2、将的得到的中缀表达式list 转为 后缀表达式  即 [1,+,(,(,2,+,3,),*,4,-,5]  => 1 2 3 + 4 * + 5 -
         */
        String expression = "1+((2+3)*4)-5";
        // 将中缀表达式格式化
        List<String> stringList = toInfixExpression(expression);
        System.out.println(stringList);
        // 中缀转后缀
        List<String> parseSuffixExpressionList = parseSuffixExpressionList(stringList);
        System.out.println("后缀表达式 = " + parseSuffixExpressionList);
        // 计算结果
        int res = calculate(parseSuffixExpressionList);
        System.out.printf("%s = %d",parseSuffixExpressionList,res);

    }


    /**
     * 将表达式分割存入List集合中
     */
    public static List<String> getListString(String suffixExpression) {
        List<String> list = new ArrayList<>();
        String[] s = suffixExpression.split(" ");
        for (String ele : s) {
            list.add(ele);
        }
        return list;
    }

    /**
     * 计算表达式的结果
     */
    public static int calculate(List<String> list) {
        Stack<Integer> stack = new Stack<Integer>();
        int num1 = 0, num2 = 0, res = 0;
        for (String ele : list) {
            // 如果数字，用正则表达式匹配  \d+ 表示是多位整数
            if (ele.matches("\\d+")) {
                stack.push(Integer.parseInt(ele));
            }
            // 如果为操作符
            else {
                num1 = stack.pop();
                num2 = stack.pop();
                res = calResult(num1, num2, ele);
                stack.push(res);
            }
        }
        return res;
    }

    /**
     * 计算结果
     *
     * @param num1
     * @param num2
     * @param operate 操作符
     * @return
     */
    public static int calResult(int num1, int num2, String operate) {
        int res = 0;
        // 条件判断
        switch (operate) {
            case "*":
                res = num1 * num2;
                break;
            case "+":
                res = num1 + num2;
                break;
            case "/":
                res = num2 / num1;
                break;
            case "-":
                res = num2 - num1;
                break;
            default:
                throw new RuntimeException("操作符有误");
        }
        return res;
    }

    /**
     * 判断是不是操作符
     */
    public static boolean isNum(String s) {
        // 数字的ASCII码区间为：[48,57]
        if (s.charAt(0) >= 48 && s.charAt(0) <= 57) {
            return true;
        }
        return false;
    }

    /**
     * 将中缀表达式转成对应的list
     * 例如：  1+((2+3)*4)-5   =>   [1,+,(,(,2,+,3,),*,4,-,5]
     */
    public static List<String> toInfixExpression(String expression) {
        List<String> list = new ArrayList<String>();
        // 用于多位数拼接
        String keepNums = "";
        for (int i = 0; i < expression.length(); i++) {
            String s = expression.substring(i, i + 1);
            // 如果是运算符
            if (!isNum(s)) {
                list.add(s);
            }
            // 如果是数字
            else {
                keepNums += s;
                // 如果是数组最后一位
                if (i == expression.length() - 1) {
                    list.add(keepNums);
                } else {
                    // 看下一位是否为运算符
                    if (!isNum(expression.substring(i + 1, i + 2))) {
                        list.add(keepNums);
                        // 置为0
                        keepNums = "";
                    }
                }
            }
        }
        return list;
    }

    /**
     * 中缀转后缀
     *
     * @return
     */
    public static List<String> parseSuffixExpressionList(List<String> infixExpression) {
        // 定义两个栈 (一般书上是这样的，但是一个栈加一个集合更为方便高效)
        // s1：符号栈
        Stack<String> s1 = new Stack<>();
        // s2：存储中间结果的集合（为什么不用栈呢，因为s2没有pop操作，而且接下来还需要逆序打印，所以用集合更合适）
        List<String> s2 = new ArrayList<String>();
        // 从左到右扫描表达式
        for (int i = 0; i < infixExpression.size(); i++) {
            String cur = infixExpression.get(i);
            // 如果是数字直接进入s2
            if (isNum(cur)) {
                s2.add(cur);
            }
            // 如果遇到左括号
            else if (cur.equals("(")){
                s1.push(cur);
            }
            // 如果遇到有括号
            else if (cur.equals(")")){
                // 依次弹出s1的运算符，并加入到s2
                while (!s1.peek().equals("(")){
                    String pop = s1.pop();
                    s2.add(pop);
                }
                // 将左括号弹出
                s1.pop();
            }
            // 遇到运算符
            else {
                // 将s1栈顶的运算符弹出并加入到s2中，再次转到(4.1)与s1中新的栈顶运算符相比较
                while (s1.size() != 0 && Operation.priority(s1.peek().charAt(0)) >= Operation.priority(cur.charAt(0))){
                    String temp = s1.pop();
                    s2.add(temp);
                }
                // 将cur压入s1
                s1.push(cur);
            }
        }
        // 将s1剩余元素加入s2
        while (s1.size() != 0){
            s2.add(s1.pop());
        }
        return s2;
    }
}

/**
 * 操作符
 */
class Operation {
    /**
     * 加
     */
    private static int ADD = 1;
    /**
     * 减
     */
    private static int SUB = 1;
    /**
     * 乘
     */
    private static int MUL = 2;
    /**
     * 除
     */
    private static int DIV = 2;

    /**
     * 可以返回运算符的优先级
     * @param ch
     * @return
     */
    public static int priority(char ch) {
        int rank = 0;
        switch (ch) {
            case '+':
                rank =  ADD;
                break;
            case '-':
                rank =  SUB;
                break;
            case '*':
                rank =  MUL;
                break;
            case '/':
                rank =  DIV;
                break;
            default:
                break;
        }
        return rank;
    }
}

```

