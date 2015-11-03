# JavaSparkPi

   算Pi是spark中自带的例子，和wordcount一样都是最简单的spark应用，相当于spark界的HelloWorld。简述一下我的做法和开发环境：
   
   一台master和两台slaves已经配置好了hadoop和spark，集群已经搭建好。我在windows中putty远程操作master。
   
   1. 先说在local本地运行。
   
     SparkConf sparkConf = new SparkConf().setAppName("JavaSparkPi").setMaster("local"); 
     还要引进一个jar包：spark-assembly-1.5.1-hadoop1.2.1.jar
     然后直接运行就行了，不需要任何spark配置。local是用本地机器的线程模拟多个电脑的做法。
     
   2. 再说在集群中运行。
   
     SparkConf sparkConf = new SparkConf().setAppName("JavaSparkPi").setMaster("spark://master:7077");
     
       2.1 将项目右键export成一个jar包。移动到master中任意路径（在这里我才用的是xftp来移动文件，直接复制粘贴很方便）。
       
       2.2 在master中找到spark目录，敲入如下代码：
       
             ./spark-submit\
             
                     --class org.apache.spark.examples.JavaSparkPi\
                     
                     --master spark://master:7077\
                     
                     --executor-memory 1024MB\
                     
                     --total-executor-cores 8\
                     
                      /home/SparkPiTest.jar\
       这就是最简单的sparkPi实例。  
