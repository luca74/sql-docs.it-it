---
title: Eseguire il commit o inviare un insieme di modifiche (Master Data Services) | Documenti Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd91aef621a480510896500070bd36e55d778d66
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>Eseguire il commit o inviare un insieme di modifiche (Master Data Services)
  Un insieme di modifiche è una raccolta delle modifiche in sospeso relative ai dati master. Se le modifiche all'entità non richiedono l'approvazione dell'amministratore, è possibile eseguire il commit dell'insieme di modifiche. Se le modifiche all'entità richiedono l'approvazione dell'amministratore, è possibile inviare l'insieme di modifiche per l'approvazione.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** . Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   Se le modifiche all'entità non richiedono l'approvazione dell'amministratore, è possibile eseguire il commit dell'insieme di modifiche solo se si è proprietari dello stesso e il suo stato è aperto.  
  
-   Se le modifiche all'entità richiedono l'approvazione dell'amministratore, è possibile inviare l'insieme di modifiche per l'approvazione solo se si è proprietari dello stesso e il suo stato è aperto o rifiutato.  
  
## <a name="to-commit-a-local-changeset"></a>Per eseguire il commit di un insieme di modifiche locale  
 L'opzione di commit è disponibile solo per gli insiemi di modifiche locali per le entità in cui l'amministratore di entità non ha abilitato la richiesta di approvazione.  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare il modello e la versione, quindi fare clic su **Visualizzatore**.  
  
2.  Scegliere un'entità nel menu **Entità** .  
  
3.  Nel riquadro destro selezionare **Insiemi di modifiche** e fare doppio clic sull'insieme di modifiche di cui eseguire il commit.  
  
4.  Fare clic su **Esegui commit**.  
  
## <a name="to-submit-a-changeset"></a>Per inviare un insieme di modifiche  
 L'opzione di invio è disponibile solo per gli insiemi di modifiche per le entità in cui l'amministratore di entità ha abilitato la richiesta di approvazione.  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare il modello e la versione, quindi fare clic su **Visualizzatore**.  
  
2.  Scegliere un'entità nel menu **Entità** .  
  
3.  Nel riquadro destro selezionare **Insiemi di modifiche** e fare doppio clic sull'insieme di modifiche da inviare.  
  
4.  Fare clic su **Invia**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Applicare e rifiutare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Applicare e aggiornare un insieme di modifiche &#40; Master Data Services &#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Applicare e rifiutare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  