---
title: About ME
date: 2016-05-23 19:02:40
---


# 联系方式

- 手机：15121152553
- Email：ybleak@gmail.com 
- QQ/微信号：202388990
- 求职意向：数据研发

# 个人信息

 - 杨磊/男/1990 
 - 2015/09-2018/07 西南大学 信号与信息处理 硕士 （前 10%）
 - 2010/09-2014/07 南阳理工学院 通信工程 学士 （前 10%）
 - 工作年限：1年+
 - 技术博客：http://www.ailcy.com
 - Github：http://github.com/xixici
 - 目前职位：大数据开发工程师
 - 期望职位：算法、机器学习、数据开发、数据分析岗
 - 期望薪资：税前月薪20k~25k，特别喜欢的公司可例外
 - 期望城市：上海

# 工作经历

## 上海爱数信息技术股份有限公司 （ 2017年10月 ~至今）

### xx所大数据分析平台建设项目 
- 主要负责算法实现，模型输出，算法应用等模块的设计与实现
  - 算法实现：采用SparkMLlib和Deeplearning4J实现了包含RF, SVM，CNN, YOLO等算法
  - 模型输出：将模型输出到PMML文件，以便于其他平台使用
  - 算法应用：分为离线数据(CSV, ES)和实时数据(Kafka)，实时数据由Spark Streaming在线应用，并写入ElasticSearch
- 个人成绩：此项目，我担当了算法部分的核心开发者，使用Scala+Sbt构建，开发了server和spark两个容器作为算法后端服务和模型计算服务，实现了模型训练，模型导出，模型应用。 模型训练支持用户上传CSV和ES选取数据两种方式，模型导出部分支持导出PMML的XML格式，实时应用实现了随时开启关闭。

### 爬虫监控与管理系统
- 主要负责爬虫管理，监控，增加等
  - 爬虫管理与监控：该系统由scrapy爬虫框架和Airflow工作流监控平台组成，由Airflow来管理和组织现有爬虫任务
  - 爬虫增加：爬虫由scrapy爬虫框架实现，后期主要增加高校数据，医院数据，政府招投标等到mysql，mongodb，Hbase等数据库
- 个人成绩：此项目，我负责爬虫系统的监控、维护以及增加爬虫。项目过程中, 通过代理中间键解决了反爬问题，通过Airflow DAG解决了分布式和自动化问题，最终 爬取了20G的招投标数据(HBase), 8000+医院数据(MySql), 3000+高校数据(MySql)...

## 重庆长安汽车有限公司 （ 2016年9月 ~ 2017年6月 ）

### 长安汽车大数据分析平台项目 
- 主要负责CDH系统的搭建与维护，故障检测算法的实现
  - CDH系统：该系统包含Hadoop，Spark，Hbase，Hive，Sqoop2，Zookeeper等组件
  - 故障检测算法：对300+维的发动机运行数据进行分析，预测发动机故障来源，该算法主要由PCA实现，由得分贡献得出故障源
- 个人成绩：我在此项目中，前期搭建了4x32G的Spark集群，并开启了Hive，Sqoop, Hbase, Spark等服务，并在后期对接入的发动机数据由java+spark实现故障检测算法。

# 科研文章

- [Bifurcation Analysis of Delayed Complex-Valued Neural Network with Diffusions](https://link.springer.com/article/10.1007/s11063-018-9899-0). *Neural Processing Letters*, SCI, IF1.787
- [Hopf-Pitchfork Bifurcation Analysis of a Coupled Neural Oscillator System with Excitatory-to-Inhibitory Connection and Time Delay](https://link.springer.com/chapter/10.1007/978-3-319-92537-0_46). *International Symposium on Neural Networks ISNN 2018: Advances in Neural Networks*, EI

# 技能清单
以下均为我熟练使用的技能
- 机器学习工程库：Spark ML, Deeplearning4J
- 机器学习算法：LR, Bayes, SVM, RF, GBT, CNN, RNN, LSTM, K-Means, YOLO
- 系统工具：Shell, vim
- 编程语言：Scala = python > Java > C
- 数据库：MySQL, MongoDB, Hbase, Redis
- 版本管理、构建工具：Svn, Git, Maven, SBT
- 单元测试：Junit
- 数据处理：Spark, SparkSQL, SparkML, AKKA, Spark Streaming, Kafka, ELK
      
---      
# 致谢
感谢您花时间阅读我的简历，期待能有机会和您共事。~~~~
    
---
{% cq %}
# 想做的事情很多,没做的事情却更多.
{% endcq %}

---

