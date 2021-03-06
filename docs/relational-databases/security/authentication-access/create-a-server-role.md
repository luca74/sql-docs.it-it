---
title: Creare un ruolo del server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.SERVERROLE.GENERAL.F1
- sql13.swb.serverrole.memberships.f1
- sql13.swb.serverrole.members.f1
helpviewer_keywords:
- SERVER ROLE, creating
ms.assetid: 74f19992-8082-4ed7-92a1-04fe676ee82d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca312c8c2d5d83b7e8fb233f9d9dfac3c37fcaab
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-a-server-role"></a>Creazione di un ruolo del server
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)] Questo argomento descrive come creare un nuovo ruolo server in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un nuovo ruolo del server utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Non è possibile concedere ai ruoli del server l'autorizzazione sulle entità a protezione diretta a livello di database. Per creare ruoli del database, vedere [CREATE ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-role-transact-sql.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
  
-   È richiesta l'autorizzazione CREATE SERVER ROLE o l'appartenenza al ruolo predefinito del server sysadmin.  
  
-   È anche richiesta l'autorizzazione IMPERSONATE in *server_principal* per gli account di accesso, l'autorizzazione ALTER per i ruoli del server usati come *server_principal*o l'appartenenza a un gruppo di Windows usato come server_principal.  
  
-   Se si utilizza l'opzione AUTHORIZATION per assegnare la proprietà del ruolo del server, sono necessarie anche le autorizzazioni seguenti:  
  
    -   Per assegnare la proprietà di un ruolo del server a un altro account di accesso, è richiesta l'autorizzazione IMPERSONATE per tale account di accesso.  
  
    -   Per assegnare la proprietà di un ruolo del server a un altro ruolo del server, è richiesta l'appartenenza al ruolo del server destinatario oppure l'autorizzazione ALTER per tale ruolo.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-new-server-role"></a>Per creare un nuovo ruolo del server  
  
1.  In Esplora oggetti espandere il server in cui si desidera creare il nuovo ruolo del server.  
  
2.  Espandere la cartella **Sicurezza** .  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Ruoli server** e scegliere **Nuovo ruolo server**.  
  
4.  Nella pagina **Generale***finestra di dialogo* Nuovo ruolo server - **nome_ruolo_server** immettere un nome per il nuovo ruolo del server nella casella **Nome ruolo server** .  
  
5.  Nella casella **Proprietario** immettere il nome dell'entità del server proprietaria del nuovo ruolo. In alternativa, fare clic sui puntini di sospensione **(...)** per aprire la finestra di dialogo **Seleziona account di accesso o ruolo server** .  
  
6.  In **Entità a protezione diretta**selezionare una o più entità a protezione diretta a livello di server. Quando è selezionata un'entità a protezione diretta, al ruolo del server è possibile concedere o negare autorizzazioni per tale entità.  
  
7.  Nella casella **Autorizzazioni: Esplicite** selezionare la casella di controllo per concedere, concedere con concessione o negare autorizzazioni al ruolo del server per le entità a protezione diretta selezionate. Se un'autorizzazione non può essere concessa o negata a tutte le entità a protezione diretta selezionate, l'autorizzazione viene rappresentata come selezione parziale.  
  
8.  Nella pagina **Membri** utilizzare il pulsante **Aggiungi** per aggiungere account di accesso che rappresentano singoli utenti o gruppi al nuovo ruolo del server.  
  
9. Un ruolo del server definito dall'utente può essere membro di un altro ruolo del server. Nella pagina **Appartenenze** selezionare una casella di controllo per impostare il ruolo del server definito dall'utente corrente come membro di un ruolo del server selezionato.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-new-server-role"></a>Per creare un nuovo ruolo del server  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    --Creates the server role auditors that is owned the securityadmin fixed server role.  
    USE master;  
    CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-role-transact-sql.md).  
  
  
