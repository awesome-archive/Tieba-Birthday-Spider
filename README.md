# Tieba-Birthday-Spider
百度贴吧生日爬虫，可抓取贴吧内吧友生日，并且在对应日期自动发送祝福

# 执行环境
Python 2.7 64bit + MongoDB （请确保环境为64位，防止爬虫中的queue容量过大导致在32位环境下内存不足的异常发生）

# 项目依赖包
- pymongo
- BeautifulSoup
- requests

# 使用方法

 1. 启动MongoDB
 2. 配置config.py中各项参数
 3. 启动spider.py进行生日等数据抓取
 4. 运行post.py测试是否能正常发送生日祝福贴
 5. 配置cron规则，让post.py能够每天定时运行，并且保证MongoDB服务一直保持开启状态

# 文件说明

- config.py 配置信息。**内部附有注释，请正确配置。** 如果有任何问题或者认为注释有描述不清需要改进的地方欢迎提issue与我讨论。
- spider.py：爬虫主文件，在config.py中正确配置好相关参数后，**先启动MongoDB服务，然后可直接执行该文件** ，抓取的信息将直接存储在MongoDB中。
- post.py：定时发帖主文件。执行该文件将会自动按照配置文件中设置好的参数，将会将指定贴吧内所有过生日的吧友信息提取出来，并且向指定帖子中发送生日祝福。**如果需要定时发送，请将该文件加入cron规则，crontab规则：`0 0 0 * *`表示在每日0点0分0秒自动执行该脚本。并且保证MongoDB服务一直保持开启状态。** 如果需要自定义祝福帖内容模版，请参照main函数中的buildContent函数调用点以及相关注释自行修改post.py下的buildContent函数。
- TiebaSpider.py：部分贴吧信息抓取方法。默认使用内置的`html_parser`作为`BeautifulSoup`的`html_parser`，用户可以自行修改TiebaSpider类的属性成员`html_parser`来使用其他`html_parser`，比如说`html5lib`等。该类使用requests第三方模块进行http通信。
- TiebaUtil.py：部分贴吧发帖回帖以及登录检测模块。该类使用urllib2模块进行http通信。
- SpiderUtil.py：爬虫助手函数，用于整理抓取到的信息，或者获取一些特殊元数据。

# 程序特点
- 使用threading多线程库+Queue队列，性能高效
- MongoDB持久化存储爬虫内容，适合抓取内容结构随时可变的场景

# 交流QQ群 
- [点击加贴吧闲聊群1：255258140][1]
- [点击加编程开发交流群2：578165753][2]


  [1]: https://jq.qq.com/?_wv=1027&k=4AO35rV
  [2]: https://jq.qq.com/?_wv=1027&k=4AO3qTM