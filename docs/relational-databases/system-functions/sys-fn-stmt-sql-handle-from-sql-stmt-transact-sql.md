---
title: Sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 6794e073-0895-4507-aba3-c3545acc843f
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1fc9b145fe662092039a5470cd4a8a0aee459177
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnstmtsqlhandlefromsqlstmt-transact-sql"></a>Sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ottiene il **stmt_sql_handle** per un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione sotto il tipo di parametrizzazione (semplice o forzata) specificato. In questo modo è possibile fare riferimento alle query archiviate nell'archivio Query usando i relativi **stmt_sql_handle** quando si conosce il testo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.fn_stmt_sql_handle_from_sql_stmt   
(  
    'query_sql_text',   
    [ query_param_type   
) [;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *query_sql_text*  
 È il testo della query in archivio query che si desidera che l'handle di. *query_sql_text* è un **nvarchar (max)**, non prevede alcun valore predefinito.  
  
 *query_param_type*  
 È il tipo di parametro della query. *query_param_type* è un **tinyint**. I valori possibili sono:  
  
-   NULL: valore predefinito è 0  
  
-   0: nessuno  
  
-   1-utente  
  
-   2-semplice  
  
-   3 – forzato  
  
## <a name="columns-returned"></a>Colonne restituite  
 Nella tabella seguente vengono elencate le colonne che sys.fn_stmt_sql_handle_from_sql_stmt restituisce.  
  
|Nome colonna|Tipo|Description|  
|-----------------|----------|-----------------|  
|**statement_sql_handle**|**varbinary(64)**|Handle SQL.|  
|**query_sql_text**|**nvarchar(max)**|Il testo del [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione.|  
|**query_parameterization_type**|**tinyint**|Il tipo di parametrizzazione di query.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="permissions"></a>Permissions  
 Richiede il **EXECUTE** autorizzazione per il database, e **eliminare** autorizzazione sulle viste del catalogo di archivio query.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguita un'istruzione e quindi utilizza `sys.fn_stmt_sql_handle_from_sql_stmt` per restituire l'handle SQL dell'istruzione.  
  
```  
SELECT * FROM sys.databases;   
SELECT * FROM sys.fn_stmt_sql_handle_from_sql_stmt('SELECT * FROM sys.databases', NULL);  
```  
  
 Utilizzare la funzione per correlare i dati di archivio Query con altre viste a gestione dinamica. Nell'esempio seguente:  
  
```  
SELECT qt.query_text_id, q.query_id, qt.query_sql_text, qt.statement_sql_handle,  
q.context_settings_id, qs.statement_context_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_id  
CROSS APPLY sys.fn_stmt_sql_handle_from_sql_stmt (qt.query_sql_text, null) AS fn_handle_from_stmt  
JOIN sys.dm_exec_query_stats AS qs   
    ON fn_handle_from_stmt.statement_sql_handle = qs.statement_sql_handle;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_query_store_force_plan &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40; Transct-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_unforce_plan &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_reset_exec_stats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [sp_query_store_remove_query &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitoraggio delle prestazioni con Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  