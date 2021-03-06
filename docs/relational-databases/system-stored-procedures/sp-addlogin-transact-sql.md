---
title: sp_addlogin (Transact-SQL) | Documenti Microsoft
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
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 09a8425f9c3d773af00a0418ff4430839c221d87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuovo account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consente a un utente di connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilizzare [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) invece.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @loginame=] '*accesso*'  
 Nome dell'account di accesso. *account di accesso* è **sysname**, non prevede alcun valore predefinito.  
  
 [ @passwd=] '*password*'  
 Password dell'account di accesso. *password* è **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*database*'  
 Database predefinito dell'account di accesso, ovvero il primo database a cui viene connesso l'account dopo l'accesso. *database* è **sysname**, il valore predefinito è **master**.  
  
 [ @deflanguage=] '*language*'  
 Lingua predefinita dell'account di accesso. *lingua* è **sysname**, con un valore predefinito è NULL. Se *language* non viene specificato, il valore predefinito *language* del nuovo account di accesso è impostato sulla lingua predefinita corrente del server.  
  
 [ @sid=] '*sid*'  
 ID di sicurezza (SID, Security Identification Number). *SID* è **varbinary (16)**, con un valore predefinito è NULL. Se *sid* è NULL, il sistema genera un SID per il nuovo account di accesso. Nonostante l'uso di un **varbinary** il tipo di dati, valori diversi da NULL devono contenere esattamente 16 byte di lunghezza e non deve essere già presente. Specifica di *sid* è utile, ad esempio, durante la creazione di script o lo spostamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli account di accesso da un server a un altro e si desidera che gli account di accesso abbia lo stesso SID in server diversi.  
  
 [ @encryptopt=] '*encryption_option*'  
 Specifica se la password viene passata in forma non crittografata o come hash della password non crittografata. Si noti che non viene applicata alcuna crittografia. Le parole "crittografia" ed "encryption" vengono utilizzate in questa descrizione per compatibilità con le versioni precedenti. Se la password viene passata in forma non crittografata, per la password viene eseguito l'hashing. Il valore hash viene archiviato. *encryption_option* è **varchar (20)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|NULL|La password viene passata in forma non crittografata. Impostazione predefinita.|  
|**della procedura skip_encryption**|Per la password è già stato eseguito l'hashing. [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve archiviare il valore senza ripetere l'hashing.|  
|**procedura skip_encryption_old**|Per la password specificata è stato eseguito l'hashing con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve archiviare il valore senza ripetere l'hashing. Questa opzione è disponibile solo in funzione delle operazioni di aggiornamento.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 I nomi degli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere composti da 1 a 128 caratteri, inclusi lettere, simboli e numeri. Gli account di accesso non può contenere una barra rovesciata (\\), un nome di accesso riservato, ad esempio sa o public, essere già esistenti oppure essere NULL o una stringa vuota (`''`).  
  
 Se viene specificato il nome di un database predefinito, è possibile connettersi a tale database senza eseguire l'istruzione USE. Tuttavia, è possibile utilizzare il database predefinito fino a quando non si concede l'accesso a tale database dal proprietario del database (tramite [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) o [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) o [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 Il numero SID è un GUID che identificherà in modo univoco l'account di accesso nel server.  
  
 Se si modifica la lingua predefinita del server non viene modificata la lingua predefinita degli account di accesso esistenti. Per modificare la lingua predefinita del server, utilizzare [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Utilizzando **della procedura skip_encryption** esclusione password hash è utile se la password è già stato eseguito l'hashing quando l'account di accesso viene aggiunto a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se è stato eseguito l'hashing della password da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare **la procedura skip_encryption_old**.  
  
 La stored procedure sp_addlogin non può essere eseguita in una transazione definita dall'utente.  
  
 Nella tabella seguente sono elencate varie stored procedure utilizzate in combinazione con sp_addlogin.  
  
|Stored procedure|Description|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Aggiunge un utente o un gruppo di Windows.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|Modifica la password di un utente.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|Modifica il database predefinito di un utente.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|Modifica la lingua predefinita di un utente.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY LOGIN.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-sql-server-login"></a>A. Creazione di un account di accesso di SQL Server  
 Nell'esempio seguente viene creato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utente `Victoria` con la password `B1r12-36`, senza specificare un database predefinito.  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. Creazione di un account di accesso di SQL Server con un database predefinito  
 Nell'esempio seguente viene creato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utente `Albert` con la password `B5432-3M6` e il database predefinito `corporate`.  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. Creazione di un account di accesso di SQL Server con una diversa lingua predefinita  
 Nell'esempio seguente viene creato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utente `TzTodorov` con la password `709hLKH7chjfwv`, il database predefinito `AdventureWorks2012` e la lingua predefinita `Bulgarian`.  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. Creazione di un account di accesso di SQL Server con un SID specifico  
 Nell'esempio seguente viene creato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utente `Michael`, con la password `B548bmM%f6`, il database predefinito `AdventureWorks2012`, la lingua predefinita `us_english` e il SID `0x0123456789ABCDEF0123456789ABCDEF`.  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
