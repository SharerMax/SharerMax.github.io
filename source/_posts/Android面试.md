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

## RecycleView 局部刷新
如果有可能尽量不直接调用 [notifyDataSetChanged][3]，尽可能使用和数据变化对应的方法来通知 Adapter 数据发生了变化。如：
> 1. [notifyItemChanged(int)]
> 2. [notifyItemInserted(int)]
> 3. [notifyItemRemoved(int)]
> 4. [notifyItemRangeChanged(int, int)]
> 5. [notifyItemRangeInserted(int, int)]
> 6. [notifyItemRangeRemoved(int, int)]

## Object 的wait() 方法


[1]: http://www.importnew.com/7010.html
[2]: http://zhaox.github.io/2016/07/05/hashmap-vs-hashtable
[3]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter#notifydatasetchanged

[notifyItemChanged(int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemChanged(int)
[notifyItemInserted(int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemInserted(int)
[notifyItemRemoved(int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRemoved(int)
[notifyItemRangeChanged(int, int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeChanged(int,%20int)
[notifyItemRangeInserted(int, int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeInserted(int,%20int)
[notifyItemRangeRemoved(int, int)]: https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeRemoved(int,%20int)