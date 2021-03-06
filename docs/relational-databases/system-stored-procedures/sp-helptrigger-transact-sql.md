---
title: sp_helptrigger (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 568e8eadad6dd63a2b2980284ec56bff9bb0293e
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="sphelptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Viene restituito il tipo o i tipi di trigger DML definiti nella tabella specificata per il database corrente. sp_helptrigger non può essere utilizzata con trigger DDL. Query di [stored procedure di sistema](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) vista del catalogo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@tabname=** ] **'***tabella***'**  
 Nome della tabella del database corrente per cui si desidera ottenere informazioni sui trigger. *tabella* è **nvarchar(776)**, non prevede alcun valore predefinito.  
  
 [  **@triggertype=** ] **'***tipo***'**  
 Tipo di trigger DML per cui restituire informazioni. *tipo* è **char(6)**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**DELETE**|Restituisce informazioni sui trigger DELETE.|  
|**INSERT**|Restituisce informazioni sui trigger INSERT.|  
|**UPDATE**|Restituisce informazioni sui trigger UPDATE.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nella tabella seguente vengono descritte le informazioni contenute nel set di risultati.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|Nome del trigger.|  
|**trigger_owner**|**sysname**|Nome del proprietario della tabella in cui il trigger è definito.|  
|**isupdate**|**int**|1 = Trigger UPDATE<br /><br /> 0 = Trigger diverso da UPDATE|  
|**isdelete**|**int**|1 = Trigger DELETE<br /><br /> 0 = Trigger diverso da DELETE|  
|**isinsert**|**int**|1 = Trigger INSERT<br /><br /> 0 = Trigger diverso da INSERT|  
|**isafter**|**int**|1 = Trigger AFTER<br /><br /> 0 = Trigger diverso da AFTER|  
|**isinsteadof**|**int**|1 = Trigger INSTEAD OF<br /><br /> 0 = Trigger diverso da INSTEAD OF|  
|**trigger_schema**|**sysname**|Nome dello schema a cui appartiene il trigger.|  
  
## <a name="permissions"></a>Permissions  
 Richiede [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md) autorizzazione per la tabella.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguita la stored procedure `sp_helptrigger` per generare informazioni sui trigger definiti nella tabella `Person.Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
