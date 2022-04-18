# ·1多线程（Java.Thread）

##  1.引言

 随着计算机的配置越来越高，我们需要将进程进一步优化，细分为线程，充分提高图形化界面的多线程的开发。这就要求对线程的掌握很彻底。

##  2. 程序，进程，线程

###  1.程序：

 是为完成特定任务，用某种语言编写的一组指令的集合，即指一段静态的代码，静态对象。 

### 2.进程：

 是程序的一次执行过程，或是正在运行的一个程序，是一个动态的过程，有它自身的产生，存在和消亡的过程。-------生命周期 

### 3.线程：

 进程可进一步细化为线程，是一个程序内部的一条执行路径 

##  3.多线程的继承方式

###  1.方式一：继承于Thread类

1.创建一个集成于Thread类的子类 （通过ctrl+o（override）输入run查找run方法）
2.重写Thread类的run（）方法
3.创建Thread子类的对象
4.通过此对象调用start（）方法 

### 2.方式二：实现Runnable接口

1.创建一个实现了Runnable接口的类
2.实现类去实现Runnable中的抽象方法：run()
3.创建实现类的对象
4.将此对象作为参数传递到Thread类中的构造器中，创建Thread类的对象
5.通过Thread类的对象调用start（） 

## 4.多线程的状态

### 4、1 线程状态

![1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224805.png)

```java
//线程状态观测
public class TestState{

    public static void main(String[] args) {
        Thread thread = new Thread(()->{
            for (int i = 0; i < 5; i++) {
                try {
                    Thread.sleep(1000);//每隔1秒刷新一次 方便观察
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("/////////////////////");
        });
        //观察状态
        Thread.State state = thread.getState();//更新状态
        System.out.println(state);
        //启动后的状态
        thread.start();
        state = thread.getState();//更新状态
        System.out.println(state);

        while(state != Thread.State.TERMINATED){//只要线程不结束就一直运行
            try {
                thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            state = thread.getState();//更新状态
            System.out.println(state);
        }
        /* thread.start();//线程结束后不可以二次启动*/
    }

}

```

![2](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224809.png)

### 4、2停止线程

```java
/**
 * 1、建议使用正常停止
 * 2、建议使用标志位
 * 3、不建议使用stop 或者 destory 等过时的方法
 */
public class Teststop implements Runnable {
    private boolean flag = true;//位置符
    @Override
    public void run() {
        int i = 0;
        while (flag){//当flag = false 时停止
            System.out.println("线程Runing"+i++);
        }
    }

    public void stop(){
        this.flag = false;
    }

    public static void main(String[] args) {
        //启动
        Teststop teststop = new Teststop();

        new Thread(teststop).start();//启动线程
        for(int i = 0; i < 1000; i++){
            System.out.println("mian"+i);
            if (i == 900) {
                teststop.stop();//停止线程
                System.out.println("线程该停止了" + i);
            }
        }
    }
}
```

### 4、3线程休眠

```java
//线程休眠
//每个对象都有一把锁 sleep不会释放锁
public class TestSleep {

    public static void main(String[] args) {
        //启动
        /*countTime();*/
        //时刻显示当前时间
        Date date = new Date(System.currentTimeMillis());//获取当前时间
        while(true){
            try {
                Thread.sleep(2000);//两秒刷新一次
                System.out.println(new SimpleDateFormat("HH:mm:ss").format(date)); //格式工厂时间
                date = new Date(System.currentTimeMillis());//更新时间

            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    //简单计时器(模拟倒计时)
    public static void countTime(){
        for (int i = 10; i >  0; i--){
            System.out.println(i);
            try {
                Thread.sleep(1000);//休眠1秒左右
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```



### 4、4线程礼让

![1619513837206](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224819.png)

```java
//礼让线程yield  线程礼让不一定会成功 完全看CPU 的心情
public class TestYield implements Runnable {
    public static void main(String[] args) {
        TestYield testYield = new TestYield();

        new Thread(testYield,"A").start();
        new Thread(testYield,"B").start();
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"线程开始");
        Thread.yield();//线程礼让
        System.out.println(Thread.currentThread().getName()+"线程结束");
    }
}

```

![1624171215774](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224819.png)

### 4、5 线程强行执行

可以理解为插队 尽量少用，会造成线程阻塞

```JAVA
//强制执行线程 join 可以理解为插队 很霸道
//不建议使用 会造成线程阻塞
public class TestJoin implements Runnable {
    public static void main(String[] args) {
        //插队线程
        TestJoin testJoin = new TestJoin();
        Thread thread = new Thread(testJoin);
        thread.start();

        //主线程
        for(int i= 1; i  <= 500; i++){
            System.out.println("main普通线程"+i);
            if (i == 200){
                try {//主线程会进入阻塞状态  等待thread线程结束才可以继续
                    thread.join();//操作对象需要时Thread类
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    @Override
    public void run() {
        for(int i = 1; i <= 1000; i++){
            System.out.println("VIP专属线程通道"+i);
        }
    }
}
```

### 4、6守护线程(deamon)

![3](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224827.png)

