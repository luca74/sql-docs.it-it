---
title: sp_password (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b461f601e94756d1406da13f1da99f8b1df50198
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="sppassword-transact-sql"></a>sp_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge o modifica una password per un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilizzare [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@old=** ] **'***old_password***'**  
 Vecchia password. *old_password* è **sysname**, con un valore predefinito è NULL.  
  
 [  **@new=** ] **'***new_password***'**  
 Nuova password. *new_password* è **sysname**, non prevede alcun valore predefinito. *old_password* deve essere specificato se non si utilizzano parametri denominati.  
  
> [!IMPORTANT]  
>  Non utilizzare una password NULL. Usare una password complessa. Per altre informazioni, vedere [Strong Passwords](../../relational-databases/security/strong-passwords.md).  
  
 [  **@loginame=** ] **'***accesso***'**  
 Nome dell'account di accesso interessato dalla modifica della password. *account di accesso* è **sysname**, con un valore predefinito è NULL. *account di accesso* deve esistere e può essere specificato solo dai membri del **sysadmin** o **securityadmin** ruoli predefiniti del server.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_password** chiama ALTER LOGIN. che supporta opzioni aggiuntive. Per informazioni sulla modifica delle password, vedere [ALTER LOGIN &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_password** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY LOGIN. È inoltre richiesta l'autorizzazione CONTROL SERVER per reimpostare una password senza specificare la vecchia password oppure se l'account di accesso da modificare dispone dell'autorizzazione CONTROL SERVER.  
  
 Un'entità può modificare la propria password.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. Modifica della password di un account di accesso con vecchia password non nota  
 Nell'esempio seguente viene illustrato l'utilizzo di `ALTER LOGIN` per modificare la password dell'account di accesso `Victoria` impostandola su `B3r1000d#2-36`. Questo è il metodo consigliato. L'utente che esegue questo comando deve disporre dell'autorizzazione CONTROL SERVER.  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. Modifica di una password  
 Nell'esempio seguente viene illustrato l'utilizzo di `ALTER LOGIN` per modificare la password dell'account di accesso `Victoria` da `B3r1000d#2-36` a `V1cteAmanti55imE`. Questo è il metodo consigliato. L'utente `Victoria` può eseguire questo comando senza disporre di autorizzazioni aggiuntive. Per gli altri utenti è richiesta l'autorizzazione ALTER ANY LOGIN.  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
