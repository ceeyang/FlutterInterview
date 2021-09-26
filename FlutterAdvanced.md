# Flutter 进阶

### 1. Widget、Element、RenderObject三者之间的关系
Widget不是真正渲染UI的对象，它只是Element的一个配置描述，去告知Element应该如何去渲染Widget 和 Element 之间是 ⼀对多的关系 。RenderObject才是实际渲染的对象，Element 持有 RenderObject 和 Widget。⼤致总结三者的关系是：配置⽂件 Widget ⽣成了 Element，⽽后创建 RenderObject 关联到 Element 的内部 renderObject 对象上，最后Flutter 通过 RenderObject 数据来布局和绘制。

### 2. 通过BoxDecoration和ClipRRect设置圆角有什么区别
使用BoxDecoration设置圆角不会影响其child控件，也就是如果child是图片或者也有背景色的话那么圆角效果就失效了。而ClipRRect是会影响到child的，加了圆角后，也会约束到child产生圆角效

### 3. Flutter与原生通信的Channel有哪几种
Flutter定义了三种不同类型的Channel，它们分别是：
> - **BasicMessageChannel**：用于传递字符串和半结构化的信息。
> - **MethodChannel**：用于传递方法调用（method invocation）。
> - **EventChannel**: 用于数据流（event streams）的通信。

### 4. Flutter 性能优化
[性能优化——如何避免应用 jank](https://github.com/awesome-tips/Flutter-Tips/blob/master/articles/Flutter%20%20%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E2%80%94%E2%80%94%E5%A6%82%E4%BD%95%E9%81%BF%E5%85%8D%E5%BA%94%E7%94%A8%20jank.md)

### 5. Flutter 如何构建视图的
在 Flutter 中，Everything is Widget，我们通过构造函数嵌套 Widget 来编写 UI 界面。实际上，Widget 并不是真正要显示在屏幕上的东西，只是一个配置信息，它永远是 immutable 的，并且可以在多处重复使用。那真正持有“屏幕上的视图”/“UI控件”树是是什么呢？Element tree！
> - **StatelessWidget:**
    首先它会调用 StatelessWidget的 createElement 方法，并根据这个 widget 生成 StatelesseElement 对象。将这个 StatelesseElement 对象挂载到 element 树上。StatelesseElement 对象调用 widget 的 build 方法，并将 element 自身作为 BuildContext 传入。
> - **StatefulWidget:**
    首先同样也是调用 StatefulWidget 的 createElement 方法，并根据这个 widget 生成 StatefulElement 对象，并保留 widget 引用。将这个 StatefulElement 挂载到 Element 树上。根据 widget的 createState 方法创建 State。StatefulElement 对象调用 state 的 build 方法，并将 element 自身作为 BuildContext 传入。


### 6. Flutter 中 BuildContext 是什么
BuildContext 对象实际上就是 Element 对象，BuildContext 接口用于阻止对 Element 对象的直接操作。

### 7. Flutter 状态管理怎么做的
- 什么是状态管理?
> Flutter中只有StateFull类型的Widget才有state,通过state管理widget的样式更新；状态管理，顾名思义 管理的是数据变化和widget的更新；
- 为什么要进行状态管理？
> 跨widget状态更新：通知另外一个widget进行状态更新. 虽然组件之前能直接传值,但是如果子组件或者父组件太多,代码会常繁琐臃肿，难以复用, 更需要一个统一的组件状态管理工具
- 常见的
- 以下是 Flutter 状态管理插件,用过一两种都行
> - **Provider**
> - **redux**
> - **fish_redux**
> - **Mobx**: 使用透明的函数响应式编程增强Dart程序中的状态管理
> > - Observables: 表示响应式的状态，也可理解为可观察对象。状态指的是应用程序里面的状态或者数据。响应式就是可以感知到、可观察到数据的变化，也就是我们经常接触到的观察者模式。
> > - Actions: Actions就是一系列可以引发状态发生变化的动作。
> > - Reactions: 状态的观察者，状态发生变化的时候，他们可以收到数据变化的通知。
