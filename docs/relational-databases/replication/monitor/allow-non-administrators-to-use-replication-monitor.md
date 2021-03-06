---
title: Consentire a utenti non amministratori di usare Monitoraggio replica | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c719a6e7585f80adc2950cacacb1fb1ba5771701
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Autorizzazione di utenti non amministratori all'utilizzo di Monitoraggio replica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come consentire agli utenti non amministratore di utilizzare Monitoraggio replica in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Monitoraggio replica può essere utilizzato da membri che appartengono ai ruoli seguenti:  
  
-   Il ruolo predefinito del server **sysadmin** .  
  
     Questi utenti possono monitorare la replica e avere il controllo completo sulla modifica delle proprietà di replica, ad esempio le pianificazioni degli agenti, i profili agente e così via.  
  
-   Il ruolo di database **replmonitor** nel database di distribuzione.  
  
     Questi utenti possono monitorare la replica, ma non possono modificare le proprietà di replica.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per consentire a utenti non amministratori di utilizzare Monitoraggio replica tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per consentire a utenti non amministratori di utilizzare Monitoraggio replica, è necessario che un membro del ruolo predefinito del server **sysadmin** aggiunga l'utente al database di distribuzione e lo assegni al ruolo **replmonitor** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Per consentire a utenti non amministratori di utilizzare Monitoraggio replica  
  
1.  Connettersi al database di distribuzione in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere **Database**, **Database di sistema**e quindi il database di distribuzione (denominato **distribuzione** per impostazione predefinita).  
  
3.  Espandere **Sicurezza**, fare clic con il pulsante destro del mouse su **Utenti**e quindi scegliere **Nuovo utente**.  
  
4.  Immettere un nome utente e un account di accesso per l'utente.  
  
5.  Selezionare uno schema predefinito di **replmonitor**.  
  
6.  Selezionare la casella di controllo **replmonitor** nella griglia **Appartenenza a ruoli del database** .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Per aggiungere un utente al ruolo predefinito del database replmonitor  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_helpuser &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md). Se l'utente non è elencato in **UserName** nel set di risultati, è necessario concedergli l'accesso al database di distribuzione usando l'istruzione [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
2.  Nel database di distribuzione del server di distribuzione eseguire [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), specificando il valore **replmonitor** per il parametro **@rolename**. Se l'utente è elencato in **MemberName** nel set di risultati, appartiene già al ruolo.  
  
3.  Se l'utente non appartiene al ruolo **replmonitor**, eseguire [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) nel database di distribuzione del server di distribuzione. Specificare il valore **replmonitor** per **@rolename** e il nome dell'utente del database o l'account di accesso di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows da aggiungere per **@membername**.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Per rimuovere un utente dal ruolo predefinito del database replmonitor  
  
1.  Per verificare se l'utente appartiene al ruolo **replmonitor**, eseguire [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) nel database di distribuzione del server di distribuzione e specificare il valore **replmonitor** per **@rolename**. Se l'utente non è elencato in **MemberName** nel set di risultati, attualmente non appartiene al ruolo.  
  
2.  Se l'utente appartiene al ruolo **replmonitor**, eseguire [sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) nel database di distribuzione del server di distribuzione. Specificare il valore **replmonitor** per **@rolename** e il nome dell'utente del database o l'account di accesso di Windows rimosso per **@membername**.  
  
  
