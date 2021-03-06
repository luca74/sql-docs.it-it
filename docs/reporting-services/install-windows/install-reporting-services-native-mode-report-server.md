---
title: "Installare un server di report di Reporting Services 2016 in modalità nativa | Microsoft Docs"
ms.custom: 
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
caps.latest.revision: "68"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: 23104fa56aeb157b19d43b332c2d570613ed5a62
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="install-reporting-services-2016-native-mode-report-server"></a>Installare un server di report di Reporting Services 2016 in modalità nativa

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Informazioni su come installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa. Questo consentirà di accedere a [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] in cui è possibile gestire report e altri elementi.

> [!NOTE]
> Per informazioni sul server di report di Power BI, vedere [Installare il server di report di Power BI](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

Un server di report in modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] costituisce la modalità server predefinita di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e può essere installato mediante l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la riga di comando. Nell'Installazione guidata è possibile scegliere di installare i file e di configurare il server con le impostazioni predefinite oppure di installare solo i file. In questo argomento viene esaminata la *configurazione predefinita per la modalità nativa* in cui tramite il programma di installazione viene sia installata e configurata un'istanza del server di report. Al termine del programma di installazione, il server di report è in esecuzione e può essere usato per la gestione di report e la visualizzazione di report di base.  Le funzionalità aggiuntive, ad esempio l'integrazione di [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] e la distribuzione della posta elettronica con l'elaborazione della sottoscrizione, richiedono una configurazione aggiuntiva.  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> Informazioni sulla configurazione predefinita  
 Tramite l'installazione vengono installate le seguenti funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quando si seleziona l'opzione di configurazione predefinita per la modalità nativa:  
  
-   Il servizio del server di report che include il servizio Web ReportServer, l'applicazione di elaborazione in background e [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] per la visualizzazione e la gestione dei report e delle autorizzazioni.  
  
-   Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Le utilità della riga di comando di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , rsconfig.exe, rskeymgmt.exe e rs.exe.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sono ora download separati.  
  
 Per un'installazione del server di report in modalità nativa, il programma di installazione configura gli elementi seguenti:  
  
-   Account del servizio del server di report.  
  
-   URL del servizio Web ReportServer.  
  
-   URL [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] .  
  
-   Database del server di report.  
  
-   Accesso dell'account del servizio ai database del server di report.  
  
-   Informazioni di connessione, anche note come nome origine dati (DSN), per i database del server di report.  
  
 Tramite il programma di installazione non viene configurato l'account di esecuzione automatica, la posta elettronica del server di report, il backup delle chiavi di crittografia o una distribuzione con scalabilità orizzontale. Per configurare queste proprietà, è possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> Casi in cui installare la configurazione predefinita per la modalità nativa  
 Una configurazione predefinita comporta l'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un stato operativo, che consente di utilizzare immediatamente il server di report al termine dell'installazione. Specificare questa modalità se si desidera ridurre il numero di passaggi, eliminando tutte le attività di configurazione altrimenti necessarie nello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 L'installazione della configurazione predefinita non garantisce il corretto funzionamento del server di report al termine dell'installazione. All'avvio del servizio, potrebbe non essere possibile registrare gli URL predefiniti. Eseguire sempre il test dell'installazione per verificare che il servizio venga avviato ed eseguito nel modo previsto.  Vedere [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).
  
##  <a name="bkmk_requirements"></a> Requisiti  
 L'opzione di configurazione predefinita consente di utilizzare i valori predefiniti per configurare le impostazioni principali necessarie per rendere operativo un server di report. Di seguito vengono indicati i requisiti per questa opzione di installazione:  
  
-   Esaminare [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) .  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] devono essere installati insieme nella stessa istanza. Nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene ospitato il database del server di report creato e configurato dal programma di installazione.  
  
-   L'account utente utilizzato per eseguire il programma di installazione deve appartenere al gruppo Administrators locale e deve disporre dell'autorizzazione per accedere e creare i database nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita i database del server di report.  
  
