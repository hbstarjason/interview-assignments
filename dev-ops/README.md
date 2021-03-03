# DevOps Assignment

### Q1

分析系统日志: DevOps_interview_data_set.gz ,文件在Repo中。分析系统日志得到关键信息，用 Json 的格式 POST 上传至服务器 https://foo.com/bar )，key的名称在括号里：

1. 设备名称: (deviceName)
2. 错误的进程号码: (processId)
3. 进程/服务名称: (processName)
4. 错误的原因（描述）(description)
5. 发生的时间（小时级），例如 0100-0200，0300-0400, (timeWindow)
6. 在小时级别内发生的次数 (numberOfOccurrence)

***使用Python或sh完成***

### Q2

作为开发团队的成员，您的任务是确保：

- 应用程序(一个简单的Java应用程序，返回Hello World)具有一定的弹性，并且单节点故障不会影响最终用户，您可以使用[此仓库](https://github.com/goxr3plus/Simplest-Spring-Boot-Hello-World)中提供的源代码，也可以创建自己的应用程序。
- 可以伸缩应用程序，最好自动伸缩以处理增加的负载。
- 基础架构和所需的服务以及应用程序部署是自动化的，可以通过在终端中单击按钮或命令来触发。
- 在将应用程序的源代码更改合并到master分支之前，可以对其进行自动测试。
- 可以启动该应用程序的特定版本以进行故障排除，测试，展示等。
- 需要监控环境、应用的日志，自动执行事件管理和警报

*您可以使用任何免费或开源的OS，软件包，工具等来开发解决方案*

**Bonus**

- 使用AWS、GCP


## 岗位描述

1.负责公司自动化运维平台的研发和建设.

2.负责公司 Tier2 技术支持.

3.基于业务场景、技术体系，不断完善问题处理机制和流程，持续帮助业务提升产品技术能力；

4.通过数据分析、平台建设, 提升基础架构稳定性，通过容量部署规划，降本提效;

5.协助并提供技术咨询，协同架构师/项目经理所提供的设计方案的落地、实施和交付工作；

## 岗位要求

1. 拥有 5 年以上工作经验，熟悉 Typescript、Java、Python，Shell 或 Powershell 编程语言至少两种，熟练的编程技巧;

2. 熟悉分布式、缓存、RPC、消息中间件、MySQL 存储, Postgres 存储至少一种;

3. 熟悉容器服务、K8S，熟悉云原生持续交付的体系架构;

4. 系统工程能力扎实过硬，深入了解系统（linux）及上下游链路服务（网络/io 等），具有很强技术敏感度和故障排查经验，并能进行技术方案的整合；

5. 有较强学习和沟通能力。有很强的动手能力和解决问题能力;

6. 熟悉云平台，有 AWS 云使用背景优先;

7. 熟悉平台运维和应用运维，能够建设运维规范和运维平台。

8. 熟悉 CI/CD 的搭建。

9. 熟悉日志收集、分析、报警的流程和工具的使用

10. 具备监控领域，包括 prometheus、zabbix 使用开发经验者优先考虑；

11. 为团队引入创新的技术和解决方案，以技术创新驱动业务，促进团队在这些领域的发展。

12. 有责任心，能在日常服务过程中很好实践客户第一，善于推动跨部门复杂项目的实施和较强的拿结果能力；

```bash
# DevOps-卓博咨询-zhang
# https://github.com/scdt-china/interview-assignments/blob/master/dev-ops/README.md

######## Q1
$ gzip -d  DevOps_interview_data_set.gz
$ cat DevOps_interview_data_set | awk -F" " 'BEGIN {printf("%s","\[")} {deviceName=$4;
gsub(/[^0-9]+/,"",$6);processId=$6;if(processId=="")next;
processName=$5;
description="";{for(i=7;i<=NF;i++) description=(description" "$i)};gsub(/"/,"\\\"",description)
gsub(/:.*/,"",$3);h1=$3;h2=$3+1;if(h2==24)h2="00";if(length(h2)<2)h2=sprintf("0%s",h2);timeWindow=sprintf("%s00-%s00",h1,h2);
dict[timeWindow]=dict[timeWindow]+1
printf("{\"deviceName\":\"%s\",\"processId\":\"%s\",\"processName\":\"%s\",\"description\":\"%s\",\"timeWindow\":\"%s\"},", deviceName,processId,processName,description,timeWindow)} END {printf("%s","\{");for (key in dict)printf("\"%s\":%s,", key, dict[key]);printf("%s","\}");printf("%s","\]")}' > zhang.json
$ ls
DevOps_interview_data_set  zhang.json
$ curl https://foo.com/bar -F "file=./zhang.json" -H "token: zhang" -v

######## Q2
请参考这个demo：https://github.com/hbstarjason/springboot-devops-demo
一直都在持续更新中，所熟悉的技术栈都运用在这个demo里了。
另，对于持续交付（CD）也有一定的了解，请参考：https://github.com/hbstarjason/Continuous-Deploy

```
