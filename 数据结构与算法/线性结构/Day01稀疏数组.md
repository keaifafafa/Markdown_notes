## 稀疏数组

### 写在前面

相关代码工程链接：[==点击这里==](https://github.com/keaifafafa/DataStructures)

### 一、实际需求

 ![image-20211228095508633](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211228095517.png)

### 二、基本介绍

当一个数组中大部分元素为0，或者为同一个值的数组时，可以使用稀疏数组来保存改数组！

稀疏数组的处理方式：

1)记录数组一共有几行几列，有多少个不同的值

2)把具有不同值的元素的行列及值记录在一个小规模的数组中，从而缩小程序的规模

 ![image-20211228205553882](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211228205556.png)

### 三、应用实例

1)使用稀疏数组，来保留类似前面的二维数组(棋盘、地图等等)

2)把稀疏数组存盘，并且可以从新恢复原来的二维数组数

3)整体思路分析

 ![image-20211228205822958](https://gitee.com/lovely-hair/blog-img/raw/master/img/20211228205823.png)

4)代码实现

> ==SparseArry.java==

```java
public class SparseArray {

    public static void main(String[] args) {
        // 实例化工具类对象 减少代码冗余
        MyArrayUtils utils = new MyArrayUtils();
        /** 
		 * 创建一个11*11的二维数组 
		 * 
		 ***/ 
        // 0：表示没有棋子，1：黑子，2：蓝子
        int[][] chessArr1 = new int[11][11];
        chessArr1[1][2] = 1;
        chessArr1[2][3] = 2;
        chessArr1[3][4] = 2;
        chessArr1[5][4] = 1;
        chessArr1[6][4] = 2;
        chessArr1[7][4] = 1;
        // 循环遍历(输出原始的二维数组)
        System.out.println("====原始二维数组====");
        utils.queryAll(chessArr1);
        /** 
		 * 将二维数组 转 稀疏数组的思路 
		 * 
		 ***/ 
        // 1、先遍历二维数组 得到非0数据的个数
        int sum = 0;
        sum = utils.getValueNum(chessArr1);
        System.out.println("sum = " + sum);

        // 2、创建对应的稀疏数组
        int[][] sparseArr = new int[sum + 1][3];
        // 行
        sparseArr[0][0] = 11;
        // 列
        sparseArr[0][1] = 11;
        // 值
        sparseArr[0][2] = sum;
        // 基数所用，针对的是行数
        int count = 1;
        /**
		 * 思路：
		 * 循环遍历  chessArr1 数组，只要不等于0，就将值赋到 稀疏数组中
		 */
        for(int i = 0; i < chessArr1.length; i++){
            for(int j = 0; j < chessArr1[i].length; j++){
                if(chessArr1[i][j] != 0){
                    sparseArr[count][0] = i;
                    sparseArr[count][1] = j;
                    sparseArr[count][2] = chessArr1[i][j];
                    // 进行累加
                    count++;
                }
            }
        }

        System.out.println("====稀疏数组====");
        utils.queryAll(sparseArr);

        /** 
		 * 将稀疏数组还原
		 * 
		 ***/
        // 1、创建一个同等大小的数组
        int [][] transform = new int [sparseArr[0][0]][sparseArr[0][1]];
        // 2、利用 循环 将稀疏数组值，复制到对应的 还原数组中去
        for(int i = 1; i < sparseArr.length; i++){
            transform[sparseArr[i][0]][sparseArr[i][1]] = sparseArr[i][2];
        }

        System.out.println("====还原后的数组====");
        utils.queryAll(transform);

    }
}
```

> ==工具类代码==

```java
public class MyArrayUtils {
    /**
	 * 循环遍历
	 */
    public void queryAll(int[][] arr) {
        for (int[] row : arr) {
            for (int data : row) {
                System.out.print(data + "\t");
            }
            System.out.println();
        }
    }

    public int getValueNum(int[][] arr){         
        int sum = 0;
        for(int i = 0; i < arr.length; i++){
            for(int j = 0; j < arr[i].length; j++){
                if(arr[i][j] != 0){
                    sum += 1;
                }
            }
        }
        return sum;
    }
}

```

### 四、课后作业

1)**在前面的基础上，将稀疏数组保存到磁盘上，比如** **map.data**

2)**恢复**原来的数组时，读取**map.data**进行恢复

> ==具体代码操作==

在工具类MyArrayUtils.java里面添加两个方法即可

```java
/**
* 将稀疏数组存盘
*
* @param sparseArray
*/
public void saveToFile(int[][] sparseArray) {
    FileWriter fileWriter = null;
    try {
        fileWriter = new FileWriter(new File("src/sparseArray.txt"));
        for (int[] array : sparseArray) {
            fileWriter.write(array[0] + "\t" + array[1] + "\t" + array[2]);
            // \r是回车符,\n是换行符(具体作用请百度)
            fileWriter.write("\r\n");
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

/**
* 从磁盘中读取稀疏数组
*
* @return
*/
public int[][] readFromFile() {
    int[][] sparseArray2 = null;
    boolean isNotRead = false;
    BufferedReader bufferedReader = null;
    try {
        bufferedReader = new BufferedReader(new FileReader(new File("src/sparseArray.txt")));
        String lineStr = null;
        int curCount = 0;
        while ((lineStr = bufferedReader.readLine()) != null) {
            String[] tempStr = lineStr.split("\t");
            if (!isNotRead) {
                sparseArray2 = new int[Integer.parseInt(tempStr[2]) + 1][3];
                sparseArray2[curCount][0] = Integer.parseInt(tempStr[0]);
                sparseArray2[curCount][1] = Integer.parseInt(tempStr[1]);
                sparseArray2[curCount][2] = Integer.parseInt(tempStr[2]);
                curCount++;
                isNotRead = true;
            } else {
                sparseArray2[curCount][0] = Integer.parseInt(tempStr[0]);
                sparseArray2[curCount][1] = Integer.parseInt(tempStr[1]);
                sparseArray2[curCount][2] = Integer.parseInt(tempStr[2]);
                curCount++;
            }
        }
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
            bufferedReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    return sparseArray2;
}

```



