http://zh.lucida.me/blog/java-8-lambdas-insideout-language-features/
</br> lambda表达式 http://www.cnblogs.com/JohnTsai/p/5584905.html

frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/DarkIconDispatcherImpl.java
```
44          mTransitionsController = new LightBarTransitionsController(context,
45                  this::setIconTintInternal);
94      private void setIconTintInternal(float darkIntensity) {
```
frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/LightBarTransitionsController.java
```
66      public LightBarTransitionsController(Context context, DarkIntensityApplier applier) {
199      /**
200       * Interface to apply a specific dark intensity.
201       */
202      public interface DarkIntensityApplier {
203          void applyDarkIntensity(float darkIntensity);
204      }
```

- lambda 表达式的语法由参数列表、箭头符号 -> 和函数体组成。函数体既可以是一个表达式，也可以是一个语句块：
```
(int x, int y) -> x + y
() -> 42
(String s) -> { System.out.println(s); }
```

- 第一个 lambda 表达式接收 x 和 y 这两个整形参数并返回它们的和；
- 第二个 lambda 表达式不接收参数，返回整数 ‘42’；
- 第三个 lambda 表达式接收一个字符串并把它打印到控制台，不返回值。


---
http://lucida.me/blog/developer-reading-list/#htdp
程序设计方法
现代编程语言的语法大多很繁杂，初学者使用这些语言学习编程会导致花大量的时间在编程语言语法（诸如指针，引用和类型定义）而不是程序设计方法（诸如数据抽象和过程抽象）之上。 程序设计方法 解决了这个问题——它专注于程序设计方法，使得读者无需把大量时间花在编程语言上。这本书还有一个与之配套的教学开发环境 DrScheme ，这个环境会根据读者的程度变换编程语言的深度，使得读者可以始终把注意力集中在程序设计方法上。

我个人很奇怪 程序设计方法 这样的佳作为什么会绝版，而谭浩强C语言这样的垃圾却大行其道——好在是程序设计方法 第二版 已经被免费发布在网上。
