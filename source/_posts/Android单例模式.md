---
title: Android单例模式
date: 2018-10-24 11:51:17
tags: 单例模式
---

## 懒汉式（线程不安全）

```Java
public class Singleton {  
    private static Singleton instance = null;  
    private Singleton() {  
        
    }    
      
    public static Singleton getInstance() {  
        if (instance == null) {  
            instance = new Singleton();  
          }  
        return instance;  
    }  
}
```
<!--more-->

## 懒汉式（线程安全）

```Java
public class Singleton {  
    private static Singleton instance = null;  
    private Singleton() {  
        
    }    
      
    public static synchronized Singleton getInstance() {  
        if (instance == null) {  
            instance = new Singleton();  
          }  
        return instance;  
    }  
}
```

## 饿汉式（线程安全）

```Java
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton() {  
        
    }
      
    public static Singleton getInstance() {  
        return instance;  
    }
}
```
## 双重校验锁（线程安全，懒加载，JDK 1.5 以上）

```Java
public class Singleton {  
    private volatile static Singleton instance = null;  
    private Singleton() {  
        
    }
      
    public static Singleton getInstance() {
        if (instance == null) { 
            synchronized(Singleton.class) {
                if (instance == null) { // 多个线程同时来到同步块，拿到锁的新建实例后，后续的线程可以做判断是否已创建 
                    instance = new Singleton(); 
                }
            }
          }
        return instance;
    }  
}
```

## 静态内部类（线程安全，懒加载）

```Java
public class Singleton {  
    private Singleton() {  
        
    }
    public static Singleton getInstance() {  
        return SingletonHolder.instance;  
    }

    private static class SingletonHolder {
        private static Singleton instance = new Singleton();
    }
}
```
<div class="tip">
上面列出的是常用的几种，还有其它方式来构建单例，比如使用枚举或容器类来构建，但我很少用到，便不再列出，需要的可自行搜索。
</div>