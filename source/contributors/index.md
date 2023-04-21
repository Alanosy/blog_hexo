---
layout: wiki
wiki: Stellar
order: 1050
title: 开发者和社区支持
---

{% tabs align:left %}

<!-- tab 开发者 -->
{% users api:https://api.github.xaox.cc/repos/xaoxuu/hexo-theme-stellar/contributors?per_page=100&direction=asc %}

<!-- tab 点赞支持者 -->
{% quot icon:hashtag 1-100 %}
{% users api:https://api.github.xaox.cc/repos/xaoxuu/hexo-theme-stellar/stargazers?per_page=100&page=1 %}
{% quot icon:hashtag 101-200 %}
{% users api:https://api.github.xaox.cc/repos/xaoxuu/hexo-theme-stellar/stargazers?per_page=100&page=2 %}
{% quot icon:hashtag 201-300 %}
{% users api:https://api.github.xaox.cc/repos/xaoxuu/hexo-theme-stellar/stargazers?per_page=100&page=3 %}
{% quot icon:hashtag 301-400 %}
{% users api:https://api.github.xaox.cc/repos/xaoxuu/hexo-theme-stellar/stargazers?per_page=100&page=4 %}

{% endtabs %}

{% image https://starchart.cc/xaoxuu/hexo-theme-stellar.svg %}

{% quot icon:hashtag 如何加入社区 %}

社区建设主要包括以下几个方面：

- [Issues](https://github.com/xaoxuu/hexo-theme-stellar/issues) 技术问题答疑、BUG反馈
- [Discussions](https://github.com/xaoxuu/hexo-theme-stellar/discussions) 论坛、相关话题讨论
- [文档](https://github.com/xaoxuu/hexo-theme-stellar-docs) 维护
- [探索号](https://xaoxuu.com/wiki/stellar/articles/) 文章收录
- QQ群：1146399464，验证码：{% psw vlts-2021 %}（以聊天为主，技术问题未必跟进。）

> 无论在什么渠道，学习并掌握 [提问的智慧(24k Stars)](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way/blob/main/README-zh_CN.md) 可以方便大家更高效地帮你解决问题。

{% grid %}
<!-- cell left -->
{% ablock color:red %}
**错误的提问**
<hr>

- XXX 功能怎么用？（文档有详细描述）
- 这个功能怎么用不了啊（不说明自己操作了什么，也不展示实际效果）
- 我怎么跑不起来，能帮我看看吗？（什么也不尝试，直接丢项目代码）
- 怎么报错了呢？（不贴或只贴极少部分的出错提示）
- 这个代码怎么改（扔过来一大段代码）
- XXX 什么意思？（没有经过任何搜索）

{% endablock %}
<!-- cell right -->
{% ablock color:green %}
**正确的提问**
<hr>

- 我这里遇到了一个问题：【问题描述】，我经过了以下尝试：【思路细节】，不能得到解决，报错如下：【报错截图/线上预览地址/仓库源代码地址】，请问该怎么解决？
- 我不太理解【某处】里的【某处】，我的理解是这样的：【思路细节】，对吗？
- 我查看了文档的【某处】，并尝试【做法】，但是没有得到【预想效果】，正确的做法应该是什么？

{% endablock %}
{% endgrid %}