-   Il programma di installazione deve poter usare i valori predefiniti per riservare gli URL necessari per accedere al server di report e al [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. Questi valori sono la porta 80, un carattere jolly complesso e i nomi delle directory virtuali nel formato **ReportServer_\<***nome_istanza***>** e **Reports_\<***nome_istanza***>**.  
  
-   È necessario poter utilizzare i valori predefiniti con il programma di installazione per creare i database del server di report. Tali valori sono **ReportServer** e **ReportServerTempDB**. Se sono presenti database esistenti da un'installazione precedente, il programma di installazione si blocca perché non è in grado di configurare il server di report nella configurazione predefinita per la modalità nativa. Per sbloccare il programma di installazione, è necessario rinominare, spostare o eliminare i database.  
  
 Se il computer non soddisfa tutti i requisiti per un'installazione predefinita, è necessario installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità "solo file", quindi utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per configurarlo al termine dell'installazione.
 
 > [!IMPORTANT]
 > Anche se Reporting Services può essere installato in un ambiente che ha un controller di dominio di sola lettura, per funzionare correttamente richiede l'accesso a un controller di dominio scrivibile. Se Reporting Services può accedere solo a un controller di dominio di sola lettura, si possono verificare errori durante l'amministrazione del servizio.
  
##  <a name="bkmk_defaultURLreservations"></a> Prenotazioni URL predefinite  
 Le prenotazioni URL sono composte da un prefisso, un nome host, una porta e una directory virtuale:  
  
|Parte|Description|  
|----------|-----------------|  
|Prefisso|Il prefisso predefinito è HTTP. Se in precedenza è stato installato un certificato SSL (Secure Sockets Layer), il programma di installazione tenterà di creare prenotazioni URL che utilizzano il prefisso HTTPS.|  
|Nome host|Il nome host predefinito è un carattere jolly complesso (+). Specifica che il server di report accetta le richieste HTTP sulla porta designata per qualsiasi nome host risolto nel computer, tra cui `http://<computername>/reportserver`, `http://localhost/reportserver`, o `http://<IPAddress>/reportserver`.|  
|Port|La porta predefinita è 80. Si noti che se si utilizza un numero di porta diverso da 80, sarà necessario aggiungerlo in modo esplicito all'URL quando si apre un'applicazione Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una finestra del browser.|  
|Directory virtuale|Per impostazione predefinita, le directory virtuali vengono create nel formato ReportServer_\<*nome_istanza*> per il servizio Web ReportServer e Reports_\<*nome_istanza*> per il [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. Per il servizio Web ReportServer, la directory virtuale predefinita è **reportserver**. Per il [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], la directory virtuale predefinita è **reports**.|  
  
 Di seguito viene fornito un esempio di stringa dell'URL completa:  
  
-   `http://+:80/reportserver` consente l'accesso al server di report.  
  
-   `http://+:80/reports` consente l'accesso al [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)].
  
##  <a name="bkmk_installwithwizard"></a> Installare la modalità nativa con l'installazione guidata di SQL Server  
 Nell'elenco seguente sono illustrati i passaggi e le opzioni specifici di  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] selezionati nell'Installazione guidata di SQL Server. Nell'elenco non vengono descritte tutte le pagine che verranno visualizzate nell'installazione guidata, bensì solo le pagine correlate a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che fanno parte di un'installazione in modalità nativa.  
  
1.  Eseguire l'installazione guidata di SQL Server (setup.exe) e procedere alle seguenti pagine preliminari:  
  
    -   Codice Product Key  
  
    -   Condizioni di licenza  
  
    -   Regole globali  
  
    -   Microsoft Update  
  
    -   Aggiornamenti del prodotto  
  
    -   Installazione dei file di installazione  
  
    -   Regole di installazione  
  
2.  Nella pagina **Impostazione ruolo** selezionare **Installazione funzionalità SQL Server**.  
  
     ![Installazione di funzionalità di SQL Server per impostazione ruolo](../../reporting-services/install-windows/media/rs-setuprole.png "Installazione di funzionalità di SQL Server per impostazione ruolo")  
  
3.  Nella pagina **Selezione funzionalità** selezionare le opzioni seguenti:  
  
    -   (1) **Servizi motore di database**a meno che non sia già installata un'istanza del motore di database.  
  
    -   (2) **Reporting Services - Nativo**.  
  
     ![Selezionare la modalità nativa di SSRS nella selezione funzionalità](../../reporting-services/install-windows/media/rs-setupfeatureselection-native-withcircles.png "Selezionare la modalità nativa di SSRS nella selezione funzionalità")  
  
4.  Esaminare le **regole delle funzionalità** passate.  
  
5.  Nella pagina Configurazione istanza tenere presente che se si sceglie di configurare un' **istanza denominata**, sarà necessario usare il nome dell'istanza negli URL quando si passa a Gestione report e al server di report stesso. Se il nome dell'istanza è "THESQLINSTANCE", gli URL avranno un aspetto simile al seguente:  
  
    -   `http://[ServerName]/ReportServer_THESQLINSTANCE`  
  
    -   `http://[ServerName]/Reports_THESQLINSTANCE`  
  
6.  **Configurazione server**: se si intende usare la funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , nella pagina **Configurazione server** è possibile verificare se SQL Server Agent è configurato per il tipo di avvio **Automatico** .   Il tipo predefinito è manuale.  
  
7.  Aggiungere gli amministratori di SQL Server nella pagina **Configurazione del motore di database** .  
  
8.  Nella pagina **Configurazione di Reporting Services** selezionare **Installazione e configurazione**.  
  
     ![Configurazione della modalità di SSRS](../../reporting-services/install-windows/media/rs-setupconfiguration-native-with-circles.png "Configurazione della modalità nativa di SSRS")  
  
    > [!NOTE]  
    >  **Installazione e configurazione** non sarà disponibile a meno che non venga selezionata anche la funzionalità del database per l'installazione.  
  
9. Regole di configurazione delle funzionalità: verificare le regole passate. L'installazione guidata passa automaticamente allo stato **Pronto per l'installazione** se passano tutte le regole.  Specifiche di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], le regole verificano che il catalogo del server di report e il database del catalogo temporaneo non esistano già.  
  
10. Nella pagina **Inizio installazione** prendere nota del percorso del file di configurazione perché sarà possibile farvi riferimento in un secondo momento per un riepilogo utile della configurazione iniziale dei server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], inclusi i componenti installati, gli account del servizio e gli amministratori.  
  
