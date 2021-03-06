---
description: >-
  如果说编码是筋骨皮，那么思想就是一口气，就是内功。内功深厚决定你功力的大小。刚刚读完了设计模式那本书。随着项目业务的复杂，越发的感觉到设计模式的重要性。在此参考CSDN、伯乐在线和开源中国社区，优秀的博文，以此总结。开始新的起点。写于2017/02/28分析内容,属于当第二次看设计模式的感悟,写于2017/12/10
  凌晨02:44
---

# 设计原则

### 一、开闭原则

#### （1）定义

```text
一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。
```

#### （2）问题由来

```text
在软件的生命周期内，因为变化、升级和维护等原因需要对软件原有代码进行修改时，
可能会给旧代码中引入错误，也可能会使我们不得不对整个功能进行重构，并且需要
原有代码经过重新测试。
```

#### （3）解决方案

```text
当软件需要变化时，尽量通过扩展软件实体的行为来实现变化，而不是通过修改已有的代码来实现变化。
```

#### （4）表达

```text
用抽象构建框架，用实现扩展细节因为抽象灵活性好，适应性广，只要抽象的合理，可以基本保持软件
架构的稳定。而软件中易变的细节，我们用从抽象派生的实现类来进行扩展，当软件需要发生变化时，
我们只需要根据需求重新派生一个实现类来扩展就可以了。当然前提是我们的抽象要合理，要对需求的
变更有前瞻性和预见性才行。
```

#### （5）分析

```text
就是对扩展开放,对修改关闭, 里式替换原则理论支持了这个一说法,及子类要能替换父类,这样子类就
可以在父类的基础上,扩展。
```

### 二、单一职责原则

#### （1）定义

```text
不要存在多于一个导致类变更的原因通俗的说，即一个类只负责一项职责。
```

#### （2）问题由来

```text
类T负责两个不同的职责:
职责P1，职责P2。当由于职责P1需求发生改变而需要修改类T时,有可能会
导致原本运行正常的职责P2功能发生故障。
```

#### （3）解决方案

```text
遵循单一职责原则。分别建立两个类T1、T2,使T1完成职责P1功能,T2完成职责P2功能。
这样当修改类T1时,不会使职责P2发生故障风险;同理,当修改T2时,也不会使职责P1发生故障风险。
```

#### （4）表达

```text
不要让责任扩散
```

#### （5）分析

```text
一个类,指责要单一,避免如果有多种职责,修改一个职责的时候,误触到其他职责的问题。
```



### 三、里氏替换原则

#### （1）定义

```text
所有引用基类的地方必须能透明地使用其子类的对象。
```

#### （2）问题由来

```text
有一功能P由类A完成，现在要扩展P,其中P由类A的子类B完成,则子类在完成的同时,可能会导致原来功能故障
```

#### （3）解决方案

```text
当使用继承时,遵循里氏替换原则。类B继承类A时,除添加新的方法完成新增功能外,尽量不要重写父类A的
方法,也尽量不要重载父类A的方法。
```

#### （4）表达

```text
使用继承的时候,不要随便修改父类中已经实现的方法。
```

#### （5）分析

```text
子类要能替换父类
```

### 四、依赖倒置原则

#### （1）定义

```text
高层模块不应该依赖低层模块,二者都应该依赖其抽象;抽象不应该依赖细节;细节应该依赖抽象。
```

#### （2）问题由来

```text
类A直接依赖类B，假如要将类A改为依赖类C，则必须通过修改类A的代码来达成。这种场景下,
类A一般是高层模块,负责复杂的业务逻辑;类B和类C是低层模块，负责基本的原子操作;
假如修改类A,会给程序带来不必要的风险。
```

#### （3）解决方案

```text
将类A修改为依赖接口I,类B和类C各自实现接口I,类A通过接口I间接与类B或者类C发生联系,
则会大大降低修改类A的几率。
```

#### （4）表达

```text
如果A依赖B,现在要改为依赖C,如果直接修改A有风险,可以让A去依赖一个接口,BC都实现这
个接口，也就是策略模式.
```

#### （5）分析

```text
白话就是说,要根据接口或者抽象去设计,不要依赖于细节。

eg1:  项目中要换数据库,不用重新写底层的数据库代码。
      就是使用了hibernate一样,替换方言就好了,因为hibernate是根据接口设计的,不同数据库有不同的实现
      可以直接使用。
 
eg2: 我生病了要去买药,如果A药铺,没有我就用B药铺买。
      因为他们都是药铺,都有一样的功能,可以友好的替换。
```

### 五、接口隔离原则

#### （1）定义

```text
客户端不应该依赖它不需要的接口;一个类对另一个类的依赖应该建立在最小的接口上。
```

#### （2）问题由来

```text
类A通过接口I依赖类B,类C通过接口I依赖类D,如果接口I对于类A和类B来说不是最小接口,
则类B和类D必须去实现他们不需要的方法。
```

#### （3）解决方案

```text
将臃肿的接口I拆分为独立的几个接口,类A和类C分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则。
```

#### （4）表达

```text
防止去实现不需要的接口方法,可以按接口拆分,避免臃肿。
```

#### （5）分析

```text
白话,接口要最小化,功能更细分。目的是:不需要的功能,就不要去实现。
```

### 六、迪米特法则

#### （1）定义

```text
一个对象应该对其他对象保持最少的了解。
```

#### （2）问题由来

```text
类与类之间的关系越密切，耦合度越大，当一个类发生改变时，对另一个类的影响也越大。
```

#### （3）解决方案

```text
尽量降低类与类之间的耦合。
```

#### （4）表达

```text
尽量降低类与类之间的耦合。
```

#### （5）分析

```text
降低类与类之间直接交互,能隐藏的属性就可以隐藏。
eg. 修电脑,去IT部门,之前一直找小张,现在小张走了,还需要重新认识小李。
    迪米特法则,就是直接找IT主管,让主管派人修。这里其实也抢到了接口的重要性。
```



