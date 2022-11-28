

# Spark入门


## Spark框架简介


## 开发环境搭建



## 运行环境-独立部署



## 框架核心组件介绍


## 分布式计算模拟



## 核心编程RDD




## 核心编程-数据结构




## SparkSQL

### 数据模型 DataFrame


### DataSet


### 核心编程-IDEA-UDF


### 核心编程-数据读取和保存


#### 使用mysql作为数据源，读取数据模型


```java
def main(args: Array[String]): Unit = {
    val conf = new SparkConf().setMaster("local[*]").setAppName("spark-mysql")
    val spark = SparkSession.builder().config(conf).getOrCreate()
    import spark.implicits._

    //读取数据
    val df = spark.read
      .format("jdbc")
      .option("url", "jdbc:mysql://localhost:3306/kuafu_db")
      .option("driver", "com.mysql.cj.jdbc.Driver")
      .option("user", "root")
      .option("password", "1234")
//      .option("dbtable", "person")
      .option("dbtable", "(select * from person limit 10) as p")
      .load()
    df.show

    //保存数据
    df.write
      .format("jdbc")
      .option("url", "jdbc:mysql://localhost:3306/kuafu_db")
      .option("driver", "com.mysql.cj.jdbc.Driver")
      .option("user", "root")
      .option("password", "1234")
      .option("dbtable", "person_1")
      .mode(SaveMode.Append)
      .save()

    spark.stop()

  }
```


#### spark内置Hive
