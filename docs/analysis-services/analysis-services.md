---
title: Analysis Services | Documenti Microsoft
ms.date: 05/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c3a514f91e9af8de54fdbd4d9ef851c72f1911e
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="what-is-analysis-services"></a>Che cos'è Analysis Services?
  Analysis Services è un motore dati analitici utilizzato per il supporto decisionale e analitica di business, fornisce i dati analitici per i report di business e applicazioni client quali Power BI, Excel, report di Reporting Services e altri strumenti di visualizzazione di dati.  
  
 Un tipico flusso di lavoro include la creazione di un modello di dati tabulari o multidimensionali, distribuzione del modello come database in un'istanza del server SQL Server Analysis Services o Azure Analysis Services locale, l'impostazione ricorrente l'elaborazione dati e l'assegnazione autorizzazioni per consentire l'accesso ai dati per gli utenti finali. Quando è pronto, il modello di dati sono accessibili da qualsiasi applicazione client che supporta Analysis Services come origine dati.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services locale e nel cloud
Analysis Services è ora disponibile nel cloud come servizio di Azure. Azure Analysis Services supporta i modelli tabulari con i livelli di compatibilità 1200 e versioni successive. DirectQuery, partizioni, sicurezza a livello di riga, relazioni bidirezionali e traduzioni sono tutte funzioni supportate. Per altre informazioni e per una prova gratuita, vedere [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Modalità server  
 Quando si installa Analysis Services tramite il programma di installazione di SQL Server, durante la configurazione specificare una modalità server per quell'istanza.  Ogni modalità include diverse funzionalità specifiche di una particolare soluzione di Analysis Services.   
  
-   **Modalità tabulare** - i dati relazionali in memoria di implementare (modello, tabelle, colonne, misure, gerarchie) di costrutti di modellazione.  

-   **Modalità multidimensionale e di data mining** -Implementare costrutti di modellazione OLAP (cubi, dimensioni, misure). 

-   **Power Pivot Mode** -modelli di dati di implementare Power Pivot e di Excel in SharePoint (PowerPivot per SharePoint è un motore dati di livello intermedio che carica, esegue una query e aggiorna i modelli di dati ospitati in SharePoint).  
  
 Una singola istanza può essere configurata con un'unica modalità e non può essere modificata in un secondo momento.  È possibile installare più istanze con modalità diverse sullo stesso server, ma è necessario eseguire il programma di installazione e specificare le impostazioni di configurazione per ogni istanza. Per informazioni dettagliate e per un confronto delle diverse funzionalità offerte da ognuna delle modalità, vedere [confronto tabulari e multidimensionali](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).
  
## <a name="authoring-and-managing-solutions"></a>Creazione e gestione di soluzioni  
 Per creare un modello e distribuirlo a un server, utilizzare SQL Server Data Tools, scegliere il modello di progetto sia tabulare o multidimensionale e Data Mining. Il modello di progetto include cartelle per tutti gli oggetti necessari in un modello. Procedure guidate e finestre di progettazione consente di creare molti degli elementi di base come la connessione a origini dati, relazioni, misure e i ruoli. Quando il database del modello viene distribuito a un server, utilizzare SQL Server Management Studio (SSMS) per configurare l'elaborazione dati, monitorare e gestire i server e i database. Per ulteriori informazioni, vedere [strumenti e applicazioni usate in Analysis Services](../analysis-services/tools-and-applications-used-in-analysis-services.md). 
  
## <a name="documentation-by-area"></a>Documentazione per area  
In generale, la documentazione per Azure Analysis Services è inclusa con la documentazione di Azure. E la documentazione per SQL Server Analysis Services è inclusa con la documentazione di SQL. Tuttavia, almeno per i modelli tabulari, come creare e distribuire i progetti è analogo a indipendentemente dalla piattaforma in uso.  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [Novità di SQL Server Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)   
*  [Confronto tra soluzioni tabulari e multidimensionali](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [Modelli tabulari](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [Modelli multidimensionali](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [Data mining](../analysis-services/data-mining/data-mining-ssas.md)  
*  [PowerPivot per SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [Gestione delle istanze](../analysis-services/instances/analysis-services-instance-management.md)    
*  [Esercitazioni](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [Documentazione per sviluppatori](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [Riferimento tecnico (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)