---
title: "Avvio di SQL Server in modalità utente singolo | Microsoft Docs"
ms.custom: 
ms.date: 09/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6e809d7098ed244ddf14331c310de8ce92f77fb7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="start-sql-server-in-single-user-mode"></a>Avvio di SQL Server in modalità utente singolo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In alcuni casi potrebbe essere necessario avviare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo usando l'**opzione di avvio -m.** Ad esempio, può risultare utile modificare le opzioni di configurazione del server oppure recuperare un database master o un altro database di sistema danneggiato. In entrambi i casi, è necessario avviare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo.  
  
 L'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo consente a qualsiasi membro del gruppo Administrators locale del computer di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come membro del ruolo predefinito del server sysadmin. Per altre informazioni, vedere [Connettersi a SQL Server se gli amministratori di sistema sono bloccati](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Quando si avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, si noti quanto segue:  
  
-   La connessione al server è consentita a un solo utente.  
  
-   Il processo CHECKPOINT non viene eseguito. Per impostazione predefinita, tale processo viene eseguito automaticamente all'avvio.  
  
> [!NOTE]  
>  Arrestare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent prima di connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo. In caso contrario, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent utilizzerà la connessione, bloccandola.  
  
Quando si avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] può connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In Esplora oggetti in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] potrebbe verificarsi un errore perché per alcune operazioni sono necessarie più connessioni. Per gestire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, eseguire istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] stabilendo la connessione solo tramite l'editor di query in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]oppure usare l'utilità [sqlcmd](../../tools/sqlcmd-utility.md).  
  
Quando si usa l'opzione **-m** con **SQLCMD** o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è possibile limitare le connessioni a un'applicazione client specifica. 

> [!NOTE]
> In Linux **SQLCMD** deve essere scritto in maiuscolo come illustrato.

Ad esempio, **-m"SQLCMD"** limita le connessioni a una singola connessione che deve identificarsi come programma client **SQLCMD**. Utilizzare questa opzione quando si avvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo e un'applicazione client sconosciuta accede all'unica connessione disponibile. Per connettersi con l'editor di query in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], usare **-m"Microsoft SQL Server Management Studio - Query"**.  
  
> [!IMPORTANT]  
>  Non utilizzare tale opzione come caratteristica di sicurezza. L'applicazione client fornisce il nome dell'applicazione client stessa e può indicare un nome falso come parte della stringa di connessione.  
  
## <a name="note-for-clustered-installations"></a>Nota per le installazioni cluster  
 Per un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente cluster, quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviato in modalità utente singolo, la dll della risorsa cluster utilizza tutta la connessione disponibile, bloccando pertanto qualsiasi altra connessione al server. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si trova in questo stato, se si tenta di portare la risorsa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] online, potrebbe venire eseguito il failover della risorsa SQL a un nodo diverso se la risorsa è configurata in modo da influire sul gruppo.  
  
 Per aggirare il problema, attenersi alla procedura seguente:  
  
1.  Rimuovere il parametro di avvio -m dalle proprietà avanzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Portare la risorsa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline.  
  
3.  Dal nodo del proprietario corrente di questo gruppo eseguire il comando seguente da a un prompt dei comandi:  
    net start MSSQLSERVER /m.  
  
4.  Verificare tramite Amministrazione cluster o tramite la console di gestione del cluster di failover che la risorsa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia ancora offline.  
  
5.  Connettersi ora a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il comando seguente ed eseguire l'operazione necessaria: SQLCMD -E -S\<nomeserver>.  
  
6.  Dopo aver completato l'operazione, chiudere il prompt dei comandi e riportare online SQL e le altre risorse tramite Amministrazione cluster.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio, arresto o sospensione del servizio SQL Server Agent](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [Utilità sqlcmd](../../tools/sqlcmd-utility.md)   
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opzioni di avvio del servizio del motore di database](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
