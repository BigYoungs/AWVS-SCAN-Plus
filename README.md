# AWVS-SCAN-Plus介绍

针对 AWVS 15版本开发的批量扫描脚本，支持SpringShell\log4j\常见CVE\Bug Bounty\常见高危\SQL注入\XSS等
专项漏洞的扫描，支持联动xray、burp、w13scan等被动批量扫描，灵活自定义扫描模板

## AWVS-SCAN-Plus功能

> 提示：本项目基于此awvs15版本开发，其他版本未测试（理论上都是支持的，自定义扫描模板需要进行单独测试）

支持AWVS15版本的API接口

* 支持URL批量添加扫描
* 支持批量仅扫描apache-log4j漏洞
* 支持对批量url添加`cooKie`凭证进行爬虫扫描
* 支持对批量url添加1个或多个不同请求头
* 支持配置上级代理地址，能结合被动扫描器进行配置扫描,如：`xray`,`w13scan`,`burp`等扫描器
* 支持一键清空所有任务
* 通过配置`config.ini`文件，支持自定义各种扫描参数，如:爬虫速度，排除路径(不扫描的目录),全局`cookie`,限制为仅包含地址和子目录
* 支持对扫描器内已有目标进行批量扫描，支持自定义扫描类型

## 基础配置：

1. 安装基础环境：`pip install -r requirements.txt`

2. 配置config_default.ini文件里的配置，比如：awvs的url、apikey、企业微信机器人webhook等，修改完后，将config_default.ini文件名改为config.ini

> 提示：config.ini 请使用编辑器更改，记事本会改会原有格式

## 使用方式一：交互式命令行

**使用场景：**

用于手动交互式进行AWVS扫描

**使用方式：**

`python awvs_scan.py`

```
********************************************************************      
AWVS-SCAN-Plus 批量添加，批量扫描，支持awvs15批量联动被动扫描器等功能                                                                                                        
作者微信：BigYoung
Blog: https://sec.bigyoung.cn
********************************************************************
1 【批量添加url到AWVS扫描器扫描】
2 【删除扫描器内所有目标与扫描任务】
3 【删除所有扫描任务(不删除目标)】
4 【对扫描器中已有目标，进行扫描】 
5 【高危漏洞消息推送】 企业微信机器人
6 【删除已扫描完成的目标】
    
请输入数字:1
1 【开始 完全扫描】
2 【开始 扫描高风险漏洞】
3 【开始 扫描XSS漏洞】
4 【开始 扫描SQL注入漏洞】
5 【开始 弱口令检测】
6 【开始 Crawl Only,，建议config.ini配置好上级代理地址，联动被动扫描器】
7 【开始 扫描意软件扫描】
8 【仅添加 目标到扫描器，不做任何扫描】
9 【仅扫描apache-log4j】(请需先确保当前版本已支持log4j扫描,awvs 14.6.211220100及以上)
10 【开始扫描Bug Bounty高频漏洞】
11 【扫描已知漏洞】（常见CVE，POC等）
12 【自定义模板】

请输入数字:?
```

## 使用方式二：命令行参数

待开发~

# 此工具使用的AWVS版本：

```
# 本项目基于此awvs版本开发，其他版本未测试（理论上都是支持的，自定义扫描模板需要进行测试）

docker pull xrsec/awvs:v15

bash <(curl -sLk https://www.fahai.org/aDisk/Awvs/check.sh) xrsec/awvs:v15

访问地址：https://127.0.0.1:3443/#/login

账户：awvs@awvs.lan
密码：Awvs@awvs.lan
```

# 版本更新记录

## V1.0.0

> 提示：此版本基于[awvs14-scan](https://github.com/test502git/awvs14-scan)开发，感谢原作者的开源分享

* 重构代码结构、优化代码逻辑

# TODO

- [ ] 增加命令行参数形式，运行脚本，方便脚本自动化调用
- [ ] 增加导出报告功能
- [ ] 漏洞通知增加多渠道：飞书、钉钉
- [ ] 增加漏洞信息推送到webhook接口，方便漏洞自动化录入漏洞管理平台

# 免责声明

本项目仅用于安全自查，请勿利用文章内的相关工具与技术从事非法测试，如因此产生的一切不良后果与本项目作者无关。

# 版权声明

本项目仅限于购买[专栏](https://note.mowen.cn/note-intro/?noteUuid=CpZRasoY4D6a3WQoJ3O4q)者使用，未经授权禁止转载、传播、复制等，否则将追究法律责任。

# 下载地址&获取最新版

[https://note.mowen.cn/note-intro/?noteUuid=CpZRasoY4D6a3WQoJ3O4q](https://note.mowen.cn/note-intro/?noteUuid=CpZRasoY4D6a3WQoJ3O4q)
