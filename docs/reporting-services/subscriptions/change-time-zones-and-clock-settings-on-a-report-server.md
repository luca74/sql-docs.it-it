---
title: Modificare i fusi orari e impostazioni dell'orologio in un Server di Report | Documenti Microsoft
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
- time zones [Reporting Services]
- clocks [Reporting Services]
- schedules [Reporting Services], clock settings
- schedules [Reporting Services], time zones
ms.assetid: 69a19468-baa1-40f6-b158-8afdab0f8968
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79f8068d11d707c4b0237d32e1645a80a12cdbbb
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="change-time-zones-and-clock-settings-on-a-report-server"></a>Modificare i fusi orari e le impostazioni dell'orologio in un server di report
  Il server di report utilizza sempre il fuso orario del computer in cui è installato. Non è infatti possibile configurare un server di report in modo che utilizzi un fuso orario diverso. Se un'applicazione client punta a un server di report di un altro fuso orario, per eseguire un'operazione pianificata viene utilizzato il fuso orario del server di report. In Gestione report e nelle pagine di gestione di SharePoint il fuso orario è indicato in tutte le pagine di pianificazione, in modo che l'utente possa sapere esattamente quando verrà eseguita un'operazione pianificata. Ad esempio, nella pagina per la creazione di pianificazioni personalizzate verrà indicato "Il tempo è espresso in (UTC - 8.00 h) Pacifico (USA e Canada)".  
  
## <a name="changing-the-time-zone-native-mode"></a>Modifica del fuso orario (modalità nativa)  
 Se si modifica il fuso orario in un computer che ospita un server di report, è necessario riavviare il servizio del server di report affinché le modifiche apportate abbiano effetto.  
  
 I valori del timestamp degli snapshot della cronologia del report esistenti vengono sincronizzati sulla nuova impostazione del fuso orario. Se, ad esempio, è stato generato uno snapshot della cronologia di un report alle 9.00 e quindi si cambia il fuso orario impostando quello successivo, per lo snapshot generato verranno indicate le 10.00 e non più le 9.00. alle 10:00  
  
 Le pianificazioni conservano le impostazioni esistenti, ma ne viene eseguito il mapping al nuovo fuso orario. Se, ad esempio, l'esecuzione di una pianificazione è impostata per le 2.00 ora di Greenwich e si cambia il fuso orario impostando l'ora solare Europa occidentale, la pianificazione verrà eseguita alle 2.00 ora solare Europa occidentale.  
  
 I valori timestamp delle proprietà, ad esempio l'ora di creazione di una cartella o di un report collegato, non vengono sincronizzati rispetto a una nuova impostazione del fuso orario. Se si crea un report il 25 giugno alle ore 9.00 e quindi si reimposta il fuso orario o l'orologio, il timestamp continuerà a indicare il 25 giugno alle ore 9.00.  
  
## <a name="changing-the-time-zone-sharepoint-mode"></a>Modifica del fuso orario (modalità SharePoint)  
 La configurazione del fuso orario per la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene gestita nell'ambito delle impostazioni internazionali di SharePoint. Per altre informazioni, vedere la pagina relativa alle [impostazioni locali in SharePoint Server 2010 (http://technet.microsoft.com/library/cc824907.aspx)](http://technet.microsoft.com/library/cc824907.aspx).  
  
## <a name="changing-the-clock-settings"></a>Modifica delle impostazioni dell'orologio  
 La modifica dell'orologio del computer non ha alcun effetto sui valori timestamp esistenti. Se, ad esempio, si sposta l'orologio avanti di un'ora, i timestamp degli snapshot della cronologia dei report non cambiano. Può verificarsi un ritardo di 10 secondi prima che Elaborazione pianificazione e recapito utilizzi la nuova impostazione. Il ritardo effettivo può variare se sono state modificate le impostazioni dell'intervallo di polling nei file di configurazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare e arrestare il servizio Server di Report](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [Pianificazioni](../../reporting-services/subscriptions/schedules.md)  
  
  