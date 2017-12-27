|spark-submit|spark-default.conf|spark-env.sh|默认值|含义|模式(第1列)|
|:--|:--|:--|:--|:--|:--|
|--total-executor-cores|spark.cores.max|\|无|spark app可以向集群(不是单个节点)申请的最多cpu核数,防止某个用户独占资源|standalone
mesos|
|--executor-cores|spark.executor.cores|SPARK_EXECUTOR_CORES|Yarn:1
standalone:所有可用cores|每个执行器分配的cpu数量，决定任务的并
发数量|Yarn
standalone|
|--num-executors|spark.executor.instances|\|2|申请执行器数量|Yarn|
|--executor-memory|spark.executor.memory|SPARK_EXECUTOR_MEMORY|1g|执行器内存|all|
|--queue|spark.yarn.queue|\|default|提交应用到Yarn上哪个队列|Yarn|
|--deploy-mode|spark.submit.deployMode|DEPLOY_MODE|client|以哪种模式(client、cluster)启动driver|all|
|--master|spark.master|MASTER|local[*]|cluster manager类型|all|
|--name|spark.app.name|\|app主类名称|应用的名称|all|
|--class||\|必须指定|app主类|all|
|--driver-cores|spark.driver.cores|\|1|driver使用cpu核数|standalone 
cluster
Yarn cluster|
|--driver-memory|spark.driver.memory|SPARK_DRIVER_MEMORY|1g|driver使用内存|all|
|--driver-java-options|spark.driver.
extraJavaOptions|\|\|传给driver的额外的Java选项|all|
|--driver-library-path|spark.driver.
extraLibraryPath|\|\|传给driver的额外的库路径|all|
|--driver-class-path|spark.driver.
extraClassPath|\|\|driver依赖的jar包，以:分隔|all|
|--jars|spark.jars|\|\|driver和executor都需要的jar包，以逗号分隔的jar包|all|
|--files|spark.files|||逗号分隔的文件，这些文件放在每个
executor的工作目录下面||
|--supervise||||Driver失败时，重启driver。指定这个参数即可，貌似不用赋值，最好还是赋值为true|standalone
mesos|
|--conf||||spark配置属性，以key=value的形式配置||
