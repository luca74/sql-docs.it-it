---
title: sp_ivindexhasnullcols (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/04/2017
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
applies_to:
- SQL Server
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dbdbe2a627eb49dbd2ab71bef5bc102f1b157d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verifica che l'indice cluster della vista indicizzata sia univoco e non includa colonne che ammettono valori Null se la vista indicizzata verrà utilizzata per la creazione di una pubblicazione transazionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@viewname** =] **'***view_name***'**  
 Nome della vista da verificare. *view_name* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@fhasnullcols** =] *field_has_null_columns* OUTPUT  
 Flag che indica se l'indice della vista include colonne che ammettono valori Null. *view_name* è **sysname**, non prevede alcun valore predefinito. Restituisce un valore di **1** se l'indice della vista include colonne che ammettono valori NULL. Restituisce un valore di **0** se la vista contiene le colonne che ammettono valori null.  
  
> [!NOTE]  
>  Se la stored procedure restituisce un codice restituito di **1**, vale a dire l'esecuzione della stored procedure ha esito negativo, questo valore è **0** e deve essere ignorato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_ivindexhasnullcols** viene utilizzato dalla replica transazionale.  
  
 Per impostazione predefinita, gli articoli di vista indicizzata di una pubblicazione vengono creati sotto forma di tabella nei Sottoscrittori. Quando tuttavia la colonna indicizzata ammette valori Null, la vista indicizzata viene creata come vista indicizzata anziché come tabella nel Sottoscrittore. Tramite l'esecuzione di questa stored procedure è possibile verificare se nella vista indicizzata corrente esiste o meno questo problema.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
