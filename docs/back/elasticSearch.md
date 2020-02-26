**关于restful**
=============

POST一般用来更新/查询/新增

GET  查询

PUT  一般用来创建

Delte 删除

****安装搭建****
============

安装好之后进入bin目录，然后sh elasticsearch.sh

访问9200端口如果可以就启动成功了。

****目录结构****
============
![](../_v_images/_1582712146_11324.png)
****术语****
==========
![](../_v_images/_1582712153_17529.png)
****创建index****
===============

PUT请求发送 localhost:9200/nbc---->创建nba索引

****创建mapping****
=================

****显示所有mapping****
-------------------
![](../_v_images/_1582712161_16384.png)
****获取mapping****
-----------------
![](../_v_images/_1582712167_801.png)
****新增mapping字段****
-------------------

![](../_v_images/_1582712175_20812.png)直接在原来的基础上新增就行了
![](../_v_images/_1582712180_13845.png)
****设置mapping****
-----------------
![](../_v_images/_1582712186_6156.png)
![](../_v_images/_1582712196_1696.png)
****创建文档Doucument****
=====================
![](../_v_images/_1582712203_27946.png)
****查看文档****
------------

### ****根据下标****
![](../_v_images/_1582712212_5030.png)
### ****根据id****
![](../_v_images/_1582712219_32533.png)
### ****查看多个文档****

第一种
![](../_v_images/_1582712225_6287.png)
第二种
![](../_v_images/_1582712230_3966.png)
第三种
![](../_v_images/_1582712234_7303.png)
第四种
![](../_v_images/_1582712239_11294.png)
****创建doc---携带ID的（/1）****
-------------------------
![](../_v_images/_1582712247_29880.png)
### ****不带ID的--POST****
![](../_v_images/_1582712255_8826.png)
****创建文档****
------------
![](../_v_images/_1582712265_31089.png)
****新增doc下的字段****
-----------------
![](../_v_images/_1582712276_12037.png)
![](../_v_images/_1582712282_3408.png)
****删除doc字段****
---------------
![](../_v_images/_1582712291_10765.png)
****修改字段****
------------
![](../_v_images/_1582712295_20199.png)
****删除文档****
------------
![](../_v_images/_1582712301_18776.png)
****简单搜索****
============
![](../_v_images/_1582712308_20604.png)
****Term查询---精确查询（查不了text类型字段）****
----------------------------------
![](../_v_images/_1582712314_858.png)
****Match查询---匹配查询（前提是查询字段类型是text，也可以查别的字段不过就是精确查询了）****
--------------------------------------------------------
![](../_v_images/_1582712324_20177.png)
position包含’得分后位’任意一个字

![](../_v_images/_1582712335_18794.png)title和name里面包含shooter的

![](../_v_images/_1582712344_26388.png)match_phrase有点像精确查询（给出的字段必须连续出现）

![](../_v_images/_1582712351_14440.png)和mathch\_phrase基本一样，不过match\_phrase要求单词一定要完整，例如i like swimming and,用match\_phrase查一定要i like swimming，用match\_phrase_prefix只要 i like sw

****分词器****
===========

****最基础的standard-->空格和特殊字符隔开，且全小写****
-------------------------------------

****Simple--->把除了字母的作为分隔符隔开，也全小写,类型为word****
--------------------------------------------

****Whiteapace--->空格隔开****
--------------------------

****Stop****
------------
![](../_v_images/_1582712359_3431.png)
****数据类型****
============

****字符串，布尔，二进制，范围类型，日期****
--------------------------
![](../_v_images/_1582712367_7078.png)
****数组类型****
------------
![](../_v_images/_1582712374_20646.png)
****对象类型****
------------
![](../_v_images/_1582712379_15387.png)
****IP类型****
------------

****批量导入数据****
==============

****term的多种查询方式（针对非text类型）****
==============================

