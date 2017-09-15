---
title: Opzione di configurazione del server cross db ownership chaining | Microsoft Docs
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: c42780edef8e57b9d8159d9dfe384554cade4fb2
ms.contentlocale: it-it
ms.lasthandoff: 08/16/2017

---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>Opzione di configurazione del server cross db ownership chaining
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  L'opzione **cross db ownership chaining** consente di configurare il concatenamento della proprietà tra database per un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Questa opzione del server consente di controllare il concatenamento della proprietà tra database a livello del database oppure di attivare il concatenamento della proprietà per tutti i database:  
  
-   Quando l'opzione **cross db ownership chaining** è impostata su 0 per l'istanza, il concatenamento della proprietà tra database è disabilitato per tutti i database.  
  
-   Quando invece l'opzione **cross db ownership chaining** è impostata su 1 per l'istanza, il concatenamento della proprietà tra database è attivato per tutti i database.  
  
-   È possibile impostare il concatenamento della proprietà tra database per singoli database utilizzando la clausola SET dell'istruzione ALTER DATABASE. Se si intende creare un nuovo database, è possibile utilizzare l'istruzione CREATE DATABASE per impostare l'opzione di concatenamento della proprietà tra database per il nuovo database.  
  
     È consigliabile non impostare l'opzione **cross db ownership chaining** su 1, a meno che tutti i database ospitati dall'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non debbano essere inclusi nel concatenamento della proprietà tra database e si sia consapevoli delle implicazioni di questa impostazione in termini di sicurezza.  

Per determinare lo stato corrente del concatenamento della proprietà tra database, eseguire la query seguente:  
```sql
SELECT is_db_chaining_on, name FROM sys.databases;
```  
Un risultato pari a 1 indica che il concatenamento della proprietà tra database è abilitato.

## <a name="controlling-cross-database-ownership-chaining"></a>Controllo del concatenamento della proprietà tra database  
 Prima di attivare o disattivare il concatenamento della proprietà tra database, tenere presente quanto segue:  
  
-   È necessario essere membri del ruolo predefinito del server **sysadmin** per attivare o disattivare il concatenamento della proprietà tra database.  
  
-   Prima di attivare o disattivare il concatenamento della proprietà tra database su un server di produzione, eseguire il test completo di tutte le applicazioni, incluse quelle di terze parti, per assicurare che le modifiche non influiscano sulla funzionalità delle applicazioni.  
  
-   Specificare RECONFIGURE con **sp_configure** per modificare l'opzione **cross db ownership chaining**mentre il server è in esecuzione.  
  
-   Se sono presenti database per i quali è necessario attivare il concatenamento della proprietà tra database, è consigliabile disattivare l'opzione **cross db ownership chaining** per l'istanza usando **sp_configure**. Usare quindi l'istruzione ALTER DATABASE per attivare il concatenamento della proprietà tra database per i singoli database.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
