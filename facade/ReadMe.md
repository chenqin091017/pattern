# 外观模式

***

###### 外观模式（Facade Pattern）隐藏系统的复杂性，并向客户端提供了一个客户端可以访问系统的接口。这种类型的设计模式属于结构型模式，它向现有的系统添加一个接口，来隐藏系统的复杂性。

###### 这种模式涉及到一个单一的类，该类提供了客户端请求的简化方法和对现有系统类方法的委托调用。

***

## 介绍

- **意图**：为子系统中的一组接口提供一个一致的界面，外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。

- **主要解决**：降低访问复杂系统的内部子系统时的复杂度，简化客户端与之的接口。

- **何时使用**：

> 1、客户端不需要知道系统内部的复杂联系，整个系统只需提供一个"接待员"即可。

> 2、定义系统的入口。

- **如何解决**：客户端不与系统耦合，外观类与系统耦合。

- **关键代码**：在客户端和复杂系统之间再加一层，这一层将调用顺序、依赖关系等处理好。

- **应用实例**： 

> 1、去医院看病，可能要去挂号、门诊、划价、取药，让患者或患者家属觉得很复杂，如果有提供接待人员，只让接待人员来处理，就很方便。 

> 2、JAVA 的三层开发模式。

- **优点**：

> 1、减少系统相互依赖。 

> 2、提高灵活性。 

> 3、提高了安全性。

- **缺点**：不符合开闭原则，如果要改东西很麻烦，继承重写都不合适。

- **使用场景**：

> 1、为复杂的模块或子系统提供外界访问的模块。 

> 2、子系统相对独立。 

> 3、预防低水平人员带来的风险。

- **注意事项**：在层次化结构中，可以使用外观模式定义系统中每一层的入口。

***

## 实现

###### 我们将创建一个 Animals 接口和实现了 Animals 接口的实体类。下一步是定义一个外观类 AnimalsFacade。

###### AnimalsFacade 类使用实体类来代表用户对这些类的调用。Main，我的演示类使用 AnimalsFacade 类来显示结果。

![外观模式的 UML 图](../img/facade_pattern_uml_diagram.jpg)


> 步骤 1：创建一个接口。

**Animals.java**

```markdown
    
    package com.dao.pattern.facade.interfaces;
    
    /**
     * 动物
     *
     * @author 阿导
     * @version 1.0
     * @fileName com.dao.pattern.facade.interfaces.Animals.java
     * @CopyRright (c) 2018-万物皆导
     * @created 2018-03-26 10:45:00
     */
    public interface Animals {
    
        /**
         * 获取动物的名称
         *
         * @author 阿导
         * @time 2018/3/26
         * @CopyRight 万物皆导
         * @param
         * @return java.lang.String
         */
        String name();
    }

```

> 步骤 2：创建实现接口的实体类。

 **Dog.java**
 
```markdown
        
    package com.dao.pattern.facade.impl;
    
    import com.dao.pattern.facade.interfaces.Animals;
    
    /**
     * 狗
     *
     * @author 阿导
     * @version 1.0
     * @fileName com.dao.pattern.facade.impl.Dog.java
     * @CopyRright (c) 2018-万物皆导
     * @created 2018-03-26 10:45:00
     */
    public class Dog implements Animals{
    
        /**
         * 获取狗的名称
         *
         * @return java.lang.String
         * @author 阿导
         * @time 2018/3/26
         * @CopyRight 万物皆导
         */
        @Override
        public String name() {
            return "狗";
        }
    }
    
```
    
**Cat.java**

```markdown
    
    package com.dao.pattern.facade.impl;
    
    import com.dao.pattern.facade.interfaces.Animals;
    
    /**
     * 猫
     *
     * @author 阿导
     * @version 1.0
     * @fileName com.dao.pattern.facade.impl.Cat.java
     * @CopyRright (c) 2018-万物皆导
     * @created 2018-03-26 10:46:00
     */
    public class Cat implements Animals {
    
        /**
         * 获取猫的名称
         *
         * @return java.lang.String
         * @author 阿导
         * @time 2018/3/26
         * @CopyRight 万物皆导
         */
        @Override 
        public String name() {
            return "猫";
        }
    }


```

> 步骤 3：创建一个外观类。

**AnimalsFacade.java**

```markdown

    package com.dao.pattern.facade.core;
    
    import com.dao.pattern.facade.impl.Cat;
    import com.dao.pattern.facade.impl.Dog;
    import com.dao.pattern.facade.interfaces.Animals;
    
    /**
     * 动物的对外接口
     *
     * @author 阿导
     * @version 1.0
     * @fileName com.dao.pattern.facade.core.AnimalsFacade.java
     * @CopyRright (c) 2018-万物皆导
     * @created 2018-03-26 10:48:00
     */
    public class AnimalsFacade {
        /**
         * 狗
         */
        private Animals dog;
    
        /**
         * 猫
         */
        private Animals cat;
    
        /**
         * 初始化
         */
        {
            dog=new Dog();
            cat=new Cat();
        }
    
        /**
         * 获取狗的名称
         *
         * @author 阿导
         * @time 2018/3/26
         * @CopyRight 万物皆导
         * @param
         * @return java.lang.String
         */
        public String getDogName(){
            return dog.name();
        }
    
        /**
         * 获取猫的名称
         *
         * @author 阿导
         * @time 2018/3/26
         * @CopyRight 万物皆导
         * @param
         * @return java.lang.String
         */
        public String getCatName(){
            return cat.name();
        }
    
    }

```

> 步骤 4：使用该外观类获取不同动物的名称。

**Main.java**
 
```markdown

    package com.dao.pattern.facade.main;
    
    import com.dao.pattern.facade.core.AnimalsFacade;
    
    /**
     * 主程序入口
     *
     * @author 阿导
     * @version 1.0
     * @fileName com.dao.pattern.facade.main.Main.java
     * @CopyRright (c) 2018-万物皆导
     * @created 2018-03-26 10:51:00
     */
    public class Main {
    
        /**
         * 主程序入口
         *
         * @author 阿导
         * @time 2018/3/26
         * @CopyRight 万物皆导
         * @param args
         * @return void
         */
        public static void main(String[] args){
            //初始化外观类
            AnimalsFacade animalsFacade=new AnimalsFacade();
    
            //获取猫狗的名字
            System.out.println("dog:"+animalsFacade.getDogName());
            System.out.println("cat:"+animalsFacade.getCatName());
        }
    
    }

```

> 步骤 5：验证输出。

```markdown
    
    dog:狗
    cat:猫
    
```
