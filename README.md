1.gradle安装，gradle版本，这个我建议先下载spring源码后，看spring目录中的build.gradle文件中的gradleVersion字段，直接搜索，然后根据这个版本去下载相应的版本，本次编译使用的是spring-framework-5.0.x，在环境变量中添加gradle，gradle已经放在工具文件中，

2.下载好了在运行cmd打开dos Terminal，进入到你的springframework项目的目录下，运行gradlew.bat，我这边这个没有出现问题，但我不保证你们不出问题，，主要是你们的版本一定要控制好。

3.idea导入gradle项目如下报错解决方案：
 a.The provided plugin org.jetbrains.kotlin.scripting.compiler.plugin.Scripting可以知道是 kotlin版本的问题,在idea 中 File -> Settings -> Plugins 搜索栏输入 Kotlin, 点击Update
  注意：如果没有显示update ，稍等一会应该会出现，如果还不行，那就重启下idea
 b.再次编译工程 idea 中 Build -> Build Project然后发现又报错Error:(30, 41) java: 找不到符号:类 DefaultNamingPolicy,Objenesis,InstantiatorStrategy,ObjectInstantiatorObjenesisException ，进入springframework项目的目录下执行 gradle objenesisRepackJar 和 gradle  cglibRepackJar（如执行gradlew.bat可忽略）
 
 c.再次 idea 编译源码工程 Build -> Build Project发现解决了上述编译报错问题:找不到符号: 类 DefaultNamingPolicy InstantiatorStrategy ObjenesisException
 但是又报了新的错误： 找不到符号: 类 AnnotationBeanConfigurerAspect ，JCacheCacheAspect ，AnnotationAsyncExecutionAspect ，AnnotationCacheAspect ，AnnotationTransactionAspect
 安装AspectJ(已经放在工具类中)，打开 系统cmd 命令行 切换工作目录到 下载的AspectJ 所在目录执行 java -jar aspectj-1.9.0.jar，安装过程中3个设置我都是默认的 直接next（注意第二步要设置自己已经安装的jdk家目录）
 
 4.File -> Project Structure -> Facets -> 点击 + 按钮 -> AspectJ -> 选择 spring-aop_main -> 点击OK -> 右键spring-aop_main的Kotlin 选择删除，给 spring-aspects_main 也添加Facets属性
 
 5.更改编译器 File ->setting ->complier->java complier->use complier Ajc ->Path to Ajc Complier (刚才Aspectj安装目录下/lib/aspectjtools.jar)->勾选delegate to javac
 
 可参考以下文档：https://blog.csdn.net/a704397849/article/details/102754505
               https://www.cnblogs.com/echola/p/10943195.html
               https://blog.csdn.net/Sex__God/article/details/103114365
 
