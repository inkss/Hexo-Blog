---
layout: docs 
title: Volantis 主题用户手册 
seo_title: Volantis 主题用户手册 
sidebar: [nextsite, wiki-hexo-theme, toc] 
top_meta: [] 
bottom_meta: [] 
sitemap: false
---

<p class="p center logo large">Volantis 主题用户手册<em><sup>自用</sup></em></p>

## 一、Front-matter

{% folding yellow, front-matter %}

| 字段        | 含义          |   值类型    |            值             | 备注                           |
| :---------- | :------------ | :---------: | :-----------------------: | :----------------------------- |
| layout      | 页面布局模版  |   String    |      post,page,docs       | 独立页面,文章页面,文档页面     |
| title       | 页面标题      |   String    |             -             |                                |
| seo_title   | 网页标题      |   String    |        page.title         | **与 title 共同存在时，不显示标题**|
| date        | 创建时间      |    Date     |       文件创建时间        |                                |
| updated     | 更新日期      |    Date     |       文件修改时间        |                                |
| link        | 外部文章网址  |   String    |             -             | 去源站阅读                     |
| music       | 内部音乐控件  |  [Object]   |             -             |                                |
| keywords    | 文章关键词    |   String    |             -             |                                |
| description | 文章摘要      |   String    |             -             |                                |
| cover       | 是否显示封面  |    Bool     |           true            | 强制指定时可以覆盖主题封面配置 |
| top_meta    | 是否显示 meta |    Bool     |           true            | 顶部 meta 信息                 |
| bottom_meta | 是否显示 meta |    Bool     |           true            | 底部 meta 信息                 |
| comments | 是否显示评论 | Bool | true |  |
| archive | 是否归档 | Bool | true | 是否出现在归档页 |
| sidebar     | 页面侧边栏    | Bool, Array | sidebar.for_page/for_post | 手动指定侧边栏                 |
| mathjax     | 是否渲染公式  |    Bool     |           false           |                                |
| thumbnail   | 缩略图        |   String    |           false           | 显示在文章页右上角             |
| icons       | 图标          |    Array    |            []             | 显示在归档页                   |
| pin         | 是否置顶      |    Bool     |           false           |                                |
| headimg     | 文章头图      |     url     |             -             | **目前修改为只在列表页显示**   |
| indent      | 是否首行缩进  |    Bool     |           false           | **自定义修改：缩进 2 字符**    |
| references | 参考资料 | Array | - | {title: xxx, url: xxx} |

{% endfolding %}

{% folding yellow, 新建文章模板 %}

```yml 新建文章模板
title: 文章名称 
seo_title: seo名称 
toc: true            # 是否生成目录 
indent: true         # 是否首行缩进 
comments: true       # 是否允许评论 
archive: true        # 是否显示在归档 
cover: false         # 是否显示封面 
mathjax: false       # 是否渲染公式 
pin: false           # 是否首页置顶 
top_meta: false      # 是否显示顶部信息 
bottom_meta: false   # 是否显示尾部信息 
sidebar: [toc] 
tag: 
  - 标签一 
  - 标签二 
categories: 分组 
keywords: 文章关键词 
date: 2021-13-13 00:00 
updated: 2021-13-13 00:00 
description: 文章摘要 
icons: [fas fa-fire red, fas fa-star green] 
references: 
  - title: 参考资料名称 
    url: https://参考资料地址 
headimg: https://文章头图 
thumbnail: https://右侧缩略图 
```

{% endfolding %}

## 二、标签插件

### 1. 行内标签

{% folding blue, text %}

{% tabs text %}
<!-- tab 效果 -->

带 {% u 下划线 %} 的文本；带 {% emp 着重号 %} 的文本；带 {% wavy 波浪线 %} 的文本；带 {% del 删除线 %} 的文本

键盘样式的文本：{% kbd ⌘ %} + {% kbd D %}

密码样式的文本：{% psw 这里没有验证码 %}

密文样式的文本：{% bb 真的没有啊喵, 这里没有验证码 %}

<!-- endtab -->
<!-- tab 源码 -->
```md
带 {% u 下划线 %} 的文本；带 {% emp 着重号 %} 的文本；带 {% wavy 波浪线 %} 的文本；带 {% del 删除线 %} 的文本 
 
键盘样式的文本：{% kbd ⌘ %} + {% kbd D %} 
 
密码样式的文本：{% psw 这里没有验证码 %} 
 
密文样式的文本：{% bb 真的没有啊喵, 这里没有验证码 %} 
```
<!-- endtab -->
{% endtabs %}

{% endfolding %}

{% folding yellow, span %}

