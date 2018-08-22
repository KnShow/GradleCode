GradleCode
   Gradle的学习之路


   
 #Gradle入门
 
 ##Gradle 版HelloWorld
    task hello{
		doLast{
			println'Hello World!'
		}
	}
	
   切换到指定文件夹下打开终端使用 gralde -q hello 命令来执行构建脚本:   Hello World!
	
    这个构建脚本定义一个任务task，任务名字hello
	并且给任务hello添加一个Action，Gradle源码中的一段Grovy语言实现的闭包。
	doLast就意味着Task执行完毕后要回调doLast的这部分闭包的代码实现
  
	gralde -q hello>?
       执行build.gradle脚本中定义的名为hello的task -q参数用于控制输出的日志级别
	   以及哪些日志可以输出被看到
	println'Hello World!'？
		System.out.println("hello world")的简写，Gradle可以识别
		因为Groovy 把println()这个方法添加到java.lang.Object 而Groovy中可以省略签名中括号
		注意：Groovy中的单引号和双引号所包含的内容都是字符串。
     	
		
 ##Gradle Wrapper
    Wrapper 就是对Gradle的一层包装，便于开发统一Gradle构建的版本
	当我们使用Wrapper启动Gradle的时候，Wrapper会检查Gradle有没有被下载关联,没有将会从配置的地址
	进行下载并运行构建
    
	###生成Wrapper
	   项目根目录终端输入: gradle wrapper 
       生成文件:
			gradle ->wrapper -> gradle-wrapper.jar、gradle-wrapper.properties
			gradlew
			gradlew.bat
        gradlew和gradlew.bat分别是Linux和windows下的可执行脚本,他们的用法和原生的gradle的用法是一样的
		gradle-wrapper.jar 是具体业务逻辑实现的jar包，gradlew最终还是使用java执行的这个jar包来执行相关Gradle操作
    
	###wrapper配置
	    参照AndroidStudio中的默认配置		
		    distributionBase=GRADLE_USER_HOME   下载的gradle压缩包解压后的存储的主目录
			distributionPath=wrapper/dists		相对于distributionBase的解压后的Gradle压缩包的路径
			zipStoreBase=GRADLE_USER_HOME       同 distributionBase，只不过是存放zip压缩包的
			zipStorePath=wrapper/dists             distributionPath 
			distributionUrl=https://services.gradle.org/distributions/gradle-3.5-all.zip gradle发行的压缩包的下载地址
			org.gradle.jvmargs=-Xmx512m
		 distributionUrl	https://services.gradle.org/distributions/gradle-3.5-bin.zip我们通常会将bin改成all，这样在开发过程中
		 就可以查看gradle源码了
		 
	 
	###自定义Wrapper Task
	   前面提过gradle-wrapper.properties是由Wrapper Task生成的。那么我们就可以自定义配置Wrapper Task来达到我们配置gradle-wrapper.properties
	   在build.gradle中录入以下脚本:
	    // 配置gradle版本
	    task wrapper(type: Wrapper){
			gradleVersion = '2.4'
		}
		同样的也可以配置其他参数
		
  ##Gradle日志
	###日志级别
     	error  quiet warning lifecycle info debug
		
	###	输出错误堆栈信息
	    错误堆栈开关选项
       :-s|--stacktrace          输出关键性的堆栈信息
       :-S|--full-stacktrace	    输出全部堆栈信息
	      
	### 自己使用日志信息调试
	   println '日志信息'|logger.quiet('日志信息');
	  

  ##Gradle 命令行
	 ###使用帮助命令
	  :gradlew -?
	  :gradlew -h
	  :gradlew -help
	  
	 ###查看所有可执行的Tasks
	    为什么:有时候我们不知道如何构建一个功能,不知道该执行哪个task，使用gradlew tasks 可以查看哪些task可执行都具备哪些功能
	  :gradlew tasks
		
     ### Gradle Help任务          
       帮助我们了解每一个task的使用帮助
      :	gradlew help -task   
	   从这些帮助信息中我们可以查看这个task作用、类型、属于哪个分组、有哪些可使用的参数
	 
     ###强制刷新依赖 	 
		强制更行第三方库的缓存
	   :gradlew --refresh -dependencies assemble
	   
	 ###多任务调用
       	 执行jar之前先进行clean   多个任务之间用空格分开
		 : gradlew clean  jar,
		 
     ###通过任务名字缩写执行 
	    gradle 提供了基于驼峰命名法的缩写调用 比如 connectCheck
		:gradlew connectCheck
		    缩写
		:gradlew cc
	   
 
 
 
 
 
 