> **提示：下载链接，在文章最底部！！！**

# AWVS-SCAN-Plus介绍

针对 AWVS 15版本开发的批量扫描脚本，支持SpringShell\log4j\常见CVE\Bug Bounty\常见高危\SQL注入\XSS等
专项漏洞的扫描，支持联动xray、burp、w13scan等被动批量扫描，灵活自定义扫描模板

## AWVS-SCAN-Plus功能

> 提示：本项目基于此awvs15版本开发，其他版本未测试（理论上都是支持的，自定义扫描模板需要进行单独测试）

支持AWVS15版本的API接口

* 支持URL批量添加扫描
* 支持批量仅扫描apache-log4j漏洞
* 支持对批量url添加 `cooKie`凭证进行爬虫扫描
* 支持对批量url添加1个或多个不同请求头
* 支持配置上级代理地址，能结合被动扫描器进行配置扫描,如：`xray`,`w13scan`,`burp`等扫描器
* 支持一键清空所有任务
* 通过配置 `config.ini`文件，支持自定义各种扫描参数，如:爬虫速度，排除路径(不扫描的目录),全局 `cookie`,限制为仅包含地址和子目录
* 支持对扫描器内已有目标进行批量扫描，支持自定义扫描类型

## 基础配置：

1. 安装基础环境：`pip install -r requirements.txt`
2. 配置config_default.ini文件里的配置，比如：awvs的url、apikey、企业微信机器人webhook等，修改完后，将config_default.ini文件名改为config.ini

> 提示：config.ini 请使用编辑器更改，记事本会改会原有格式

## 功能说明

## 使用方式一：交互式命令行

**使用场景：**

用于手动交互式进行AWVS扫描

**使用方式：**

```bash
python awvs_scan.py

AWVS-SCAN-Plus 批量添加，批量扫描，支持awvs15批量联动被动扫描器等功能
作者微信：BigYoung
Blog: https://sec.bigyoung.cn

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

请输入数字:1

选择本次扫描需要生成的报告模板（无需要报告，直接回车）:
1 【PCI DSS 3.2】
2 【Sarbanes Oxley】
3 【DISA STIG】
4 【WASC Threat Classification】
5 【Developer】
6 【Comprehensive (new)】
7 【Quick】
8 【Executive Summary】
9 【HIPAA】
10 【Affected Items】
11 【Scan Comparison】
12 【CWE Top 25】
13 【ISO 27001】
14 【NIST SP 800-53】
15 【OWASP Top 10 2013】
16 【OWASP Top 10 2017】
17 【OWASP Top 10 2021】

请输入数字:
```

## 使用方式二：命令行参数

用于自动化处理场景，通过命令直接调用，无需交互式操作

**使用方式：**

```bash
Usage: awvs_cli.py [options]

Options:
-h, --help                  show this help message and exit
-t TARGET, --target=TARGET  Please Enter the AWVS Target, eg: https://test.com
-f FILE, --file=FILE        Please Enter the url.txt filepath, eg: ./urls.txt
-m MOD, --mod=MOD           Please Enter Your AWVS Scan mod, eg:查看config.ini配置文件[awvs_mod]配置，有注释说明
-s SWITCH, --switch=SWITCH  是否开启扫描,eg:1：开启扫描，0：不开启扫描
-l LABEL, --label=LABEL     添加扫描任务的目标描述
-r REPORT, --report=REPORT  是否开启报告导出，eg：1，数字含义，查看config.ini awvs_template_id配置
```

**使用示例：**

添加一个目标，配置扫描模式：1，并开启生成报告模板1：

`python3 awvs_cli.py -t https://test.com -m 1 -l 任务描述 -r 1`

批量添加目标，配置扫描模式：1，并开启生成报告模板1：

`python3 awvs_cli.py -f ./url.txt -m 1 -l 任务描述 -r 1`

**[awvs_mod]参数特别说明**

1-11参数两种使用模式都可以直接使用。

12这个参数，在交互式命令的使用场景下，会要求你手动输入已经在AWVS里定义好的模板profile_id。如果通过方式二使用时，12这个参数是无效的，如果需要使用自定义profile_id，使用方式是 `-m 11111-1111-222-333`，直接输入profile_id即可。

**[awvs_template_id]参数特别说明**

报告模板是系统内置的，不要修改config.ini配置文件的此模块内容，否则会导致程序异常。

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

## V1.0.0 @2023-11-28

> 提示：此版本基于[awvs14-scan](https://github.com/test502git/awvs14-scan)开发，感谢原作者的开源分享

* 重构代码结构、优化代码逻辑

## V1.1.0 @2023-11-30

* 增加命令行参数形式，运行脚本，方便脚本自动化调用

## V1.2.0 @2023-12-09

- 【功能】增加AWVS发起扫描时，可以选择是否生成扫描报告功能

**提示：此版本新增功能，可配合AWVS配置里的邮件发送功能一起使用。可以实现：发起任务扫描，并自动获取到漏洞报告模板的效果。** 

# TODO

- [X]  增加命令行参数形式，运行脚本，方便脚本自动化调用
- [X]  增加发起扫描时，同时生成报告功能
- [ ]  漏洞通知增加多渠道：飞书、钉钉
- [ ]  增加漏洞信息推送到webhook接口，方便漏洞自动化录入漏洞管理平台

# 免责声明

本项目仅用于安全自查，请勿利用文章内的相关工具与技术从事非法测试，如因此产生的一切不良后果与本项目作者无关。

# 版权声明

本项目仅限于购买者使用，未经授权禁止转载、传播、复制等，否则将追究法律责任。

# 下载地址&获取最新版

[https://ifdian.net/a/bigyoung?tab=shop](https://ifdian.net/a/bigyoung?tab=shop)
