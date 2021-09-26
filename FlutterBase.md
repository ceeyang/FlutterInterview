# Flutter 基础
Flutter 基础问题, 随便抽查几个面试即可

### 1. Dart 基本数据类型
- Numbers, String, Boolean, List, set, Map, Rune, Symbol
- 其中 Numbers 只有 int 和 double 类型, 并没有 float 类型
- Dart 中所有数据类型都是 Object, 默认为 null

### 2. Dart 中的抽象类和抽象方法
- 和 Java 中的抽象类一样，Dart 中的抽象类也是使用 abstract 关键字类修饰。如： abstract class shape{}
- 抽象类不能直接被实例化，需要实现一个子类来继承它。
- 抽象类中可以包含抽象方法和非抽象方法。抽象方法不能包含方法体且子类必须实现，非抽象方法可以包含方法体且子类可以重写。
- 抽象类中也可以定义的实例变量。
- 抽象方法只能定义在抽象类中

### 3. Dart 高阶函数运用
- 四则运算: 
```dart
    /// 四则运算调用
    var plusResult = arithmetic(12, 3, (a, b) =a + b);
    var reduceResult = arithmetic(12, 3, (a, b) =a - b);
    var multiplyResult = arithmetic(12, 3, (a, b) =a * b);
    var divideResult = arithmetic(12, 3, (a, b) =a / b);

    /// 四则运算函数, 包含方法调用
    double arithmetic(double a, double b Function function) {
        return function(a, b)
    }
```

### 4. Dart 中 var 与 dynamic 的区别
- var 声明的变量，dart 会在编译阶段自动推导出类型。
- dynamic 声明的变量，不在编译期间做类型检查而是在运行期间做类型校验

### 5. const 和 final 的区别
const 的值在编译期确定，final 的值在运⾏时确定

### 6. Dart 中 ?? 与 ??= 的区别
两者都是dart中的操作符，?? 表示如果为空则返回，??= 表示如果为空则赋值。例如: 
```dart
   String a;
   String b = a ?? "1";
   print(b);//打印结果：1
   print(a);//打印结果：null
   a ??= "2";
   print(a);//打印结果：2
```

### 7. Dart 中 Future、async、await, Future.wait 的作用
- async 描述一个执行异步操作的方法
- await 表示一直等待异步方法返回结果，才继续往后执行
- Future 返回一个可能包含异步方法的对象
- Future.wait 表示等待多个异步操作完后再执行, 接收参数为 Future 对象数组, 返回值也是数组

### 8. Flutter中的GlobalKey是什么，有什么作用
Globalkey可以主动获取以及主动改变子控件的状态

### 9. 简述 Widget 的 StatelessWidget 和StatefulWidget 的区别与用法, 以及常见的组件
- StatelessWidget: 
> - 一旦创建就不关心任何变化，在下次构建之前都不会改变。它们除了依赖于自身的配置信息（在父节点构建时提供）外不再依赖于任何其他信息。比如典型的 Text、Row、Column、Container 等，都是StatelessWidget。它的生命周期相当简单：初始化、通过 build()渲染。
> - 常见的 StatelessWidget: Container, Column, Row, Text...

- StatefulWidget: 
> - 在生命周期内，该类 Widget 所持有的数据可能会发生变化，这样的数据被称为 State，这些拥有动态内部数据的 Widget 被称为 StatefulWidget。比如复选框、Button 等。State 会与 Context 相关联，并且此关联是永久性的，State 对象将永远不会改变其 Context，即使可以在树结构周围移动，也仍将与该 context 相关联。当 state 与 context关联时，state 被视为已挂载。StatefulWidget 由两部分组成，在初始化时必须要在 createState()时初始化一个与之相关的 State 对象。
> - 常见的 StatefulWidget: Scaffold (此处可以询问 Scaffold 属于哪一种),

### 10. Flutter 中 Widget 的生命周期是什么( Widget 的生命周期实际上就是 State 的生命周期), 分别有什么作用
![周期图片](./assets/flutter_life_cycle.webp)

1. initState：state创建初始化时调用，表示state将和一个BuildContext产生关联，需要注意的是此时BuildContext还没有完全加载完成，如果需要获取BuildContext及监听第一次build完成可以在下面回调中获取
2. didChangeDependencies：在 initState() 之后调⽤，当 State 对象的依赖关系发⽣变化时，该⽅法被调⽤，初始化时也会调⽤
3. deactivate：当state暂时在视图树种移除时被调用，页面切换时也会调用
4. dispose：state销毁时调用，在调用此方法之前会先调用deactivate()
5. didUpdateWidget：当widget状态发生变化时调用

### 11. Flutter 屏幕适配一般怎么做
* 插件相关:
> 1. flutter_screenutil: ScreenUtil.init() 方法初始化屏幕比例, 根据比例计计算各个设备的值

* 适配方案:
> 1. rem rem是给根标签（HTML标签）设置一个字体大小；但是不同的屏幕要动画设置不同的字体大小（可以通过媒体查询，也可以通过js动态计算）；其它所有的单位都使用rem单位（相对于根标签）；
> 2. vw、wh： vw和vh是将屏幕（视口）分成100等份，一个1vw相当于是1%的大小；其它所有的单位都使用vw或wh单位；
> 3. rpx： rpx是小程序中的适配方案，它将750px作为设计稿，1rpx=屏幕宽度/750；其它所有的单位都使用rpx单位；

### 12. Flutter在Debug和Release下分别使用什么编译模式，有什么区别？
Debug模式下使用JIT编译模式，即Just in time（即时编译），Release下使用AOT模式，即Ahead of time（提前编译）。JIT模式因为需要边运行边编译，所以会占用运行时内存，导致卡顿现象，但是有动态编译效果对于开发者来说非常方便调试。AOT模式提前编译不会占用运行时内存，相对来说运行流畅，但是会导致编译时间增加。

### 13. Flutter出现异常时如何友好的提示用户？
使用ErrorWidget.builder进行全局设置自定义界面即可。

### 14. Flutter iOS Android 打包上架流程
略...




#### 文本摘抄多处: 
- https://juejin.cn/post/6844903775207948301#heading-25
- https://juejin.cn/post/6844904176489594893