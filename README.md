# Text-matching
【正式赛】2019中国高校计算机大赛——大数据挑战赛

[比赛链接](https://www.kesci.com/home/competition/5cc51043f71088002c5b8840/content/1)

正式赛题——文本点击率预估
----------------------
搜索中一个重要的任务是根据query和title预测query下doc点击率，本次大赛参赛队伍需要根据脱敏后的数据预测指定doc的点击率，
结果按照指定的评价指标使用在线评测数据进行评测和排名，得分最优者获胜。

比赛数据
---------
|列名|	类型 | 示例|
|-----|-----|-----|
|query_id|int| 3|
|query |hash string，term空格分割| 1 9 117|
|query_title_id|	title在query下的唯一标识	|2|
|title |hash string，term空格分割 |3 9 120|
|label| int，取值{0, 1}| 0|

选手提交结果
-----------
|列名	|类型| 示例|
|------|------|------|
|query_id |int |1|
|query_title_id	|title在query下的唯一标识|	4|
|prediction	|对应title点击率的预测值，范围∈(0,1)|	0.5|

评估标准
-----------
选手提交结果的评估指标是qAUC，qAUC为不同query下AUC的平均值，计算如下：

![](https://cdn.kesci.com/upload/images/ps2bm1iwq.png?imageView2/0/w/400/h/400)

其中AUCi为同一个query_id下的AUC（Area Under Curve）。

最终使用qAUC作为参赛选手得分，qAUC越大，排名越靠前。

scut问题不大
------------
1、提取tfidf文本特征，利用逻辑回归作为分类器。 2000万测试集55+

2、手工提取的文本特征、相似度特征和统计特征，使用lgb分类。

3、采用textcnn模型，使用query和title作为双端输入，在全连接层加入手工提取的文本特征、相似度特征和统计特征。 2000万测试集55+

4、对模型进行线性加权融合。2000万测试集56.8+ 1亿数据集57.6+

初赛成绩

![](https://github.com/zhangxiaoling/Text-matching/blob/master/%E5%88%9D%E8%B5%9B.png)

复赛成绩

![](https://github.com/zhangxiaoling/Text-matching/blob/master/%E5%A4%8D%E8%B5%9B.png)

ps: 刚刚入门比赛的萌新嘻嘻，欢迎各位大佬提出建议，相互学习交流。欢迎大佬带我打比赛。
