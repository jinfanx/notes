||ant|maven|gradle|
|:----|:--|:----|:------|
|复杂度|高|低|低|
|拓展性|差|插件|插件或脚本|
|配置继承|不支持|支持，通过parent指定父pom|通过parent指定或通过`apply from xxx.gradel`继承自指定文件|
|全局属性||`<properties/>`|`ext`|
|全局依赖管理||`<dependencyManagement>`|`force`或使用spring提供的dependencyManagement插件|