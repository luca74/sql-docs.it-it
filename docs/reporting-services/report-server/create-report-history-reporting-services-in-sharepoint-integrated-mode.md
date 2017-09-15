---
title: "Creare la cronologia del Report (Reporting Services in modalità integrata SharePoint) | Documenti Microsoft"
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
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e1388fba5963d5571d293f2d995c73bb3d83d3b
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>Creare la cronologia dei report (Reporting Services in modalità integrata SharePoint)
  La cronologia di un report è una raccolta di snapshot del report creati nel tempo. Ogni snapshot è una copia del report nello stato in cui si trovava al momento della creazione. e include il layout e i dati del report aggiornati al momento della creazione dello snapshot. Le informazioni sul rendering non vengono archiviate con lo snapshot. Gli snapshot della cronologia del report vengono aperti in una pagina HTML nella web part Visualizzatore report. Dopo il rendering, lo snapshot può essere esportato in altri formati di applicazione.  
  
 Per creare la cronologia del report, è necessario che il report possa essere eseguito automaticamente, ovvero che il server di report sia in grado di eseguire il report senza l'interazione dell'utente. È necessario disporre dell'autorizzazione Modifica elementi sulla raccolta che contiene il report. Per visualizzare o eliminare la cronologia del report, è necessario disporre dell'autorizzazione Visualizzazione versioni o Eliminazione versioni.  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>Per creare uno snapshot o una cronologia del report su richiesta  
  
1.  Selezionare il report.  
  
2.  Fare clic per visualizzare la freccia in giù e quindi selezionare **Visualizza cronologia report**.  
  
3.  Fare clic su **Nuovo snapshot**. Se tale pulsante non è visualizzato, significa che non si dispone delle autorizzazioni necessarie per la creazione di snapshot nella cronologia del report.  
  
4.  Per visualizzare lo snapshot appena creato, selezionarlo dall'elenco. Ogni snapshot è identificato da un timestamp che ne indica la data e l'ora di creazione. Non è possibile rinominare lo snapshot, spostarlo in un altro percorso o modificarlo.  
  
### <a name="to-schedule-report-history"></a>Per pianificare la cronologia di un report  
  
1.  Selezionare il report.  
  
2.  Fare clic per visualizzare la freccia in giù e quindi selezionare **Gestisci opzioni di elaborazione**.  
  
3.  In **Opzioni snapshot cronologia**fare clic su **Crea snapshot della cronologia del report in base a una pianificazione**.  
  
4.  Se si dispone di una pianificazione condivisa che contiene le informazioni di pianificazione che si desidera usare, fare clic su **In base a una pianificazione condivisa** e selezionare la pianificazione da usare. In caso contrario fare clic su **In base a una pianificazione personalizzata**, quindi su **Configura** per specificare le opzioni relative alla creazione della cronologia del report in base a una pianificazione ricorrente.  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>Per creare la cronologia del report quando i dati del report vengono aggiornati  
  
1.  Selezionare il report.  
  
2.  Fare clic per visualizzare la freccia in giù e quindi selezionare **Gestisci opzioni di elaborazione**.  
  
3.  In **Opzioni snapshot cronologia**fare clic su **Archivia tutti gli snapshot di dati del report nella cronologia del report**.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le opzioni di elaborazione &#40; Reporting Services in SharePoint integrata modalità &#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  