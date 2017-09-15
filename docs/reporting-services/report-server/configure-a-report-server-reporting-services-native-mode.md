---
title: "Configurare un Server di Report (Reporting Services in modalità nativa) | Documenti Microsoft"
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
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da2a367b582d39ea8cc8dc7ffc281a3515bb2d8b
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>Configurare un server di report (modalità nativa di Reporting Services)
  A seconda delle opzioni selezionate durante l'installazione, il server di report potrebbe richiedere passaggi di configurazione aggiuntivi prima che sia possibile utilizzarlo. La configurazione di un server di report è costituita almeno dai componenti seguenti:  
  
-   Un account del servizio del server di report configurato durante l'installazione.  
  
-   Un URL di servizio Web che fornisce l'accesso al server di report.  
  
-   Un database del server di report che archivia i dati dell'applicazione, i report e altri elementi.  
  
 Durante l'installazione vengono configurate le impostazioni minime se si seleziona una delle modalità di installazione seguenti: configurazione predefinita in modalità nativa o configurazione predefinita in modalità di integrazione con SharePoint. Se il server di report è stato installato in modalità "solo file", ovvero è stata selezionata l'opzione **Installa senza configurare il server di report** nell'Installazione guidata, viene configurato solo l'account del servizio. L'URL del servizio Web e il database del server di report devono essere configurati al termine dell'installazione.  
  
 Gestione report è una caratteristica facoltativa per un server di report in modalità nativa. È tuttavia consigliabile configurare questa funzionalità in modo da poter concedere agli utenti l'accesso al server di report e la gestione del relativo contenuto. Se il server di report è distribuito in modalità integrata SharePoint, utilizzare il front-end Web di un server di SharePoint per concedere l'accesso.  
  
 Se necessario, è possibile configurare caratteristiche aggiuntive come ad esempio la posta elettronica e l'account di esecuzione automatica del server di report. Per altre informazioni, vedere [Gestione di un server di report in modalità nativa](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Per configurare un server di report, utilizzare lo strumento di configurazione di Reporting Services.  
  
### <a name="to-minimally-configure-a-report-server-installation"></a>Per eseguire la configurazione minima di un'installazione del server di report  
  
1.  Avviare lo strumento di configurazione di Reporting Services e connettersi all'istanza del server di report. Per le istruzioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Fare clic su **URL servizio Web** per aprire la pagina per la configurazione di un URL per il server di report. Per istruzioni su come definire l'URL, vedere [configurare un URL &#40; Gestione configurazione SSRS &#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3.  Fare clic su **Database** per creare il database del server di report. Per istruzioni, vedere [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Tornare nella pagina **URL servizio Web** e fare clic sull'URL per verificarne il funzionamento.  
  
5.  Seguire le istruzioni riportate nella sezione "Passaggi successivi" per completare la distribuzione.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per completare la distribuzione, configurare Gestione report o l'integrazione con SharePoint. Per altre informazioni, vedere [Configurare Gestione report &#40;modalità nativa&#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md).  
  
 Se Windows Firewall è abilitato, la porta configurata per l'utilizzo da parte del server di report è probabilmente chiusa. La visualizzazione di una pagina vuota quando si tenta di aprire Gestione report da un computer client remoto indica che una porta potrebbe essere chiusa. Per informazioni sulla configurazione del firewall, vedere [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
 Se si utilizza Windows Vista o Windows Server 2008, è necessario completare altri passaggi prima che sia possibile aprire Gestione report in locale. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 Per verificare l'installazione, creare cartelle, caricare elementi ed eseguire report. Seguire le istruzioni in [Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) per verificare l'installazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di un server di report in modalità nativa](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Configurare un Firewall per l'accesso al Server di Report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Configurare un Server di Report in modalità nativa per amministratori locali &#40; SSRS &#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [Configurare un Server di Report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)   
 [Reporting Services di Configuration Manager &#40; Modalità nativa &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  