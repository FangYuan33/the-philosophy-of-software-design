### [《软件设计的哲学》](https://yingang.github.io/aposd2e-zh/)

增量开发（如敏捷开发）意味着 **永远不会完成软件设计**，开发人员在系统的整个生命周期中应始终在思考设计问题；增量开发还意味着不断的重新设计。系统或组件的初始设计几乎从来都不是最好的，随着经验累积，不可避免地会产生更好的设计方式。作为软件开发人员，应该始终在寻找机会来改进现有系统设计，并且应该计划将部分时间花费在设计改进上。

### 2

评价系统是否复杂的我觉得可以从两方面考虑：一是代码的可读性；二是是否易于扩展。可读性这一点我觉得相对来说是难以控制的，比如在某个业务逻辑下，这段代码是否好读，很大程度上取决于写这段代码的人的代码风格，而代码风格又是很主观的，而且通常情况下并不会有强制的规则来要求代码规范，只是会借助一些代码扫描工具来尽可能的推动，这就会会导致需要花费较多的经历去理解才能完成较小的改进。当然，抛开不同的代码风格影响，我觉得代码可读性还受系统设计的影响，合理的设计让代码在结构上是容易理解的，而过度设计和抽象则会让人一头雾水。关于是否易于扩展，我觉得是一个更加客观的指标，一个系统是否易于扩展，取决于系统的设计是否符合**开闭原则**，是否符合**单一职责原则**，是否符合依赖倒置原则等等，凡是符合这些原则的，当开发者在书写相关的代码时，会非常直观的感受到做起来是多么轻松和容易，如果从成本和收益的角度来评估的话，扩展性更好的系统可以投入更少的人力来完成更大的改进。

当无法孤立地理解和修改给定的一段代码时，便存在依赖关系。依赖关系是软件的基本组成部分，不能完全消除，比如方法的签名创建了方法实现方和方法调用方之间的依赖关系：如果向方法添加了一个新参数，则必须修改调用该方法的代码以指定该参数。但是，软件设计的目标之一是减少依赖关系的数量，并使依赖关系保持尽可能简单和明显。之前修改的系统中“增加渠道”要更改一串系统，就是很强的依赖性的体现，同样的渠道在不同的系统间以不同的枚举值维护，但是其表示的含义都是一样的。

另一个复杂性的体现是模糊性，同一个变量名用于两个不同的目的或者声明的魔数并没有注释上明确的含义，那么开发人员就无法清楚地知道某个特定变量的目的是什么。

复杂性不是由单个灾难性错误引起的；它是累积的表现。单个依赖项或模糊项本身不太可能显著影响软件系统的可维护性，而且如果这段代码不再需要变更，那么通常也不会影响什么。之所以会出现复杂性，是因为随着时间的流逝，成千上万的小依赖项和模糊项逐渐形成。最终，这些小问题太多了，以至于对系统的每次更改都会受到其中几个问题的影响。

复杂性来自于依赖性和模糊性的积累。

### 3

战术式编程：能用就行，暴铺式开发完成快速交付，像龙卷风一样，所到之处都是混乱的，没有任何规划和设计，这就会使得复杂性不断的累积，最终导致需求开发成本增加，重构可能是有帮助的，但是解决一两个问题似乎区别不大，而解决所有需要几个月的时间导致日程安排没办法接受这种延迟，所以会一直陷入在这种恶性循环中

战略式编程：是长期的事情，仅仅“能用”是远远不够的，引入复杂性来完成开发工作是不可接受的，长远看是成本更低的一种选择。最重要的工作是帮助已有的代码完成 **扩展**

建议将总开发时间的 10% 到 20% 用于投资技术建设

即使在初创公司需要尽快发布产品的情况下，采取战术式编程也并不是一个好的选择，因为这种方法很有可能并不会加快交付速度，而且应该意识到，一旦代码库变成了一坨意大利面，几乎是不能够修复的，而且在产品的生命周期内，很可能需要付出高昂的成本。

公司成功的最重要因素之一是工程师的素质，降低开发成本的最佳方法是聘请优秀的工程师：他们的成本不会比普通工程师高很多，但生产率却高得多，而且他们会对良好的设计感兴趣，一旦不重视良好设计的原则或者公司内缺乏工程师土壤，这家公司不会被优秀的工程师青睐，比较鲜明的例子就是 Facebook。而采用战略式编程的 Google 在硅谷拥有极好的声誉也极为成功（这些例子表明，使用任何一种方法公司都有可能成功。但是，在一家关心软件设计并拥有整洁代码库的公司中工作会有趣得多）

**一旦开始延迟设计改进，就很容易使延迟永久化**

### 4

将模块的接口与其实现分开，便能将其复杂性隐藏起来。

将模块设计成“深”的，是本章比较重要的启示，它在其中提到了多类症是与代码整洁之道相反的理论

### 5

信息隐藏是实现深模块的重要方式。在读本章时，其中提到了信息和知识两个名词，起初为了读起来通顺，将两者全部视为一个概念，但是在我了解了“最少知识原则（一个类对于其他类知道的越少越好）”时，“知识（knowledge）”也是软件开发中的重要概念，而且用它形容一个模块或类中的信息也更为准确

它提出了适当使类稍大一些来完成信息隐藏，这一点与《代码整洁之道》提出的观点相反。这样可以减少类的数量，并且在类中尽可能的隐藏了“知识”

