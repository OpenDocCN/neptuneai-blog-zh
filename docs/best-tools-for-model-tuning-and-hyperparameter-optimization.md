# 模型调整和超参数优化的最佳工具

> 原文：<https://web.archive.org/web/https://neptune.ai/blog/best-tools-for-model-tuning-and-hyperparameter-optimization>

我清楚地记得两年前我参加的一次机器学习黑客马拉松，当时我正处于数据科学职业生涯的初期。这是尼日利亚数据科学组织的训练营的资格预审黑客马拉松。

该数据集包含某些雇员的信息。我必须预测一个员工是否应该得到晋升。经过几天努力改进和设计功能，该模型的准确性似乎在 80%左右波动。

我需要做些什么来提高我在排行榜上的分数。我开始手动调整模型——得到了更好的结果。通过改变一个参数，准确率提高到了 82%(这一步非常重要，任何参加过黑客马拉松的人都可以证明！).兴奋之余，我开始调整其他超参数，但结果并不都很好。我已经精疲力尽了，想象一下连续工作 7 个小时来改进一个模型。挺累的。

我知道 GridSearchCV T1 和 T2 randomsearccv T3。我试用了 GridSearchCV，花了 3 个多小时才从我提供的一系列值中得出结果。更糟糕的是，来自 GridSearchCV 的结果并没有更好。沮丧之余，我决定试试 RandomSearchCV。这带来了一点喜悦，我的准确率从 82%上升到了 86%。

经过大量的试验，没有改善，我回到手动调谐，看看我能得到什么。在黑客马拉松结束时，我达到了 90%的准确率。我希望我已经知道了更快优化超参数的工具！幸运的是，尽管我没有进入前 50 名，我仍然有资格参加训练营。

那是过去的事了。现在，我知道有很好的超参数调优工具我可以使用，我很高兴与您分享它们。

在开始超调之前，请确保完成以下工作:

*   **获得基线**。您可以通过较小的模型、较少的迭代、默认参数或手动调整的模型来实现这一点。
*   **将您的数据**分成训练集、验证集和测试集。
*   使用**提前停止周期**来防止过度拟合。
*   在培训前设置好您的**完整模型管道**。

现在，我想讨论一下我将在文章中使用的一些术语:

