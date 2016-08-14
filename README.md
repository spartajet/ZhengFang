#正方教务系统助手
The helper of ZhengFang System
具体参见：http://blog.csdn.net/nghuyong/article/details/52203443
##1.项目定义
这个项目实现了正方教务系统的一套API：
包括模拟登陆，个人信息查询，课表获取，成绩查询等等。
随着API的不断完善于扩充，可以很方便的作为后台服务。
比如教务系统手机客户端，桌面客户端，也可以作为某些特定应用需要学生课表，信息的后台。

同时这个项目定义为助手，会继续开发便捷的工具：
* 自动完成评教任务
* 期末新的成绩公布，邮件通知
* 分学期，分学年绩点计算
* 公选课抢课功能

##2.项目依赖
* 爬虫相关：requests
* 网页解析：lxml,BeautifulSoup
* 数据存储：peewee
* 数据库：Sqlite

##3.项目结构
1. ZhengFang.db 数据库
2. model.py 模型层，通过ORM与数据库相连
3. spyder.py 业务层，网页爬虫，**项目入口**
4. parseHtml.py 业务层，网页解析工具


##4.项目功能
项目均已江南大学正方教务系统为例测试。若在你学校测试不通过欢迎开issue。
###4.1模拟登陆
登陆有两种方式

1. 默认登陆：

需要处理验证码。将验证码下载到本地。code.jpg。人工识别验证码后，手动输入验证码。实现登陆。

2. 绕过验证码登陆：

由于正方教务系统的漏洞在若存在**default5.asp**页面，可以不用验证码直接登陆。可以从default3，default4，都试一试。

###4.2个人信息获取
通过教务系统个人信息页面，抓取，个人信息（真的有很多信息！）并持久化保存到数据库中。

###4.3课表获取
通过抓取的个人信息读到学生入学的年份，在结合当前时间，就可以知道能够抓取到哪些学期的课表。

例如学生2014年入学，当前是2016年8月，说明至少可以抓取到：

2014-2015年度 第 1 学期

2014-2015年度 第 2 学期

2015-2016年度 第 1 学期

2015-2016年度 第 2 学期

这4个学期的课表，当然由于现在是2016年8月，可能可以抓取到2016-2017年度第 1 学期课表，可以试着抓取。

将抓取到的课表持久化到数据库中。



