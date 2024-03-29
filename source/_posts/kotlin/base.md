---
title: kotlin基本语法
date: 2024-03-20 20:02:37
tags:
---

入口
fun main() {
    println("Hello world!")
}

函数

//sampleStart
fun sum(a: Int, b: Int): Int {
    return a + b
}
//sampleEnd

fun main() {
    print("sum of 3 and 5 is ")
    println(sum(3, 5))
}

变量
定义只读局部变量使用关键字 val 定义。只能为其赋值一次。
可重新赋值的变量使用 var 关键字。

when写法