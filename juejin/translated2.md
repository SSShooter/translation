> * 原文地址：[Imaginary problems, the root of bad software](https://medium.com/@george3d6/imaginary-problems-d4f2921bd1b8)
> * 原文作者：[George](https://medium.com/@george3d6?source=post_header_lockup)
> * 译文出自：[掘金翻译计划](https://github.com/xitu/gold-miner)
> * 本文永久链接：[https://github.com/xitu/gold-miner/blob/master/TODO1/imaginary-problems.md](https://github.com/xitu/gold-miner/blob/master/TODO1/imaginary-problems.md)
> * 译者：
> * 校对者：

# 想象中的问题，坏软件的根源
# Imaginary problems, the root of bad software

从使用的工具，到团队内部的沟通质量，到开发人员的利益，以及你使用的测试方法，有许多因素可以成为低质量软件的催化剂。

我认为其中最主要的问题是，几乎所有低质量软件的根源：**想象中的问题**。

最复杂或最破碎的软件并非过于复杂或功能失调。它只是为了做其他事情而非其预期目的。
Most complicated or broken software is not designed to be overly complex or dysfunctional. It’s just designed to do something else than its intended purpose.

### 播客应用

假设您是播客主持，想拥有自己的网站，可以在其中销售促销产品，可以不经第三方接广告，最重要的是，向您的观众提供播客，视频和博客文章。

你这个小小的网页应用可能有如下要求：

*   北美地区可以快速加载内容，播客直播与下载。
*   99.99% 的用户在前 15 分钟内不会遇到应用崩溃，当然，最好永远不会发生。
*   与 Google AdWords 较好地集成，有时间的话再接入其他广告商。
*   动态链接到我的 Zazzle 上的最新产品，可以的话，根据用户观看的剧集向用户提供推荐。
*   因为我在 Facebook 做直播，所以要集成 Facebook 直播模块。如果可以自己做出一套直播系统，不依赖于 Facebook，那就更好了。

你把这些要求交给一个承包团队，聊了一下。两个月后，他们向你展示 MVP，你气炸了，你觉得浪费了 15000 美元在一件垃圾上，你只想把你的钱要回来。

这个应用程序生气是很正常的，因为第一次打开它时屏幕会冻结。你问过这个人如何选择允许在网站上运行的广告类型……他指出你是一个丑陋且难以理解的自定义用户界面。在Zazzle上你商品的一半链接被打破或缺少图像，Facebook直播流是滞后的！
It’s normal to get mad at this app, because the first time you open it the screen froze. You asked the guy how to select the type of ads allowed to run on the website… and he pointed you to an ugly and hard to understand custom UI. Half the links to your merchandise on Zazzle are broken or lack an image and the Facebook live stream is laggy !

但开发团队对你的愤怒感到困惑，从他们的角度来看，他们已经为你赴汤蹈火了。
But the dev team is confused at your anger, and rightfully so, from their point of view, they’ve gone to hell and back for you.

他们全心全意地创造了这个应用程序，它有一些惊人的功能：
They’ve put their heart and soul into creating this app, it has some amazing features:

*   最先进的推荐系统。
*   生成所有流的转录本的算法，LIVE（用于前面提到的推荐者）。
*   An algorithm generating the transcript of all your streams, LIVE (for usage in the previously mentioned recommender).
*   世界各地可在 200ms 内加载你的首页。
*   Your front-page loads in sub 200ms times all over the world.
*   流媒体协议和客户端几乎从头开始构建，以防您想从Facebook直播切换。
*   A streaming protocol and client build almost from scratch, in case you want to switch from Facebook live.
*   可让你轻松集成 20 多个广告平台的服务。

问题在于，如果它们很容易实现，您认为您需要一个具有一些额外功能的核心产品。然而，开发团队听到了别的东西。开发团队听说了他们可以解决的一些激动人心的挑战……还有一些无聊的基本功能，他们无法正常测试或关心。
The problem, is that you thought you requested a core product, with some extra features, if they were easy enough to implement. The dev team, however, heard something else. The dev team heard about some exciting challenges they could work on…. and a slew of boring, basic features they couldn’t be bothered to test properly or care about.

更糟糕的是，你没有直接与开发者沟通，你通过中国人的低语传播。你跟一个销售人员谈过，后者与一些中层管理人员会面，然后编写了一些业务规范并将它们交给了PM，后者编写了一些技术规范并将它们交给了团队负责人/架构师，后者开始设计产品与他的团队。他们中的每一个，都有点扭曲。
Even worse, you didn’t communicate directly with the devs, you communicated through a game of Chinese whispers. You spoke to a sales guy, which held a meeting with some middle management chap, which then wrote some business specs and gave them to a PM, which wrote some technical specs and gave them to a team lead/architect, which then started designing the product with his team. Every single one of them, put a bit of a twist on it.

### 这是一种应对机制

想象问题通常比实际问题更好玩。天才喜欢玩竞技游戏，构建和解决数学问题，甚至编写试图回答有关人类状况这种抽象问题的书籍，所有这些都是免费的。不过，一般程序员可能会向您收取相当数量的费用，为你构建一个相对简单的 Android 应用。这不是因为平庸的程序员比天才更难找到，只是因为前者做的事情都很有趣，后者可能会相当无聊。

大多数程序员希望获得报酬并同时获得乐趣。但是，对大多数人来说，这可能相当困难。当然，对于我们大多数人来说，“乐趣”的定义是完全不同的，但对于许多工程师来说，“乐趣”可以归结为，可解决性范围内，有趣并具有挑战性的问题。

你给一个有点头脑的人一堆不能自动化完成的无聊任务，他们迟早会被逼疯。不过经历了数十亿年的进化，人类大脑在保持理智方面非常有才能。就像童年困难或虐待的受害者可以在童话书中得到解脱，企业编程或自由网络开发的受害者可以在解决 想象中的问题 中得到解脱。

![](https://cdn-images-1.medium.com/max/1000/1*8jPa3TYWKxx2PU5A87_4Xg.png)

软件工程师为自己创造的想象问题的数量，与他们的想象力和他们应该解决的实际问题的难度有关。

我们应该意识到，这个问题并不是开发人员所独有的。管理，销售，HR，顾问，法务甚至会计都有自己独特的方式来创造想象中的问题。当他们出席会议只是一种形式或根本没有要求时，他们试图让自己更多地参与决策。他们会过分强调与他们角色有关的问题（例如：我们的狗狗日托 App 必须从上线第 1 天 101% 符合 GDPR，我们不能等待法律先例）。尽管没有必要，他们还是雇用了一个大团队处理这个问题，这么做显得他们很重要，并且有在办事。

许多人都很聪明，但很多问题都是愚蠢的，所以聪明人总能找到**一种应对方式**。
Many individuals are intelligent, but many problems are dumb, so intelligent individuals will find a **way of coping**.

### 传话驱动式设计

但想象中的问题不仅仅是开发人员太无聊的结果，也是沟通链太长的结果。

我偶尔会接一些外包，以前不能自己选择客户，这就意味着我甚至可能会在工作中遇到 DID 和 ADHD 病例。我曾收发了 100 多封邮件，讨论内部 MVP 里微不足道的细节，曾遇到让人在一周内把项目中的每一个需求都改了个遍的情况，曾有客户问过诸如“这可以发行虚拟货币吗？”或“我们可以在这里加人工智能吗？”等问题。

当然，大多数客户还是理智的，但他们往往因为缺乏相关知识，无法清晰表达他们的需求。但这没问题，因为这是我“计算机专业人员”工作的一部分，帮助人们根据他们的使用场景，判断他们的软件需要或不需要什么。但是当你和客户之间隔着很多人，这样做会变得十分困难。

大多数公司喜欢雇佣销售人员安利潜在客户，协商价格并概述这个价格可以得到什么功能。他们有 [people person](https://www.youtube.com/watch?v=hNuu9CpdjIo) 与客户讨论更多深度要求和细节，其实他们也算是销售人员，只是职位名称不同。接着是内部领导层的意见，多级管理层以及技术团队内部的层级结构。

需求经历这么多人，即使这些人有最好的意图，一些事情也会发生变化。有些事情可能会因为没有意义而改变，因为定义是愚蠢的，所以需要重新定义。销售人员可能会说“只要多付 39999，我们就可以在区块链上实现这个功能”……让其他所有人都明白了“在区块链上做什么”的意思。
When requirements go through so many people, even if those people have the best of intentions, some things will get changed. Some things might get changed because they make no sense, they need to be redefined because the definition is stupid. The sales guy might have said “For only 39,999 extra we can do this on the Blockchain”… leaving everyone else down the line of define what the hell “doing it on the Blockchain” means.

所以通常需求变化的原因有两点，在多级传递中有人误解了某些事情，或者有人使用上述应对机制来使他或团队的工作更有趣和令人印象深刻。

因此，真正要求，必须解决的真正问题，在各级传达中丢失。并被假想的问题和一些空缺所取代，你已经有很多人准备并愿意用他们自己想象的问题填补这些空白，因为他们必须解决的问题很无聊，并填补空白给他们一个**应对方式**。
So the original requirements, the real problems that have to be solved, get lost in transcription. They are replaced with imaginary problems and with voids, and you’ve got plenty of people ready and willing to fill those voids with their own imaginary problems, because the problems they have to solve are boring, and filling the voids gives them a **way of coping**.

### 过度复杂和自然选择
### Overcomplexity and natural selection

通常情况下，存在虚构问题更深层的原因是，它们有助于团队或公司的成长，并成为其功能中不可或缺的一部分。
Often enough, there’s an even darker reason for the existence of imaginary problems, they help a team or a company grow and they become an integral part of its function.

> 培养，选择和补偿以找到复杂解决方案的人没有动力去实施简化的解决方案。 - 塔勒布
> People who are bred, selected and compensated to find complicated solutions do not have an incentive to implement simplified ones. — Taleb

您是否听说过，只需要三位工程师就能搭建网上银行系统？他们使用功能设计方法和内存安全语言，从头开发了一些完美无瑕的银行软件，然后开始将主要银行迁移到他们惊人的基础设施。
Have you ever heard about those three engineers that figured out online banking is actually quite an easy problem ? They developed some flawless banking software from scratch, using a functional design methodology and memory safe languages, then started migrating major banks to their amazing infrastructure.

可能没听过，因为根本不存在。然而，有成千上万的团队[成千上万的开发人员，无法掌握简单的概念，如“回滚”]（https://www.theguardian.com/business/2018/apr/28/warning-signs-for- tsbs-it-meltdown-a-a-year-ago-insider），无休止地创建银行软件。
Probably not, because they don’t exist. There are however, plenty of teams of [thousands of developers, that are unable to grasp simple concepts such “rollbacks”](https://www.theguardian.com/business/2018/apr/28/warning-signs-for-tsbs-it-meltdown-were-clear-a-year-ago-insider), perpetually creating banking software.

数字的存储和传输的技术要求并不高。建立整个互联网的索引，在 2 秒内提供问题搜索结果才是一个难题，[只有少数聪明人去想方设法解决这个问题](https://en.wikipedia.org/wiki/History_of_Google)。

不，问题是银行生态系统已经变得非常善于保持无人机存活。一台运行良好的机器意味着保留自己的钱财等级。它的领导者是[腐败的浸出]（https://en.wikipedia.org/wiki/Ben_Bernanke），它掠夺社会，但组织中的领导者只是其成员的一个症状。
No, the problems is that the banking ecosystem has become really good at keeping its drones alive. A well oiled machine meant to preserve its own money grabbing hierarchy. Its leaders are [corrupt leaches](https://en.wikipedia.org/wiki/Ben_Bernanke) that prey on society, but the leaders in an organizations are just a symptom of its members.

我的意思不是在银行工作的人都是坏人。相反，他们通常是很友善，致力于为家人提高生活质量。但他们要的不是修复银行软件，而是保持就业。在今天的经济中失去工作对某些人来说并不是一件令人开玩笑的事情......一个大嘴巴或太多的主动性很容易让你发现自己在银行业的纪律委员会面前。
I wouldn’t suggest most underling working for banks are evil or malicious in any way. Far from it, they are usually friendly lads, working to provide food, shelter and an education for their families. But their chief incentive is not fixing the banking software, their chief incentive is staying employed. Losing your job in today’s economy is no joking matter for some… and a big mouth or too much initiative is an easy way find yourself in front of a disciplinary committee in the banking industry.

所以银行业仍然是相同的，不是因为它有效，而是因为它有惯性。这种惯性以处理想象问题的形式出现，以避免解决实际问题。曾经指出的真正的问题会威胁到其他人的工作。这可能会导致你被解雇，或者像高盛这样一些特别令人讨厌的“机构”，[给一些联邦调查局官员发送一些棕色信封，毁掉你的整个生命或让你做出一个奇怪的自杀。 ]（https://en.wikipedia.org/wiki/Sergey_Aleynikov）
So banking remains the same not because it’s efficient, but because it has inertia. This inertia comes in the form of working on imaginary problems in order to avoid fixing real problems. Real problems which, once pointed out, would threaten the jobs of other people. Which may well lead to you getting fired, or in the case of some particularly nasty “institutions” like Goldman Sachs, [getting a few brown envelopes sent to a few FBI officers and ruining your whole life or getting you to commit a strange suicide.](https://en.wikipedia.org/wiki/Sergey_Aleynikov)

> **当他的工资取决于他的不理解时，很难让一个人理解某些东西！**  -  Upton Sinclair
> **It is difficult to get a man to understand something, when his salary depends upon his not understanding it!** — Upton Sinclair

高级管理人员忽略了这样一个事实，即他们的高层管理人员将90％的时间花在涉及热带岛屿的“客户会议”和“其他费用”的百万美元预算上。因为高层管理人员对他们的上级腐败视而不见。
The C-suite ignores the fact that their upper management spends 90% of their time on “client meetings” that involve tropical islands and million dollar budgets for “other expenses”. Because upper management tuns a blind eye to their superior’s corruption.

高层管理人员忽视了中层管理人员购买古怪的办公室，并雇佣了三名秘书和十几名实习生。因为中层管理人员鼓励他们生活在他们的华尔街狼幻想中。
The upper management ignores middle managers buying eccentric offices and hiring themselves three secretaries and a dozen interns. Because middle management encourages them to live in their Wolf of Wall Street fantasy.

中层管理人员忽略了这样一个事实，即直线经理将时间花在关于“改进我们的敏捷方法”而非降低成本的电源点演示上。因为线路管理不抱怨他们的小独裁权力幻想。
Middle management ignores the fact that line managers spend their time working on power point presentations about “Improving our Agile methodology” instead of cutting costs. Because line management doesn’t complain about their little dictatorial power fantasy.

直线经理忽略了团队领导和架构师谈论“使用JRPC和使用Hibernate和Spring的微服务之间的下一代系统接口”......而不是让那些血腥的Mysql查询花费不到一天的时间。因为团队负责人似乎并没有注意到他们的上司甚至不能正确使用Excel并且每隔几周才能到办公室。
Line managers ignore the team leads and architects talking about “Next generation interfacing between our systems using JRPC and microserviceization using Hibernate and Spring”… instead of getting those bloody Mysql queries to take less than a day. Because the team leads don’t seem to notice the fact that their superiors can’t even use Excel properly and only hit the office every few weeks.

团队负责人不会抱怨他们的开发人员使用新的JS框架在当年第10次重新设计UI，而不是查看EXPLAIN以获得上述慢速查询。因为开发人员似乎没有注意到他们的潜在客户并没有真正编写除DOT图之外的任何代码。
Team leads don’t complain about their developers re-designing the UI for the 10th time that year using a new JS framework, instead of looking at an EXPLAIN for the aforementioned slow query. Because the developers don’t seem to notice their leads don’t really write any code except DOT diagrams.

这是一个解决想象问题的恶性循环，从没有意识到窃取另外3000万人的CEO不会让他的父亲爱他。对于未实现使用Angular-Material-Boostrap 19.13.5重新设计“提交”按钮的UX实习生，不会使他们以纯文本形式存储密码（并将其作为auth cookie的一部分使用）远。
It’s a vicious cycle of solving imaginary problems, from the CEO that doesn’t realize stealing another 30 million won’t make his dad love him. To the UX intern that doesn’t realize redesigning the “submit” button using Angular-Material-Boostrap 19.13.5, won’t make the fact that they store passwords in plain text (and use them as part of the auth cookie) go away.

但每个人都需要不断解决想象中的问题，因为如果他们停下来，如果他们开始关注真正的问题，他们可能会意识到整个系统都被打破了。他们可能会意识到Debra已经坐在那个角落，盯着内部服务器农场的正常运行时间图表10年，尽管该公司5年前搬到了AWS。他们可能会意识到他们99％的工作就是让别人的工作永久存在......这是一个很难实现的东西，对于大多数人来说是不可能的，我敢说，所以他们找到了一种应对方式**。
But everyone needs to keep solving the imaginary problems, because if they stop, if they start focusing on the real problems, they might realize the whole system is broken. They might realize Debra has been sitting in that corner, staring at uptime graphs of the internal server farm for 10 years, despite the fact the company moved to AWS 5 years ago. They might realize 99% of their job is to perpetuate the existence of someone else’s job… and that’s a hard realization to take in, an impossible one for most, I dare say, so they find a **way of coping**.

> 如果发现译文存在错误或其他需要改进的地方，欢迎到 [掘金翻译计划](https://github.com/xitu/gold-miner) 对译文进行修改并 PR，也可获得相应奖励积分。文章开头的 **本文永久链接** 即为本文在 GitHub 上的 MarkDown 链接。


---

> [掘金翻译计划](https://github.com/xitu/gold-miner) 是一个翻译优质互联网技术文章的社区，文章来源为 [掘金](https://juejin.im) 上的英文分享文章。内容覆盖 [Android](https://github.com/xitu/gold-miner#android)、[iOS](https://github.com/xitu/gold-miner#ios)、[前端](https://github.com/xitu/gold-miner#前端)、[后端](https://github.com/xitu/gold-miner#后端)、[区块链](https://github.com/xitu/gold-miner#区块链)、[产品](https://github.com/xitu/gold-miner#产品)、[设计](https://github.com/xitu/gold-miner#设计)、[人工智能](https://github.com/xitu/gold-miner#人工智能)等领域，想要查看更多优质译文请持续关注 [掘金翻译计划](https://github.com/xitu/gold-miner)、[官方微博](http://weibo.com/juejinfanyi)、[知乎专栏](https://zhuanlan.zhihu.com/juejinfanyi)。

