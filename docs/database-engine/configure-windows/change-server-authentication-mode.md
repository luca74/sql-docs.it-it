---
title: "Modifica della modalità di autenticazione del server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 63282fbc0b88a940f1a3d90a40d025a8338f3427
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="change-server-authentication-mode"></a>Modifica della modalità di autenticazione del server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento descrive come modificare la modalità di autenticazione del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durante l'installazione [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] è impostato su **Autenticazione di Windows** o **Autenticazione di SQL Server e di Windows**. Dopo l'installazione, è possibile modificare in qualsiasi momento la modalità di autenticazione.  
  
 Se si seleziona **Modalità di autenticazione di Windows** durante l'installazione, l'account di accesso sa viene disabilitato e il programma di installazione assegna una password. Se in seguito si modifica la modalità di autenticazione in **Autenticazione di SQL Server e di Windows**, l'account di accesso sa resterà disabilitato. Per usare l'account di accesso sa, usare l'istruzione ALTER LOGIN per abilitare l'account sa e assegnare una nuova password. È possibile connettersi al server tramite l'account sa solo se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per modificare la modalità di autenticazione del server utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 L'account sa è un account noto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che viene spesso preso di mira da utenti malintenzionati. Non abilitare l'account sa a meno che l'applicazione non lo richieda. È estremamente importante utilizzare una password complessa per l'accesso all'account sa.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-change-security-authentication-mode"></a>Per modificare la modalità di autenticazione di sicurezza  
  
1.  In Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fare clic con il pulsante destro del mouse sul server e quindi scegliere **Proprietà**.  
  
2.  Nella pagina **Sicurezza** selezionare la nuova modalità di autenticazione del server dall'elenco **Autenticazione server**e quindi fare clic su **OK**.  
  
3.  Nella finestra di dialogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fare clic su **OK** per confermare il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  In Esplora oggetti fare clic con il pulsante destro del mouse sul server e quindi scegliere **Riavvia**. Se è in esecuzione, è necessario riavviare anche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
#### <a name="to-enable-the-sa-login"></a>Per abilitare l'account di accesso sa  
  
1.  In Esplora oggetti espandere **Sicurezza**e quindi Account di accesso, fare clic con il pulsante destro del mouse su **sa**e infine scegliere **Proprietà**.  
  
2.  Nella pagina **Generale** potrebbe essere necessario creare e confermare una password per l'account di accesso.  
  
3.  Nella pagina **Stato** fare clic su **Abilitato** nella sezione **Account di accesso**, quindi scegliere **OK**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per abilitare l'account di accesso sa**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. Nell'esempio seguente viene abilitato l'account di accesso sa e viene impostata una nuova password.  
  
    ```  
    ALTER LOGIN sa ENABLE ;  
    GO  
    ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
    GO  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Password complesse](../../relational-databases/security/strong-passwords.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [Connettersi a SQL Server se gli amministratori di sistema sono bloccati](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  
