#  GUI编程(图形界面编程)

## 1、引言

- Swing Awt 技术是核心
- 不流行的原因： 界面不美观   需要jre环境(太耗费资源)
- ![1618757683415](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331225531.png)

## 2、AWT

### 2、1 Frame界面

```java
//Frame JDK 看源码
Frame frame = new Frame("我的第一个图形界面！");
//需要设置可见性
frame.setVisible(true);
//设置大小
frame.setSize(400,400);
//设置背景颜色
frame.setBackground(new Color(111, 26, 113));
//初始坐标
frame.setLocation(0,0);
//设置大小固定
//frame.setResizable(false);
```

 ![1618756705698](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331225537.png)

### 2、2 Panel面板

可以看成是一个空间，但是不能单独存在

```java
//创建frame对象
Frame frame = new Frame("Panel面板");
//创建panel对象
Panel panel = new Panel();
//设置布局
frame.setLayout(null);
//设置frame初始位置、大小
frame.setBounds(400,200,500,500);
//设置panel初始位置、大小
panel.setBounds(50,50,400,400);
//设置颜色
frame.setBackground(Color.red);
panel.setBackground(Color.green);
//将panel 添加到 frame里
frame.add(panel);
//设置可见性
frame.setVisible(true);
```

 ![1618756735243](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331225541.png)

### 2、3 三大基本设置布局

 ***容器中的组件排放方式，就是布局*** 

#### 1、流式布局 FlowLayout

 (流式布局管理器，构造方法可指定对齐方式、水平垂直间距)

 特点：从左到右的顺序排列，默认居中。 

```java
Frame frame = new Frame("流式布局");
//创建 组件--->按钮 对象
Button button1 = new Button("button1");
Button button2 = new Button("button2");
Button button3 = new Button("button3");

//设置流式布局
//frame.setLayout(new FlowLayout());//默认是居中的
//frame.setLayout(new FlowLayout(FlowLayout.LEFT));//最左端
frame.setLayout(new FlowLayout(FlowLayout.RIGHT));//最右端

//设置 frame 界面大小
frame.setSize(400,400);
//设置背景颜色
frame.setBackground(Color.GREEN);
//将按钮添加到frame界面里
frame.add(button1);
frame.add(button2);
frame.add(button3);

//frame 界面可见性
frame.setVisible(true);
```

 ![1618756640194](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331225548.png)

#### 2、东西南北中布局 BorderLayout

特点：按照东南西北中的顺序排列， Frame默认的布局管理器。

 其中每个部分只可添加一个组件，若添加多个组件，则最后添加的组件会覆盖前面的。 

```java
Frame frame = new Frame();

Button east = new Button("east");
Button west = new Button("west");
Button north = new Button("north");
Button south = new Button("south");
Button center = new Button("center");

//布局
frame.add(east,BorderLayout.EAST);
frame.add(west,BorderLayout.WEST);
frame.add(north,BorderLayout.NORTH);
frame.add(south,BorderLayout.SOUTH);
frame.add(center,BorderLayout.CENTER);

//设置大小 和 起始位置
frame.setBounds(500,500,500,500);
//设置背景颜色
frame.setBackground(new Color(245, 64, 251));
//设置可见
frame.setVisible(true);
```

 ![1618756590546](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331225551.png)

#### 3、表格布局 GridLayout

 （网格布局管理器，构造方法可指定水平垂直间距）

   特点：规则的矩阵 ，系统自带的计算器用的就是这个布局。 

```java
Frame frame = new Frame();

Button button1 = new Button("button1");
Button button2 = new Button("button2");
Button button3 = new Button("button3");
Button button4 = new Button("button4");
Button button5 = new Button("button5");
Button button6 = new Button("button6");
//设置布局
frame.setLayout(new GridLayout(3,2));
frame.add(button1);
frame.add(button2);
frame.add(button3);
frame.add(button4);
frame.add(button5);
frame.add(button6);
//自动设置页面大小
frame.pack();
//界面可见
frame.setVisible(true);
```

 ![1618756544682](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331225556.png)

### 2、4 事件监听器

```java
//监听事件ActionListener  类似交互
//创建 实现接口的对象
MyMonitor myMonitor = new MyMonitor();
//给按钮添加 事件监听
button.addActionListener(myMonitor);//需要传递一个接口 或者实现接口的对象
//实现 接口 就一定要实现里面的方法
class MyMonitor implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("点击成功！！！");
    }
}
```

### 2、5 画笔 Paint

