# 机器学习团队实际使用的最好的工具、库、框架和方法论——我们从 41 ML 初创公司学到的东西[综述]

> 原文：<https://web.archive.org/web/https://neptune.ai/blog/tools-libraries-frameworks-methodologies-ml-startups-roundup>

为您的机器学习团队建立一个良好的工具堆栈对于高效工作和能够专注于交付结果非常重要。如果你在一家初创公司工作，你会知道建立一个可以与你的团队、用户需求和快速发展的 ML 环境一起成长的环境是特别重要的。

我们想知道:**“ML 创业公司使用的最好的工具、库和框架是什么？”**应对这一挑战。

为了回答这个问题，我们询问了来自世界各地的 41 家机器学习初创公司。

结果呢？

我们总结了大量的好建议:

*   方法学
*   软件开发设置
*   机器学习框架
*   MLOps
*   意外的🙂

继续读下去，找出对你的机器学习团队有用的东西。

## 好的方法是关键

工具的强度取决于使用它们的方法。

如果你在随机获取的数据上运行训练模型，并部署你能得到的任何模型，迟早会有麻烦🙂

psyML 的 Kai Mildenberger 说:

> 对我们来说，对所有的训练和测试数据进行细致的版本控制可能是最重要的工具/方法。我们希望这仍然是我们工具箱中最关键的元素之一，即使所有的技术和数学模型都在不断迭代。第二个方面可能是假设驱动。我们将此作为开发模型的最重要的方法。”

我认为对你想用你的工具做什么(以及你实际上需要它们)有一个强烈的理解是非常重要的第一步。

也就是说，重要的是要知道那里有什么，以及在类似情况下人们成功使用了什么。

让我们开始吧！

## 软件开发工具是 ML 团队的支柱

开发环境是每个团队工作流程的基础。因此，了解世界各地的公司认为这一领域最好的工具是非常有趣的。

![](img/387db404f7e69eeaea61b2863a917255.png)

*Source: giphy.com*

ML 团队使用各种工具作为集成开发环境。像 simple report T1 和 T2 Hypergiant T3 这样的许多团队使用 Jupyter 笔记本和 Jupyter Lab 及其 NB 扩展生态系统。

