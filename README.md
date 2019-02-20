# Hao HIDS 


[![License](https://img.shields.io/badge/License-GPL%20v2-blue.svg?style=flat-square)](https://github.com/ysrc/github.com/winstark212/hao-hids/blob/master/LICENSE)
[![Golang](https://img.shields.io/badge/Golang-1.9-yellow.svg?style=flat-square)](https://www.golang.org/) [![Mongodb](https://img.shields.io/badge/MongoDB-3.4-red.svg?style=flat-square)](https://www.mongodb.com/download-center?jmp=nav) [![elasticsearch](https://img.shields.io/badge/Elasticsearch-5.6.4-green.svg?style=flat-square)](https://www.elastic.co/downloads/elasticsearch)


**Hao HIDS(Forked from yulong HIDS)** is a open source intrusion detection system, it's has 4 parts `Agent`, `Daemon`, `Server` and `Web`. the main features are anomaly detection, monitoring, abnormal detection, rapid blocking, advanced analysis and others functions.  

**Agent** is the collector role, collecting server information, booting items, scheduled tasks, listening ports, services, login logs, user lists, real-time monitoring of file operation behavior, network connection, execution commands, initial screening and transmission to the server through RPC protocol node.

**Daemon** is a deamon service process, providing the agent with process guard and silent environment deployement. Its task execution function implements agent hot update, blocking function and custom command execution by reveiving instructions from the server. The task transmission process uses RSA for encryption.

**Server** is the  brain of the whole system, supports horizontally distributed deployment, parses user-defined rules(built-in partial basic rules), analyzes and detects the information and behavior, abnormal login behavior, abnormal network connection behavior, abnormal command invocation behaviro, etc., to achieve real-time warning of intrusion behavior.  

## Document

* [部署文档](./docs/install.md)
* [Docker快速体验部署文档](./docs/docker.md)
* [使用帮助](./docs/help.md)
* [规则编写](./docs/rule.md)
* [编译指南](./docs/build.md)
* [Web安装向导指南](./docs/guide.md)
* [Q&A](./qa.md)

## Features

- Real-time monitoring, sencod-level response
- The first global concept, you can find unknown threats
- Support for custom rules, high scalabiltiy
- Advanced analysis capabitities, traceable
- Global fast blocking(process, file)
- Threat intelligence query(customize interface)


> 相比其他同类应用，维护使用此系统需要有一定的安全判断分析能力。


## Overall architecture

![](./docs/jg.png)

## Test effect chart

![](./docs/yulong.gif)


## TODO
- Create an instrusion case library, automated case simulation test  
- Machine learning to judge suspicious behavior, as a supplement the the rules
- Asset inventory, such as identification patches, application versions, responsible persons, various package/kernel versions...
- Supplement with a vulnerability library, it can respond more quickly, which must be repaired, and those that can be repaired are acceptable.
- Distinguish communication mode(active, passive)
- Use message queue instead of RPC
- Baseline verification
- Phantom honey pot, agent dynamic proxy honeyport port, large-scale upgrade honeypot coverage desnity
- Support multiple scenarios(office environment, Docker), currently Snapdragon is only suitable for online server environment
- Lightweight linux kernel protection, immune to some attach without upgrading the kernel  

## Source structure
```
├─agent // Agent工程
│  ├─client // RPC client 传输模块
│  ├─common
│  ├─collect // 信息收集（开机启动项、计划任务、监听端口、服务、登录日志、用户列表）
│  └─monitor // 行为监控（文件操作、网络连接、执行命令）
├─bin
│  ├─linux-64 // Linux 64位的依赖包
│  ├─win-32 // Windows 32位的依赖包
│  └─win-64 // Windows 64位的依赖包
├─daemon // Daemon工程
│  ├─common
│  ├─install // 安装Agent和相关依赖
│  └─task // 任务接收
├─docs // 说明文档
├─driver // Windows 命令监控驱动
├─server // Server节点工程
│  ├─action // Server基本功能
│  ├─models // 数据库相关
│  └─safecheck // 安全检测模块（黑白名单，规则解析引擎）
├─syscall_hook # 监控执行命令的Linux内核代码
│  └─test_bench // 方便调试的
└─web // Web控制台项目
    ├─conf // web端配置文件
    ├─controllers // 控制器，负责转发请求，对请求进行处理
    ├─httpscert // https证书和RSA私钥，内置的会在向导过程中自动更新
    ├─models // 模型，数据管理和数据库设计
    ├─routers // 路由
    ├─settings // 部分全局变量
    ├─static // 静态文件
    ├─upload_files // agent、daemon、依赖包文件
    ├─utils // 功能模块
    └─views // 视图层，前端模板
```