{% tabs span %}
<!-- tab 效果 -->
各种颜色的标签，包括：{% span red, 红色 %}、{% span yellow, 黄色 %}、{% span green, 绿色 %}、{% span cyan, 青色 %}、{% span blue, 蓝色 %}、{% span gray, 灰色 %}。

超大号文字：

{% span center logo large, Volantis %}

{% span center small, A Wonderful Theme for Hexo %}

<!-- endtab -->

<!-- tab 源码 -->
```md
各种颜色的标签，包括：{% span red, 红色 %}、{% span yellow, 黄色 %}、{% span green, 绿色 %}、{% span cyan, 青色 %}、{% span blue, 蓝色 %}、{% span gray, 灰色 %}。 
 
超大号文字： 
 
{% span center logo large, Volantis %} 
 
{% span center small, A Wonderful Theme for Hexo %} 
 
```
<!-- endtab -->

<!-- tab 参数 -->

|   属性   | 可选值                                                    |
| :------: | --------------------------------------------------------- |
|   字体   | `logo`, `code`                                            |
|   颜色   | `red`, `yellow`, `green`, `cyan`, `blue`, `gray`          |
|   大小   | `small`, `h4`, `h3`, `h2`, `h1`, `large`, `huge`, `ultra` |
| 对齐方向 | `left`, `center`, `right`                                 |

<!-- endtab -->
{% endtabs %}

{% endfolding %}

{% folding red, p %}

{% tabs p %}
<!-- tab 效果 -->
{% p center logo large, Volantis %}
{% p center small, A Wonderful Theme for Hexo %}
<!-- endtab -->
<!-- tab 源码 -->
```md
{% p center logo large, Volantis %} 
{% p center small, A Wonderful Theme for Hexo %} 
```
<!-- endtab -->
<!-- tab 参数 -->
{% p center code blue large, “与 span 参数相同”  %}
<!-- endtab -->
<!-- tab 额外 -->

<p class="p center logo large"><em>Volantis 主题用户手册 <sup>自用</sup></em></p>

{% codeblock lang:markdown 上文所对应源码 line_number:false  %}
<p class="p center logo large"><em>Volantis 主题用户手册 <sup>自用</sup></em></p>
{% endcodeblock %}
<!-- endtab -->
{% endtabs %}

{% endfolding %}

### 2. 增强标签

#### 2.1 图片 image

```md 单个图片应用场景的标签
{% image 链接, width=宽度（可选）, height=高度（可选）, alt=描述（可选）, bg=占位颜色（可选） %} 
 
PS: 为了兼顾暗黑模式占位颜色可使用 bg=var(--color-card) 的形式（#ffffff/#282c34） 
```

#### 2.2 画廊 gallery

```md 一组图片应用场景的标签
{% gallery 参数, 列数 %} 
![图片描述](https://xxx1) 
![图片描述](https://xxx2) 
{% endgallery %} 
```

#### 2.3 音频 audio

```md 可以加载并渲染音频的标签
{% audio https://github.com/volantis-x/volantis-docs/releases/download/assets/Lumia1020.mp3 %} 
```

### 3. 增强功能

#### 时间线 timeline

{% folding red, timeline %}

{% tabs timeline %}
<!-- tab 效果 -->

{% timeline 时间线标题（可选） %}

{% timenode 时间节点（标题） %}

正文内容

{% endtimenode %}

{% timenode 时间节点（标题） %}

正文内容

{% endtimenode %}

{% endtimeline %}

<!-- endtab -->
<!-- tab 源码 -->

```md 最后更新于 <u>3.0</u> 版本
{% timeline 时间线标题（可选） %} 
 
{% timenode 时间节点（标题） %} 
 
正文内容 
 
{% endtimenode %} 
 
{% timenode 时间节点（标题） %} 
 
正文内容 
 
{% endtimenode %} 
 
{% endtimeline %} 
```
<!-- endtab -->
<!-- tab 额外 -->

{% timelines '一个自制时间线（标题可选）' %}

{% timenodes fal fa-bat %} 2021/13/32 巴啦啦小魔仙。{% endtimenodes %}
{% timenodes fal fa-glass-cheers %} 2021/13/16 好好学习，天天向上。 {% endtimenodes %}
{% timenodes fal fa-genderless %} 2021/13/15 风声雨声读书声声声入耳，国事家事天下事事事关心。 {% endtimenodes %}
{% timenodes fal fa-narwhal %} 2021/13/10 楼主以屎，有事烧纸。 {% endtimenodes %}
{% timenodes fal fa-genderless %} 2021/13/08 那么就可以有星期八了。 {% endtimenodes %}
{% timenodes fal fa-genderless %} 2021/13/01 是的没错，这里是 13 月。 {% endtimenodes %}
{% timenodes fal fa-fan fa-spin %}这里是时间线的起点~{% endtimenodes %}

