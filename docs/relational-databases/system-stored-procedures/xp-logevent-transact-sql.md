---
title: xp_logevent (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
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
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9ac262c1d16baf15eb9f1eafd05960f8d1905ec9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="xplogevent-transact-sql"></a>xp_logevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra un messaggio definito dall'utente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di log e nel Visualizzatore eventi di Windows. xp_logevent può essere utilizzato per inviare un avviso senza inviare un messaggio al client.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *error_number*  
 Numero di errore definito dall'utente maggiore di 50.000. Il valore massimo è 2147483647 (2^31 - 1).  
  
 **'** *messaggio* **'**  
 Stringa di caratteri con lunghezza massima di 2048 caratteri.  
  
 **'** *gravità* **'**  
 Una delle tre stringhe di caratteri seguenti: INFORMATIONAL, WARNING o ERROR. *gravità* è facoltativo e il valore predefinito è Informational.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 La stored procedure xp_logevent restituisce il messaggio di errore seguente per l'esempio di codice incluso:  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>Osservazioni  
 Quando si inviano messaggi da [!INCLUDE[tsql](../../includes/tsql-md.md)] procedure, trigger, batch e così via, utilizzare l'istruzione RAISERROR anziché xp_logevent. xp_logevent non richiama un gestore di messaggi di un client né imposta@ERROR. Per scrivere messaggi nel Visualizzatore eventi di Windows e nel file di log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguire l'istruzione RAISERROR.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del database db_owner nel database master o al ruolo predefinito del server sysadmin.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il messaggio viene registrato, insieme alle variabili passate, nel Visualizzatore eventi di Windows.  
  
```  
DECLARE @@TABNAME varchar(30, @@USERNAME varchar(30),DECLARE @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Estese generali Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