11. Al completamento dell'installazione guidata di SQL Server, verificare l'installazione della modalità nativa predefinita tramite i passaggi di base riportati di seguito.  
  
    -   Aprire Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e verificare che sia possibile connettersi al server di report.  
  
    -   Aprire il browser **con privilegi di amministratore** e connettersi al [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], ad esempio `http://localhost/Reports`.  
  
    -   Aprire il browser con i privilegi di amministratore e connettersi alla pagina del server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Ad esempio,  `http://localhost/ReportServer`  
  
 Per ulteriori informazioni, vedere la sezione relativa alla modalità nativa dei due argomenti seguenti:  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Risoluzione dei problemi di installazione di Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
  
##  <a name="bkmk_additional_configuration"></a> Configurazione aggiuntiva  
  
-   Per configurare l'integrazione di [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] in modo che sia possibile aggiungere elementi di report a un dashboard di [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)], vedere [Integrazione del server di report e di Power BI](../../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
-   Per configurare la posta elettronica per l'elaborazione delle sottoscrizioni, vedere [Impostazioni posta elettronica - Modalità nativa di Reporting Services](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [Recapito tramite posta elettronica in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Per configurare il portale Web in modo che sia possibile accedervi in un computer remoto per visualizzare e gestire report, vedere [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) e [Configurare un server di report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
## <a name="see-also"></a>Vedere anche

[Risoluzione dei problemi di installazione di Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
[Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Configurare l'account del servizio del server di report](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
[Configurare gli URL del server di report](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Configurare una connessione del database del server di report](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Installazione di tipo "solo file" &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
[Inizializzare un server di report](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
[Configurare connessioni SSL in un server di report in modalità nativa](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   

Altre domande? [Visitare il forum su Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
