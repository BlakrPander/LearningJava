# Java编程思想笔记

## 	对象

### 对象的创建

​	初始化变量并不是意味着创建了一个对象，而是创建了对一个对象的引用。
例如：

```java
String s="hello world!";
```

​	此操作仅仅是创建了一个初始化为带引号的文本的引用，并不是创建了一个字符串对象。
​	如果需要创建一个**引用**与**对象**相**关联**，通常用 **new** 关键字来表示。

例如：

```java
String s=new String("hello world!");
```

### 对象的存储

​	对于内存分配，有五大位置：

1. 寄存器：**最快**的存储区域，位于**处理器内部**
2. 堆栈：位于**通用RAM**中，第二快速有效
3. 堆：通用内存池，位于**RAM**中，用于存放**所有的Java对象**
4. 常量存储：
5. 非RAM存储，对象被存储在**磁盘**之上或是可以存储在其他媒介上的事物。

### 基本类型

#### 变量的类型

​	对于一些小的、简单的变量，用**new**将其创建于“**堆**”中不高。因此Java中采用与C等同样的方法：创建一个“自动”变量，直接存储**值**并且存储于**堆栈**之中。

例如：

```java
int tmp=114514;
```

​	在Java中，每种基本类型的大小不随着机械硬件架构的变化而变化。

| 基本类型    | 大小         | 最小值    | 最大值         | 包装器类型    |
| ----------- | ------------ | --------- | -------------- | ------------- |
| **boolean** | -            | -         | -              | **Boolean**   |
| **char**    | 16-bit / 2B  | Unicode 0 | Unicode 2^16-1 | **Character** |
| **byte**    | 8 bits / 1B  | -128      | +127           | **Byte**      |
| **short**   | 16 bits / 2B | -2^15     | +2^15-1        | **Short**     |
| **int**     | 32 bits / 4B | -2^31     | +2^31-1        | **Integer**   |
| **long**    | 64 bits / 8B | -2^63     | +2^63-1        | **Long**      |
| **float**   | 32 bits / 4B | IEEE754   | IEEE754        | **Float**     |
| **double**  | 64 bits / 8B | IEEE754   | IEEE754        | **Double**    |
| **void**    | -            | -         | -              | **Void**      |

**boolean**类型的存储大小没有明确指定，仅能定义为**true**或**false**。	

#### 高精度

除此之外，Java内还有**高精度计算**的类：

1. **BigInteger**：支持任意精度的整数
2. **BigDecimal**：支持任意精度的定点数

这两个类所包含的方法与**int**和**float**相似，但必须要以方法调用的形式来实现。

#### 数组

​	在Java中，创建的引用数组会自动被初化一个特定值**null**。试图使用一个值仍然是**null**的引用将会报错，而这促使开发者创建数组时对其进行初始化管理。

​	同时在Java中，对数组的访问也会保证下标在范围之内，这也保证了**不会产生下表越界**的情况。

### 不需要销毁对象

​	在Java中，以下行为是不合法的：

```java
{
	int x=114514;
	{
		int x=1919; //illegal
	}
}
```

​	即不能存在对同一名称变量的重定义。

​	而在一个变量在执行完其作用域之外的代码之后，**其对象仍然会继续占据内存空间**，只不过在作用域无法访问。事实上，由**new**创建的对象，只要需要将会一直保存下去。这个对象的释放将会由Java自带的*垃圾回收器*来监视是否需要删除。由此Java解决了可能产生的**内存泄漏**的问题。