> Jupyter 笔记本对于快速实验和可视化非常有用，尤其是在多个团队成员之间交换想法时。因为我们使用 Tensorflow，所以 Google Colab 是一个自然的扩展，可以更容易地共享我们的代码。”—[巨集](https://web.archive.org/web/20220926094533/https://juji.io/)的陈文茜说。

各种口味的 Jupyter 也被提及。Deepnote(一个托管的 Jupyter 笔记本解决方案)被 Intersect Labs 的团队*“因为他们的 ML 内容而受到喜爱”*，而 Google Colab *对于 [Juji](https://web.archive.org/web/20220926094533/https://juji.io/) 团队来说“是更容易分享我们代码的自然扩展”*。

其他人选择更标准的软件开发 ide。在这些 Pycharm 中，来自 [Hotelmize](https://web.archive.org/web/20220926094533/https://hotelmize.com/) 的 tooted by 或 Izchak 被称为*【最好的 Python IDE】*以及 [Scanta](https://web.archive.org/web/20220926094533/http://www.scanta.io/) 使用的 Visual Studio 代码因其*“易于与 Azure 连接并提供许多基于 ML 的扩展”*而被提及最多。

对于使用像 SimpleReport 这样的 R 语言的团队来说，RStudio 无疑是首选的 IDE。正如来自 [Advanced Symbolics](https://web.archive.org/web/20220926094533/https://www.advancedsymbolics.com/) 的 Kenton White 提到的

"*我们大多使用 R + RStudio 进行分析和建模。我们人工智能建模的主力是用于时间序列预测的 VARX。”*

说到代码版本控制，Github 显然是最受欢迎的。正如本影人工智能的丹尼尔·陈晗所说:

" *Github(现在对所有团队免费！！)及其超级健壮的版本控制系统和简单的存储库共享功能对大多数 ML 团队来说都非常有用。*

在最流行的语言中，我们有 Python、R，有趣的是还有 clo jure T1(由来自 T2 的陈文茜提到)。]

至于环境/基础设施设置，值得注意的是 ML 初创公司:

*   *“AWS 作为部署的平台”* ( [简单汇报](https://web.archive.org/web/20220926094533/https://www.simplereport.ca/))
*   *“Anaconda 是我们运行 ML 实验的 goto 工具，因为它具有*live code*特性，可用于将软件代码、计算输出、说明性文本和多媒体资源合并到一个文档中。”* ( [扫描](https://web.archive.org/web/20220926094533/http://www.scanta.io/))
*   Redis 作为内存数据结构存储占主导地位，因为它支持不同种类的抽象数据结构，如字符串、列表、映射、集合、排序集、超对数、位图、流和空间索引 ( [扫描](https://web.archive.org/web/20220926094533/http://www.scanta.io/))
*   " *[雪花](https://web.archive.org/web/20220926094533/https://www.snowflake.com/)和亚马逊 S3 进行数据存储."* ( [超级巨人](https://web.archive.org/web/20220926094533/http://hypergiant.com/))
*   “Spark-py Spark–非常简单的 api，用于分配工作以处理大数据。” ( [酒店化](https://web.archive.org/web/20220926094533/https://hotelmize.com/))

## 这么多机器学习框架

![](img/54afed64ec8fea6e2a33c19f94a2e592.png)

*Source: giphy.com*

集成开发环境是至关重要的，但是需要一个好的 ML 框架来将愿景转化为项目。这里，初创公司指出的工具范围相当多样化。

在处理表格数据时，熊猫被提到的次数最多。

适马北极星公司的首席执行官尼莫·德克尔提到的使用熊猫的额外好处是:

> “我认为 Pandas 可能是最有价值的工具之一，尤其是在与外部开发人员合作进行各种项目时。让所有的数据文件以数据框的形式存在于团队和个人开发者之间，有助于更顺畅的协作和避免不必要的麻烦。”

来自 [Hotelmize](https://web.archive.org/web/20220926094533/https://hotelmize.com/) 的软件开发人员提到的有趣的库是[dov panda](https://web.archive.org/web/20220926094533/https://github.com/dovpanda-dev/dovpanda)——panda 的 python 扩展库，它让你在使用 panda 时能够洞察你的 panda 代码和数据。

当谈到可视化时，matplotlib 被像 [Trustium](https://web.archive.org/web/20220926094533/https://www.trustium.com/) 、 [Hotelmize](https://web.archive.org/web/20220926094533/https://hotelmize.com/) 、 [Hypergiant](https://web.archive.org/web/20220926094533/http://hypergiant.com/) 和其他人使用得最多。

Plotly 也是一个常见的选择。正如来自[wordners](https://web.archive.org/web/20220926094533/https://www.wordnerds.ai/)的开发者所解释的*“为了更好的可视化，让数据看起来更好理解”*。Dash 是一款用于在 Plotly 图表上构建交互式仪表盘的工具，由来自 [Behavioral Signals](https://web.archive.org/web/20220926094533/http://behavioralsignals.com/) 的西奥多·詹纳科普洛斯推荐给需要以友好、用户友好的方式展示分析结果的 ML 团队。

对于更标准的机器学习问题，大多数团队像[书呆子](https://web.archive.org/web/20220926094533/https://www.wordnerds.ai/)、[感觉信任](https://web.archive.org/web/20220926094533/https://www.sensitrust.io/)或[行为信号](https://web.archive.org/web/20220926094533/http://behavioralsignals.com/)使用 Scikit-Learn。来自 iSchoolConnec t 的 ML 团队解释了为什么它是如此伟大的工具:

> 它是机器学习研究人员、工程师和开发人员使用的最流行的工具包之一。你可以轻而易举地得到你想要的东西，这是惊人的！从功能工程到可解释性，scikit-learn 为您提供了所有功能。”

说实话，熊猫和 Sklearn 真的是世界各地 ML 团队的主力。

正如来自[number](https://web.archive.org/web/20220926094533/http://www.numer.ai/)的数据科学家迈克尔·菲利普斯所说:

“像 Pandas 和 Scikit-learn 这样的现代 Python 库拥有 99%的 ML 团队需要超越的工具。虽然简单，但这些工具在经验丰富的数据科学家手中却拥有非凡的力量"

在我看来，虽然在一般的 ML 团队中这可能是真的，但在 ML 初创公司的情况下，很多工作都进入了最先进的方法，这通常意味着深度学习模型。

当谈到通用深度学习框架时，我们有许多不同的意见。

很多团队像[书呆子](https://web.archive.org/web/20220926094533/https://www.wordnerds.ai/)和[行为信号](https://web.archive.org/web/20220926094533/http://behavioralsignals.com/)选择 PyTorch。

来自 iSchoolConnect 的 ML 专家团队告诉我们为什么这么多 ML 从业者和研究者选择 PyTorch。

“如果你想去深水区，PyTorch 是你最合适的工具！最初，习惯它需要时间，但是一旦你习惯了，就没有什么比它更好的了！该库甚至针对快速训练和评估您的 ML 模型进行了优化。”

但人气领先的还是 Tensorflow 和 Keras。

像 Strayos 和 Repetere 这样的大多数团队选择它作为他们的 ML 开发框架。信托基金会的雪松·米拉佐说:

*“当然是 Tensorflow。尤其是有了 2.0！热切的执行是 TF 真正需要的，现在它来了。我应该注意，当我说“tensorflow”时，我指的是“tensorflow + keras”，因为 keras 现在内置在 TF 中。*

还有很重要的一点要提的是，你不必选择一个框架而排斥其他框架。

例如， [Melodia](https://web.archive.org/web/20220926094533/https://melodia.io/) 的创始人奥米德·雅利安说:

> “对我们最有益的工具是 TensorFlow、PyTorch 和 Python 的老 scikit-learn 工具。”

对于更专业的应用程序，有一些流行的框架。

在自然语言处理中，我们听说过:

*   拥抱脸:这是有史以来最先进、性能最高的 NLP 库。这是同类研究中的第一个，因为研究人员直接为高度可扩展的 NLP 库做出了贡献。Hypergiant[公司的首席执行官本·拉姆(Ben Lamm)说，它与其他类似的工具不同，它在新型号发布后几个月就推出了生产级工具。](https://web.archive.org/web/20220926094533/http://hypergiant.com/)
*   Spacy 是一个非常酷的自然语言工具包。NLTK 是目前最流行的，我当然也在使用它，但是 spacy 做了很多 NLTK 做不到的事情，比如词干分析和依赖解析。”提到 Cedar Milazzo， [Trustium](https://web.archive.org/web/20220926094533/https://www.trustium.com/) 的首席执行官
*   Gensim 对单词向量和文档向量也很好，我相信它不是很受欢迎添加雪松米拉佐。

在计算机视觉中:

*   *[OpenCV](https://web.archive.org/web/20220926094533/https://opencv.org/)是计算机视觉工作不可或缺的*对于 [Hypergiant](https://web.archive.org/web/20220926094533/http://hypergiant.com/) 。他们的首席执行官说*“这是从 20 世纪 60 年代到 2014 年的经典 CV 方法集合，是有用的预处理和后处理，在神经网络可能被过度破坏的情况下可以很好地工作。”*

同样值得注意的是，并不是每个团队自己都在实现深度学习模型。

正如来自 Munchron 的 Iuliia Gribanova 和 Lance Seidman 所说，现在有一些 API 服务，你可以外包一些(或全部)工作:

> *“Google ML kit 是目前最好的易于进入的工具之一，它让移动开发人员可以轻松地将 ML API 服务(如人脸识别、图像标记和 Google 提供的其他项目)嵌入到 Android 或 iOS 应用程序中。但此外，你还可以引入自己的 TF (TensorFlow) lite 模型来进行实验，然后使用谷歌的 ML 工具包将它们投入生产。”*

我认为值得一提的是，并不是所有时候你都可以选择最新最好的库，当你加入团队的时候，工具栈就会交给你。

来自 [Meshcapade](https://web.archive.org/web/20220926094533/https://www.meshcapade.com/) 的 Naureen Mahmood 分享道:

“过去，一些重要的 autodiff 库使我们有可能运行多种联合优化，并在这样做的过程中帮助我们构建了一些我们今天仍在使用的核心技术，这些库是友好的& OpenDR。现在有更好更快的了，比如 Pytorch 和 TensorFlow。”

当谈到模型部署时，来自 [Private AI](https://web.archive.org/web/20220926094533/http://www.private-ai.ca/) 的 Patricia Thaine 提到了*“tflite，flask，tfjs 和 coreml”*作为他们的首选框架。她还表示，可视化模型对他们来说非常重要，他们正在为此使用 [Netron](https://web.archive.org/web/20220926094533/https://github.com/lutzroeder/netron) 。

但是有超越框架的工具可以帮助 ML 团队快速交付真正的价值。

这就是 MLOps 的用武之地。

## MLOps 开始对机器学习初创公司变得更加重要

您可能想知道什么是 MLOps，或者为什么您应该关心它。

![](img/9eef09e3fc25df5f106c00d2be4e3e37.png)

*Source: giphy.com*

该术语暗指 DevOps，描述用于机器学习活动操作化的工具。

Acerta 的首席技术官 Jean-Christophe Petkovich 为我们提供了一个极其详尽的解释，说明他们的 ML 团队是如何处理 MLOps 的。太好了，我决定(几乎)全文分享:

> *“我认为大多数有趣的工具将在 2020 年被更广泛地采用，它们都是以 MLOps 为中心的。去年大力推动了这些工具的开发，今年我们将揭晓谁将是赢家。*

对我来说，MLflow 似乎在跟踪实验、工件和结果方面处于领先地位。我们为此在内部构建的许多东西都是对 MLflow 功能的扩展，以纳入更多类似于 DVC 跟踪数据的数据跟踪。

*MLOps 中的其他知名公司有 Kubeflow、Airflow 和采用 Apache Beam 的 TFX，它们都是专为端到端捕获数据科学工作流和管道而设计的工具。*

*一个完整的 MLOps 系统有几个组成部分:*

*   您需要能够构建包含预处理数据和生成结果所需的所有信息的模型工件。
*   一旦你能够构建模型工件，你必须能够跟踪构建它们的代码，以及它们被训练和测试的数据。
*   你需要跟踪这三样东西，模型、它们的代码和它们的数据，是如何联系在一起的。
*   一旦您可以跟踪所有这些东西，您还可以将它们标记为准备就绪和生产，并通过 CI/CD 流程运行它们。
*   最后，要在流程结束时实际部署它们，您需要某种方法来基于模型工件旋转服务。

*说到跟踪，MLflow 是我们的选择，它已经在 [Acerta](https://web.archive.org/web/20220926094533/http://acerta.ca/) 试用过，因为我们的一些员工已经将它作为他们个人工作流程的一部分，现在它是我们数据科学家事实上的跟踪工具。*

为了跟踪数据管道或工作流本身，我们目前正在开发 Kubeflow，因为我们已经在 Kubernetes 上使部署变得轻而易举，并且我们的内部模型管道基础设施与 Kubeflow 组件概念非常契合。

在所有这些 MLOps 开发的基础上，有一个向构建特征库的转变——基本上是专门的数据湖，用于存储各种形式的预处理数据——但是我还没有看到任何真正脱颖而出的真正竞争者。

这些都是需要到位的工具——我知道很多地方正在针对这个问题制定自己的解决方案，但我认为今年我们将会看到更多围绕机器学习应用的标准化。"

来自 [Kaskada](https://web.archive.org/web/20220926094533/https://kaskada.com/) 的 Emily Kruger，她是一家创建特色商店解决方案的初创公司🙂添加:

> 从我们的角度来看，最有用的工具是特性库、自动化部署管道和实验平台。所有这些工具都解决了 MLOps 的挑战，这是数据团队的一个重要新兴领域，尤其是那些在生产和大规模运行 ML 模型的团队。”

好的，鉴于此，其他团队用什么来解决这些问题呢？

一些团队更喜欢端到端平台，另一些团队则在内部创建一切。许多团队介于两者之间，混合了一些特定的工具和自己开发的解决方案。

就较大的平台而言，经常提到的两个名称是:

*   亚马逊 SageMaker，据来自 [VCV](https://web.archive.org/web/20220926094533/https://www.vcv.ai/) *的 ML 团队称，“有多种分布式协作工具”*和 [SimpleReport](https://web.archive.org/web/20220926094533/https://www.simplereport.ca/) 选择作为他们的部署平台。
*   azure,[Scanta](https://web.archive.org/web/20220926094533/http://www.scanta.io/)团队告诉我们*“作为一种构建、训练和部署我们的机器学习应用程序的方式，它还通过语言、视觉和语音识别支持，帮助我们的应用程序增加智能。由于快速部署和低成本虚拟机，Azure 一直是我们选择的 IaaS。”*

实验跟踪工具出现了，我们看到 ML 初创公司使用各种选项:

*   Strayos 使用 Comet ML *“用于模型协作和结果共享”*。
*   [Hotelmize](https://web.archive.org/web/20220926094533/https://hotelmize.com/) 和其他人正在使用 tensorboard，这是*“可视化你的模型行为的最好工具，特别是对于神经网络模型。”*
*   MLflow 似乎在跟踪实验、工件和结果方面处于领先地位正如之前提到的 [Acerta](https://web.archive.org/web/20220926094533/http://acerta.ca/) 的首席技术官 Jean-Christophe Petkovich 所说
*   像 [Repetere](https://web.archive.org/web/20220926094533/https://repetere.ai/) 这样的其他团队试图保持简单，并说*“我们的工具非常简单，我们使用 tensorflow 和 s3 来版本化模型工件以供分析”*。

通常，实验跟踪工具会跟踪指标和超参数，但是正如来自 MeetKai 的 James Kaplan 指出的:

对我们来说，最有用的 ML 工具是任何有助于处理由除了模型架构之外的任何事物引起的模型回归的工具。其中大部分是我们自己开发的工具，但我认为还有很多现有的选择。我们喜欢看混淆矩阵，它可以在以下场景中进行视觉区分:

*–添加到训练集的新数据(以及所述数据的普罗维登斯)*

*–量化配置*

*–修剪/提取*

*我们发现，能够跟踪新增加数据的性能比仅仅跟踪模型本身超参数的性能重要得多。当数据集的增长/变化远快于模型配置时尤其如此"*

谈到修剪/蒸馏， [deepset](https://web.archive.org/web/20220926094533/https://deepset.ai/) 的联合创始人 Malte Pietsch 解释说:

> *“我们发现越来越需要工具来帮助我们分析&在速度和硬件利用率方面优化模型。随着 NLP 模型规模的增长，提高训练和推理效率变得越来越重要。*

虽然我们仍在寻找理想的工具，但我们发现 pytest-benchmark、NVIDIA 的 Nsight Systems 和 kernprof 非常有用。"

另一个有趣的基准训练/推理工具是来自[divide ti](https://web.archive.org/web/20220926094533/http://dividiti.com/)的 Anton Lokhmotov 建议的 [MLPerf](https://web.archive.org/web/20220926094533/http://mlperf.org/) 。

实验模型无疑是非常重要的，但是将模型放在最终用户面前才是神奇的地方(对我们大多数人来说)。在这方面，来自托尔斯泰的 Rosa Lin 提到了使用 streamlit.io，这是一个*“轻松构建 ML 模型网络应用的伟大工具。”*

Sensitrust 的联合创始人 Gianvito Pio 在谈到使用以 ML 为中心的解决方案时提出了宝贵的警告:

还有像 Knife 和 Orange 这样的工具可以让你以拖放的方式设计整个管道，还有 AutoML 工具(见 AutoWEKA、auto-sklearn 和 JADBio)可以为特定任务自动选择最合适的模型。

然而，在我看来，在机器学习和人工智能领域的专业知识仍然是必要的。如果没有良好的实地背景，即使是“最好的、自动化的”工具也可能被误用。"

### 你可能会感兴趣

在 ML 找工作？在此检查[开仓。](https://web.archive.org/web/20220926094533/https://jooble.org/jobs-machine-learning)

## 意外的

好吧，当我开始研究这个的时候，一些像 PyTorch，Pandas 或者 Jupyter Lab 这样的答案是我所期望的。

但是我们收到的一个回答确实是现成的。

![](img/7160fe52d4018d0d8040bb5bd24635fc.png)

*Source: giphy.com*

这让我看清了所有其他事情，并让我想到，也许我们应该后退一步，看看更大的图景。

来自 [Trust Insights](https://web.archive.org/web/20220926094533/https://www.trustinsights.ai/) 的 Christopher Penn 建议 ML 团队应该使用一个相当有趣的“工具”:

> “Wetware——你两耳之间的硬件和软件组合——是你拥有的最重要、最有用、最强大的机器学习工具。

太多太多的人希望人工智能是一根魔杖，可以在很少甚至没有人类输入的情况下解决一切问题。反之亦然；人工智能比以往任何时候都需要更多的管理和审查，因为我们对复杂的模型缺乏太多的可见性。

在大规模偏见和歧视丑闻之后，可解释性和可解释性是我们现在面临的最大挑战。人工智能供应商把重点放在模型的事后解释上，而不是在模型中建立昂贵但有价值的解释和检查点，这使情况变得更糟。

因此，在 2020 年以及可预见的未来，湿件——循环中的人类——是最有用的工具。"

## 我们的视角

因为我们正在为 ML 团队构建工具，而且我们的一些客户是人工智能初创公司，所以我认为给你我们的观点是有意义的。

所以我们看到:

…由于这些是我们的客户，他们自然会使用 neptune-notebook 来跟踪 jupyter notebooks 中的探索，并使用 Neptune 来跟踪实验和组织他们的机器学习项目。

信息图表

* * *

## 特别感谢

## 非常感谢所有参与此次综述的机器学习团队。分享你的知识和经验给社区带来了难以置信的价值！

**对本文有贡献的初创公司:**

Acerta 是一家软件公司，为制造业和汽车行业提供机器学习技术。

一家市场研究公司，利用人工智能分析社交媒体来监控品牌健康，同时预测趋势和消费者行为。

alance 是一个自助式高级分析平台，允许用户从单一平台准备、管理、建模和可视化数据。

与人工智能发展情感智能对话。Oliver API 是发展最快的健壮情感人工智能引擎。

机器学习机构，专注于基于深度学习的自然语言处理(NLP)。

开发开源工具并提供 R&D 服务，帮助客户自动化其复杂的 AI、ML 和 quantum 研发

一个大数据和机器学习平台，使用预测为 CPG、零售和电子商务提供支持。它通过大规模的大数据实时分析受众行为模式。

GenRocket 是软件测试和机器学习数据生成领域的技术领导者。

Hazy 可以生成安全使用的智能合成数据，实际上可以替代真正的数据科学和分析工作负载。

Hotelmize 是一个平台，旨在利用大数据分析来改善酒店房间的定价和预订流程。

我们是机器智能领域的领导者，在从石油钻探和流体动力学到卫星成像、国防和安全等领域为客户量身定制解决方案和产品方面有着令人印象深刻的记录。

使用人工通用智能的认知计算。

Intersect Labs 提供的服务可以实现智能决策，包括通过 3 次点击从电子表格数据中进行机器学习。

人工智能，国际学生入学，国际大学和学院。

构建人工智能聊天机器人的最简单方法——比制作 PowerPoint 更简单。Juji 是 DIY AI 聊天机器人的头号聊天机器人平台。

Kaskada 通过提高创新速度和实时计算功能，帮助组织做出更好的预测，并从机器学习中获得更多影响。

SaaS，移动应用程序，医疗技术，生物技术，医疗保健，物联网，人工智能，人工智能，大数据。

Luden.io 是一家专注于有意义、有教育意义游戏的独立游戏开发商。

MeetKai 是一个语音操作的虚拟助手，通过对话、个性化和策展让您的生活更加轻松。

Melodia 是一个智能音乐流媒体平台，提供了一种更简单的播放和探索音乐的方式。

SaaS，最先进的三维人体模型。自动将身体扫描、mocap 或测量转换为装配的网格。

医生和实验室使用机器学习和人工智能进行早期疾病和疾病检测。

Numerai 将金融数据转换和规范化为数据科学家全球网络的机器学习问题。

我们希望您停止浪费时间构建报告，因此我们构建了一个平台，在尊重您的数据隐私的同时自动构建报告。

授权隐私保护软件开发。

psyML 结合了现代心理学、高级心理测量学、机器学习和人工智能，实现了对人类行为的前所未有的理解。

Repetere 通过机器学习和人工智能生成自动化的销售和产品组合预测。

SavantX 使用分析来整理和理解所有类型的数据。2.Trust Insights 美国|马萨诸塞州|诺福克

保护机器学习算法和使用它们的企业。

智能交通信号实时软件。

客户和专业人士联系、交易和设计新项目的平台。每个阶段都利用区块链技术，由智能合同管理，并由人工智能支持。

候选人评估和入围技术。自动化雇佣流程以提高效率、多样性和雇佣质量。

SimpleReport 是一款安全报告和分析工具，适用于以 OHS 为优先业务的公司。

Strayos 是一个 3D 空中智能平台，用于采矿和采石场爆破作业，以降低成本。

文本的机器学习工具。

Trust Insights 帮助公司点亮黑暗的数据，并通过分析和洞察帮助你采取行动。

SaaS B2B 平台决定信誉和保护品牌形象。

模拟，人工智能，数据搜索引擎，问答，全球建模。

VCV 是一名人工智能机器人招聘人员。

一个结合了前沿人工智能(AI)和老派语言学的文本分析和洞察平台允许计算机阅读——并真正理解——人们实际上的意思，而不仅仅是计算他们使用的单词。

AI 24/7 监控的实时视频监控软件。

雅各布·查肯

### 大部分是 ML 的人。构建 MLOps 工具，编写技术资料，在 Neptune 进行想法实验。

**阅读下一篇**

* * *

最佳 MLOps 工具以及如何评估它们

## 12 分钟阅读| Jakub Czakon |年 8 月 25 日更新

12 mins read | Jakub Czakon | Updated August 25th, 2021

在我们的一篇文章中——[机器学习团队实际使用的最好的工具、库、框架和方法——我们从 41 家 ML 初创公司学到的东西](https://web.archive.org/web/20220926094533/https://neptune.ai/blog/tools-libraries-frameworks-methodologies-ml-startups-roundup)——Acerta 的 CTO Jean-Christophe Petkovich 解释了他们的 ML 团队如何接近 MLOps。

**据他所说，一个完整的 MLOps 系统有几个要素:**

您需要能够构建包含预处理数据和生成结果所需的所有信息的模型工件。

*   一旦您能够构建模型工件，您必须能够跟踪构建它们的代码，以及它们被训练和测试的数据。
*   您需要跟踪所有这三样东西，模型、它们的代码和它们的数据，是如何关联的。
*   一旦您可以跟踪所有这些内容，您还可以将它们标记为准备就绪，进行生产，并通过 CI/CD 流程运行它们。
*   最后，为了在该过程的最后实际部署它们，您需要某种方法来基于该模型工件旋转服务。
*   这是对如何在公司中成功实施 MLOps 的高度概括。但是理解高层需要什么只是拼图的一部分。另一个是采用或创建适当的工具来完成工作。

这就是为什么我们编制了一份**最佳 MLOps 工具**的清单。我们将它们分为六类，以便您可以为您的团队和业务选择合适的工具。让我们开始吧！

That’s why we’ve compiled a list of the **best MLOps tools**. We’ve divided them into six categories so you can choose the right tools for your team and for your business. Let’s dig in!

[Continue reading ->](/web/20220926094533/https://neptune.ai/blog/best-mlops-tools)

* * *