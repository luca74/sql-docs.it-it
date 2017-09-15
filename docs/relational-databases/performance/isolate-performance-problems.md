---
title: Isolare i problemi relativi alle prestazioni | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolating performance problems [SQL Server]
- monitoring performance [SQL Server], isolating problems
- database monitoring [SQL Server], isolating problems
- tuning databases [SQL Server], isolating problems
- monitoring server performance [SQL Server], isolating problems
- database performance [SQL Server], isolating problems
- server performance [SQL Server], isolating problems
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9ae4ada18ad96ba2675b95610316186c417c986
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="isolate-performance-problems"></a>Isolare i problemi relativi alle prestazioni
  Per isolare i problemi relativi alle prestazioni del database, è in genere preferibile utilizzare più strumenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o di Microsoft Windows in combinazione, anziché uno per volta. La caratteristica grafica Piano di esecuzione, detta anche Showplan, consente, ad esempio, di individuare in modo semplice deadlock in una singola query. È tuttavia possibile rilevare in modo più semplice altri problemi relativi alle prestazioni utilizzando le caratteristiche di monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows in combinazione.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] può essere utilizzato per monitorare e risolvere i problemi correlati a Transact-SQL e alle applicazioni. Per controllare l'hardware e altri problemi relativi al sistema è possibile utilizzare Monitoraggio di sistema.  
  
 Per risolvere i problemi, è possibile eseguire il monitoraggio degli elementi seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Stored procedure o batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] inviate da applicazioni utente.  
  
-   Attività degli utenti, ad esempio blocchi o deadlock.  
  
-   Attività hardware, ad esempio utilizzo del disco.  
  
 Tra i problemi che possono verificarsi, sono inclusi i seguenti:  
  
-   Errori di sviluppo delle applicazioni correlati a istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] non corrette.  
  
-   Errori hardware, ad esempio errori correlati al disco o alla rete.  
  
-   Un numero eccessivo di blocchi causato da un database progettato in modo non appropriato.  
  
## <a name="tools-for-common-performance-problems"></a>Strumenti per la risoluzione dei problemi comuni relativi alle prestazioni  
 È inoltre importante scegliere con attenzione lo strumento per il monitoraggio o l'ottimizzazione dei problemi relativi alle prestazioni. Lo strumento e l'utilità dipendono dal tipo di problema che si desidera risolvere.  
  
 Negli argomenti seguenti vengono descritti numerosi strumenti di monitoraggio e ottimizzazione e i problemi che tali strumenti consentono di rilevare.  
  
 [Individuare i colli di bottiglia](../../relational-databases/performance/identify-bottlenecks.md)  
  
 [Monitoraggio dell'utilizzo della memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)  
  
  