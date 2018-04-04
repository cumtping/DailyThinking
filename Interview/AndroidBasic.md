#Andriod基础
1. 安卓四大组件有哪些？(component)
    activity, service, broadcast receiver, content provider。
    四大组件是安卓应用开发的基石。activity负责界面显示，service负责后台服务，broadcast receiver负责进程内和进程间通信，content provider负责数据共享。
  为什么称它们是组件呢？

2. activity的生命周期有哪些？activity有几种启动方式？

activity生命周期：

    onCreate（创建），onStart（可见），onResume（获取焦点），onPause（失去焦点），onStop（不可见），onDestroy（销毁）；
    
    Q1:从activity A1启动activity A2，它们各自会经历哪些生命周期？
    A： A1 onPause；A2 onCreate；A2 onStart；A2 onResume； A1 onStop；
    解析：为什么是这个顺序，而不是先A2 onCreate再A1 onPause？
         因为先执行A1 onPause 将会释放掉很多系统资源，为切换Activity提供流畅性的保障，而不需要再等多两个阶段，这样做切换更快。

    参考：https://www.jianshu.com/p/fb44584daee3
    
activity的启动模式：

    standard默认模式；
    singleTop 这种模式是在创建了Activlty a 之后再创建Activity a的时候 就不会创建成功，而是会调用你第一个创建的Activyt a里面的getNewIntent方法。但是要注意的是你的Activity a这时候在栈顶的时候再创建Activity a才会不重复创建，在栈顶的意思就是你当前这个页面就是Activity a，如果你在a的时候 startActivity了 Activity b，之后再创建Activiyt a是不会调用Activity a的getNewIntent方法的，因为他此时不会处于栈顶；
    singleTask 就是创建了Activitiy a，之后又创建了b c d，当在d的时候再创建a，会把中间的b c都finish了。。意思就是这个栈中该Activity的实例只能存在一个，并且会将中间的都清空，并且调用自身的getNewIntent方法，如果是Activity a创建了Activity a 则只会调用自己的getNewIntent。 适用的场景：当你要创建一个东西（页面0），比如第一个页面要选择时间，第二个页面要选择地点，第三个页面选择费用，在第三个页面选择完成后，要把 1 2 3 页面拿到的东西回传给页面0，有两种方式，一种就是startActivityForRsult，但是每个页面都要加一次。。这样子感觉比较复杂，这时候只要将创建东西的页面改为singleTask就能完美解决这个问题；
    singleInstance如果应用1的任务栈中创建了MainActivity实例，如果应用2也要激活MainActivity，则不需要创建，两应用共享该Activity实例；大概就是比如来了通知，要打开Activity a，之后另外一个应用也要打开Activity a这样子会进入到两个不同的栈中，设置他的属性为singleInstace就会使他们进入到同一个栈。。不会重复创建Activity；

    参考：https://www.jianshu.com/p/78554606ea27

3. broadcast有哪几种？</br>
4. service 有哪几种启动方式?</br>
5. android 数据存储方式有哪几种？</br>
6. 如何保证content provider访问安全?</br>
