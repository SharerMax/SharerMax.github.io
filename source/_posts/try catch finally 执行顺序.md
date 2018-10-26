---
title: try catch finally 执行顺序
date: 2018-10-26 15:03:23
tags: [Java, 异常捕获, 执行顺序]
---

## 无异常发生
#### 有finally
```Java
static int demo() {
    int i = 10;
    try {
        System.out.println("try block");     
        return i - 1; // #1
    } catch (Exception e) {
        System.out.println("catch block");
        return i - 2; // #2
    } finally {
        System.out.println("finally block");  
        return i - 3; // #3
    }
}
```
**输出**：
> try block
> finally block

**返回值**：
> 7

#### 无finally
```Java
static int demo() {
    int i = 10;
    try {
        System.out.println("try block");     
        return i - 1; // #1
    } catch (Exception e) {
        System.out.println("catch block");
        return i - 2; // #2
    }
}
```
**输出**：
> try block

**返回值**：
> 9
<!--more-->

## 有异常发生
#### 有finally
```Java
static int demo() {
    int i = 10;
    try {
        System.out.println("try block before");
        i = i / 0; // 触发异常
        System.out.println("try block after");
        return i - 1; // #1
    } catch (Exception e) {
        System.out.println("catch block");
        return i - 2; // #2
    } finally {
        System.out.println("finally block");  
        return i - 3; // #3
    }
}
```
**输出**：
> try block before
> catch block
> finally block

**返回值**：
> 7

#### 无finally
```Java
static int demo() {
    int i = 10;
    try {
        System.out.println("try block before");
        i = i / 0; // 触发异常
        System.out.println("try block after");
        return i - 1; // #1
    } catch (Exception e) {
        System.out.println("catch block");
        return i - 2; // #2
    }
}
```
**输出**：
> try block before
> catch block

**返回值**：
> 8

## 总结

1. try 块先执行，若未发生异常，则执行 finally 块；若try 中有异常发生，则从异常处中断，执行catch块，最后再执行 finally 块；
2. 三个块中的 return 以最后执行 return 的值为结果返回。