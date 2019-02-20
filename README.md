# Hao HIDS 


[![License](https://img.shields.io/badge/License-GPL%20v2-blue.svg?style=flat-square)](https://github.com/ysrc/github.com/winstark212/hao-hids/blob/master/LICENSE)
[![Golang](https://img.shields.io/badge/Golang-1.9-yellow.svg?style=flat-square)](https://www.golang.org/) [![Mongodb](https://img.shields.io/badge/MongoDB-3.4-red.svg?style=flat-square)](https://www.mongodb.com/download-center?jmp=nav) [![elasticsearch](https://img.shields.io/badge/Elasticsearch-5.6.4-green.svg?style=flat-square)](https://www.elastic.co/downloads/elasticsearch)


**Hao HIDS(Forked from yulong HIDS)** is a open source intrusion detection system, it's has 4 parts `Agent`, `Daemon`, `Server` and `Web`. the main features are anomaly detection, monitoring, abnormal detection, rapid blocking, advanced analysis and others functions.  

**Agent** is the collector role, collecting server information, booting items, scheduled tasks, listening ports, services, login logs, user lists, real-time monitoring of file operation behavior, network connection, execution commands, initial screening and transmission to the server through RPC protocol node.

**Daemon** is a deamon service process, providing the agent with process guard and silent environment deployement. Its task execution function implements agent hot update, blocking function and custom command execution by reveiving instructions from the server. The task transmission process uses RSA for encryption.

**Server** is the  brain of the whole system, supports horizontally distributed deployment, parses user-defined rules(built-in partial basic rules), analyzes and detects the information and behavior, abnormal login behavior, abnormal network connection behavior, abnormal command invocation behaviro, etc., to achieve real-time warning of intrusion behavior.  

## Document

* [Deployment document](./docs/install.md)
* [Docker quick experience deployement documentation](./docs/docker.md)
* [Using help](./docs/help.md)
* [Rule writing](./docs/rule.md)
* [Compliation guide](./docs/build.md)
* [Web installation wizard guide](./docs/guide.md)
* [Q&A](./qa.md)

## Features

- Real-time monitoring, sencod-level response
- The first global concept, you can find unknown threats
- Support for custom rules, high scalabiltiy
- Advanced analysis capabitities, traceable
- Global fast blocking(process, file)
- Threat intelligence query(customize interface)


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
├─agent // Agent engineering
│  ├─client // RPC client tranmission module
│  ├─common
│  ├─collect // information collection(starup items, scheduled tasks, listening ports, services, login logs, user lists)
│  └─monitor // behavior monitoring(file operations, network connections, exection commands)
├─bin
│  ├─linux-64 // Linux 64-bit dependencies
│  ├─win-32 // Windows 32-bit dependencies
│  └─win-64 // Windows 64-bit dependencies
├─daemon // Daemon engineering
│  ├─common
│  ├─install // install agent and related dependencies
│  └─task // task reception
├─docs // documention
├─driver // Windows command monitor driver
├─server // Server node engineering
│  ├─action // server basic functions
│  ├─models // database related
│  └─safecheck // security detection module(black and white list, rule analysis engine)
├─syscall_hook # monitor the Linux kernel code that executes the command
│  └─test_bench //
└─web // Web console project
    ├─conf // web configuration file
    ├─controllers // controller, responsible for forwarding requests and procession requests
    ├─httpscert // https certificate and RSA private key, built-in will be automaticaly update during the wizard process
    ├─models // model, data management and database design
    ├─routers // routing
    ├─settings // partial global variable
    ├─static // static file
    ├─upload_files // agent、daemon、dependency package file
    ├─utils // functional module
    └─views // view layer, front end template
```
