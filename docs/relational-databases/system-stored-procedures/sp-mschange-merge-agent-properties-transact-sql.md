---
title: sp_MSchange_merge_agent_properties (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3563086e662ceb1dbe5cb8e8ea5b96b0c9430cc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangemergeagentproperties-transact-sql"></a>sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le proprietà di un processo dell'agente di Merge eseguito in un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva del server di distribuzione. Questa stored procedure viene utilizzata per modificare le proprietà quando il server di pubblicazione viene eseguito in un'istanza di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher**  =] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication =** ] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@subscriber=** ] **'***sottoscrittore***'**  
 Nome del Sottoscrittore. *Sottoscrittore* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 Nome del database di sottoscrizione. *subscriber_db* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@property =** ] **'***proprietà***'**  
 Proprietà della pubblicazione da modificare. *proprietà* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@value =** ] **'***valore***'**  
 Nuovo valore della proprietà. *valore* è **nvarchar (524)**, con un valore predefinito è NULL.  
  
 Nella tabella seguente vengono descritte le proprietà del processo dell'agente di merge che è possibile modificare e le limitazioni previste per i valori di tali proprietà.  
  
|Proprietà|Valore|Description|  
|--------------|-----------|-----------------|  
|**Descrizione**||Breve descrizione della sottoscrizione.|  
|**merge_job_login**||Account di accesso per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente.|  
|**merge_job_password**||Password dell'account di Windows utilizzato per l'esecuzione del processo dell'agente.|  
|**publisher_login**||Account di accesso da utilizzare durante la connessione a un server di pubblicazione per sincronizzare la sottoscrizione.|  
|**publisher_password**||Password del server di pubblicazione.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Autenticazione di Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_login**||Account di accesso da utilizzare durante la connessione a un Sottoscrittore per sincronizzare la sottoscrizione.|  
|**subscriber_password**||Password del Sottoscrittore.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Autenticazione di Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_MSchange_merge_agent_properties** viene utilizzata nella replica di tipo merge.  
  
 Quando il server di pubblicazione viene eseguito in un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva, è necessario utilizzare [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) per modificare le proprietà di un processo di agente di Merge che sincronizza una sottoscrizione push eseguita nel server di distribuzione.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server nel server di distribuzione possono eseguire **sp_MSchange_merge_agent_properties**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergepushsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
