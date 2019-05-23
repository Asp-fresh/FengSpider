# FengSpider

---
自己的一些爬虫经验总结

## [学习](./learn)

 * [Ajax的处理方式](./learn/1.Ajax的处理方式)
 * [requests库的学习和使用](./learn/2.requests库的学习和使用)
 * [网络信息采集](./learn/3.网络信息采集)
 * [Selenuim](./learn/4.Selenuim)
 * [Scrapy框架学习使用](./learn/5.Scrapy框架学习)

## [资源]
* [爬虫学习资源总和](学习目录.md)
* [正则表达式](正则表达式.md)
* [pc端的user_agent](pc_user_agent.txt) 
* [移动端的user_agent](mobile_user_agent.txt)

## [项目](./project)
* [新浪军事](./project/sina)
* [豆瓣影评抓取](./project/douban)
* [豆瓣-猎毒人短评-词云](./project/douban&wordcloud)
* [拉钩网数据抓取](./project/lagou)
* [博客爬虫](./project/blog)
* [优酷视频链接](./project/youku)
* [华师大讲座报告爬虫](./project/华师大讲座会议)
* [proxy-template 代理池](./project/proxy-template)
* [斗鱼弹幕](./project/douyu)

## 目录

- 爬取
- 解析
- 存储
- 防反爬
- 加速

## 爬取

### 爬取类型

- 网页爬取
- - 服务端渲染
  - 客户端渲染
- App 爬取
- - 普通接口
  - 加密参数接口
  - 加密内容接口
  - 非常规协议接口

### 页面渲染方式

- 服务端渲染：页面结果是由服务器渲染后返回的，有效信息包含在请求的HTML页面中
- 客户端渲染：页面结果由JavaScript渲染而成，数据一般经过ajax获取

### 网页爬取

- 对于服务端渲染的只需要获取到相应的页面即可
- 对于客户端渲染
  - 寻找ajax接口：通过浏览器的开发者工具
  - 模拟浏览器执行：使用selenium
  - 模拟执行JavaScript：使用js2py等类库

### app爬取

- 对于普通无加密接口，这种直接抓包拿到接口的具体请求形式就好了，可用的抓包工具有 Charles、Fiddler、mitmproxy。
- 对于加密参数的接口，一种方法可以实时处理，例如 Fiddler、mitmdump、Xposed 等，另一种方法是将加密逻辑破解，直接模拟构造即可，可能需要一些反编译的技巧。
- 对于加密内容的接口，即接口返回结果完全看不懂是什么东西，可以使用可见即可爬的工具 Appium，也可以使用 Xposed 来 hook 获取渲染结果，也可以通过反编译和改写手机底层来实现破解。
- 对于非常规协议，可以使用 Wireshark 来抓取所有协议的包，或者使用 Tcpdump 来进行 TCP 数据包截获。

## 解析

### 常用解析规则

- CSS 选择器
- xpath语法
- 正则表达式
- json数据处理
- xml处理

> 注意：这里有一个研究方向——智能解析
>
> 问题：如果我们要爬上万个网站，如果每个网站都去写对应的规则，这样会很累而且繁琐
>
> 提出需求：如果能提供一个页面，算法可以自动来提取页面的标题、正文、日期等内容，同时把无用的信息给刨除，这将大大节省时间

### 智能解析

- readability 算法，这个算法定义了不同区块的不同标注集合，通过权重计算来得到最可能的区块位置。
- 疏密度判断，计算单位个数区块内的平均文本内容长度，根据疏密程度来大致区分。
- Scrapyly 自学习，是 Scrapy 开发的组件，指定⻚页⾯面和提取结果样例例，其可⾃自学习提取规则，提取其他同类⻚页⾯面。
- 深度学习，使⽤用深度学习来对解析位置进⾏行行有监督学习，需要⼤大量量标注数据。

**现成可以使用的框架**

- you-get:爬取视频
- newspaper:爬取新闻

## 存储

- 文件，如 JSON、CSV、TXT、图⽚、视频、⾳频等，常用的一些库有 csv、xlwt、json、pandas、pickle、python-docx 等。
- 数据库，分为关系型数据库、非关系型数据库，如 MySQL、MongoDB

## 反爬

- 封IP:设置代理
- 验证码
  - 找打码平台
  - 深度学习
  - 需要登录的封账号：多注册几个账号，维护Cookie池

## 加速

- 单机多线程
- 多机多进程
- 使用成熟的工程化框架

