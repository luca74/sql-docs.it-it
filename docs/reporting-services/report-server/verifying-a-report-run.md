---
title: Verifica dell'esecuzione di un Report | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97015ca82fd8a58c3c5cd351b2f7379711d65aa1
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="verifying-a-report-run"></a>Verifica dell'esecuzione di un report
  Per visualizzare informazioni sullo stato di elaborazione di un report, è possibile utilizzare i file di log oppure controllare le informazioni sullo stato visualizzate con il report in Gestione report.  
  
## <a name="sources-of-report-execution-data"></a>Origini dei dati per l'esecuzione del report  
 I log di esecuzione di un report contengono tutte le informazioni sull'esecuzione del report, tra cui il nome del report, il nome dell'utente che lo ha eseguito, la data e l'ora di esecuzione e l'estensione per il recapito utilizzata per distribuire il report. Per visualizzare e analizzare questi dati, è possibile copiare il log di esecuzione del report in tabelle di database, in modo che sia più semplice eseguire query e creare report sui dati di esecuzione.  
  
 I file di log contengono numerose voci sull'esecuzione dei report e su altre attività del server. Dato che i file di log contengono una così grande quantità di dati, è consigliabile utilizzare Gestione report se si desidera verificare unicamente quando è avvenuta l'ultima esecuzione del report. Se sono necessarie informazioni aggiuntive, è necessario visualizzare i file di log.  
  
> [!NOTE]  
>  In Gestione report non vengono visualizzate la data e l'ora di elaborazione dei report eseguiti su richiesta.  
  
 Nella tabella seguente viene descritto come visualizzare la data e l'ora di elaborazione per vari tipi di report.  
  
|Tipo di report|Posizione delle informazioni sulla data e l'ora|Operazioni da eseguire per visualizzare le informazioni|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|Report che viene eseguito come snapshot del report|Pagina Contenuto. Per ulteriori informazioni, vedere [pagina contenuto &#40; Gestione report &#41; ](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378).|1) Individuare la cartella che contiene il report.<br /><br /> 2) Impostare la visualizzazione Dettagli per la cartella.<br /><br /> 3) Osservare data e ora nella colonna **Data ultima esecuzione** .|  
|Snapshot della cronologia del report|Pagina delle proprietà Cronologia. Per ulteriori informazioni, vedere [pagina delle proprietà Opzioni Snapshot &#40; Gestione report &#41; ](http://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).|1) Aprire il report.<br /><br /> 2) Fare clic sulla pagina **Proprietà** .<br /><br /> 3) Fare clic sulla scheda **Cronologia** .<br /><br /> 4) Osservare data e ora nella colonna **Data ultima esecuzione** .|  
|Report memorizzato nella cache|Pianificazione utilizzata per creare e aggiornare il report memorizzato nella cache.|1) Aprire il report.<br /><br /> 2) Fare clic sulla pagina **Proprietà** .<br /><br /> 3) Fare clic sulla scheda **Esecuzione** .<br /><br /> 4) Aprire la pianificazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [File di log e origini di Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Impostare le proprietà di elaborazione di Report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gestione report &#40; Modalità nativa SSRS &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  