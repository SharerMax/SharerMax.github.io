---
title: Android面试
date: 2018-09-17 15:03:41
tags: [Android, 面试]
---

## 1. HashMap 与 HashTable 的区别

HashMap 和 HashTable 都实现了Map接口，

#### 线程安全性
HashMap是线程不安全的，并且可以接受 *null* 做为键值或 value 值, HashTable是线程安全的，但是不能接受 *null* 值

#### 速度
HashMap因为非 synchronized，所以在单线程模式下性能会优于HashTable

#### 迭代器
HashMap使用的迭代器 fail-fast 迭代器 *Iterator*，而 HashTable 使用的是非 fail-fast 的迭代器 *Enumerator* 

> 1. [HashMap 和 Hashtable 的区别][1]
> 2. [HashMap 和 HashTable 到底哪不同？][2]

## 2. RecycleView 局部刷新
如果有可能尽量不直接调用 [notifyDataSetChanged][3]，尽可能使用和数据变化对应的方法来通知 Adapter 数据发生了变化。如：
> 1. [notifyItemChanged(int)]
> 2. [notifyItemInserted(int)]
> 3. [notifyItemRemoved(int)]
> 4. [notifyItemRangeChanged(int, int)]
> 5. [notifyItemRangeInserted(int, int)]
> 6. [notifyItemRangeRemoved(int, int)]

## 3. Object 的 wait() 方法
*wait()* 方法需要写在同步块（*synchronized*）中，并与*notify()* 或 *notifyAll()* 搭配使用。

*wait()*、 *notify()* 和 *notifyAll()* 都是object的方法，当一个对象调用 *wait()* 当前线程会进入WAITING状态进入等待池并释放当前持有的锁。当对象的 *notify()* 或 *notifyAll* 方法被调用，等待状态的线程会进入锁池重新争取锁，一旦获得锁，便进入可RUNNABLE状态，等待执行。

#### notify() 和 notifyAll()的区别
首先要明确一点，等待池中的线程是不参与锁的竞争的，也就无法直接执行；锁池中的线程要先或的锁才能进入RUNNABLE状态，随之执行

*notify()* 随机唤醒等待池中的一个线程进入锁池
*notifyAll()* 唤醒等待池中的所有线程进入锁池

> [java中的notify和notifyAll有什么区别](https://www.zhihu.com/question/37601861/answer/145545371)

## 4. 动态代理
代理模式的定义：代理模式给某一个对象提供一个代理对象，并由代理对象控制对原对象的引用。

代理模式的一种实现，与静态代理相比更适合大量需要代理处理的场景，可实现所谓的AOP思想的编程方式

#### 使用步骤
1. 被代理对象必须为接口，或接口的实现类
2. 代理对象必须实现InvocationHandler接口
3. Proxy.newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h)生成代理对象
4. 使用生成的代理对象替换被代理对象

[动态代理为什么传接口，内部实现接口，而不直接传类，直接继承类?](https://www.zhihu.com/question/264948554/answer/287647598)
<div class="tip">
依一个接口的输入与数据的参数规则去动态的对这个接口进行实现，这种形式是 java 动态代理最常用的一种场景。所以第二个参数实际是对于这个实现的规则的表述，就是一个接口。
</div>




[1]: http://www.importnew.com/7010.html
[2]: http://zhaox.github.io/2016/07/05/hashmap-vs-hashtable
[3]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter#notifydatasetchanged

[notifyItemChanged(int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemChanged(int)
[notifyItemInserted(int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemInserted(int)
[notifyItemRemoved(int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRemoved(int)
[notifyItemRangeChanged(int, int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeChanged(int,%20int)
[notifyItemRangeInserted(int, int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeInserted(int,%20int)
[notifyItemRangeRemoved(int, int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeRemoved(int,%20int)