---
title: python 可迭代，生成器，迭代器
toc: true
date: 2018-06-11 08:14:29
---


# 缘由：


之前再书上看到过可迭代，生成器，迭代器，但是不大记得了，看视频又看到了，但是感觉讲的还是有点模糊，因此要总结下。


## 要点如下：



    # yield 还是不是很明白


    # 生成器
    # 用到这个元素的时候再去做计算，没有用到的时候不做计算

    # 平方表
    # square_table = []
    # for i in range(1000000):
    #     square_table.append(i * i)
    # for i in range(10):
    #     print(square_table[i])

    # 生成器可以使用 next 和 for 来进行循环
    square_generator = (x * x for x in range(1000000))
    for i in range(10):
        print(next(square_generator))

    # print(type(range(10)))  # 返回的是一个 range 类 ，因为 range 是一个生成器
    # g = range(10)
    # print(next(g))#'range' object is not an iterator

    # 生成器可以从第一个元素开始迭代，但是不能从第 10 个元素开始迭代

    # 生成器 和迭代器和可迭代不是一个概念。
    def fib(limit):
        n, a, b = 0, 0, 1
        while n<limit:
            yield b
            a,b=b,a+b
            n+=1
        return 'done'

    import traceback
    f=fib(6)
    print(type(f))
    print(next(f))
    print(next(f))
    print(next(f))
    print(next(f))
    print(next(f))
    print(next(f))
    # 如果不是从 yield 中返回就是
    # 对于 traceback 的使用
    try:
        print(next(f))
    except StopIteration:
        traceback.print_exc()

    for i in fib(5):
        print(i)


输出：


    0
    1
    4
    9
    16
    25
    36
    49
    64
    81
    <class 'generator'>
    1
    1
    2
    3
    5
    8
    1
    1
    2
    3
    5
    Traceback (most recent call last):
      File "E:/01.Learn/01.Python/01.PythonBasic/c3_8.py", line 46, in <module>
        print(next(f))
    StopIteration: done






代码如下：


    # 可以直接作用于 for 循环的对象统称为可迭代对象 Iterable
    # 可以被 next 函数调用并不断返回下一个值的对象成为迭代器：Iterator(表示一个惰性计算的序列# )
    # 所有可以用 for 循环访问的都是可迭代，只有满足惰性计算才是迭代器
    # 迭代器强调的一点是：惰性计算，用到的时候才计算，而不是预先计算
    # 生成器肯定是个迭代器，因为生成器一定是惰性计算的。


    from collections import Iterable
    from collections import Iterator

    # 看看列表对象和字典对象是否是可迭代的

    print(isinstance([1, 2, 3], Iterable))
    print(isinstance({}, Iterable))

    print(isinstance("aaa", Iterable))
    print(isinstance(1, Iterable))

    print(isinstance([1, 2, 3], Iterator))  # 虽然是可迭代的，但是不是迭代器

    g = (x * x for x in range(10))
    print(type(g))
    print(isinstance(g, Iterable))  # 是可迭代的
    print(isinstance(g, Iterator))  # 而且是迭代器
    for i in g:
        print(i)


    def fib(limit):
        n, a, b = 0, 0, 1
        while n < limit:
            yield b
            a, b = b, a + b
            n += 1
        return 'done'


    f = fib(6)
    print(type(f))
    print(isinstance(f, Iterable))  # 也是可迭代的
    print(isinstance(f, Iterator))  # 也是一个迭代器
    for i in f:
        print(i)


输出：


    True
    True
    True
    False
    False
    <class 'generator'>
    True
    True
    0
    1
    4
    9
    16
    25
    36
    49
    64
    81
    <class 'generator'>
    True
    True
    1
    1
    2
    3
    5
    8
