# 树莓派官方文档简体中文版 翻译项目

## 关于我们

本项目由树莓派爱好者基地 FreeBSD 子部门和 FreeBSD 中文社区）联合发起。

我们是树莓派爱好者基地的子部门，如有问题请加入 QQ 群 893333927

>目前树莓派爱好者基地的所有大群都无法加入，因为群主已经将群人数降级，原因未知，联系不上。有需要的，请加上面的群。

- 微信公众号: rpicn2025 （扫码关注）

![](./.gitbook/assets/qr.png)

- 微信公众号: 树莓派爱好者基地 （可能已不再更新）

![](./.gitbook/assets/logo1.png)

## 版本说明

当前版本指向 2024.7.10 <https://github.com/raspberrypi/documentation/commit/b68a629c7212e668fdfba94d227cc9ec32d9bfbb>

## 对于想要更新树莓派文档以追踪上游的人的建议

**树莓派官方文档实际上基本上不会变化，只有在每个版本发行后的半年内才会经常变动。如果你看到他有很多提交甚至有几千个，但是实际上他一个字也没动，就是可能把顺序改了。而且每次只改几个字。**

为了对付这种行为对译者的影响，建议你使用以下方法追踪上游更新：

- **原文从哪获取？** 首先，文档原文来源应该来自[官方文档页面](https://www.raspberrypi.com/documentation/)，而非直接对着 [Github](https://github.com/raspberrypi/documentation) 的 adoc 文档进行翻译，那样你是对付不了他的，他一天能提交上百次，你能吗？而且他默认分支是 `develop`，你翻译该分支也是错误的，应该是翻译 `master`，因为根据官方构建指南，官方文档页面是从 `master` 分支生成的。
- **如何追踪或同步上游更新？** 最简单的办法是，直接复制网页，粘贴到 Markdown 软件里，本项目使用的是思源笔记，如果表格错乱，你可以用 Marktext 代替之。对于该操作，Typora、Obsidian 均表现不佳，对于该项目应该优先选用思源笔记，少部分项目必须使用 Marktext 才能达到效果。然后将每个页面存起来，下次需要对比的时候，再次生成覆盖原文即可，在线对比信息会由 Github 自动生成，简单明了。为什么不直接对比 Github adoc 原文？因为他将一个文档每个小节都拆成了单独的 adoc，多达数百个，笔者个人认为这是多余的行为。且不利于他人对树莓派文档进行更新。如果你按原文对比，会发现他提交了几千次更改，但实际上你会发现，他其实一个字也没改。
- **绝不能使用 deepl 进行任何英中翻译** deepl 有一个最大的问题就是 **吞字、吞句**。他会把他不理解的句式或者单词（比如使用了比喻义）直接无视掉。这个问题至少在 3 年前就存在。**而且 deepl 对整句话的翻译往往呈现出相反的意思。** 起码对于树莓派官方文档和 FreeBSD 官方手册来说，都是如此。长文本翻译时，有时甚至会直接把他不理解的句子跳过五六七八个不等，无论网页版还是 API 都是如此。而且对句子的理解意思往往是相反的。这对技术文档来说，是致命性的错误，因为 0 和 1 是对立的，在这里不存在辩证法。
- 本项目基于的 Markdown 英文原文存档位于 <https://github.com/taophilosophy/rpi-documentation-diff/>
- 想要更新本项目，请提出 issue（**请先赞助，没 key 了**）或直接 PR。

## 版权说明

树莓派官方英文文档使用 [Creative Commons Attribution-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/)（CC BY-SA 4.0，署名-相同方式共享 4.0 国际）授权。非常抱歉，根据协议要求，本项目也只能使用 [Creative Commons Attribution-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/)（CC BY-SA 4.0，署名-相同方式共享 4.0 国际）及兼容的协议（兼容协议要求与该协议基本相同）进行授权。该协议要求您：

- 您必须给出适当的署名 ，提供指向本许可协议的链接，同时标明是否（对原始作品）作了修改。树莓派官方英文文档项目位于 <https://github.com/raspberrypi/documentation>。**我们特别授予所有人免于对本项目进行署名及链接的权利。但是您仍然需要遵守[树莓派文档项目](https://github.com/raspberrypi/documentation)本身的许可协议。**
- 相同方式共享 — 如果您再混合、转换或者基于本作品进行创作，您必须基于与原先许可协议相同的许可协议分发您贡献的作品。

>Raspberry Pi documentation is copyright © 2012-2024 Raspberry Pi Ltd and is licensed under a Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA) licence.
>
>Some content originates from the eLinux wiki, and is licensed under a Creative Commons Attribution-ShareAlike 3.0 Unported licence.
>
>The terms HDMI, HDMI High-Definition Multimedia Interface, HDMI trade dress and the HDMI Logos are trademarks or registered trademarks of HDMI Licensing Administrator, Inc
