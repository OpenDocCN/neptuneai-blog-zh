# 了解 LightGBM 参数(以及如何调整它们)

> 原文：<https://web.archive.org/web/https://neptune.ai/blog/lightgbm-parameters-guide>

我已经用了 [lightGBM](https://web.archive.org/web/20230127191010/https://github.com/microsoft/LightGBM/tree/master/python-package) 一段时间了。这是我解决大多数表格数据问题的常用算法。[的令人敬畏的特性](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Features.html)的列表很长，我建议你如果还没有看的话看一看。

但是我一直很想了解哪些参数对性能影响最大，以及我应该如何调优 lightGBM 参数以充分利用它。

我想我应该做一些研究，了解更多关于 lightGBM 的参数…并分享我的旅程。

具体来说，我:

在此过程中，我获得了更多关于 lightGBM 参数的知识。我希望读完这篇文章后，你能够回答以下问题:

*   LightGBM 中实现了哪些梯度提升方法，有什么不同？
*   一般来说，哪些参数是重要的？
*   需要调整哪些正则化参数？
*   如何在 python 中调优 lightGBM 参数？

## 梯度推进方法

使用 LightGBM，您可以运行不同类型的梯度增强方法。您有:GBDT、达特和戈斯，它们可以用`boosting`参数来指定。

在接下来的部分中，我将解释和比较这些方法。

### **lgbm gbdt(梯度增强决策树)**

这种方法是传统的梯度推进决策树，在这篇 [**文章**](https://web.archive.org/web/20230127191010/https://statweb.stanford.edu/~jhf/ftp/trebst.pdf) 中首次提出，并且是 XGBoost 和 pGBRT 等一些伟大库背后的算法。

如今，gbdt 因其准确性、高效性和稳定性而被广泛使用。你可能知道 gbdt 是决策树的集合模型，但是它到底是什么意思呢？

让我给你一个要点。

它基于三个重要原则:

*   弱学习者(决策树)
*   梯度优化
*   助推技术

所以在 gbdt 方法中，我们有很多决策树(弱学习者)。这些树是按顺序建造的:

*   第一棵树学习如何适应目标变量
*   第二棵树学习如何拟合第一棵树的预测和地面真实值之间的残差(差异)
*   第三棵树学习如何拟合第二棵树的残差，以此类推。

所有这些树都是通过在整个系统中传播误差梯度来训练的。

gbdt 的主要缺点是在每个树节点中寻找[最佳分裂点](https://web.archive.org/web/20230127191010/https://papers.nips.cc/paper/6907-lightgbm-a-highly-efficient-gradient-boosting-decision-tree.pdf)是耗时且消耗内存的操作。其他 boosting 方法试图解决这个问题。

### **镖梯度增强**

在这篇出色的[论文](https://web.archive.org/web/20230127191010/https://arxiv.org/abs/1505.01866)中，您可以了解关于 DART 梯度提升的所有事情，DART 梯度提升是一种使用神经网络中的标准下降来改善模型正则化并处理其他一些不太明显的问题的方法。

也就是说，gbdt 遭受过度特殊化，这意味着在后面的迭代中添加的树往往只影响少数实例的预测，而对其余实例的贡献可以忽略不计。添加 dropout 会使树在以后的迭代中更难专注于这几个样本，从而提高性能。

### **lgbm goss(基于梯度的单侧采样)**

事实上，将这种方法命名为 lightgbm 的最重要原因是使用了基于这篇[论文](https://web.archive.org/web/20230127191010/https://papers.nips.cc/paper/6907-lightgbm-a-highly-efficient-gradient-boosting-decision-tree.pdf)的[Goss](https://web.archive.org/web/20230127191010/https://papers.nips.cc/paper/6907-lightgbm-a-highly-efficient-gradient-boosting-decision-tree.pdf)方法。Goss 是更新更轻的 gbdt 实现(因此是“轻”gbm)。

标准的 gbdt 是可靠的，但是在大型数据集上不够快。因此，goss 提出了一种基于梯度的采样方法，以避免搜索整个搜索空间。我们知道，对于每个数据实例，当梯度较小时，这意味着不用担心数据训练良好，当梯度较大时，应该再次重新训练。所以我们这里有**两边**，有大梯度和小梯度的数据实例。因此，goss 保留所有具有大梯度的数据，并对具有小梯度的数据进行随机采样(**，这就是为什么它被称为单侧采样**)。这使得搜索空间更小，goss 可以更快地收敛。最后，为了获得更多关于戈斯的信息，你可以看看这篇[的博文](https://web.archive.org/web/20230127191010/https://towardsdatascience.com/what-makes-lightgbm-lightning-fast-a27cf0d9785e)。

让我们将这些差异放在一个表格中:

| 方法 | 注意 | 需要改变这些参数 | 优势 | 不足之处 |
| --- | --- | --- | --- | --- |
|  | 

是

的默认增压类型 | 

因为 gbdt 是 lgbm 的默认参数，所以您不必为它更改其余参数的值(仍然必须进行调整！)

 |  | 

过度特殊化，耗时耗力

 |
|  | 

试图解决 gbdt

中的过度专业化问题 | 

drop_seed:用于选择丢弃模式的随机种子 sUniform_dro:如果要使用统一丢弃 xgboost_dart_mode:如果要使用 xgboost dart 模式，请将其设置为 true skip _ drop:在提升迭代期间跳过丢弃过程的概率 max_dropdrop_rate:丢弃率:在丢弃过程中要丢弃的先前树的分数

 |  |  |
|  | 

戈斯通过分离那些梯度较大的实例为 GBDT 提供了一种新的采样方法

 | 

top_rate:大梯度数据保留率 other_rate:小梯度数据保留率

 |  | 

数据集小时过拟合

 |

![](img/e26f9310772a1cfa52ddfe91020e2852.png)

如果你设置提升为 RF，那么 lightgbm 算法表现为随机森林，而不是提升的树！根据文档，要使用 RF，必须使用小于 1 的 bagging_fraction 和 feature_fraction。

## 正规化

在这一节中，我将介绍 lightgbm 的一些重要的正则化参数。显然，这些是您需要调整以防止过度拟合的参数。

您应该知道，对于小数据集(< 10000 条记录)，lightGBM 可能不是最佳选择。调优 lightgbm 参数可能对您没有帮助。

此外，lightgbm 使用[逐叶](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Features.html#leaf-wise-best-first-tree-growth)树生长算法，而 eXGBoost 使用深度树生长算法。逐叶方法允许树更快地收敛，但是过度拟合的机会增加了。

也许这个来自 PyData 会议的[演讲给了你更多关于 Xgboost 和 Lightgbm 的见解。值得一看！](https://web.archive.org/web/20230127191010/https://youtu.be/5CWwwtEM2TA)

[https://web.archive.org/web/20230127191010if_/https://www.youtube.com/embed/5CWwwtEM2TA?feature=oembed](https://web.archive.org/web/20230127191010if_/https://www.youtube.com/embed/5CWwwtEM2TA?feature=oembed)

视频

![](img/e26f9310772a1cfa52ddfe91020e2852.png)

如果有人问你 LightGBM 和 XGBoost 的主要区别是什么？你可以很容易地说，它们的区别在于它们是如何实现的。

根据 [lightGBM 文档](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Parameters-Tuning.html#deal-with-over-fitting)，当面临过拟合时，您可能希望进行以下参数调整:

*   使用小 max_bin
*   使用小数量的叶子
*   使用叶中最小数据和叶中最小和
*   通过设置 bagging_fraction 和 bagging_freq 来使用 bagging
*   通过设置 feature_fraction 使用特征子采样
*   使用更大的训练数据
*   尝试 lambda_l1、lambda_l2 和 min_gain_to_split 进行正则化
*   尝试 max_depth 以避免树越长越深

在接下来的几节中，我将更详细地解释这些参数。

### **λ_ L1**

Lambda_l1(和 lambda_l2)控制到 l1/l2，并与 min_gain_to_split 一起用于对抗**过拟合**。我强烈建议您使用参数调整(在后面的小节中探讨)来找出这些参数的最佳值。

### **叶子数量**

当然 **num_leaves** 是控制模型的**复杂度**的最重要参数之一。使用它，您可以设置每个弱学习者拥有的最大叶片数。较大的 num_leaves 增加了训练集的准确性，也增加了因过度训练而受伤的机会。根据文档，一个简单的方法是 **num_leaves = 2^(max_depth)** 然而，考虑到在 lightgbm 中，逐叶树比逐层树更深，你需要小心过度拟合！**因此，有必要将** **num_leaves** **与** **max_depth** **一起调。**

### **子样本**

使用[子样本](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Parameters.html#learning-control-parameters)(或 bagging_fraction)，您可以指定每个树构建迭代中使用的行的百分比。这意味着将随机选择一些行来适应每个学习者(树)。这不仅提高了泛化能力，还提高了训练速度。

我建议对基线模型使用较小的子样本值，然后在完成其他实验时增加这个值(不同的特征选择，不同的树结构)。

### **特征 _ 分数**

[Feature fraction](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Parameters.html#learning-control-parameters) 或 sub_feature 处理列采样，LightGBM 将在每次迭代(树)中随机选择一个特征子集。例如，如果将其设置为 0.6，LightGBM 将在训练每棵树之前选择 60%的特征。

该功能有两种用法:

*   可以用来加速训练
*   可以用来处理过度拟合

### **最大深度**

该参数控制每个训练树的最大深度，并将影响:

*   num_leaves 参数的最佳值
*   模型性能
*   训练时间

请注意，如果您使用较大的值 **max_depth** ，您的模型将很可能**过度适合**列车组。

### **max_bin**

宁滨是一种在离散视图(直方图)中表示数据的技术。Lightgbm 使用基于直方图的算法来寻找最佳分割点，同时创建弱学习器。因此，每个连续的数字特征(例如，视频的观看次数)应该被分成离散的箱。

还有，在这个 [GitHub r](https://web.archive.org/web/20230127191010/https://github.com/szilard/GBM-perf) epo 里，你可以找到一些全面的实验，完整的解释了改变 max_bin 对 CPU 和 GPU 的影响。

如果将 max_bin 定义为 255，这意味着每个特性最多可以有 255 个唯一值。那么小的 max_bin 导致更快的速度，大的值提高精度。

## 训练参数

训练时间！当您希望使用 lightgbm 训练模型时，训练 lightgbm 模型时可能出现的一些典型问题是:

*   培训是一个耗时的过程
*   处理计算复杂性(CPU/GPU RAM 限制)
*   处理分类特征
*   拥有不平衡的数据集
*   对定制指标的需求
*   分类或回归问题需要进行的调整

在本节中，我们将尝试详细解释这些要点。

### **迭代次数**

Num_iterations 指定提升迭代的次数(要构建的树)。构建的树越多，模型就越精确，代价是:

*   更长的训练时间
*   过度拟合的可能性更高

从较低数量的树开始构建基线，稍后当您想要从模型中挤出最后的%时，增加基线。

建议使用较小的**学习速率**和较大的**次数迭代**。此外，如果你的训练没有学到任何有用的东西，你应该使用 early_stopping_rounds 来停止你的训练。

### **提前 _ 停止 _ 回合**

如果验证指标在最后一轮提前停止后没有改善，该参数将停止**训练**。这应该与迭代次数的**成对定义。如果你设置的太大，你会增加**过度拟合**的机会(但是你的模型可以更好)。**

经验法则是在 num_iterations 的 10%时使用它。

### **light GBM category _ feature**

使用 lightgbm 的一个优点是它可以很好地处理分类特征。是的，这个算法非常强大，但是你必须小心使用它的参数。lightgbm 使用一种特殊的[](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Features.html#optimal-split-for-categorical-features)**整数编码方法(由 [**费希尔**](https://web.archive.org/web/20230127191010/http://www.csiss.org/SPACE/workshops/2004/SAC/files/fisher.pdf) 提出)来处理分类特征**

 **实验表明，该方法比常用的**一键编码**具有更好的性能。

它的缺省值是“auto ”,这意味着:让 lightgbm 决定哪个意味着 lightgbm 将推断哪些特征是分类的。

它并不总是工作得很好(一些实验显示了为什么这里的[和这里的](https://web.archive.org/web/20230127191010/https://www.kaggle.com/mlisovyi/beware-of-categorical-features-in-lgbm)和[和](https://web.archive.org/web/20230127191010/https://www.kaggle.com/c/home-credit-default-risk/discussion/58950))我强烈建议你简单地用这段代码手动设置[分类特征](https://web.archive.org/web/20230127191010/https://www.kaggle.com/mlisovyi/beware-of-categorical-features-in-lgbm#339301)

**cat _ col = dataset _ name . select _ dtypes(' object '). columns . to list()**

但是幕后发生了什么，lightgbm 如何处理分类特性？

根据 lightgbm 的 [**文档**](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/Features.html#optimal-split-for-categorical-features) ，我们知道树学习者不能很好地使用一种热编码方法，因为他们通过树深入生长。在所提出的替代方法中，树学习器被最佳地构造。例如，对于具有 k 个不同类别的一个特征，存在 2^(k-1)-1 个可能的分区，并且使用 [fisher](https://web.archive.org/web/20230127191010/http://www.csiss.org/SPACE/workshops/2004/SAC/files/fisher.pdf) 方法，该方法可以通过在分类特征中的值的排序直方图上找到最佳分割方式来改进为 **k * log(k)** 。

### **light GBM is _ unbalance vs scale _ pos _ weight**

在**二元分类问题**中你可能面临的一个问题就是如何处理**不平衡**数据集。显然，您需要平衡正/负样本，但是在 lightgbm 中您如何做到这一点呢？

lightgbm 中有两个参数可以让你处理这个问题 **is_unbalance 和 scale_pos_weight** ，但是它们之间有什么区别，如何使用？

*   当您设置 Is _ un lace:True 时，算法将尝试自动平衡受支配标签的权重(使用训练集中的正/负分数)
*   如果您想要在不平衡数据集的情况下更改 **scale_pos_weight** (默认为 1，这意味着假设正负标签相等)，您可以使用以下公式(基于 lightgbm 存储库上的这个[问题](https://web.archive.org/web/20230127191010/https://github.com/microsoft/LightGBM/issues/1299))来正确设置它

**样本位置权重=阴性样本数/阳性样本数**

### **lgbm feval**

有时你想要定义一个定制的评估函数来测量你的模型的性能，你需要创建一个`feval`函数。

**Feval 函数**应该接受两个参数:

并返回

*   评估名称
*   评估结果
*   越高越好吗

让我们一步一步地创建一个定制的度量函数。

定义一个单独的 python 函数

使用此函数作为参数:

```py
def feval_func(preds, train_data):

    return ('feval_func_name', eval_result, False)
```

要使用 feval 函数而不是公制，您应该设置公制参数“无”。

```py
print('Start training...')
lgb_train = lgb.train(...,
                      metric=None,
                      feval=feval_func)
```

![](img/e26f9310772a1cfa52ddfe91020e2852.png)

**分类参数与回归参数**

### 我之前提到的大多数事情对于分类和回归都是正确的，但是有些事情需要调整。

具体来说，您应该:

参数的名称

| 分类说明 | 回归注释 |  |
| --- | --- | --- |
| 

设置为二进制或多类

 | 将其设置为二进制或多类 |  |
| 

Binary_logloss 或 AUC 等。

 | Binary_logloss 或 AUC 或 etc。 | RMSE 或平均绝对误差和或等。 |
|  |  |  |
| 

仅用于二进制和多类应用

 | 仅用于二进制和多类应用 |  |
| 

仅在多类分类应用中使用

 | 仅用于多类分类应用 |  |
|  | 

用于拟合 sqrt(标签)代替原始值用于大范围标签

 | 用于拟合 sqrt(标签),而不是大范围标签的原始值 |

## 在前面的章节中，我们已经回顾并了解了一些关于 lightgbm 参数的知识，但是如果不提到 Laurae 的令人难以置信的基准测试，任何一篇关于 boosted trees 的文章都是不完整的🙂

您可以了解 lightGBM 和 XGBoost 的许多问题的最佳缺省参数。

你可以[点击这里](https://web.archive.org/web/20230127191010/https://sites.google.com/view/lauraepp/parameters)查看，但最重要的几点是:

参数名称

| 默认值 | 范围 | 参数类型 | 别名 | 约束或注释 | 用于 |  |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  | 

当你改变它时会影响其他参数

 | 当你改变它时会影响其他参数 | 指定 ML 模型的类型 |
|  |  |  |  | 

空表示将使用指定目标对应的度量

 | 空表示将使用与指定目标相对应的指标 | 指定指标，支持多个指标 |
|  |  |  |  | 

如果设置为 RF，那将是一个装袋方式

 | 如果设置为 RF，这将是一种打包方法 |  |
|  |  |  |  |  |  |  |
|  |  |  |  | 

0.0 <套袋 _ 分数<= 1.0

 | 0.0 <套袋 _ 分数< = 1.0 | 随机选择部分数据，无需重采样 |
|  |  |  |  | 

要启用 bagging，bagging_fraction 也要设置成小于 1.0 的值

 | 为了启用 bagging，bagging_fraction 也应设置为小于 1.0 的值 | 0 表示禁用装袋；k 表示每 k 次迭代进行打包 |
|  |  |  |  |  | 

一棵树的最大叶子数

 | 一棵树的最大叶子数 |
|  |  |  |  | 

0.0 <特征 _ 分数<= 1.0

 | 0.0 <特征 _ 分数< = 1.0 | 如果设置为 0.8，LightGBM 将选择 80%的功能 |
|  |  |  |  | 

通常越大越好，但是过拟合速度会增加

 | 通常越大越好，但是过度拟合速度会增加 | 限制树模型的最大深度 |
|  |  |  |  |  |  |  |
|  |  |  |  |  | 

助推迭代次数

 | 升压迭代次数 |
|  |  |  |  | 

学习率>0.0 典型值:0.05

 | 学习率>0.0 典型值:0.05 | 在 dart 中，它也影响掉落树木的归一化权重 |
|  |  |  |  | 

如果最后一次验证没有改善，将停止训练 _ 停止

_ 回合

 | 如果验证在最近一次提前停止中没有改善，将停止培训 | 模型性能、迭代次数、训练时间 |
|  | 

指定某一列的编号指标

 | 为列索引指定一个数字 |  |  | 

处理分类特征

 | 处理分类特征 |
|  |  |  |  | 

0 表示禁用装袋；k 表示每 k 次迭代进行打包

 | 0 表示禁用装袋；k 表示每 k 次迭代进行打包 | 为了启用 bagging，bagging_fraction 也应设置为小于 1.0 的值 |
|  |  |  |  | 

< 0:致命，= 0:错误(警告)，= 1:信息，> 1:调试

 | < 0:致命，= 0:错误(警告)，= 1:信息，> 1:调试 |  |
|  |  |  |  |  | 

可以用来处理过拟合

 | 可用于处理过拟合 |

你不应该认为任何参数值是理所当然的，并根据你的问题来调整它。也就是说，这些参数是您的超参数调整算法的一个很好的起点

![](img/e26f9310772a1cfa52ddfe91020e2852.png)

python 中的 Lightgbm 参数调优示例(lightgbm 调优)

## 最后，在解释完所有重要参数之后，是时候进行一些实验了！

我就用一个流行的 Kaggle 比赛:[桑坦德客户交易预测](https://web.archive.org/web/20230127191010/https://www.kaggle.com/c/santander-customer-transaction-prediction/data)。

我将使用这篇文章解释如何在任何脚本上运行 Python 中的超参数调优。

值得一读！

在我们开始之前，一个重要的问题！我们应该调整哪些参数？

注意您想要解决的问题，例如，Santander 数据集**高度不平衡**，在您的调优中应该考虑到这一点！ [Laurae2](https://web.archive.org/web/20230127191010/https://github.com/Laurae2) ，lightgbm 的贡献者之一[在这里](https://web.archive.org/web/20230127191010/https://github.com/microsoft/LightGBM/issues/695#issuecomment-315591634)很好的解释了这一点。

*   有些参数是相互依赖的，必须一起调整或逐个调整。例如，min_data_in_leaf 取决于训练样本的数量和 num _ leaf。
*   注意:最好为超参数创建两个字典，一个包含您不想优化的参数和值，另一个包含您想要优化的参数和值范围。

通过这样做，您可以将基线值从搜索空间中分离出来！

```py
SEARCH_PARAMS = {'learning_rate': 0.4,
                 'max_depth': 15,
                 'num_leaves': 20,
                 'feature_fraction': 0.8,
                 'subsample': 0.2}

FIXED_PARAMS={'objective': 'binary',
              'metric': 'auc',
              'is_unbalance':True,
              'boosting':'gbdt',
              'num_boost_round':300,
              'early_stopping_rounds':30}
```

现在，我们要做的是。

首先，我们在 [**笔记本**](https://web.archive.org/web/20230127191010/https://app.neptune.ai/mjbahmani/LightGBM-hyperparameters/notebooks?notebookId=Some-experiments-based-on-lightgbm-1-dc193057-c63d-41a3-9144-eb1759e5b8f9) 中生成代码。它是公开的，你可以**下载。**

1.  第二，我们在 [**neptune.ai**](/web/20230127191010/https://neptune.ai/) 中跟踪每个实验的结果。你可以[在应用](https://web.archive.org/web/20230127191010/https://app.neptune.ai/mjbahmani/LightGBM-hyperparameters/experiments?split=tbl&dash=charts&viewId=standard-view)中看到这个例子，因为它是我作为公共项目创建的。

2.  查看文档，了解更多关于使用 [Neptune-LightGBM 集成](https://web.archive.org/web/20230127191010/https://docs.neptune.ai/integrations/lightgbm/)跟踪模型构建元数据的信息。

**结果分析**

### 如果您已经检查了前面的部分，您会注意到我已经在数据集上做了超过 14 个不同的实验。在这里，我解释如何一步一步地调整超参数的值。

*注:最新的代码示例请参考 [Neptune-LightGBM 集成文档](https://web.archive.org/web/20230127191010/https://docs.neptune.ai/integrations/lightgbm/)。*

创建基准培训代码:

```py
from sklearn.metrics import roc_auc_score, roc_curve
from sklearn.model_selection import train_test_split
import neptunecontrib.monitoring.skopt as sk_utils
import lightgbm as lgb
import pandas as pd
import neptune
import skopt
import sys
import os

SEARCH_PARAMS = {'learning_rate': 0.4,
                'max_depth': 15,
                'num_leaves': 32,
                'feature_fraction': 0.8,
                'subsample': 0.2}

FIXED_PARAMS={'objective': 'binary',
             'metric': 'auc',
             'is_unbalance':True,
             'bagging_freq':5,
             'boosting':'dart',
             'num_boost_round':300,
             'early_stopping_rounds':30}

def train_evaluate(search_params):
   # you can download the dataset from this link(https://www.kaggle.com/c/santander-customer-transaction-prediction/data)
   # import Dataset to play with it
   data= pd.read_csv("sample_train.csv")
   X = data.drop(['ID_code', 'target'], axis=1)
   y = data['target']
   X_train, X_valid, y_train, y_valid = train_test_split(X, y, test_size=0.2, random_state=1234)
   train_data = lgb.Dataset(X_train, label=y_train)
   valid_data = lgb.Dataset(X_valid, label=y_valid, reference=train_data)

   params = {'metric':FIXED_PARAMS['metric'],
             'objective':FIXED_PARAMS['objective'],
             **search_params}

   model = lgb.train(params, train_data,
                     valid_sets=[valid_data],
                     num_boost_round=FIXED_PARAMS['num_boost_round'],
                     early_stopping_rounds=FIXED_PARAMS['early_stopping_rounds'],
                     valid_names=['valid'])
   score = model.best_score['valid']['auc']
   return score
```

使用您选择的超参数优化库(例如 scikit-optimize):

```py
neptune.init('mjbahmani/LightGBM-hyperparameters')
neptune.create_experiment('lgb-tuning_final', upload_source_files=['*.*'],
                              tags=['lgb-tuning', 'dart'],params=SEARCH_PARAMS)

SPACE = [
   skopt.space.Real(0.01, 0.5, name='learning_rate', prior='log-uniform'),
   skopt.space.Integer(1, 30, name='max_depth'),
   skopt.space.Integer(10, 200, name='num_leaves'),
   skopt.space.Real(0.1, 1.0, name='feature_fraction', prior='uniform'),
   skopt.space.Real(0.1, 1.0, name='subsample', prior='uniform')
]
@skopt.utils.use_named_args(SPACE)
def objective(**params):
   return -1.0 * train_evaluate(params)

monitor = sk_utils.NeptuneMonitor()
results = skopt.forest_minimize(objective, SPACE,
                                n_calls=100, n_random_starts=10,
                                callback=[monitor])
sk_utils.log_results(results)

neptune.stop()
```

尝试不同类型的配置，并在 Neptune 应用程序中跟踪您的结果。

最后，在下表中，您可以看到参数发生了什么变化。

超参数

| 调谐前 | 调谐后 |  |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  | 最后的想法 |

## 长话短说，你学到了:

什么是主要的 lightgbm 参数

*   如何使用 feval 函数创建定制指标
*   主要参数有哪些好的默认值
*   查看了如何调整 lightgbm 参数以提高模型性能的示例
*   和其他一些东西🙂更多详细信息，请参考参考资料。

资源

### [Laurae 广泛的指南，具有良好的默认设置等](https://web.archive.org/web/20230127191010/https://sites.google.com/view/lauraepp/parameters)

1.  [https://github . com/Microsoft/light GBM/tree/master/python-package](https://web.archive.org/web/20230127191010/https://github.com/microsoft/LightGBM/tree/master/python-package)
2.  [https://lightgbm.readthedocs.io/en/latest/index.html](https://web.archive.org/web/20230127191010/https://lightgbm.readthedocs.io/en/latest/index.html)
3.  [https://papers . nips . cc/paper/6907-light GBM-a-high-efficient-gradient-boosting-decision-tree . pdf](https://web.archive.org/web/20230127191010/https://papers.nips.cc/paper/6907-lightgbm-a-highly-efficient-gradient-boosting-decision-tree.pdf)
4.  [https://statweb.stanford.edu/~jhf/ftp/trebst.pdf](https://web.archive.org/web/20230127191010/https://statweb.stanford.edu/~jhf/ftp/trebst.pdf)
5.  [https://statweb.stanford.edu/~jhf/ftp/trebst.pdf](https://web.archive.org/web/20230127191010/https://statweb.stanford.edu/~jhf/ftp/trebst.pdf)**