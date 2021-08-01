+++
title = "196 GR Vishwanath"
date = "2017-10-11"
upstream_url = "https://lists.advaita-vedanta.org/archives/advaita-l/2017-October/047204.html"

+++
[Archive link](https://lists.advaita-vedanta.org/archives/advaita-l/2017-October/047204.html)

package util

import org.apache.spark.SparkConf
import org.apache.spark.sql.SparkSession

import dataxu.etl.config.ETLProperties
import dataxu.etl.spark.{SparkETL, SparkModule, SparkSessionProvider}
import dataxu.etl.spark.workflow.CICRefreshETLWorkflow

/**
  * Test utility for running an impressions ETL workflow locally.
Modify the input vals in order
  * to tweak input to the runner (e.g. impressionsInputManifestPath,
swapOutputPath, etc.)
  */
object LocalCICRefreshETLWorkflowRunner {

  def main(args: Array[String]): Unit = {
    System.setProperty("spark.dataxu.environment", "test")

    val basePath =
s"file://${System.getProperty("user.home")}/test/rwh-etl/data/"
    val CICRefreshETLOutputPath = s"${basePath}out/cicrefresh"

    val session = buildSparkSession2()


    import dataxu.etl.spark.SparkModule.sparkSessionProvider.sparkSession
    //sparkSession.sql("select object_uid, brand_safety_level,
brand_safety_level_description,'CAMP' from dx_campaign limit 10
").collect().foreach(println)

    //sparkSession.sql("select campaign_cost_model,count(*)  from
dx_campaign group by 1 order by 2 desc limit 20
").collect().foreach(println)
   // sparkSession.sql("select * from rpt_flight_dimensions limit 20
").collect().foreach(println)

    sparkSession.sql("select * from
dx_flight_content_channel").collect().foreach(println)

    sparkSession.sql("select * from FAIL").collect().foreach(println)



    new CICRefreshETLWorkflow(
      new SparkETL(new SparkModule {
        override lazy val sparkSessionProvider: SparkSessionProvider =
new SparkSessionProvider {
          override def sparkSession: SparkSession = session
        }
      }),
      CICRefreshETLOutputPath = CICRefreshETLOutputPath,
      queryLimit = Some(20000),
      numParallelProcesses = 1,
      addResultsToMetastore = true,
      properties = ETLProperties())
      .runETLWorkflow()
  }


  private def buildSparkSession2(): SparkSession = {
    val conf = new SparkConf(true)
    conf.setMaster("local[4]")
    conf.setAppName("Local Impressions ETL")

    conf.set("spark.ui.enabled", "false")
    conf.set(
      "spark.hadoop.mapreduce.fileoutputcommitter.algorithm.version",
      "2")
    conf.set("spark.sql.catalogImplementation", "hive")
    conf.set(  "spark.hadoop.javax.jdo.option.ConnectionURL",
      "jdbc:mariadb://warehouse-etl-metastore-t-rdshivemetastorecluster-1d18t23yjdjch."
+
        "cluster-cvyprmjkfqcg.us-east-1.rds.amazonaws.com"
        + ":3306/hive")
    conf.set("spark.hadoop.javax.jdo.option.ConnectionDriverName",
"org.mariadb.jdbc.Driver")

    conf.set("spark.hadoop.javax.jdo.option.ConnectionUserName", "hive")
    conf.set("spark.hadoop.javax.jdo.option.ConnectionPassword",
"thaes(oo3pheiRio,nei")

    conf.set("fs.s3a.impl", "org.apache.hadoop.fs.s3a.S3AFileSystem")
    conf.set("fs.s3.impl", "org.apache.hadoop.fs.s3native.NativeS3FileSystem")

    conf.set("fs.s3.awsAccessKeyId", "AKIAI7OGCK3Y2QEOQ2CA")
    conf.set("fs.s3.awsSecretAccessKey",
"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")
    val sessionBuilder = SparkSession.builder()
    sessionBuilder.enableHiveSupport()
    sessionBuilder.config(conf).getOrCreate()
  }

  private def buildSparkSession(): SparkSession = {
    val conf = new SparkConf(true)
    conf.setMaster("local[4]")
    conf.setAppName("Local Impressions ETL")

    conf.set("spark.ui.enabled", "false")
    conf.set(
      "spark.hadoop.mapreduce.fileoutputcommitter.algorithm.version",
      "2")
    val sessionBuilder = SparkSession.builder()
    sessionBuilder.enableHiveSupport()
    sessionBuilder.config(conf).getOrCreate()
  }



}
