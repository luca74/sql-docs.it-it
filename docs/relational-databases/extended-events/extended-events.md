---
title: Eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7d0c0b825a65c72ba8d106b2e0d145760f266aa9
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="extended-events"></a>Eventi estesi
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Gli eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono dotati di un'architettura estremamente scalabile e configurabile che consente agli utenti di raccogliere le informazioni necessarie per diagnosticare o identificare un problema legato alle prestazioni.  

Per altre informazioni sulle destinazioni degli eventi estesi, vedere:

- [Avvio rapido: Eventi estesi in SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
- Blog: [Eventi estesi di SQL Server](http://blogs.msdn.com/b/extended_events/)

  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Vantaggi degli eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Si tratta di un sistema di monitoraggio delle prestazioni leggero in cui vengono utilizzate poche risorse per le prestazioni. Per gli eventi estesi sono disponibili due interfacce utente grafiche (**Creazione guidata nuova sessione** e **Nuova sessione**) per creare, modificare, visualizzare e analizzare i dati della sessione.  
  
## <a name="extended-events-concepts"></a>Concetti degli eventi estesi  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gli eventi estesi sono basati su concetti esistenti, ad esempio un evento o un consumer di eventi, usano concetti di Event Tracing for Windows (ETW) e ne introducono di nuovi.  
  
 Nella seguente tabella vengono descritti i concetti negli eventi estesi.  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Pacchetti degli eventi estesi di SQL Server](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|Vengono descritti i pacchetti degli eventi estesi che contengono oggetti utilizzati per ottenere ed elaborare dati durante l'esecuzione di una sessione degli eventi estesi.|  
|[Destinazioni degli eventi estesi di SQL Server](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|Vengono descritti i consumer di eventi che possono ricevere dati durante una sessione dell'evento.|  
|[Motore degli eventi estesi di SQL Server](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|Viene descritto il motore che implementa e gestisce una sessione degli eventi estesi.|  
|[Sessioni degli eventi estesi di SQL Server](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|Viene descritta la sessione Eventi estesi.|  
  
## <a name="extended-events-architecture"></a>Architettura degli eventi estesi  
 Gli eventi estesi (Eventi estesi) costituiscono un sistema generale di gestione degli eventi per sistemi server. L'infrastruttura degli eventi estesi supporta la correlazione di dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e in certe condizioni, la correlazione di dati dal sistema operativo e dalle applicazioni di database. Nel secondo caso, l'output degli eventi estesi deve essere indirizzato a ETW (Event Tracing for Windows) per correlare i dati degli eventi con i dati degli eventi delle applicazioni o del sistema operativo.  
  
 In tutte le applicazioni sono presenti punti di esecuzione utili sia all'interno che all'esterno di un'applicazione. All'interno dell'applicazione, l'elaborazione asincrona può essere accodata utilizzando informazioni raccolte durante l'esecuzione iniziale di un'attività. All'esterno dell'applicazione, i punti di esecuzione forniscono utilità di monitoraggio con informazioni sulle caratteristiche relative al funzionamento e alle prestazioni dell'applicazione monitorata.  
  
 Gli eventi estesi supportano l'utilizzo di dati degli eventi all'esterno di un processo. Questi dati sono in genere utilizzati da:  
  
-   strumenti di analisi, ad esempio Traccia SQL e il Monitoraggio di sistema.  
  
-   strumenti di log, ad esempio il registro eventi di Windows o il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Utenti che amministrano un prodotto o sviluppano applicazioni su un prodotto.  
  
 Gli aspetti chiave della progettazione degli eventi estesi sono i seguenti:  
  
-   Il motore degli eventi estesi è agnostico in termini di eventi. In questo modo, il motore è in grado di associare qualsiasi evento a qualsiasi destinazione perché il motore non è vincolato al contenuto dell'evento. Per ulteriori informazioni sul motore degli eventi estesi, vedere [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md).  
  
-   Gli eventi sono separati dai consumer di eventi chiamati *destinazioni* negli eventi estesi. Ciò significa che qualsiasi destinazione può ricevere qualsiasi evento. Inoltre, qualsiasi evento generato può essere utilizzato automaticamente dalla destinazione, che può scrivere nel log o fornire un contesto dell'evento supplementare. Per ulteriori informazioni, vedere [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
-   Gli eventi sono distinti dall'azione da intraprendere quando un evento si verifica. Di conseguenza, qualsiasi azione può essere associata a qualsiasi evento.  
  
-   I predicati consentono di filtrare dinamicamente i casi in cui i dati degli eventi devono essere acquisiti. Questa possibilità garantisce maggiore flessibilità per l'infrastruttura degli eventi estesi. Per ulteriori informazioni, vedere [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
 Gli eventi estesi possono generare in modo sincrono dati degli eventi (e in modo asincrono elaborare tali dati) il che fornisce una soluzione flessibile per la gestione degli eventi. Inoltre, gli eventi estesi forniscono le funzionalità seguenti:  
  
-   Approccio unificato alla gestione degli eventi nel sistema server, consentendo agli utenti di isolare eventi specifici ai fini della risoluzione dei problemi.  
  
-   Supporto e integrazione con gli strumenti ETW esistenti.  
  
-   Meccanismo di gestione degli eventi interamente configurabile, basato su [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Possibilità di monitorare dinamicamente i processi attivi, con un impatto minimo su tali processi.  
  
-   Sessione di integrità di sistema predefinita che viene eseguita senza effetti visibili sulle prestazioni. Tale sessione consente di raccogliere dati di sistema che è possibile utilizzare per risolvere i problemi relativi alle prestazioni. Per altre informazioni, vedere [Utilizzare la sessione system_health](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="extended-events-tasks"></a>Attività degli eventi estesi  

L'utilizzo di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] per eseguire funzioni, DMV e istruzioni DDL (Data Definition Language) [!INCLUDE[tsql](../../includes/tsql-md.md)] o viste del catalogo consente di creare soluzioni per la risoluzione dei problemi relativi agli eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] semplici o complesse per l'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Utilizzare **Esplora oggetti** per gestire sessioni di eventi.|[Gestire sessioni di eventi in Esplora oggetti](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|Viene descritto come creare una sessione di eventi estesi.|[Creare una sessione Eventi estesi](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|Viene descritto come visualizzare e aggiornare i dati di destinazione.| [Visualizzazione avanzata dei dati di destinazione da eventi estesi in SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|Viene descritto come utilizzare gli strumenti degli eventi estesi per creare e gestire sessioni di eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Strumenti degli eventi estesi](../../relational-databases/extended-events/extended-events-tools.md)|  
|Viene descritto come alterare una sessione Eventi estesi.|[Modificare una sessione Eventi estesi](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|Viene descritto come ottenere informazioni sui campi associati agli eventi.|[Recuperare i campi per tutti gli eventi](http://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|Viene descritto come individuare gli eventi disponibili nei pacchetti registrati.|[Visualizzare gli eventi per i pacchetti registrati](http://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|Viene descritto come individuare le destinazioni degli eventi estesi disponibili nei pacchetti registrati.|[Visualizzare le destinazioni degli eventi estesi per i pacchetti registrati](http://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|Viene descritto come visualizzare gli eventi e le azioni Eventi estesi equivalenti a ogni evento di Traccia SQL e alle colonne associate.|[Visualizzare gli eventi estesi equivalenti alle classi di eventi di Traccia SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Viene descritto come trovare i parametri che è possibile impostare quando si utilizza l'argomento ADD TARGET in CREATE EVENT SESSION o ALTER EVENT SESSION.|[Recuperare i parametri configurabili per l'argomento ADD TARGET](http://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|Viene descritto come convertire uno script di Traccia SQL esistente in una sessione Eventi estesi.|[Convertire uno script di Traccia SQL esistente in una sessione Eventi estesi](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Viene descritto come determinare quali query mantengono il blocco, il piano della query e lo stack [!INCLUDE[tsql](../../includes/tsql-md.md)] al momento del blocco.|[Individuare le query che mantengono attivi i blocchi](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|Viene descritto come individuare l'origine dei blocchi che hanno effetti negativi sulle prestazioni del database.|[Cercare gli oggetti con il maggior numero di blocchi acquisiti](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Viene illustrato come utilizzare gli eventi estesi con Analisi eventi per Windows al fine di monitorare l'attività del sistema.|[Monitorare l'attività del sistema mediante gli eventi estesi](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
| Uso delle viste catalogo e delle viste a gestione dinamica (DMV) per gli eventi estesi | [Istruzioni SELECT e JOIN da viste di sistema per eventi estesi in SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |

  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Supporto dell'applicazione livello dati per oggetti e versioni di SQL Server](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Distribuire un'applicazione livello dati](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Monitorare le applicazioni livello dati](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)   
 [Viste a gestione dinamica degli eventi estesi](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Viste del catalogo degli eventi estesi &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
  
  
