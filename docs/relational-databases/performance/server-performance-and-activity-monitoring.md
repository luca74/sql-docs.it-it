---
title: "Monitoraggio delle prestazioni e dell'attività del server | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dda58f07b5a39855218a5a0c8302179cea8c6dd3
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="server-performance-and-activity-monitoring"></a>Monitoraggio delle prestazioni e dell'attività del server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] L'obiettivo del monitoraggio dei database consiste nella valutazione delle prestazioni di un server. Un monitoraggio efficace implica l'esecuzione di snapshot periodici delle prestazioni correnti al fine di isolare i processi che causano problemi, nonché la raccolta continua di dati nel tempo per tenere traccia delle tendenze delle prestazioni. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows offrono utilità che consentono di visualizzare la condizione corrente del database e di tenere traccia delle prestazioni in caso di variazioni.  
  
 Nella sezione seguente sono contenuti argomenti che descrivono l'utilizzo degli strumenti di monitoraggio delle prestazioni e dell'attività disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e in Windows. Questa lezione contiene i seguenti argomenti:  
  
## <a name="in-this-section"></a>Argomenti della sezione  
 **Per eseguire attività di monitoraggio con gli strumenti di Windows**  
  
-   [Avvio di Monitoraggio di sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
-   [Visualizzazione del log applicazioni di &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
 **Per creare avvisi del database di SQL Server con gli strumenti di Windows**  
  
-   [Impostazione di un avviso del database di SQL Server &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)  

 **Per eseguire attività di monitoraggio con Eventi estesi**  
 
 -   [Eventi estesi](../../relational-databases/extended-events/extended-events.md)
 
  -   [Avvio rapido: Eventi estesi in SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
   
 **Per eseguire attività di monitoraggio con SQL Server Management Studio**  
  
-   [Visualizzazione del log degli errori di SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
-   [Aprire Monitoraggio attività &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **Per eseguire attività di monitoraggio con Traccia SQL utilizzando stored procedure Transact-SQL**  
  
-   [Creare una traccia &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
-   [Impostare un filtro di traccia &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
-   [Modificare una traccia esistente &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [Visualizzare una traccia salvata &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [Visualizzare informazioni sui filtri &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)  
  
-   [Eliminare una traccia &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/delete-a-trace-transact-sql.md)  
  
 **Per creare e modificare le tracce tramite SQL Server Profiler**  
  
-   [Creare una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [Impostare opzioni di traccia globali &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [Specificare eventi e colonne di dati per un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [Creare uno script Transact-SQL per l'esecuzione di una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [Salvare i risultati della traccia in un file &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [Impostare le dimensioni massime di un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [Salvare i risultati della traccia in una tabella &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [Impostare le dimensioni massime di un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [Filtrare eventi in una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [Visualizzare informazioni sui filtri &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [Modificare un filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [Filtrare gli eventi in base all'ora di inizio &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [Filtrare gli eventi in base all'ora di fine &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [Filtrare gli ID del processo server &#40;SPIDs&#41; in una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [Organizzare le colonne visualizzate in una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **Per avviare, sospendere e arrestare le tracce tramite SQL Server Profiler**  
  
-   [Avviare una traccia automaticamente dopo la connessione a un server &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [Sospendere una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [Arrestare in pausa una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [Eseguire una traccia dopo la sospensione o l'arresto &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **Per aprire le tracce e configurare la relativa modalità di visualizzazione tramite SQL Server Profiler**  
  
-   [Aprire un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [Aprire una tabella di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [Cancellare il contenuto di una finestra di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [Chiudere una finestra di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [Impostare i valori predefiniti per una definizione di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [Impostare i valori predefiniti per la visualizzazione di una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **Per riprodurre le tracce tramite SQL Server Profiler**  
  
-   [Riprodurre un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [Riprodurre una tabella di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [Riprodurre un solo evento alla volta &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [Riprodurre fino a un punto di interruzione &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [Riprodurre fino a un cursore &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Riprodurre uno script Transact-SQL &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **Per creare, modificare e utilizzare modelli di traccia tramite SQL Server Profiler**  
  
-   [Creare un modello di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [Modificare un modello di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
-   [Ottenere un modello da una traccia in esecuzione &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [Derivare un modello da un file di traccia o da una tabella di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [Esportare un modello di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [Esportare un modello di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **Per raccogliere e monitorare le prestazioni del server tramite le tracce di SQL Server Profiler**  
  
-   [Trovare un valore o una colonna di dati durante l'esecuzione di una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Salvare eventi Deadlock Graph &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Salvataggio di eventi Showplan XML in modo indipendente &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Salvataggio della classe di eventi Showplan XML Statistics Profile Events in file distinti &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [Estrarre uno script da una traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [Correlare una traccia e i dati dei registri di prestazioni di Windows &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
