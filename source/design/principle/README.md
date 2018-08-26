# 设计原则

## 单一职责原则
单一职责原则（SRP）定义：
应该有且仅有一个原因引起类的变更。

单一职责解释：
单一职责原则提出一个编写程序的标准，用“职责“或 “变化原因”来衡量类和接口设计是否优良。 单一职责适用于类、接口、方法，一个方法尽可能只做一件事情，每个方法的职责十分明确，不仅开发简单，便于日后维护。对于接口，在设计的时候需要做到单一，但对于实现类，不要对类进行过度拆分，过度拆分会人为地提高系统的复杂性，对系统的耦合性也会造成影响。

单一职责好处：
类的复杂性降低
代码可读性提高
可维护性提高
变更引起的风险降低

最佳实践：
在实际开发过程中，由于项目的工期、人员等不可预知因素，可能对单一职责不能完全遵守，但有个建议：接口和方法一定要做到单一职责原则，类的设计尽量做到只有一个原因引起变化。

## 里氏替换原则
里氏替换原则（LSP）定义：
所有引用基类（父类）的地方必须能透明地使用其子类的对象（何意？）

里氏替换原则解释：
首先要明白里氏替换原则要解决的问题：在面对对象的语言中，继承是必不可少的，但继承有利有弊，为了让利更多，弊更少，引出了里氏替换原则。
只要有父类出现的地方子类就可以出现，而且可以将父类直接替换为子类，不会产生任何错误或异常，使用者不必知道是父类还是子类。反过来就不行，有子类的地方，不能直接替换为父类。

里氏原则为继承定义一个规范，包含4个含义；
1. 子类必须完全实现父类的方法
      子类不能完整地实现父类的方法，建议断开父子继承关系，采用依赖、聚集、组合等关系代
      替继承。
2. 子类可以有自己的方法和属性
      这里主要是解释有子类的地方，父类就不一定能用。
3. 覆盖或实现父类的方法时输入参数可以被放大
      子类方法的参数（Map）可以比父类方法参数（HashMap）的范围大【重载父类的方法】
4. 覆盖或实现父类的方法时输出结果可以被缩小
      父类的一个方法的返回值是T，子类的相同方法（重载或覆写）的返回值是S，那么S必须小于等于T，即S和T要么是同一类型，要么S是T的子类。

最佳实践：
在项目中，尽量避免子类有“个性”

## 依赖倒置原则
依赖倒置（DIP）包含三个含义：
1. 高层模块不应该依赖低层模块，两者都应该依赖其抽象
2. 抽象不应该依赖细节
3. 细节应该依赖抽象

依赖倒置在Java中表现就是：
1. 模块间的依赖通过抽象发生，实现类之间不发生直接的依赖关系，其依赖关系通过接口或抽象类来产生的
2. 接口或抽象类不依赖于实现类
3. 实现类依赖接口或抽象类

依赖倒置的三种写法：
1. 构造函数传递依赖对象
2. Setter方法传递依赖对象
3. 接口声明依赖对象

最佳实践：
1. 每个类尽量都有接口接口或抽象类，或者两者都有
2. 变量的表面类型尽量是接口或者是抽象类
3. 任何类都不应该从具体类派生
4. 尽量不要覆写基类的方法
5. 结合里氏替换原则使用

## 接口隔离原则
接口隔离原则含义：
建立单一接口，接口尽量细化，同时接口中的方法尽可能少

保证接口的纯洁性，有以下几点：
接口尽量小
接口要高内聚
定制服务
接口设计是有限度的，注意适度

最佳实践：
1. 一个接口只服务于一个子模块或业务逻辑
2. 通过业务逻辑压缩接口的方法
3. 接口被污染，尽量去修改，或者采用适配器模式进行转化处理

## 迪米特法则
迪米特法则含义：
一个类应该对自己需要耦合或调用的类知道得最少

最佳实践：
一个类不要对外公开太多的public方法和非静态的public变量，而使用private， protected修饰。修改或者删除public的方法或者属性需要十分小心，别的类可能正在用。
如果一个方法放在本类中，既不会增加类之间关系，也不影响本类，那么就放在本类中。

## 开闭原则
开闭原则含义：
一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。

注意：
开闭原则对扩展开放，对修改关闭，并不意味着不做任何修改，底层模块的变更，必然要有高层模块进行耦合。