---
layout: post
title: jax_implementation
date: 2023-02-12 13:01 +0800
---
https://jax.readthedocs.io/en/latest/autodidax.html#pytrees-and-flattening-user-functions-inputs-and-outputs

当你想要通过使用 JAX 来自动求解梯度或者进行向量化操作时，你需要理解一些基本的 JAX 概念，包括“tracer”、“trace”等。本文将对这些概念进行介绍，帮助你更好地理解 JAX 的工作原理。

# 从JVP说起

## JVP(Jacobian-Vector products)

函数在一点周围的展开可以被看作是线性化，和原点之间的差就是JVP。


被叫做products是因为算子可以看作先作用在x上得到线性映射，再作用在v向量上得到结果，可以被写作$$(x,v)|->f'(x)v$$.


想要获得导数，可以看作是想要获取JVP的矩阵标准表示，所以我们经常需要输入input 1， 可以被看作一个标准基。

在机器学习中，我们通常使用一个巨大维度到一维的惩罚函数，所以jocob矩阵是非常宽的，我们需要的是vjp，可以看作把jocob矩阵进行转置的操作。

## How to compute them

考虑$f(x_1,x_2,x_3)=\frac{x_1x_2sin(x_3)+e^{x_1x_2}}{x_3}$



# tracer、trace

首先，我们来看一个函数 f(x) 的例子，它实现了对 x 的 sin 函数求值并进行一些简单的数学运算：
```
def f(x):
  y = sin(x) * 2.
  z = - y + x
  return z
```

怎么把这函数捕获以后进行转化呢？一种处理的方式是将根据python语法将函数解析为AST，下面我们来看看jax所采用的另一种做法。

在 JAX 中，我们将一个tracer类作为参数传入函数 f(x)，这是一个已经重载了所有数学运算操作符的类。在函数转换过程中，我们将输入参数 x 转换为 tracer 对象，并使用重载规则进行数学运算，从而实现运算律的捕获和重载。

几个可以用tracer建模的例子：

- 前向求导过程

- vmap向量化

- 获得中间表示进行jit

## jvp

JVP 解释器的输入是一个函数 f，输入参数 x 和一个向量 v。JVP 解释器的函数接口是 (a -> b) -> (a, T a) -> (b, T b)，其中原函数 f 的类型是 (a -> b)，输入参数 x 的类型是 a，向量 v 的类型是 T a。

在 JVP 解释器中，输入参数 x 和向量 v 先被包装成 JVPTracer 类。然后，这些数据会被传入函数中进行运算。bind 函数会根据输入参数 JVPTrace 找到对应的 Trace 类进行处理。Trace 类会找到各种运算规则的重载，比如在原始输入空间中的乘法 x1*x2 对应在向量空间中的乘法规则 v1 * x2 + x1 * v2，然后将原始输入和梯度从 tracer 中解包出来进行运算。

## vmap

vmap 是一个利用 tracer 实现批次向量化的操作，它可以在 batch 上忽略一些索引来对函数进行操作。在执行 vmap 操作时，我们将函数的参数打包成 BatchTracer，然后进行提升匹配。如果有一个非批次和批次的 tracer 进行运算，我们使用 np.broadcast 来提升非批次的向量。

例子：

假设我们有一个形状为(4,3)的numpy数组a，他可以和形状为(3,)的数组做broadcast，但是不能和形状为(4,)的数组做broadcast。我们可以设计一个tracer保存a的batch_dim,也就是1，这样每次做运算的时候，可以根据batch_dim所在的维度对其他非batch的数组进行expand，然后进行运算。



## 数据依赖性

需要注意的是，解释器实际上是一个嵌套包装的过程，它会将包装好的 tracer 数据解包，然后调用规则来计算变换。

在 JAX 中，我们使用 tracer 对象来追踪函数的执行过程，并在需要时将值包装在 tracer 对象中以便实现自动微分等功能。我们定义 bind 函数，来根据 tracer 对象的类型来选择相应的 trace 类来处理操作。这个选择原则被称为数据依赖性。


具体来说，数据依赖性是一个决定在多个解释过程中如何选择使用哪个 trace 类来处理特定操作的原则。在 JAX 中，这个原则是基于栈的。根据 tracer 对象在栈中的顺序，JAX 决定使用哪个 trace 类来处理特定的操作。


在 JAX 中，每个转化过程被抽象为两个类：tracer 类和 trace 类。trace 类的功能是将处理重载算符的过程进行包装，这个过程可能包括将输入的非本类 Tracer 转化为本类 Tracer，查找并调用重载的算符，以及包含一些额外的全局解释器信息。

当使用 bind 函数求值时，我们需要使用 find_top_trace 操作来找到与级别最高的 tracer 对应的 trace 类，并将所有参数提升到这个 tracer 上，然后使用该 trace 类来处理所有原语。这样可以跳过与转换无关的步骤。

因此，bind 函数实际上是一个调度不同 trace 类的过程。当我们需要执行一个解释过程的时候，可以将这个值包装在一个 tracer 对象中，以便 bind 函数使用相应的 trace 类来处理操作。




# jaxprs

基本上是讲如何从上面所说trace捕获方式来实现一个从源代码到表示的生成。
语法：lambda后面的binder部分其实就是输入变量（之所以称为binder是因为他把一个symbol和value绑定起来了），中间的let部分其实就是执行的语句。最后的in 后面的列表就是返回参数。
在python中一个变量类Var就是aval的包装，

在生成过程中，并不需要变量名字。同时，在重载运算的时候获取变量名是不可能的。在打印的时候，使用下面这段非常pythonic的代码来生成名字