```java
class PaintTools extends Frame {
    public void loadFrame(){
        setBounds(500,500,600,400);
        setVisible(true);
        Exit(this);
    }

    @Override//画笔是自动调用的  默认只执行一次
    public void paint(Graphics g) {
        /*super.paint(g);*/
        Color color = g.getColor(); //保存原有的颜色
        //画笔可以画画 （但是需要有颜色）
        g.setColor(Color.red);//设置画笔颜色
        g.drawOval(100,100,100,100);//空心圆
        g.setColor(Color.red);//设置画笔颜色
        g.fillOval(200,200,100,100);//实心圆
        g.setColor(color);//还原颜色
    }
    //关闭 监听
    public static void Exit(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}
```

### 2、6 简易计算器

```java
//oop原则之一：组合 大于继承
//使用完全的面向对象思想   （属性 加 方法）
//使用内部类实现
public class TestCalculator03 {
    public static void main(String[] args) {
        //启动
        Calculator02 calculator = new Calculator02();
    }
}
//计算器类 (将监听类加入其中)
class Calculator02 extends Frame {
    //属性
    TextField num1,num2,sum;
    //方法
    public Calculator02(){
        //标题  super 要放在第一位
        super("简易计算器");
        //设置布局
        setLayout(new FlowLayout());
        setBounds(500,500,400,300);
        //可见性
        setVisible(true);
        //三个输入框
        num1 = new TextField(10);//columns:列
        num2 = new TextField(10);
        sum = new TextField(20);

        //一个按钮（=）
        Button button = new Button("=");
        //添加监听事件
        button.addActionListener(new MyCalculatorListener02()); //把自己传进去
        //一个标签
        Label label = new Label("+");

        add(num1);
        add(label);
        add(num2);
        add(button);
        add(sum);
        //关闭
        Exit(this);
    }
    //关闭监听的方法
    public static void Exit(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
    //监听类
    private class MyCalculatorListener02 implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            //1、转型 成为整型
            int n1 = Integer.parseInt(num1.getText());
            int n2 = Integer.parseInt(num2.getText());
            int s1 = n1 + n2;
            System.out.println(n1+" + "+n2+" = "+s1);
            //2、将前两个数相加的结果 写到第三个框里
            sum.setText(""+(n1+n2));

            //3、清除前两个框
            num1.setText("");
            num2.setText("");
        }
    }
}

```

### 2、7 键盘监听

```java
//键盘监听内部类
this.addKeyListener(new KeyAdapter() {
    @Override
    public void keyPressed(KeyEvent e) {
        //获取按下键盘的数值
        int keyCode = e.getKeyCode();
        System.out.println(keyCode);
    }
});
```

## 3、SWING

### 3、1 JFrame窗口

JFrame 是 Frame 的子类   而且里面的属性基本都多了一个“ J ” 

```java
//swing 技术 是AWT的升级版
public class TestJFrame01 {
    public static void main(String[] args) {
        //启动
        MyJFrame myJFrame = new MyJFrame();
        myJFrame.init();
    }
}
class MyJFrame extends JFrame{
    public MyJFrame() throws HeadlessException {
        super("JFrame界面");
        this.setBounds(100,100,400,300);
        this.setBackground(Color.red);
        this.setVisible(true);
        //内置关闭监听
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //初始化
    public void init(){
        //设置文字
        JLabel jLabel = new JLabel("这是内容，位置居中！");
        //设置位置居中
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);
        this.add(jLabel);
        //获得一个容器
        Container container = this.getContentPane();
        container.setBackground(Color.red);
    }

}
```

### 3、2 弹窗

JDialoy

```java
//主界面
class MyjFrame extends JFrame {
    public MyjFrame(){
        super("弹窗测试");
        setLayout(null);
        setBounds(100,100,500,400);
        setVisible(true);
        //setBackground(Color.red);  //颜色等设置需要放在容器里
        //创建一个容器  JFrame 放东西的容器
        Container container = this.getContentPane();
        //绝对布局
        container.setLayout(null);
        //创建一个按钮
        JButton jButton = new JButton("点击我会弹出一个窗口！");
        jButton.setBounds(100,100,500,400); //给按钮设置个初始位置

        //关联一个事件监听
        jButton.addActionListener(new ActionListener(){
            @Override
            public void actionPerformed(ActionEvent e) {
                //弹出一个窗口
                new Dialogstart();
            }
        });
        container.add(jButton);//将按钮添加到容器中

        //关闭窗口
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
    //写一个弹窗内部类
    private class Dialogstart extends JDialog{
        public Dialogstart() {
            //弹窗默认是不可见的
            this.setVisible(true);
            this.setBounds(100,100,500,500);
            //容器
            Container container = this.getContentPane();
            JLabel jLabel = new JLabel("这是一个弹窗");
            JButton jButton = new JButton("妞妞111");
            jLabel.setBounds(100,100,50,50);//label需要设置位置才可以显示
            container.add(jLabel);
            //container.add(jButton);
            container.setBackground(Color.pink);

        }
    }
}
```



###  
