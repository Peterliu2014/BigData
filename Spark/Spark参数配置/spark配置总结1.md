|spark-submit|spark-default.conf|spark-env.sh|默认值|含义|模式(第1列)|备注|
|:--|:--|:--|:--|:--|:--|:--|
|--total-executor-cores|spark.cores.max|\|无|spark app可以向集群(不是单个节点)申请的最多cpu核数,防止某个用户独占资源|standalone
mesos|spark.deploy.defaultCores|
|--executor-cores|spark.executor.cores|SPARK_EXECUTOR_CORES|Yarn:1
standalone:所有可用cores|每个执行器分配的cpu数量，决定任务的并
发数量|Yarn
standalone|floor(cores.max/executor.cores)
计算standalone下分配的executor数
量，yarn直接通过--num-executores指定。

HDFS client 在大量并发线程时会有性能问题，大概的估计是每个executor 中最多5个并行的 task 就可以占满的写入带宽。
   2~4个较合适。

运行微型 executor （比如只有一个core而且只有够执行一个task的内存）会抛弃在一个JVM上同时运行多个task的好处。比如 broadcast 变量需要为每个executor 复制一遍，这么多小executor会导致更多的数据拷贝，如果executor有多个核，只需要复制一次，多个task就可以共享。

|
|--num-executors|spark.executor.instances|\|2|申请执行器数量|Yarn|从 Spark 1.3 开始，可以避免使用
这个参数，只要你通过设置 spark.dynamicAllocation.enabled 参数打开动态分配 。动态分配可以使的 Spark 的应用在有积压的等待 task 时请求 executor，并且在空闲时释放这些 executor。
   50~100较为合适|
|--executor-memory|spark.executor.memory|SPARK_EXECUTOR_MEMORY|1g|执行器内存|all|4G~8G较为合适|
|--queue|spark.yarn.queue|\|default|提交应用到Yarn上哪个队列|Yarn||
|--deploy-mode|spark.submit.deployMode|DEPLOY_MODE|client|以哪种模式(client、cluster)启动driver|all|client模式下driver运行在提交应用的机器上，cluster模式下driver运行在某个worker(NM)节点上。|
|--master|spark.master|MASTER|local[*]|cluster manager类型|all|spark://node:ip,yarn,memsos:...|
|--name|spark.app.name|\|app主类名称|应用的名称|all|如果是Yarn，env.sh中可以配置
SPARK_YARN_APP_NAME|
|--class||\|必须指定|app主类|all||
|--driver-cores|spark.driver.cores|\|1|driver使用cpu核数|standalone 
cluster
Yarn cluster||
|--driver-memory|spark.driver.memory|SPARK_DRIVER_MEMORY|1g|driver使用内存|all||
|--driver-java-options|spark.driver.
extraJavaOptions|\|\|传给driver的额外的Java选项|all||
|--driver-library-path|spark.driver.
extraLibraryPath|\|\|传给driver的额外的库路径|all|启动driver jvm时需要使用的库路径|
|--driver-class-path|spark.driver.
extraClassPath|\|\|driver依赖的jar包，以:分隔|all|其实就是spark的lib和libext下没
有，而应用又依赖的jar包|
|--jars|spark.jars|\|\|driver和executor都需要的jar包，以逗号分隔的jar包|all|其实就是spark的lib和libext下没
有，而应用又依赖的jar包|
|--files|spark.files|||逗号分隔的文件，这些文件放在每个
executor的工作目录下面|||
|--supervise||||Driver失败时，重启driver。指定这个参数即可，貌似不用赋值，最好还是赋值为true|standalone
mesos||
|--conf||||spark配置属性，以key=value的形式配置|||
