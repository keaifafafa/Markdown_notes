## 1、为什么使用Builder

lombok注解在java进行编译时进行代码的构建，对于java对象的创建工作它可以更优雅，不需要写多余的重复的代码，这对于JAVA开发人员是很重要的，在出现lombok之后，对象的创建工作更提供Builder方法，它提供在设计数据实体时，对外保持private setter，而对属性的赋值采用Builder的方式，这种方式最优雅，也更符合封装的原则，不对外公开属性的写操作！

@Builder声明实体，表示可以进行Builder方式初始化，@Value注解，表示只公开getter，对所有属性的setter都封闭，即private修饰，所以它不能和@Builder现起用

## 2、@Builder注解的使用

```java
@Getter
@Setter
@Builder
public class Father {

    private Integer id;
    private String name;
    private Integer age;

}

```

> ==然后看一下编译后的文件内容==

```java
public class Father {
    private Integer id;
    private String name;
    private Integer age;

    Father(final Integer id, final String name, final Integer age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    public static Father.FatherBuilder builder() {
        return new Father.FatherBuilder();
    }

    public Integer getId() {
        return this.id;
    }

    public String getName() {
        return this.name;
    }

    public Integer getAge() {
        return this.age;
    }

    public void setId(final Integer id) {
        this.id = id;
    }

    public void setName(final String name) {
        this.name = name;
    }

    public void setAge(final Integer age) {
        this.age = age;
    }

    public static class FatherBuilder {
        private Integer id;
        private String name;
        private Integer age;

        FatherBuilder() {
        }

        public Father.FatherBuilder id(final Integer id) {
            this.id = id;
            return this;
        }

        public Father.FatherBuilder name(final String name) {
            this.name = name;
            return this;
        }

        public Father.FatherBuilder age(final Integer age) {
            this.age = age;
            return this;
        }

        public Father build() {
            return new Father(this.id, this.name, this.age);
        }

        public String toString() {
            return "Father.FatherBuilder(id=" + this.id + ", name=" + this.name + ", age=" + this.age + ")";
        }
    }
}

```

**生成了全参构造器和构造器模式代码**

## 3、需要注意的坑

仔细看会发现此时并没有生成无参构造，一些框架序列化喜欢用反射new对象，比如现在比较流行的序列化框架Fastjson，这时候就会报错，而反射new对象在编译期是发现不了的，所以容易导致线上问题。此时有几种解决方式

1. 同时加上无参和有参的注解,让对象同时生成有参和无参方法（==推荐==）

   ```java
   @AllArgsConstructor
   @NoArgsConstructor
   ```

   

2. 自己写无参构造，加上@Tolerate注解让lombok忽略它（这种写法不推荐，ide程序会无法识别出全参构造，导致你写全参构造的时候代码标红，强迫党不能忍）

   ```java
   @Getter
   @Setter
   @Builder
   public class Father {
   
       private Integer id;
       private String name;
       private Integer age;
   
       @Tolerate
       Father() {
       }
   }
   
   ```

   > **==总结==**

   使用@Builder的时候，最好和@AllArgsConstructor，@NoArgsConstructor一起用。