{% endtimelines %}

```md 自制标签
{% timelines '一个自制时间线（标题可选）' %} 
 
{% timenodes fal fa-bat %} 2021/13/32 巴啦啦小魔仙。{% endtimenodes %} 
{% timenodes fal fa-glass-cheers %} 2021/13/16 好好学习，天天向上。 {% endtimenodes %} 
{% timenodes fal fa-genderless %} 2021/13/15 风声雨声读书声声声入耳，国事家事天下事事事关心。 {% endtimenodes %} 
{% timenodes fal fa-narwhal %} 2021/13/10 楼主以屎，有事烧纸。 {% endtimenodes %} 
{% timenodes fal fa-genderless %} 2021/13/08 那么就可以有星期八了。 {% endtimenodes %} 
{% timenodes fal fa-genderless %} 2021/13/01 是的没错，这里是 13 月。 {% endtimenodes %} 
{% timenodes fal fa-fan fa-spin %}这里是时间线的起点~{% endtimenodes %} 
 
{% endtimelines %} 
```
<!-- endtab -->
{% endtabs %}

{% endfolding %}

#### 引用块 note/blocknote

{% folding yellow, note/blocknote %}

{% tabs note %}
<!-- tab 效果 -->

{% note info, *blocknote* 比 *note* 多出了显示标题的能力 %}

{% blocknote quote, 《寻隐者不遇》 %}
松下问童子，言师采药去。
只在此山中，云深不知处。
{% endblocknote %}

<!-- endtab -->
{% endtabs %}

{% endfolding %}

#### 链接 link

{% folding blue, link %}

{% tabs link %}

<!-- tab 效果 -->

