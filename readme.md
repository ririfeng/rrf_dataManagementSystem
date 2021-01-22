# 日日峰数据个人工作数据获取及管理系统
主要用于管理个人工作中从浏览器获得数据,以便于横跨更多的人群,以及横跨更多的日期做分析,或者说横跨更多的维度做分析.
系统主要有三大板块构成
## 一、chrome_extension
谷歌插件部分,变便于过多公开介绍
### 1.安全性有保障
从谷歌浏览器空间去获取数据,插件只和浏览器有交互行为,不和网站(阿里,京东等等)有交互行为。
数据请求只有在用户操作数据请求的时候才能从浏览器获得，所有请求都是完全用户真实请求。
### 2.数据规范性
通过服务器清洗数据返回标准化自定义数据格式 actionid,d,encryptedindex,fieldid,fieldvalue
## 二、服务器部分
出于保密性原因,此部分架构不对外公开
## 三、webonlocal
统一数据管理的本地B/S架构的系统，端口只对本地开放，数据存储在本地sqlite数据库，采用RSA非对称加密
(就算db文件被黑客获取到,数据还是RSA加密过的密文)。
本系统主要有四个模块。
### 1.本地存储
/data
### 2.配置信息
/conf
### 3.数据管理的简易WEB
采用flask+waitress简易WEB  在env/webapis 系统采用 Anti 996 License 详情参考链接 https://zh.wikipedia.org/wiki/%E5%8F%8D996%E8%AE%B8%E5%8F%AF%E8%AF%81 
简单说就是如果要对代码二次开发请严格遵守当地劳动法规,仅满足此条件可以无条件使用代码二次开发商业化等等.
对数据表唯一索引字符串拼接后进行RSA加密,然后对运算字段进行逆透视得到新的表,然后对新表进行存储。
就算本地db文件被黑道盗取.那么对方也只能得到类似于. 00001,adfabadfxfa012313243556(一堆16进制),001,9800

目前本WEB系统有两部分
##### 1)/base
1.加密
为了保障就算本地DB文件被截获数据也不会泄露,对数据的唯一索引进行了加密
采用RSA公钥在__init__.py,私钥在服务器,缩短了RSA的位数,为了贴近业务
2.持久化连接sqlite的办法
##### 2)/webService
本地的数据管理系统。
目前数据管理系统只有数据预览导出一个模块
###### a)/manager
主要是管理数据的写入和导出的接口
###### b)/static
flask static 目录 
###### c)/templates
flask templates 
###### d)/bi
在规划范中,通过页面交互数据库的核心接口
### 4.python虚拟环境
/env

