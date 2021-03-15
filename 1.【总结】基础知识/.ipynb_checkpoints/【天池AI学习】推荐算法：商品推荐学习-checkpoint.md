#### 一、学习路线

#### 二、推荐系统基本概念及架构说明
##### （一）什么是推荐系统  
***（1）常见的推荐业务场景***
* 基于搜索Query的推荐
* 基于用户和商品属性的Feed流的推荐 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709111801739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)

***（2）个性化推荐业务流程***
* 【用户】用户进入app/网站
* 【用户行为】用户选择item（商品）
* 【粗筛】召回模块进行处理：找出用户可能喜欢的item（商品）
* 【细排】排序模块进行排序：根据用户喜爱的程度对item（商品）进行排序
* 【推送】推送推荐物品：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709112138754.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
##### （二）什么是推荐系统

> 推荐系统 = 推荐算法 + 系统工程
###### （1）推荐算法
* 学术研究
* 深入研究
###### （2）系统工程：企业级推荐系统要求
* 【目标】百万级MAU应用的推荐业务：  
1. 亿级别样本训练
2. 算法插件化部署
3. 毫秒级反馈
4. 支持资源弹性拓展  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070911304443.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_2,color_FFFFFF,t_70)

* 【架构】推荐整体架构  
5.  推荐业务：
6.  训练（离线）+ 推理（在线）：
7. 数据存储加工（离线）：
8. 底层基础数据：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709113224486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 基于PAI的推荐技术架构
1. 推荐服务（在线）
2. 训练（在线）
3. 数据加工服务（离线）
4. 数据加工存储（离线）
5. 底层基础数据
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709124520952.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
#### 三、推荐系统召回算法级架构说明
 

> 召回算法的作用是从海量待推荐对象中抽选出待排序的候选集

***推荐召回算法：流行算法介绍***
##### （一）向量召回相关算法（偏向于机器学习）

 - [ ] 产出user_embedding
 - [ ] 产出item_embedding  

* GraphSage：图神经网络召回算法
* ALS：矩阵分解经典算法
* FM-Embedding：内积加强特征表现
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709133327528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 召回流程说明

> 通过算法Graph召回、矩阵分解召回、FM召回生成向量表：用户向量表、物料向量表
> 向量表均为KV形式，即为Key-Value形式
> 通过用户向量在Fasis服务器中的物料向量表中检索，获取检索结果
> 检索结果如图所示

* 向量召回架构算法ALS举例：以PAI为例
1. 算法输入：用户id，行为(用户评分)，歌曲id
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709134651722.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 算法输出：user向量、item向量
2. user向量
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709134043174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
3. item向量  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709134939459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 向量召回架构算法Graph举例：以PAI为例
4. 算法输入一（行为表）：用户id，商品id，行为
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709135945730.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
5. 算法输入二（用户特征）： ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709141940167.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
6. 算法输入三（商品特征）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709142002459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 算法输出：user向量、item向量
7. user向量
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709134939459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
9. item向量  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709142531415.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
##### （二）协同过滤算法（统计）

 - [ ] 找到user和item的联系
* 协同过滤：认定为一种统计方式
* 基于物品的协同过滤算法
* 基于用户的协同过滤算法
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709132100810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 协同过滤算法举例：以PAI为例
1. 算法输入：商品id、用户id、用户行为
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709133950231.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
* 算法输出：商品id、购买可能性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709134043174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
#### 四、推荐系统排序算法级架构说明
##### （一）排序模块的作用

> 【前提】：已知用户感兴趣的商品集合
   【作用】：获取最受用户喜爱的topN物品

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709144447534.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
##### （二）排序算法
***排序算法：流行算法介绍***

> 排序算法的作用是针对推荐的候选集进行用户兴趣从强到弱的排序，通常使用机器学习领域的二分类算法解决该问题

* LR：经典的现行二分类算法
* GBDT+LR：行业应用最为广泛
* FM：通过内积增强表现力
* DeepFM：深度学习+FM
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709145039988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)

###### （三）排序模型-离线排序模型训练架构
* 样本生成流程
* PAI完成离线训练过程
* 样本基于用户行为事件构建，根据事件类型地板及，评论，分享，加入用户及物料特征join生成大宽表，作为训练及测试数据（过去N天训练，过去M天测试）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709161810734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)
###### （四）排序模型-在线排序模型训练架构：充分利用时效性数据
* 基于Flink框架时下流式模型训练能力
* 基于事实生成的模型去实时评估模型效果
* 具备线上模型回滚和版本管控

***在线模型是在离线模型的基础上构建的***
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070916343833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1BldGVyVmVn,size_16,color_FFFFFF,t_70)

#### 五、推荐系统线上服务编排（阿里云应用）
#### 六、简单的推荐系统实现：基于阿里云（阿里与应用）