{% link 如何参与项目, https://volantis.js.org/contributors/, https://cdn.jsdelivr.net/gh/xaoxuu/cdn-assets@master/logo/256/safari.png %}

<!-- endtab -->

{% endtabs %}

{% endfolding %}

## 三、表情包

{% folding, emoji %}

| 代码                     |            效果             | 代码                   |           效果            | 代码                      |             效果             |
| ------------------------ | :-------------------------: | ---------------------- | :-----------------------: | ------------------------- | :--------------------------: |
| `{% emoji youling %}`    |  {% emoji youling %} 幽灵   | `{% emoji bizui %}`    |  {% emoji bizui %} 闭嘴   | `{% emoji baiyan %}`      |   {% emoji baiyan %} 白眼    |
| `{% emoji aixin %}`      |   {% emoji aixin %} 爱心    | `{% emoji dajing %}`   |  {% emoji dajing %} 大惊  | `{% emoji ziya %}`        |    {% emoji ziya %} 呲牙     |
| `{% emoji daxiao %}`     |   {% emoji daxiao %} 大笑   | `{% emoji esi %}`      |   {% emoji esi %} 饿死    | `{% emoji fadai %}`       |    {% emoji fadai %} 发呆    |
| `{% emoji fankun %}`     |   {% emoji fankun %} 犯困   | `{% emoji ganga %}`    |  {% emoji ganga %} 尴尬   | `{% emoji fennu %}`       |    {% emoji fennu %} 愤怒    |
| `{% emoji hanyan %}`     |   {% emoji hanyan %} 汗颜   | `{% emoji guaiwu %}`   |  {% emoji guaiwu %} 怪物  | `{% emoji haochi %}`      |   {% emoji haochi %} 好吃    |
| `{% emoji emo %}`        |    {% emoji emo %} 恶魔     | `{% emoji renzhe %}`   |  {% emoji renzhe %} 忍者  | `{% emoji jingya %}`      |   {% emoji jingya %} 惊讶    |
| `{% emoji kaixin %}`     |   {% emoji kaixin %} 开心   | `{% emoji lengku %}`   |  {% emoji lengku %} 冷酷  | `{% emoji danao %}`       |    {% emoji danao %} 大闹    |
| `{% emoji feiwen %}`     |   {% emoji feiwen %} 飞吻   | `{% emoji liulei %}`   |  {% emoji liulei %} 流泪  | `{% emoji mengbi %}`      |   {% emoji mengbi %} 懵逼    |
| `{% emoji bianbian %}`   |  {% emoji bianbian %} 便便  | `{% emoji nanguo %}`   |  {% emoji nanguo %} 难过  | `{% emoji shuizhuo %}`    |  {% emoji shuizhuo %} 睡着   |
| `{% emoji xiaochulei %}` | {% emoji xiaochulei %} 笑哭 | `{% emoji jingkong %}` | {% emoji jingkong %} 惊恐 | `{% emoji santiaoxian %}` | {% emoji santiaoxian %} 尴尬 |
| `{% emoji tiaopi %}`     |   {% emoji tiaopi %} 调皮   | `{% emoji ganmao %}`   |  {% emoji ganmao %} 感冒  | `{% emoji wuliao %}`      |   {% emoji wuliao %} 无聊    |
| `{% emoji fankun1 %}`    |  {% emoji fankun1 %} 犯困   | `{% emoji xieyan %}`   |  {% emoji xieyan %} 斜眼  | `{% emoji xiasi %}`       |    {% emoji xiasi %} 吓死    |
| `{% emoji xiaolian %}`   |  {% emoji xiaolian %} 笑脸  | `{% emoji huaixiao %}` | {% emoji huaixiao %} 坏笑 | `{% emoji shengqi %}`     |   {% emoji shengqi %} 生气   |
| `{% emoji liuhan %}`     |   {% emoji liuhan %} 流汗   | `{% emoji outu %}`     |   {% emoji outu %} 呕吐   | `{% emoji keshui %}`      |   {% emoji keshui %} 瞌睡    |
| `{% emoji tianshi %}`    |  {% emoji tianshi %} 天使   | `{% emoji xianwen %}`  | {% emoji xianwen %} 献吻  | `{% emoji yiwen %}`       |    {% emoji yiwen %} 疑问    |
| `{% emoji shimo %}`      |   {% emoji shimo %} 什么    | `{% emoji dianzan %}`  | {% emoji dianzan %} 点赞  | `{% emoji biti %}`        |    {% emoji biti %} 鼻涕     |
| `{% emoji fendou %}`     |   {% emoji fendou %} 奋斗   | `{% emoji huqi %}`     |   {% emoji huqi %} 呼气   | `{% emoji kulou %}`       |    {% emoji kulou %} 骷髅    |
| `{% emoji tanchi %}`     |   {% emoji tanchi %} 贪吃   | `{% emoji shuixing %}` | {% emoji shuixing %} 睡醒 | `{% emoji aini %}`        |    {% emoji aini %} 爱你     |
| `{% emoji aixin1 %}`     |   {% emoji aixin1 %} 爱心   | `{% emoji zhadan %}`   |  {% emoji zhadan %} 炸弹  | `{% emoji xinsui %}`      |   {% emoji xinsui %} 心碎    |
| `{% emoji maren %}`      |   {% emoji maren %} 骂人    | `{% emoji zhutou %}`   |  {% emoji zhutou %} 猪头  | `{% emoji qie %}`         |     {% emoji qie %} 企鹅     |
| `{% emoji shoushang %}`  | {% emoji shoushang %} 受伤  | `{% emoji jingsong %}` | {% emoji jingsong %} 惊悚 | `{% emoji taoyan %}`      |   {% emoji taoyan %} 讨厌    |

| 代码                         |                效果                 | 代码                    |             效果             | 代码                |         效果         |
| ---------------------------- | :---------------------------------: | ----------------------- | :--------------------------: | ------------------- | :------------------: |
| `{% emoji mianwubiaoqing %}` | {% emoji mianwubiaoqing %} 面无表情 | `{% emoji bushufu %}`   |  {% emoji bushufu %} 不舒服  | `{% emoji ku %}`    |  {% emoji ku %} 酷   |
| `{% emoji xiaodiaodaya %}`   |  {% emoji xiaodiaodaya %} 笑掉大牙  | `{% emoji yousiliao %}` | {% emoji yousiliao %} 又死了 | `{% emoji yun %}`   |  {% emoji yun %} 晕  |
| `{% emoji siliao %}`         |      {% emoji siliao %} 去死了      | `{% emoji liubixie %}`  | {% emoji liubixie %} 流鼻血  | `{% emoji xiong %}` | {% emoji xiong %} 凶 |
| `{% emoji taoyan1 %}`        |     {% emoji taoyan1 %} 讨厌啦      | `{% emoji en %}`        |      {% emoji en %} 恩       | `{% emoji leng %}`  | {% emoji leng %} 冷  |
| `{% emoji xingxingyan %}`    |   {% emoji xingxingyan %} 星星眼    | `{% emoji a %}`         |       {% emoji a %} 啊       |                     |                      |
| `{% emoji liukoushui %}`     |    {% emoji liukoushui %} 流口水    |                         |                              |                     |                      |

{% endfolding %}