```java
//守护线程Daemon
//守护线程不用自己关闭   用户线程结束后 守护线程也会随之结束
public class TestDaemon {
    public static void main(String[] args) {
        God god = new God();
        You you = new You();

        Thread thread = new Thread(god);
        thread.setDaemon(true);//守护线程 默认是false
        thread.start();//启动

        new Thread(you).start();//用户线程启动
    }

}

//上帝
class God implements Runnable{
    @Override
    public void run() {
        while (true){
            System.out.println("上帝守护着你");
        }
    }
}
//人
class You implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 36500; i++) {
            System.out.println("开心地渡过每一天！！！");
        }
        System.out.println("-==========你离开了这个世界！==========-");
    }
}

```



## 5.线程同步

### 5、1 介绍

![4](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224835.png)

### 5、2 同步方法 synchronized

![5](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224838.png)

```java
// 一定要明确锁的对象 默认是this(锁的一定要是变化的量)
public class UnsafeTicket implements Runnable {
    int ticketnum = 10;//初始时十张票
    @Override
    public synchronized void run() {//抢票问题

        while(true)
        {
            if(ticketnum <= 0){ //当 票数 为 0 时 停止
                return;
            }
            System.out.println(Thread.currentThread().getName()+"抢到了第"+ticketnum--+"票");//Thread 里有一个获取名字的方法
        }

    }

    public static void main(String[] args) {
        UnsafeTicket action = new UnsafeTicket();

        new Thread(action,"小明").start();
        new Thread(action,"王老师").start();
        new Thread(action,"黄牛党").start();
    }
}

```

### 5、3同步块

![6](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224850.png)

```java
//不安全的银行案例
//两个人去银行取钱，账户
public class UnsafeBank {
    public static void main(String[] args) {
        Account account = new Account(100,"结婚基金");

        withDrawal Boyfriend = new withDrawal(account,50,"男朋友");
        withDrawal Girlfriend = new withDrawal(account,100,"女朋友");

        //启动
        Boyfriend.start();
        Girlfriend.start();
    }
}
//账户
class Account{
    int money;//卡内余额
    String name;//卡号
    public Account(int money, String name) {
        this.money = money;
        this.name = name;
    }
}

//银行：模拟取款
class withDrawal extends Thread{

    Account account;//账户
    int withdrawalmoney;//提取的金额
    int nowmoney;//手里的钱
    public withDrawal(Account account, int withdrawalmoney,String name) {
        super(name);
        this.account = account;
        this.withdrawalmoney = withdrawalmoney;
    }

    @Override
    public void run() {
        //同步块   synchronized默认锁的是this
        synchronized (account){  //（）里就是需要锁的对象
            if(account.money - withdrawalmoney < 0){ //如果卡内余额小于需要提取的金额
                System.out.println("卡内余额不足！！！");
                return;//截断
            }
            try {
                this.sleep(2000); //增加sleep 可以更添加明显的看出效果
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            account.money -= withdrawalmoney;//更新卡内余额
            nowmoney += withdrawalmoney;//更新手里的钱
            System.out.println(account.name+"余额为"+account.money);
            System.out.println(this.getName()+"余额为"+nowmoney);

        }

    }
}
```

### 5、4 JUC安全类型的集合

```java
CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
//本身就是安全的，不需要使用synchronized
```

### 5、5 死锁（deadlock）

多个线程互相拥抱着对方的资源，形成僵持

![11](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224911.png)

```java
//死锁
public class DeadLock {
    public static void main(String[] args) {
        //启动
        MakeUp makeUp = new MakeUp(0,"灰姑凉");
        MakeUp makeUp2 = new MakeUp(1,"白雪公主");
        Thread thread = new Thread(makeUp);
        Thread thread2 = new Thread(makeUp2);

        thread.start();
        thread2.start();
    }
}
//口红
class LipStick{

}
//镜子
class Mirror{

}

//化妆
class MakeUp implements Runnable{
    //需要的资源只有一份，用static 来保证只有一份
    static LipStick lipStick = new LipStick();
    static Mirror mirror = new Mirror();
    int choice;//选择
    String girlName;//使用化妆品的人
    public MakeUp(int choice,String girlName) {
        this.choice = choice;
        this.girlName = girlName;
    }

    @Override
    public void run() {
        //化妆
        makeup();
    }
    public void makeup(){
        if (choice == 0){
            synchronized (lipStick){//先锁口红
                System.out.println(this.girlName+"正在使用口红！");
                synchronized (mirror){//锁镜子
                    System.out.println(this.girlName+"正在使用镜子！");
                }
            }
        }else{
            synchronized (mirror){//先锁镜子
                System.out.println(this.girlName+"正在使用镜子！");
                synchronized (lipStick){//锁口红
                    System.out.println(this.girlName+"正在使用口红！");
                }
            }
        }
    }
}
```

### 5、6  死锁避免方案

![12](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224916.png)

### 5、7 可重入锁（ReentrantLock）

![1](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224920.png)

![2](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220331224931.png)

```java
//锁 ReentrantLock 可重入锁
public class Lock {
    public static void main(String[] args) {
        ticket ticket = new ticket();

        new Thread(ticket,"alne").start();
        new Thread(ticket,"bob").start();
        new Thread(ticket,"cici").start();
    }
}

class ticket implements Runnable{
    int ticket = 10;
    //定义lock锁
    private final ReentrantLock lock = new ReentrantLock();
    @Override
    public void run() {
        while(true) {
            try{
                lock.lock();//加锁
                if (ticket > 0) {
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + "抢到了" + ticket-- + "张票");
                } else {
                    break;
                }
            }finally{
                //解锁
                lock.unlock();
            }
        }
    }
}
```

