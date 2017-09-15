---
title: Prerequisiti per le esercitazioni (Generatore Report) | Documenti Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2c2056dccbb2d65e880928e4ec37a70080cfbf53
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---

# <a name="prerequisites-for-tutorials-report-builder"></a>Prerequisiti per le esercitazioni (Generatore report)

Per eseguire le esercitazioni di Generatore report è necessario essere in grado di visualizzare e salvare i report impaginati di [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] in un server di report o in un sito di SharePoint integrato in un server di report. Per i dati, tutte le esercitazioni utilizzano query letterali che devono essere elaborate da un'istanza di SQL Server.  
  
Se non si dispone dell'accesso a un server di report, a un sito o a un'origine dati, sarà possibile apprendere l'utilizzo di Generatore report attraverso la compilazione di un report offline. Vedere [esercitazione: creare un Report grafico rapido Offline &#40; Generatore report &#41; ](../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  

## <a name="requirements"></a>Requisiti

Per completare le esercitazioni di Generatore report, è necessario soddisfare i requisiti seguenti:  
  
-   Accesso a Generatore Report. È possibile eseguire Generatore report da un server di report di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o un server di report di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] in modalità integrata SharePoint. Nei diversi tipi di server l'unica differenza riguarda il primo passaggio, ovvero l'apertura di Generatore report.  
  
    In un server di report selezionare **Nuovo** > **Report impaginato**.
  
    In un server di report in modalità integrata SharePoint, nella scheda **Documenti** selezionare **Nuovo documento**, quindi selezionare **Report di Generatore report**nell'elenco a discesa. Ad esempio, `http://<servername>/sites/mySite/reports`. L'amministratore di SharePoint deve abilitare la caratteristica Report di Generatore report per ogni raccolta documenti.  
  
-   URL di un server di report di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o di un sito di SharePoint integrato con un server di report di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . È necessario disporre dell'autorizzazione per il salvataggio e la visualizzazione di report, origini dati condivise, set di dati condivisi, parti di report e modelli. Per impostazione predefinita, l'URL per un server di report è `http://<servername>/reportserver`. Per impostazione predefinita, l'URL per un sito SharePoint è `http://<sitename>` o `http://<server>/site`.  
  
-   Il nome di un'istanza di SQL Server e credenziali sufficienti per l'accesso in sola lettura a qualsiasi database. Le query del set di dati nelle esercitazioni vengono utilizzati dati letterali, ma ogni query deve essere elaborata da un'istanza di SQL Server per restituire i metadati necessari per un set di dati del report. Ad esempio, nella stringa di connessione seguente viene specificato solo un server: `data source=<servername>`. È necessario disporre dell'accesso in lettura al database predefinito assegnato all'utente dall'amministratore di sistema che concede l'autorizzazione per l'accesso al server. È inoltre possibile specificare un database, come illustrato nella stringa di connessione seguente: `data source=<servername>;initial catalog=<database>`.  
  
-   Per il [esercitazione: Report mappa (Generatore Report)](Tutorial:%20Map%20Report%20\(Report%20Builder\).md), il server di report deve essere configurato per supportare le mappe di Bing come sfondo. Per altre informazioni, vedere [Pianificare il supporto dei report mappa](http://msdn.microsoft.com/en-us/5ddc97a7-7ee5-475d-bc49-3b814dce7e19).   

-   Il [esercitazione: creazione di drill-through e report principali (Generatore Report)](Tutorial:%20Creating%20Drillthrough%20and%20Main%20Reports%20\(Report%20Builder\).md) esercitazione richiede l'accesso al cubo vendite Contoso. Per altre informazioni, vedere l'esercitazione. 
  
L'amministratore del server di report deve concedere le autorizzazioni necessarie per il server di report, configurare i percorsi delle cartelle [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] e configurare le opzioni predefinite di Generatore report. Per altre informazioni, vedere [Installare e disinstallare Generatore report](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416).  

## <a name="next-steps"></a>Passaggi successivi

[Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md)  

Ulteriori domande? [Provare a porre il forum di Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)