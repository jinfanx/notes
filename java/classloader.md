## 类加载机制
双亲委派模型，当一个classloader需要加载类时，先尝试用parent classloader加载，没加载到再调用自己的类加载方法。`不同的类加载器区别在于查找class文件的路径和方法不同`，这种机制可以保证不会因为类重名而造成混乱，假如不用这种机制，自定义的classLoader去加载一个重新实现的java.lang.String，就会导致系统中存在两个同名的类。

## 自定义classloader
继承ClassLoader或某个子类，实现findClass方法，在findClass方法中找到对应类的class文件读取到字节数组中，然后将字节数组传递给
defineClass得到一个Class对象返回即可

## 常见问题
### 类何时被加载
真正使用时或使用反射显示加载，import不会加载类

### classloader涉及到哪些设计模式
- 模板方法

### 类加载涉及到哪些阶段
- 加载
- 验证
- 准备
- 解析
- 初始化
- 使用
- 卸载
