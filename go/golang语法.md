## 特有语法
- 切片
变长数组

- range
遍历数组、切片、channel、map等

- channel
协程间通信用

- 协程
轻量级线程

- init函数和`import _ "package"`



## 习惯用法
- 函数和库
golang的库用法类似C语言，不像java一样把方法绑定到类，调用时通过package.FunctionName调用，而非通过对象调用。当然也可以为对象实现接口，然后通过objectName.MethodName来调用

- 文件组织
- 

## 缺点
- 不支持泛型
- 依赖管理
从github下载的项目

## 常见问题
- 如何实现接口

- 如何区分公有方法和私有方法

- 方法和函数的区别

- 何时使用指针变量，何时使用普通变量