*   **模型参数**–模型参数是您的模型从数据中学习的参数，如特征、关系等。，不能手动调整(不是特征工程)。
*   **模型超参数**–超参数是您可以从模型本身手动调整的值，如学习率、估计器数量、正则化类型等..
*   **优化**–通过使用**优化**技术之一，调整超参数以最小化成本函数的过程。
*   **超参数优化**–超参数优化只是一个搜索，以获得最佳超参数集，从而在特定数据集上给出模型的最佳版本。
*   [**贝叶斯优化**](https://web.archive.org/web/20220928202019/https://github.com/fmfn/BayesianOptimization)–一类基于模型的顺序优化(SMBO)算法的一部分，用于使用之前实验的结果来改进下一次实验。
*   **超参数采样**–简单指定在超参数空间使用的参数采样方法。

我不反对使用 GridSearchCV。这是一个很好的选择，只是它非常耗时，计算量也很大。如果你像我一样，日程繁忙，你一定会找到更好的选择。

更好的替代方法是 RandomSearch CV，它使用随机超参数值来挑选最佳超参数。这比 GridSearchCV 快多了。这里的缺点是，由于它采用随机值，我们不能确定这些值是最佳组合。

但是说真的，**我什么时候知道我需要做超参数优化**？

作为数据科学家，我们经常犯的一个错误是使用模型的默认参数。根据您使用的默认参数，您可能没有使用模型的最佳版本。

有时，当您的模型过度拟合(在训练集上表现良好，在测试数据集上表现不佳)或欠拟合(在训练数据集上表现不佳，在测试数据集上表现良好)时，优化您的超参数确实会有所帮助。一点小小的调整就能带来很大的不同，从 60%的准确率到 80%的准确率，甚至更多！

好了，让我们结束介绍。在本文结束时，您将了解到:

*   最好的超参数调优工具，
*   各种开源服务(免费使用)和付费服务，
*   它们的特征和优点，
*   他们支持的框架，
*   如何为你的项目选择最好的工具，
*   如何将它们添加到您的项目中。

我们从一个 TL 开始。下面讨论的所有工具的灾难恢复比较。

## 模型调整和超参数优化的比较工具

如果您时间紧迫，这张表可以帮助您选择一个好的工具，在您的用例中进行尝试。有关每个工具的详细描述，请继续阅读下表。

接下来，我将从一些开源工具开始。每个工具将按以下方式描述:

*   工具简介，
*   工具的核心特性/优势，
*   如何使用该工具的步骤，
*   关于如何在项目中使用该工具的其他链接。

### 1.射线调谐

Ray 为构建分布式应用程序提供了一个简单、通用的 API。Tune 是一个 Python 库，用于任何规模的实验执行和超参数调整。Tune 是 Ray 众多包中的一个。Ray Tune 是一个 Python 库，它通过大规模利用尖端的优化算法来加速超参数调整。

为什么应该使用 RayTune？

**下面是一些[的特点](https://web.archive.org/web/20220928202019/https://docs.ray.io/en/master/tune/user-guide.html) :**

*   它很容易与许多优化库集成，如 [Ax/Botorch](https://web.archive.org/web/20220928202019/http://ax.dev/) 和[hyperpt](https://web.archive.org/web/20220928202019/https://github.com/hyperopt/hyperopt)。
*   缩放可以在不改变代码的情况下完成。
*   Tune 利用各种尖端优化算法，如 [Ax/Botorch](https://web.archive.org/web/20220928202019/http://ax.dev/) 、[hyperpt](https://web.archive.org/web/20220928202019/https://github.com/hyperopt/hyperopt)和[贝叶斯优化](https://web.archive.org/web/20220928202019/https://github.com/fmfn/BayesianOptimization)，使您能够透明地扩展它们。
*   Tune 跨多个 GPU 和多个节点并行化，因此您不必构建自己的分布式系统来加速训练。
*   你可以用 Tensorboard 之类的工具自动显示结果。
*   它为优化算法提供了一个灵活的[接口，您可以用几行代码轻松实现和扩展新的优化算法。](https://web.archive.org/web/20220928202019/https://ray.readthedocs.io/en/latest/tune-searchalg.html#contributing-a-new-algorithm)
*   它支持任何机器学习框架，包括 Pytorch、Tensorflow、XGBoost、LIghtGBM、Scikit-Learn 和 Keras。

使用它需要五个简单的步骤(我假设您已经对数据进行了预处理):

```py
pip install ray[tune]
```

无论您想在 ML 项目中使用 Tensorflow、Pytorch 或任何其他框架实现 Ray Tune，都有很多教程可供选择。以下是一些可供参考的例子:

您可以从本文中了解更多关于配置光线调节及其功能的信息:[“光线调节:一个超参数库，可在任何比例下快速调节超参数”](https://web.archive.org/web/20220928202019/https://towardsdatascience.com/fast-hyperparameter-tuning-at-scale-d428223b081c)。

### 2.奥普图纳

[Optuna](https://web.archive.org/web/20220928202019/https://optuna.readthedocs.io/en/stable/) 是专门为机器学习设计的。这是一个[黑盒优化器](https://web.archive.org/web/20220928202019/https://sahinidis.coe.gatech.edu/bbo#:~:text=We%20refer%20to%20systems%20of,specified%20values%20of%20system%20inputs)，所以它需要一个目标函数。这个目标函数决定在即将到来的试验中从哪里采样，并返回数值(超参数的性能)。它使用不同的算法，如网格搜索，随机搜索，贝叶斯和进化算法来寻找最佳的超参数值。

**一些特征是:**

*   高效的采样和剪枝算法。
*   易于安装，要求不高。
*   比远视更容易使用。
*   使用分布式优化。
*   您可以使用 Python 语法定义搜索空间，包括条件和循环。
*   您可以直观地分析优化结果。
*   简单的可伸缩性，很少或不需要修改代码。

Optuna 使用修剪算法。**修剪**是一种在**机器学习**和搜索算法中使用的技术，通过删除树中对分类实例来说非关键和冗余的部分来减少决策树的大小。

Optuna 中的修剪会在训练的早期阶段自动停止没有希望的试验，您也可以称之为自动提前停止。Optuna 提供了以下修剪算法:

我将重点介绍使用 Optuna 所需的简单步骤:

1.  首先，用“pip install optuna”安装 Optuna，如果它还没有安装的话。
2.  定义你的模型。
3.  选择要优化的参数。
4.  创建一个研究。
5.  定义目标函数。
6.  优化。
7.  检查试验结果。

要查看的教程和示例代码:

您也可以阅读此文章:[“Optuna 指导如何监控超参数优化运行”](/web/20220928202019/https://neptune.ai/blog/optuna-guide-how-to-monitor-hyper-parameter-optimization-runs)，以更好地了解 Optuna 如何优化您的超参数。

### 可能有用

检查如何使用 [Neptune + Optuna](https://web.archive.org/web/20220928202019/https://docs.neptune.ai/integrations-and-supported-tools/hyperparameter-optimization/optuna) 集成来跟踪您的超参数优化过程。

### 3.远视

从官方文档来看， [Hyperopt](https://web.archive.org/web/20220928202019/https://github.com/hyperopt/hyperopt) 是一个 Python 库，用于在笨拙的搜索空间上进行串行和并行优化，搜索空间可能包括实值、离散和条件维度。

**Hyperopt** 使用贝叶斯优化算法进行超参数调整，为给定模型选择最佳参数。它可以优化具有数百个超参数的大规模模型。

Hyperopt 目前实现了三种算法:

*   随机搜索，
*   Parzen 估计量树，
*   自适应 TPE。

Hyperopt 的设计是为了适应基于高斯过程和回归树的贝叶斯优化算法，但不幸的是，它们目前还没有实现。

**远视的特征:**

超视需要 4 个基本组件来优化超参数:

*   搜索空间，
*   损失函数，
*   优化算法，
*   用于存储历史(分数、配置)的数据库

在您的项目中使用 Hyperopt 的步骤:

1.  初始化要搜索的空间。
2.  定义目标函数。
3.  选择要使用的搜索算法。
4.  运行**远视**功能。
5.  分析存储在 trials 对象中的评估输出。

这里有一些实践教程，你可以看看:

这里还有一款不错的 [kaggle 笔记本](https://web.archive.org/web/20220928202019/https://www.kaggle.com/prashant111/bayesian-optimization-using-hyperopt)你可以试试。

### 4.sci kit-优化

[Scikit-Optimize](https://web.archive.org/web/20220928202019/https://scikit-optimize.github.io/stable/auto_examples/hyperparameter-optimization.html) 是 Python 中超参数优化的开源库。它是由 Scikit-learn 背后的团队开发的。与其他超参数优化库相比，它相对容易使用。

它有基于模型的连续优化库，称为贝叶斯超参数优化(BHO)。BHO 的优势在于，他们可以在更少的迭代中找到比随机搜索更好的模型设置。

贝叶斯优化到底是什么？

贝叶斯优化是一种用于黑盒函数全局优化的顺序设计策略，它不采用任何函数形式。它通常用于优化计算量大的函数。至少维基百科是这么说的。

但是，简单地说，BO 评估了从过去的结果看起来更有希望的超参数，并找到了更好的设置，而不是使用迭代次数更少的随机搜索。过去超参数的表现影响未来的决策。

**sci kit-Optimize 的特性:**

*   基于顺序模型的优化，
*   构建于 NumPy、SciPy 和 Scikit-Learn 之上，
*   开源，商业可用，BSD 许可。

Scikit-Optimize 使用高斯过程的贝叶斯优化基于一种叫做 **gp_optimize 的算法。**你可以在这里了解更多[。如果你对如何从零开始构建自己的贝叶斯优化器感兴趣，你也可以看看这个教程:“](https://web.archive.org/web/20220928202019/https://scikit-optimize.github.io/stable/modules/generated/skopt.gp_minimize.html)[如何用 Python](https://web.archive.org/web/20220928202019/https://machinelearningmastery.com/what-is-bayesian-optimization/) 从零开始实现贝叶斯优化”。

以下是使用 Scikit-Optimize 需要遵循的简单步骤:

1.  如果尚未安装 skopt，请使用 pip install skopt 安装 skopt。
2.  定义模型。
3.  决定要优化的参数。
4.  定义搜索空间。
5.  定义目标函数。
6.  运行优化。

以下是在您的项目中实现 Scikit Optimize 的教程列表:

关于 Scikit 优化特性的深入解释，请查看本文。

### 可能有用

检查如何使用 [Neptune + Scikit 优化集成](https://web.archive.org/web/20220928202019/https://docs.neptune.ai/integrations-and-supported-tools/hyperparameter-optimization/scikit-optimize)跟踪您的超参数优化过程。

### 5.[微软的 NNI](https://web.archive.org/web/20220928202019/https://www.microsoft.com/en-us/research/project/neural-network-intelligence/) (神经网络智能)

NNI 是由微软开发的免费、开源的 AutoML 工具包。它用于自动化特征工程、模型压缩、神经架构搜索和超参数调整。

它是如何工作的？

该工具调度并运行由调整算法生成的试验作业，以在不同的环境(如本地机器、远程服务器和云)中搜索最佳的神经架构和/或超参数。

微软的 NNI 支持 Pytorch、Tensorflow、Keras、Theano、Caffe2 等框架。，以及像 Sckit-learn、XGBoost、CatBoost 和 LightGBM 这样的库。

**[NNI 的特色](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Overview.html) :**

*   很多流行的[自动调谐算法](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Tuner/BuiltinTuner.html)(像 [TPE](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Tuner/BuiltinTuner.html#TPE) 、[随机搜索](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Tuner/BuiltinTuner.html#Random)、 [GP 调谐器](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Tuner/BuiltinTuner.html#GPTuner)、 [Metis 调谐器](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Tuner/BuiltinTuner.html#MetisTuner)等等)和[提前停止算法](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Assessor/BuiltinAssessor.html) ( [Medianstop](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Assessor/BuiltinAssessor.html#MedianStop) 、 [Curvefitting](https://web.archive.org/web/20220928202019/https://nni.readthedocs.io/en/stable/Assessor/BuiltinAssessor.html#Curvefitting) assessors)。
*   NAS(神经架构搜索)框架，用户可以轻松指定他们想要使用的神经架构。
*   通过 NNI 试用 SDK 支持 NAS 算法，如 ENAS(高效神经架构搜索)和飞镖(可区分架构搜索)。
*   通过 NNI 试用软件开发工具包的自动特征工程:您不必创建一个 NNI 实验，只需在您的试用代码中导入一个内置的自动特征工程算法并运行！
*   命令行工具和 web UI 来管理培训实验。
*   可扩展的 API 来定制您的自动 ML 模型。
*   它可以在本地机器、远程服务器、Azure 机器学习、基于 kubernetes 的服务(如 Kube Flow、Adapt DL、Open pal 等)上进行训练..
*   它具有用于超参数调整的方法，包括穷举搜索、启发式搜索、贝叶斯优化和基于 RL。
*   它的一些贝叶斯优化算法的超参数调整是 TPE，GP 调谐器，Metis 调谐器，BOHB，等等。

以下是使用 NNI 时需要遵循的步骤:

1.  [在 Windows 或 Linux 上安装 NNI](https://web.archive.org/web/20220928202019/https://github.com/Microsoft/nni) 并验证安装。
2.  定义和更新模型。
3.  启用 NNI API。
4.  定义搜索空间。
5.  定义你的实验。
6.  准备庭审。
7.  准备调谐器。
8.  准备配置文件。
9.  进行实验。

要了解更多关于这些步骤的信息，请查看 NNI 的官方文档。你也可以从 [Github](https://web.archive.org/web/20220928202019/https://github.com/Microsoft/nni) 了解更多关于微软的 NNI 算法。

寻找如何在您的项目中实现这一点？看看这个教程:“[如何将微软的 NNI 添加到你的项目](https://web.archive.org/web/20220928202019/https://galhever.medium.com/nni-an-automl-toolkit-e0e4234ebf12)”。

### 6.谷歌的 Vizer

[AI 平台 Vizier](https://web.archive.org/web/20220928202019/https://research.google/pubs/pub46180/) 是一个黑盒优化服务，用于调整复杂机器学习模型中的超参数。

它不仅通过调整超参数来优化模型的输出，还可以有效地用来调整函数中的参数。

它是如何工作的？

*   通过设置结果和影响结果的超参数来确定研究配置。
*   根据已设置的配置值创建研究，使用它来执行实验以产生结果。

为什么要用 Vizer？

*   很好用。
*   需要最少的用户配置和设置。
*   托管最先进的黑盒优化算法。
*   高可用性。
*   可扩展到每项研究数百万次试验，每项研究数千次平行试验评估，以及数十亿项研究。

按照以下步骤使用 Vizer:

在[文档页面](https://web.archive.org/web/20220928202019/https://cloud.google.com/ai-platform/optimizer/docs/using-optimizer)中，显示了如何使用 [curl](https://web.archive.org/web/20220928202019/https://curl.se/docs/httpscripting.html) 进行 API 请求的步骤。

### 7.AWS Sage 制造商

[AWS Sage Maker](https://web.archive.org/web/20220928202019/https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html) 是一款完全托管的机器学习服务。使用 SageMaker，您可以快速轻松地构建和训练机器学习模型。您可以在构建后直接将它们部署到生产就绪的托管环境中，就像一个完整的包一样。

它还提供了机器学习算法，这些算法经过优化，可以针对分布式环境中的海量数据高效运行。 **SageMaker 本身支持自带算法和框架**，还提供灵活的分布式培训选项，以适应您的特定工作流程。

SageMaker 使用随机搜索或贝叶斯搜索进行模型超参数调整。对于贝叶斯搜索，它要么使用接近来自最佳先前训练作业的组合的超参数值的组合来提高性能，要么选择远离它所尝试的那些超参数值的一组超参数值。

[为什么要使用 AWS？](https://web.archive.org/web/20220928202019/https://towardsdatascience.com/why-do-we-need-aws-sagemaker-79bce465f19f)

AWS Sagemaker 负责提取完成任务所需的大量软件开发技能，同时保持高效、灵活和成本效益。您可以专注于更重要的核心 ML 实验，SageMaker 用类似于您现有工作流程的简单抽象工具补充了剩余的必要技能。您的所有工具都在一个地方，因此您可以在一个平台上轻松地从数据预处理转移到模型构建和模型部署。

简而言之，你可以使用 SageMaker 的自动模型调优，内置算法，自定义算法，以及 SageMaker 为机器学习框架预先构建的容器。

在这些教程中了解更多信息:

👉也检查一下 [SageMaker 和 Neptune](/web/20220928202019/https://neptune.ai/vs/sagemaker) 之间的比较。

### 7.Azure 机器学习

Azure 由微软开发，利用其不断扩张的全球数据中心网络。Azure 是一个云平台，可以在任何地方构建、部署和管理服务和应用。

**Azure Machine Learning** 是一个独立的现代化服务，提供完整的数据科学平台。从数据预处理到模型构建、模型部署和维护，整个数据科学之旅都在一个平台上完成。它支持代码优先和低代码体验。如果你喜欢很少或不喜欢代码，你应该考虑使用 Azure Machine Learning Studio。

Azure Machine Learning Studio 是一个关于 Azure Machine Learning 的门户网站，包含用于项目创作和资产管理的低代码和无代码选项(拖放)。

Azure 机器学习支持以下超参数采样方法:

*   随机抽样用于为每个超参数随机选择一个值，该值可以是离散值和连续值的混合。它还支持低性能运行的提前终止，就像基于树的模型中的提前停止一样。
*   仅当所有超参数都是离散的时，才可以采用网格采样，并且网格采样用于尝试搜索空间中参数的每个可能组合。
*   贝叶斯采样基于贝叶斯优化算法来选择超参数值，该算法尝试选择将导致先前选择的性能提高的参数组合。

对于一个非常大的超参数搜索空间(数百个超参数或更多)，将需要很多次迭代来尝试每一个组合。为了节省您的时间，您可以将早期迭代停止设置为那些结果比早期差的实验(迭代)。Azure 有提前停止策略来帮助你:

*   **土匪政策**。如果目标性能指标的表现比迄今为止的最佳运行差了一个指定的差值，您可以使用 bandit 策略来停止运行(实验或迭代)。
*   **中位数停止策略**。像 bandit 策略一样，它放弃目标性能度量比所有运行的运行平均值的中值差的运行。
*   **截断选择策略**。如果百分比低于您指定的截断百分比值，截断选择策略将取消每个评估间隔的所有运行。

如何在项目中开始使用 Azure 进行超参数调优？

1.  定义搜索空间。
2.  配置采样。您可以选择格网外采样、贝叶斯采样或随机采样。
3.  配置提前终止。您可以使用 Bandit 策略、中值停止策略或截断停止策略。
4.  运行一个超调训练实验。

查看微软的这个教程模块:[“用 Azure 机器学习调优超参数”](https://web.archive.org/web/20220928202019/https://docs.microsoft.com/en-us/learn/modules/tune-hyperparameters-with-azure-machine-learning/)。

## 结论

我希望我能够教你一两件关于超参数工具的事情。不要只是让它停留在你的脑海里，尝试一下吧！请随时联系我，我很乐意了解您的意见和偏好。感谢阅读！

还可以查看其他资源:

### 文米·阿基雷米

一位热爱为移动设备构建 AI 解决方案的数据科学家和 Android 开发人员。我是一个有抱负的演讲者，对关于人工智能的技术演讲感兴趣。我从事过各种项目，包括图像分类、文本生成、聊天机器人、回归和分类问题。我也写科技文章和博客。

* * *

**阅读下一篇**

## 如何跟踪机器学习模型的超参数？

卡米尔·卡什马雷克|发布于 2020 年 7 月 1 日

**机器学习算法可通过称为超参数**的多个量规进行调整。最近的深度学习模型可以通过数十个超参数进行调整，这些超参数与数据扩充参数和训练程序参数一起创建了非常复杂的空间。在强化学习领域，您还应该计算环境参数。

数据科学家要**控制好** **超参数** **空间**，才能**使** **进步**。

在这里，我们将向您展示**最近的** **实践**，**提示&技巧，**和**工具**以最小的开销高效地跟踪超参数。你会发现自己掌控了最复杂的深度学习实验！

## 为什么我应该跟踪我的超参数？也就是为什么这很重要？

几乎每一个深度学习实验指南，像[这本深度学习书籍](https://web.archive.org/web/20220928202019/https://www.deeplearningbook.org/contents/guidelines.html)，都建议你如何调整超参数，使模型按预期工作。在**实验-分析-学习循环**中，数据科学家必须控制正在进行的更改，以便循环的“学习”部分正常工作。

哦，忘了说**随机种子也是一个超参数**(特别是在 RL 领域:例如检查[这个 Reddit](https://web.archive.org/web/20220928202019/https://www.reddit.com/r/MachineLearning/comments/76th74/d_why_random_seeds_sometimes_have_quite_large/) )。

## 超参数跟踪的当前实践是什么？

让我们逐一回顾一下管理超参数的常见做法。我们关注于如何构建、保存和传递超参数给你的 ML 脚本。

[Continue reading ->](/web/20220928202019/https://neptune.ai/blog/how-to-track-hyperparameters)

* * *