# 3.3 离线召回与排序介绍

## 学习目标

- 目标
  - 了解召回排序作用
  - 知道头条推荐召回排序设计
- 应用
  - 无

### 3.3.1 召回与排序介绍

召回：从海量文章数据中得到若干候选文章召回集合(数量较多)

排序：从召回集合中读取推荐文章，构建样本特征进行排序过滤筛选

#### 3.3.1.1 黑马召回与排序业务流程

![](../images/黑马头条推荐流程图.png)

![](../images/召回排序1.png)

### 3.3.2 黑马头条推荐的召回排序设计

* 匿名用户：
  * 通常使用用户冷启动方案，**区别在于user_id为匿名用户手机识别号(黑马头条不允许匿名用户)**

* 所有只正针对于登录用户：

* 用户冷启动（前期点击行为较少情况）
  * 非个性化推荐
    * **热门召回**：自定义热门规则，根据当前时间段热点定期更新维护人点文章库
    * **新文章召回**：为了提高新文章的曝光率，建立新文章库，进行推荐
  * 个性化推荐：
    * **基于内容的协同过滤在线召回**：基于用户实时兴趣画像相似的召回结果用于首页的个性化推荐
* 后期离线部分（用户点击行为较多，用户画像完善）
  *  建立用户长期兴趣画像（详细）：包括用户各个维度的兴趣特征
  *  训练排序模型
    *  **LR模型、FTRL、Wide&Deep**
  *  离线部分的召回：
     *  **基于模型协同过滤推荐离线召回**：ALS
     *  **基于内容的离线召回**：或者称基于用户画像的召回