****精确查找****
------------
![](../_v_images/_1582712387_7504.png)
****字段非空查找****
--------------
![](../_v_images/_1582712393_1572.png)
****前缀查找（只要单词中是有Rock开头的  比如xxx Rock或者Rock xxx）****
--------------------------------------------------
![](../_v_images/_1582712400_190.png)
****通配符查找****
-------------
![](../_v_images/_1582712408_8803.png)
****正则表达式查找****
---------------
![](../_v_images/_1582712413_14091.png)
****ID查找****
------------
![](../_v_images/_1582712421_17018.png)
****范围查询（针对日期，数字，字符串非text）****
==============================
![](../_v_images/_1582712429_24932.png)
****布尔查询****
============
![](../_v_images/_1582712436_10419.png)
****Es排序****
============
![](../_v_images/_1582712443_28559.png)
****聚合函数****
============

格式都是

“aggs”:{

“name”:{

    “type”:{

         内容

      }

}

}

Type的种类有:max min sum avg
![](../_v_images/_1582712459_27093.png)
![](../_v_images/_1582712466_24295.png)
![](../_v_images/_1582712472_8885.png)
![](../_v_images/_1582712482_16942.png)
![](../_v_images/_1582712489_26440.png)
****桶聚合+范围分组聚合+时间分组****
=======================

Term:分组相当于group by

Range:范围分组聚合

Date_range:时间范围分组聚合

****Query_String****
====================
![](../_v_images/_1582712526_24793.png)
![](../_v_images/_1582712532_7996.png)
****别名_alias****
================

别名相当于给index取了一个别名，就可以用别名操作index
![](../_v_images/_1582712539_29119.png)
如果一个别名对应多个索引，可以为别名设置属性
![](../_v_images/_1582712546_25699.png)
****重建索引****
============
![](../_v_images/_1582712551_21595.png)
****Refresh操作和高亮查询****
======================

****Refresh****
---------------
![](../_v_images/_1582712559_22906.png)
****高亮****
----------
![](../_v_images/_1582712565_1276.png)
****建议器****
===========

****Missing输入的字段，索引中不存在时提示****
------------------------------

Text是输入，suggest_mode就是建议模式，field是指明输入是哪个字段，然后根据索引下这个字段所有的值进行匹配。
![](../_v_images/_1582712572_25608.png)
****Phrase****
--------------
![](../_v_images/_1582712579_11163.png)
****Completion完成建议--->就补全****
-----------------------------
![](../_v_images/_1582712585_19059.png)
****整合Springboot****
====================

D:\\elsearchdemo

****相关API****
-------------

### ****Add****

通过调用IndexRequest来进行数据的添加，表明id和source（Map类型）

通过RestHighLevelClient.index的方法进行数据的添加
![](../_v_images/_1582712607_25129.png)
### ****Get****

GetRequest（“索引的名字”,”获取id”）

通过RestHighLevelClient.get获得
![](../_v_images/_1582712612_32634.png)
### ****Update****

通过构造UpdateRequest，设置索引和id，然后放入新的资源

通过RestHighLevelClient.update进行更新
![](../_v_images/_1582712617_30362.png)
### ****Delete****
![](../_v_images/_1582712623_28337.png)
### ****DeleteAll****
![](../_v_images/_1582712631_19959.png)
### ****Search****

通过SearchRequest，构造一个SearchBuilder

通过RestHighLevelClient.search进行搜索

把response调用getHits2次得到数据，然后转成JSON字符串进行解析
![](../_v_images/_1582712641_31159.png)
****集群的搭建--->去集群文档看****
=======================

****集群的基本概念（客户端节点用来进行负载均衡）****
==============================
![](../_v_images/_1582712649_31027.png)
****集群工作原理****
==============

****写入****
----------
![](../_v_images/_1582712658_5177.png)
****读取（主分片副分片都可以读，会负载均衡）****
----------------------------
![](../_v_images/_1582712664_20903.png)
****集群路由原理（就是如何找到分片）****
========================

就是对主分片数取模
![](../_v_images/_1582712673_7432.png)
****Elastic的乐观锁****
===================

使用version作为控制变量，读的时候不上锁，但是去更新的时候可以带上版本号，如果带上的version比当前版本高则更新成功，否则说明有人更新了，就失败
![](../_v_images/_1582712678_25177.png)
****倒排索引****
============

就是记录每个单词的id，频率，第几个单词的一张表
![](../_v_images/_1582712686_17599.png)
![](../_v_images/_1582712692_19570.png)