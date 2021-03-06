---
title: table_types (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- table_types_TSQL
- sys.table_types
- sys.table_types_TSQL
- table_types
dev_langs:
- TSQL
helpviewer_keywords:
- table types [SQL Server]
- table-valued parameters, sys.table_types
- sys.table_types
- UDTT
ms.assetid: c05fd873-aff2-4a89-9936-a54c2ea09996
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9c55e83d67fcd5817575b0b045bb680b0269217
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="systabletypes-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Visualizza le proprietà dei tipi di tabella definiti dall'utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un tipo di tabella è un tipo dal quale potrebbero essere dichiarati variabili della tabella o parametri con valori di tabella. Ogni tipo di tabella ha un **type_table_object_id** che rappresenta una chiave esterna nel [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista del catalogo. È possibile utilizzare questa colonna ID per eseguire una query sulle viste del catalogo, in modo simile a un **object_id** colonna di una normale tabella per individuare la struttura del tipo di tabella, ad esempio le colonne e vincoli.    
 
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|*\<colonne ereditate >*||Per un elenco di colonne ereditate da questa vista, vedere [Sys. Types &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-types-transact-sql.md).|  
|**type_table_object_id**|**int**|Numero di identificazione dell'oggetto. Numero univoco all'interno di un database.|  
|**is_memory_optimized**|**bit**|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Di seguito sono indicati i valori possibili:<br /><br /> 0 = senza ottimizzazione per la memoria<br /><br /> 1 = con ottimizzazione per la memoria<br /><br /> Il valore predefinito è 0.<br /><br /> I tipi di tabella vengono sempre creati con DURABILITY = SCHEMA_ONLY. Solo lo schema è persistente su disco.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto viste del catalogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Utilizzare i valori di tabella parametri &#40; motore di Database &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