时间顺序分解是开发中常出现的一个问题，往往我们会根据先做什么再做什么来抽象接口，但是往往接口中处理逻辑的步骤是可以合并的，这样能够隐藏更多的知识。书中提出了“读取特定格式的文件，修改文件内容，然后再次将文件写入”的例子，因为文件读取和文件写入步骤都有文件格式相关的知识，这会导致信息泄露，所以将前两步合并，可以用于解决该问题，并且开放出的接口更简单

### 6

不管是专用的类或方法还是代码里的特殊情况，都是软件复杂性的主要来源。专用代码无法完全消除，但通过好的设计能够显著减少专用代码，并将专用代码与通用代码分开。这能使类更深、做到更好的信息隐藏以及让代码更简单、更清晰。 

对于开发需求，尽可能不进行定制化开发，而是思考通用的实现逻辑，即使在不考虑复用的情况下，通用性代码也是更合理的。可以尝试考虑的问题：满足当前需求最简单的接口是什么？这个方法会在多少种情况下被使用？目前通用的API使用起来是否简单？

针对“代码里的特殊情况”本章提出了通过在代码实现中**正确处理边界条件**以去掉针对这些特殊情况的 if 判断，这一点是比较好的启发

### 7

透传方法是项目中比较常见的问题，它除了将参数传递给另外一个与其有相同 API 的方法外，不执行任何操作，表示相关的类没有明确的职责划分，使得类变浅。解决透传问题的方法可以直接将底层接口暴露出来，或者直接将它们合并，如果合并起来不合适，可以将它们放在多个类中。

但是，只要每个方法都提供了有用且独特的功能，它们具有相同的签名是可以接受的。

参数透传相对比较好的解决方式是使用上下文对象

### 8

让模块的接口简单比让其实现简单更为重要，这是本章的重要观点。其中谈到“应该尽可能避免使用配置参数”我认为是不错的点，这让我想到了在开发延保补购查询接口时的配置，虽然这个仅供研发配置使用，但是这其实也提高了接口复杂性，我尽可能的将其中的参数指定了默认值，但是如果默认值产生了不明所以的问题，排查起来也是有难度的。自适应变更配置值是一个不错的考虑方向，但是还是要尽量避免配置参数的使用。

### 9

判断哪些代码能组合在一起的原则：它们共享信息、它们总是一起被使用、它们在概念上重叠和不看其中的一段代码就很难理解另一段。

拆分方法时，方法长度并不能成为理由。如果拆分方法后发现自己在父方法和子方法之间来回跳转以了解它们如何一起工作，就表明拆分可能不是一个好主意。

长方法并不总是坏的，假设一个方法包含按顺序执行的五个 20 行的代码块。如果这些块是相对独立的，则可以一次阅读并理解该方法的一个块。将每个块移动到单独的方法中并没有太大的好处。如果这些块之间具有复杂的交互，则将它们保持在一起就显得更为重要，这样读者就可以一次看到所有代码。如果每个块使用单独的方法，则读者将不得不在这些分散开的方法之间来回切换，以了解它们如何协同工作。

与《代码整洁之道》不同的观点：《代码整洁之道》强调“方法要尽可能的短小，如果方法超过 10 行，都太长了，而且在每个方法的 if else while 中出现的语句应该只有一行，这意味着方法的缩进不会超过两层，这样的方法易于阅读和理解”。而本书认为：方法的长度少到几十行再缩短时，进一步拆分带来的可读性提升非常有限，虽然单个小方法更容易理解，但是阅读几个相关联的短方法并理解它们如何协同工作通常比阅读一个较大的方法要难，因为更多的方法通常意味着更多的学习，并且不停的在各个方法之间跳转，会给读者一种意犹未尽的感觉。

> 深度比长度更重要：首先使方法变深，然后尝试使它们足够短，以便易于阅读，不要为了长度而牺牲深度。

不过，两者所强调的**每个方法只做一件事并且完整地做这件事**的观点是一致的。

### 10

减少异常处理代码的方法之一是“通过定义来规避异常”：意思是说在定义程序时，就将可能出现的异常情况考虑在内，而不是在程序运行时将异常情况抛出，比如说 Java 的 substring 方法，当指定超过有效范围内的索引值时，会抛出异常，这种情况便增加了复杂性，不如说在方法内部对索引值进行判断，如果超出范围则返回一个空字符串，在程序内部兼容处理异常是比较不错的选择，而且也降低了后续开发人员使用该方法的复杂性。

异常屏蔽和异常聚合的相似之处在于，这两种方式都将异常处理程序置于可以捕获最多异常的位置，从而消除了许多本来需要创建的异常处理程序。前者对于一些通用的接口调用或库方法非常有用，它避免了调用者在每次调用时都要处理异常，而后者则是将异常处理统一收口，比如针对 web 端的响应或接口的最终返回。

异常与软件设计中的许多其他领域一样，您必须确定哪些是重要的，以及哪些是不重要的。不重要的事物应该被隐藏起来，它们越多越好。但是，当某件事很重要时，必须将其暴露出来，比如说封装 rpc 调用接口时，调用失败可以抛出异常，而不是返回 null，否则这会引起很多调用该方法处对结果的判断，而且，调用该接口都是想获取到结果的，如果没有结果值，还是依然需要判断异常来结束请求的处理的。
