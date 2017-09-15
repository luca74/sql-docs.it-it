---
title: Riferimento (Ottimizzazione guidata motore di Database) a un File di Input XML | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d98a6bfc0fc61d76c434f20609205c52c202a257
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Guida di riferimento ai file di input XML (Ottimizzazione guidata motore di database)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]Ottimizzazione guidata è possibile utilizzare un file di input XML per ottimizzare un database. In questo file XML sono specificati i database, le tabelle, i file o le tabelle del carico di lavoro e le opzioni di ottimizzazione da utilizzare per la sessione di ottimizzazione. È inoltre possibile utilizzare questo file per definire una configurazione specificata dall'utente per eseguire un'analisi di simulazione.  
  
 Un file di input XML di Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene una gerarchia di elementi XML, ognuno dei quali include testo o altri elementi che specificano le impostazioni della sessione di ottimizzazione. È necessario che il file di input XML di Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] sia conforme agli standard di correttezza del formato XML. Per tutti i nomi degli elementi viene pertanto fatta distinzione tra maiuscole e minuscole. Gli elementi vengono specificati mediante l'uso della distinzione tra maiuscole e minuscole Pascal, in base alla quale il primo carattere e la prima lettera della parola successiva concatenata sono in maiuscolo.  
  
 Tutti i valori degli elementi devono essere conformi alle convenzioni di denominazione XML. Per altre informazioni su queste convenzioni, vedere [Contenuto testuale XML](http://go.microsoft.com/fwlink/?LinkId=7614) in MSDN Library.  
  
 Si noti che questa Guida di riferimento non è completa. Per informazioni su tutti gli elementi che è possibile utilizzare per definire l'input XML, fare riferimento all'XML Schema DTASchema.xsd di Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="xml-declaration"></a>Dichiarazione XML  
  
-   [Dati XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Elemento radice DTAXML  
  
-   [Elemento DTAXML &#40; DTA &#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Elementi DTAInput  
  
-   [Elemento DTAInput &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Elemento server &#40; DTA &#41;](../../tools/dta/server-element-dta.md)  
  
-   [Elemento Workload &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)  
  
-   [Elemento TuningOptions &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Elemento Configuration &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>Elementi server  
  
-   [Elemento Name per Server &#40; DTA &#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Elemento database per Server &#40; DTA &#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Elementi del carico di lavoro  
  
-   [Elemento file &#40; DTA &#41;](../../tools/dta/file-element-dta.md)  
  
-   [Elemento database per Workload &#40; DTA &#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [Elemento EventString &#40; DTA &#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Elementi delle opzioni di ottimizzazione  
  
-   [Elemento TuningTimeInMin &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [Elemento StorageBoundInMB &#40; DTA &#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [Elemento TestServer &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [Elemento FeatureSet &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partizionamento elemento &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [Elemento DropOnlyMode &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [Elemento KeepExisting &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [Elemento OnlineIndexOperation &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [Elemento DatabaseToConnect &#40; DTA &#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Elementi di configurazione  
  
-   [Elemento server per Configuration &#40; DTA &#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Elemento database per Configuration &#40; DTA &#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Elemento Recommendation &#40; DTA &#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Creare l'elemento &#40; DTA &#41;](../../tools/dta/create-element-dta.md)  
  
-   [Elemento index &#40; DTA &#41;](../../tools/dta/index-element-dta.md)  
  
-   [Elemento Name per Index &#40; DTA &#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Elemento Column per Index &#40; DTA &#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Elemento Name per Column &#40; DTA &#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Elemento filegroup per Index &#40; DTA &#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Elementi di database  
  
-   [Elemento Name per Database &#40; DTA &#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Elemento schema per Database &#40; DTA &#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Elemento Name per Schema &#40; DTA &#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Elemento TABLE per Schema &#40; DTA &#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Elemento Name per Table &#40; DTA &#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Ottimizzazione guidata motore di database](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  