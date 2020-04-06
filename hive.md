## hive
1. replication join和hash join介绍。还有打乱到多台reduce中的参数
2. 在Hive中，用户可以自定义一些函数，用于扩展HiveQL的功能，而这类函数叫做UDF（用户自定义函数）。UDF分为两大类：UDAF（用户自定义聚合函数）和UDTF（用户自定义表生成函数）。

Hive有两个不同的接口编写UDF程序。一个是基础的UDF接口，一个是复杂的GenericUDF接口。

org.apache.hadoop.hive.ql. exec.UDF 基础UDF的函数读取和返回基本类型，即Hadoop和Hive的基本类型。如，Text、IntWritable、LongWritable、DoubleWritable等。
org.apache.hadoop.hive.ql.udf.generic.GenericUDF 复杂的GenericUDF可以处理Map、List、Set类型。