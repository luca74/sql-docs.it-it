---
title: Installare SQL Server | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/24/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 3bf6c76a72b4414163b68f4cbdd00756b5f4f0bf
ms.contentlocale: it-it
ms.lasthandoff: 09/08/2017

---
# <a name="install-sql-server"></a>Installare SQL Server

 > Per contenuti relativi alle versioni precedenti di SQL Server, vedere [Installare SQL Server 2014](https://msdn.microsoft.com/en-US/library/bb500395(SQL.120).aspx).

 A partire da [!INCLUDE[sssql15](../../includes/sssql15-md.md)], [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] è disponibile solo come applicazione a 64 bit. Di seguito sono riportati importanti dettagli su come ottenere SQL Server e su come eseguire l'installazione.

## <a name="installation-details"></a>Informazioni sull'installazione
  
*  **Opzioni**: eseguire l'installazione con l'Installazione guidata, il prompt dei comandi oppure sysprep
 
*  **Requisiti**: prima di eseguire l'installazione, rivedere i requisiti di installazione, i controlli di configurazione del sistema e le considerazioni sulla sicurezza in [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Processo**: per istruzioni dettagliate sul processo di installazione, vedere [Installazione per SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md)

* **Esempi di database e di codice**: 
    * Non sono installati come parte predefinita dell'installazione di SQL Server 
    * Per installare tali elementi per edizioni non Express di SQL Server, vedere il [GitHub](http://github.com/Microsoft/sql-server-samples)
    

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>Modalità di installazione [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]
 
|Title|Description|  
|-----------|-----------------|  
|[Installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] in Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Vedere questo argomento per installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] in Windows Server Core.|  
|[Parametri di controllo di Controllo configurazione sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Descrive la funzione di controllo configurazione sistema (SCC).|  
|[Installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] dall'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Argomento contenente le procedure per un'installazione tipica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite l'Installazione guidata.|  
|[Installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Argomento contenente le procedure, la sintassi di esempio e i parametri di installazione per l'esecuzione dell'installazione automatica.|  
|[Installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] tramite un file di configurazione](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Argomento contenente procedure in cui vengono forniti la sintassi di esempio e i parametri di installazione per l'esecuzione del programma di installazione tramite un file di configurazione.|  
|[Installare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] con SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Argomento contenente procedure che fornisce la sintassi di esempio e i parametri di installazione per l'esecuzione del programma di installazione con SysPrep.|  
|[Aggiungere funzionalità a un'istanza di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] &#40;programma di installazione&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Argomento contenente le procedure per l'aggiornamento dei componenti di un'istanza esistente di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Ripristinare un'installazione non riuscita di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Argomento contenente le procedure per il ripristino di un'installazione danneggiata di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Rinominare un computer che ospita un'istanza autonoma di SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Argomento contenente le procedure per l'aggiornamento dei metadati di sistema archiviati in sys.servers.|  
|[Installare gli aggiornamenti di manutenzione per [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|Argomento contenente le procedure per l'installazione di aggiornamenti per [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Argomento contenente le procedure per la verifica degli errori nei file di log del programma di installazione.|  
|[Convalidare un'installazione di SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Esaminare l'utilizzo del report SQL Discovery per verificare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer.|  
  
  
## <a name="how-to-install-individual-components"></a>Come installare i singoli componenti  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Installare il motore di database di SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Viene descritto come installare e configurare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Installare la replica di SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Viene descritto come installare e configurare la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Install Distributed Replay - Overview](../../tools/distributed-replay/install-distributed-replay-overview.md)|Vengono elencati gli argomenti sull'installazione della funzionalità Riesecuzione distribuita.|  
|[Install SQL Server Management Tools with SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|Viene descritto come installare e configurare gli strumenti di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Installare SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Vengono fornite considerazioni per l'installazione dei componenti di PowerShell per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  

## <a name="how-to-configure-sql-server"></a>Per configurare SQL Server  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|In questo argomento viene fornita una panoramica della configurazione dei firewall e viene illustrato come configurare Windows Firewall.|  
|[Configurare un computer multihomed per l'accesso a SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|In questo argomento viene descritto come configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows Firewall con sicurezza avanzata per fornire le connessioni di rete a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente multihomed.|  
|[Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Le procedure descritte in questo argomento consentono di configurare le impostazioni delle porte e del firewall necessarie per accedere ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint.|  
  
## <a name="related-sections"></a>Sezioni correlate  
[Edizioni e funzionalità supportate di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[Aggiungere caratteristiche di Business Intelligence [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [Installazione del cluster di failover di SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Vedere anche  

[Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Aggiornamento a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Disinstallare [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
