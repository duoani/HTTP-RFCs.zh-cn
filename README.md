# HTTP 相关的 RFCs 中英文对照

本项目不只是一个单纯对 HTTP RFCs 的翻译，中间夹杂着大量的英文标注和译注，这是出于提高英文水平和 HTTP 学习笔记双重目的的，所以排版看起来会比较混乱一点。

虽说 HTTP/1.1 也不是什么新技术了（HTTP/3 is coming!），但还是应该最为广泛的一个版本，因此，本项目会先从 HTTP/1.1 的现行规范开始翻译。

目前已翻译完成 [RFC7230](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7230.html)，正在翻译 [RFC7231](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7231.html)。

## 翻译计划

- [x] [RFC7230: HTTP/1.1: Message Syntax and Routing](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7230.html)
- [ ] [RFC7231: HTTP/1.1: Semantics and Content](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7231.html)
- [ ] [RFC7232: HTTP/1.1: Conditional Requests](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7232.html)
- [ ] [RFC7233: HTTP/1.1: Range Requests](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7233.html)
- [ ] [RFC7234: HTTP/1.1: Caching](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7234.html)
- [ ] [RFC7235: HTTP/1.1: Authentication](https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7235.html)
- [ ] RFC7260: Hypertext Transfer Protocol Version 2 (HTTP/2)

另外，目前 RFC723* 已有多个堪误表（Errata），目前还未有计划对其进行翻译。如果要查看最新的堪误，[请移步这里](https://datatracker.ietf.org/wg/httpbis/documents/)。

## 初衷

不得不说，基本上计算机领域里绝大部分技术标准都是用英文编写的，但国内技术资料相对比较滞后，看英文文档太吃力？有时也想偷偷懒嘛。但网上基本上能找到的 HTTP/1.1 的完整翻译文档仅限于 RFC2616，要知道，RFC2616 早已经被明确废弃了，即使它的许多内容都被继承到 RFC723* 系列文档中，但还是变动非常大的，包括一些术语、要求等，因此，想看最新的资料就只能看英文了。那于那些英文不太好的人怎么办？

我还是建议还是努力学好英文（但难要开始进入劝退模式了？）但学英文不是一朝一夕的事，有没有一种能够一边学习技术、一边学习英文的好事？我选择的是强制阅读或翻译英文技术文档，这就是本项目诞生的初衷，出于私人目的，嗯嗯。

## 有时我们在不经意地误导人

前段时候我在翻译的时候，经常要到网上对比相关的术语翻译，令我意外的是近一年内发表的很多介绍 HTTP 的文章里都提及到“实体”（Entity）这个术语，这分明就是 RFC2616 的术语，而且那些文章里的很多参考资料都引自被废弃的 RFC2616 。还有就是，现在都 Java 11 了，网上搜一下最近半年内所发表的 JDK 安装教程还在教人设置 `CLASSPATH` 环境变量，你知道吗？早在 Java 5 开始就完全可以不用设置环境变量了。也就是说，*我们在努力学习过期的技术，然后将学到的“新知识”分享给等待学习新知识的新人。*

我也很怕会误导人，所以采用了 *中英文版本*，一段英文，一段译文。译文中还会对必要的词组进行英文标注，以及偶尔在译文后添加本人的（蹩脚的）译注，虽然这样会导致篇幅加倍，但我觉得值得的，毕竟本项目还有一个目的是学英文。

那我们如何能找到最可靠的资料？最简单的办法就是：“找可能找到第一手资料！也就是说，要从最权威的渠道里获取原生资料”，本项目会原文引用H[httpwg.org](https://httpwg.org/specs/) 版本的 RFC，而不是 [tools.ietf.org](https://tools.ietf.org/) 版或者纯文本版本，是因为 httpwg.org 并没有对原文进行强制换行，但内容都是一样的。

## 如何使用？

我会直接转换为 HTML 版本，你可以直接访问：<https://duoani.github.io/HTTP-RFCs.zh-cn/RFC7230.html>

## 如何参与？
额，老实说，这个只是我的个人项目而已，所以我选择了我最喜欢的 [Org mode](https://orgmode.org/) 来进行写作。当然，这不是我任性，实在是 Org mode 太适合于写作了，完爆 Markdown。

But，它是基于 Emacs 的，而 Emacs 的学习曲线...你懂的，反正我断断续续用了几年还是觉得很难驾驭它，所以不是很建议你们提 PR 啦，不过我还是很欢迎你们多提 issue 的。