```
namegen = (''.join(s) for r in it.count(1)
            for s in it.permutations(string.ascii_lowercase, r))
names = defaultdict(lambda: next(namegen))
```
整个生成过程为，把输入raise成JaxprTracer,然后根据中间过程中，所使用python对象的地址（id）来追踪不同中间变量。trace中被注入了一个全局builder来储存：1、所有的生成tracer信息以便识别同一个变量。2、保存所有的eqn。最后调用builder的build方法，并且附上输入的tracer和返回的tracer就能获取最终的中间表示了。

虽然Var只有一个实现了__eq__的成员aval，但是（首先python不做类型检查，aval不一定和notation中的类型一致），但由于类本身没有实现__eq__，所以Var相等当且仅当他们是同一个对象。

由于find_top_trace是数据依赖的，所以我们运行下面代码的时候，会直接忽略乘法。我们可以在find_top_trace中加入一个更高等级的tracer来hijack所有的解析，这有点像拿走栈中所有的解释器，然后使用dynamic_trace当作栈底的解释器，但是使用dynamic_trace的概念可以让函数内继续再使用其他的依赖tracer的转化叠加在上面。但这样会让底下的trace失效。


文中唯一用到的dynamic_trace的地方是，make_jaxpr。考虑在jvp中调用make_jaxpr，此时我们不再得到计算前向微分的代码，而是得到原始计算代码的中间表达。这也是为什么我们需要在xla_call的时候将原始代码重新计算前向微分。
```
jaxpr, consts, _ = make_jaxpr_v1(lambda: mul(2., 2.))
print(jaxpr)
```

# jit

jit的两种方式实现：

第一种"final-style"，把jaxprs的生成推迟到数据被真的喂到函数中，然后根据实际的操作来捕获表达式，然后生成对应的jit代码。可以在函数中使用Python控制流。


第二种"init-style"，直接通过输入tracer来生成表达式，这种方式更加的直接，因为jax的目的是把python的计算移到xla中，不需要Python控制流，所以采用第二种。

jit转换函数的过程是，先通过make_jaxpr获取输入函数f的jaxpr，这涉及到使用tracer作为f的输入。然后通过原语`xla_call`来生成或者获取缓存中的编译后的函数。


jit需要1.对函数的输入进行hash影响从而缓存签名相同的函数。2.把生成的表达式转化为xla表达式。



有时候我们在jit中也会调用到jit函数，我们将这些输入的jaxpr看作一个subprocess，然后call it。

一个问题是：我们需要对jit后的函数再做前向求导或者vmap，这意味着我们需要为每个解释器堆栈实现一个jaxpr转换。在jvp中，我们通过jaxpr_as_fun把jaxpr转换回成函数，然后再对这个函数做jvp，返回的函数放入jit中。








A noval way to create partition:

```
def partition_list(bs: List[bool], l: List[Any]) -> Tuple[List[Any], List[Any]]:
  assert len(bs) == len(l)
  lists = lst1, lst2 = [], []
  for b, x in zip(bs, l):
    lists[b].append(x)
  return lst1, lst2
```

# linearize

在linearize中，我们也要生成jaxpr以便后面使用，但是我们只按需要生成所需的jaxpr。


我们把这个过程抽象成以下的函数，其中这个函数以一个python函数和一组输入为输入参数，输入中有些已知有些未知。我们需要把已知参数带入过程，将未知参数的生成过程表达为jaxpr来将来调用。这个过程有点像把一个函数算子解压成为两个。

具体实现是生成一个PartialEvalTracer的有向无环图。PartialEvalTrace会根据输入tracer的是否已知来决定将参数all_lower以后调用bind还是（也就是直接求值），还是生成JaxprEqnRecipe节点。根据节点直接的关系对节点进行拓扑排序后直接求值就行了。

考虑两种情况，第一种，我们在partial eval的过程中遇到了xla_call,第二种：我们解析的对象是jaxpr。

考虑我们对一个被jit装饰的函数进行partial_eval，我们需要对生成的jaxpr编写规则来进行partial eval。
在第一种情况我们需要编写partial_eval_jaxpr来先对原来的jaxpr进行解析，如果输入的jaxpr的eqn可以被成已知和未知两组，然后对已知的eqn组直接运行xla_callq，然后剩下的eqn

# Cond原语

Cond在jax中被实现为一个原语，这意味着我们需要给不同的解释器层添加它。

jvp层：


## some thoughts

1. 不同解析器需要实现不同的xla_call规则。比如在这是因为遇到xla_call意味着进入了一个jit函数的内部。从函数变换的角度看，在trace类中我们需要处理tracer函数的变换规则，在xla类中我们需要处理从jaxepr的变换规则。在partial_eval中，我们要把一个jaxpr也进行

2. jvp和linearize的区别是我们需要把线性计算的部分transpose一下。基本思路是，在线性变换中我们只用处理加法和数乘，如果我们可以对这两种操作进行transpose的话，就能把整个部分transpose掉。即T=t1 t2... tn . Transpose(T)=transpose(t_n) ...transpose(t_n-1) transpose(t_1)。（如果t是线性映射的话证明是显然的）。注意在这部分中，我们也可以对部分是线性的函数做transpose。（反向如何保持中间正常非线性的运算？）

3. undefprimal的定义动机是：输入的线性函数可以还依赖其他的常数，除了undefprimal的其他部分都可以被当作常数看待。所以反向中的非线性部分都在unzip过程中变成常数了。

