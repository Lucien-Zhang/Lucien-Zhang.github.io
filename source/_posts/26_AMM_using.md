---
title: 737NG AMM 使用简编
date: 2018-12-02 16:44:52
tags: 
category: Aircraft
---
详细使用说明请阅读AMM Introduction
<!--more-->
# 手册结构
```
#include <stdio.h>
#include <编写依据：AMM Introduction>
double float main(void)
{
    {
        Front Matter 
            - Effective Aircraft  /* 手册内容只对清单中所列飞机有效 */
            /* P.S: 手册中通常以客户适用性代码(Identification Code + Effectivity Code)代表某架飞机 */
            /* (区别：WDM 和 SWPM 用的是 Block Number) */

            - Highlights          /* 对手册内容修改的集中描述 */

            - Effective Pages     /* 核查每页内容的有效性 */

            - Revision Record & Record of Temporary Revisions
            /* 定期修订记录 & 临时修订记录 */
            /* 手册在线化后这一部分基本不需要用到，更多体现在纸质版上 */

            - Service Bulletin List /* 服务通告情况跟踪*/

            - Introduction  /* 手册的介绍 & 使用说明*/
                - Airplane Circuit Breaker Lists /* 跳开关清单 */
                - Consumable Material Lists /* 耗材清单 */
                - Tool Lists /* 工装清单,有STD标准工装，COM通用工装，SPL特殊工装 */
                - Supplier List for Consumables and Tools /* 耗材与工装供应商清单 */

        Chapter
            章节分类
                ATA5~12 通用 Aircraft General Group
                ATA20~49 机身系统 Airframe Systems Group
                ATA51~57 结构 Structure Group
                ATA70~80 动力系统 Power Plant Group
            特殊章节
                ATA-20 机体标准施工 AIRFRAME STANDARD PRACTICES
                ATA-51 结构（件）检查、防护和维护 STRUCTURES
                ATA-70 发动机标准施工 (specific) ENGINE STANDARD PRACTICES
    }
return 0;
}
```
# 章节和页编号规则
```
#include <stdio.h>
#include <编写依据：AMM Introduction>


Chapter Numbering & Page Numbering
{
    Chapter/system - Section/sub-ystem - Subject/unit - page number
    
    e.g: 23-12-31-401-801
    = COMMUNICATION - VHF COMM SYSTEM - VHF COMM CONTROL PANEL - REMOVAL/INSTALLATION 
    
    /* 特例 23-00-00 这种第二和第三各元素的位置为0的章节为系统的一般介绍*/


    Page Numbering see [Table 1]
    }
```
## Table 1
|MAINTENANCE CATEGORY/PAGE BLOCK |PAGE NUMBERS|
|--------------|-----------------|
|Maintenance Practices (MP)| 201-299
|Servicing (SRV)| 301-399
|Removal/Installation (R/I)| 401-499
|Adjustment/Test (A/T)| 501-599
|Inspection/Check (I/C)| 601-699
|Cleaning/Painting (C/P)| 701-799
|Repairs| 801-899
|DDG Maintenance Procedures| 901-999

# 工卡编号规则
```
#include <stdio.h>
#include <编写依据：AMM Introduction>

    AMTOSS Task numbers
    {
        拿这两份工卡为例
        For a task: TASK 29-11-05-400-801-002
        For a subtask: SUBTASK 29-11-05-870-001-002

        结构如下：
        Chapter 29 - Section 11 - Subject 05 - Function Code 400 - Sequence Number 801 - Configuration 002

        解释：
        Sequence Number /* 当有多份前四个号码一模一样的工卡时，这个号码用来确定其唯一性 */

            TASK 的 Sequence Number 范围为801~999，超出使用 A01~A99，再超出用B01~B99以此类推
            SUBTASK 的 Sequence Number 范围为 001~799

        Configuration /* 用来区别不同构型 */

        Function Code /* page numbers 的细分*/
        /* 例如 page numbers 200 是  INSPECTION/CHECK */
        /* 210 为 General Visual, 211 为 Detailed Visual, 260 为 X-Ray/Holographic 等等 */
    }



    return 0;
}
```


