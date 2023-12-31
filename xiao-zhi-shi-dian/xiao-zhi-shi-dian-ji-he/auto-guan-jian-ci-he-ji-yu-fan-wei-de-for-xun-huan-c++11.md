# auto 关键词和基于范围的 for 循环（C++11）

**auto不再是一个存储类型指示符，而是作为一个新的类型 指示符来指示编译器，auto声明的变量必须由编译器在编译时期推导而得**。

也就是说，我们在定义一个变量时，不需要自己去考虑这个变量的类型，而是把这件事情交给了编译器来进行

## 使用细则

1. auto 与指针和引用结合起来使用\
   用 auto 声明指针类型时，用 auto 和auto\*没有任何区别，但用auto声明引用类型时，则必须加 &
2. 同一行定义多个变量\
   同一行声明多个变量时，这些变量必须是同一类型。
3. auto不适用的场景\
   &#x20;1）auto 不能作为函数的函数\
   &#x20;2）auto 不能直接用来声明数组

## 基于范围的for循环（C+11）

### 范围 for 语法

#### C++98

```cpp
void TestFor()
{
     int array[] = { 1, 2, 3, 4, 5 };
     for (int i = 0; i < sizeof(array) / sizeof(array[0]); ++i)
     array[i] *= 2;
 
     for (int* p = array; p < array + sizeof(array)/ sizeof(array[0]); ++p)
     cout << *p << endl;
}
```

#### C ++11

对于一个**有范围的集合**而言，由程序员来说明循环的范围是多余的，有时候还会容易犯错误。因此C++11中 引入了基于范围的for循环。**for循环后的括号由冒号“ ：”分为两部分：第一部分是范围内用于迭代的变量， 第二部分则表示被迭代的范围**。

```cpp
void TestFor()
{
	int a[] = { 1, 2, 3, 4, 5 };
	for (auto& e : a)
		e *= 2;
	for (auto e : a)
		cout << e << " ";
	return;
}
 
int main()
{
	TestFor();
	return 0;
}
```

### 使用条件

1. for 循环迭代的范围必须是确定的\
   &#x20;**对于数组而言，就是数组中第一个元素和最后一个元素的范围**；对于类而言，应该提供begin和end的 方法，**begin**和**end**就是for循环迭代的范围。
2. 迭代的对象要实现++和==的操作
