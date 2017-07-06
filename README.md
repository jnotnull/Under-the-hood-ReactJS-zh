# Under the hood: ReactJS
# ReactJS引擎解密

<em> This repository contains an explanation of inner work of ReactJS. In fact, I was debugging through the entire code base and put all the logic on visual block-schemes, analyzed them, summarized and explained main concepts and approaches. I've already finished with Stack version and now I work with the next, Fiber version.  </em>

<em> 该知识库讲解了ReactJS内部原理. 事实上，我是在调试了所有代码的基础上才把所有的逻辑画成图，然后分析总结，从而进行解释它的主要概念和方法。基于Stack的版本已经完成，现在正在研究下一代Fiber版本。</em>

>> Read in the best format from [github-pages website](https://bogdan-lyashenko.github.io/Under-the-hood-ReactJS/).

>> 你也可以访问这里进行阅读 [github-pages website](https://bogdan-lyashenko.github.io/Under-the-hood-ReactJS/).

> Feel free to open an issue regarding any ideas you have to make it better.

> 如果你发现有啥问题，或者有更好的建议，欢迎提issue.

Each scheme is clickable and can be opened in a new tab, use that to zoom it and be able to read from it. Keep the article and a scheme you are reading about at that moment in separate windows (tabs), that will help to match text and code flow easier.

每幅图都可以点击，点击后会在另一个窗口在打开，为了方便阅读，你可以进行缩放。文章和图放在两个tab中会有助你阅读。

We are gonna talk here about both ReactJS versions, current one with Stack reconciler and the next one with Fiber (as you probably know, the next version of ReactJS will be released soon), so, you can understand better how current React works and appreciate huge achievements on React-Fiber.  We use React v15.4.2 for explaining how ‘legacy React’ works and React v16.*.*** for ‘Fiber’. Let’s start from old (I have fun to say that) stack version.

我们这里讨论的都是关于ReactJS的版本，当前是Stack，下一个将会是Fiber。这样你就不仅能够知道当前React是如何工作的，还能了解React-Fiber的基础架构。我们使用15.4.2版本来解释老版本React如何工作的，以及16.*.***版本的Fiber。现在让我们从stack版本开始吧。


## Stack reconciler
[![](./stack/images/intro/all-page-stack-reconciler-25-scale.jpg)](./stack/images/intro/all-page-stack-reconciler.svg)

The entire scheme is divided into 15 parts, let's get started.

这幅整图被切分为15个部分。

* [Intro](./stack/book/Intro.md)
* [Part 0](./stack/book/Part-0.md)
* [Part 1](./stack/book/Part-1.md)
* [Part 2](./stack/book/Part-2.md)
* [Part 3](./stack/book/Part-3.md)
* [Part 4](./stack/book/Part-4.md)
* [Part 5](./stack/book/Part-5.md)
* [Part 6](./stack/book/Part-6.md)
* [Part 7](./stack/book/Part-7.md)
* [Part 8](./stack/book/Part-8.md)
* [Part 9](./stack/book/Part-9.md)
* [Part 10](./stack/book/Part-10.md)
* [Part 11](./stack/book/Part-11.md)
* [Part 12](./stack/book/Part-12.md)
* [Part 13](./stack/book/Part-13.md)
* [Part 14](./stack/book/Part-14.md)



## Fiber
1. [Intro](./fiber/book/Intro.md) [TODO]
