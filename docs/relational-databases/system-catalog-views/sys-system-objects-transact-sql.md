---
title: Sys. system_objects (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.system_objects
- system_objects
- system_objects_TSQL
- sys.system_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_objects catalog view
ms.assetid: 069e9045-97f2-4463-8e8f-c73855f3ea0a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4e947beabc03f97a3e764fc72f7d0b8edf1296d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="syssystemobjects-transact-sql"></a>sys.system_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una riga per tutti gli oggetti di sistema con ambito schema inclusi in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tutti gli oggetti di sistema sono inclusi negli schemi denominati sys o INFORMATION_SCHEMA.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome dell'oggetto.|  
|object_id|**int**|Numero di identificazione dell'oggetto. Valore univoco all'interno di un database.|  
|principal_id|**int**|ID del singolo proprietario se diverso dal proprietario dello schema. Per impostazione predefinita, gli oggetti contenuti nello schema appartengono al proprietario dello schema stesso. È tuttavia possibile specificare un altro proprietario tramite l'istruzione ALTER AUTHORIZATION per modificare la proprietà.<br /><br /> È NULL se non è presente un altro proprietario singolo.<br /><br /> È NULL se il tipo di oggetto è uno dei seguenti:<br /><br /> C = vincolo CHECK<br /><br /> D = DEFAULT (vincolo o valore autonomo)<br /><br /> F = vincolo FOREIGN KEY<br /><br /> PK = vincolo PRIMARY KEY<br /><br /> R = regola (tipo obsoleto, autonoma)<br /><br /> TA = Trigger di assembly (CLR)<br /><br /> TR = trigger SQL<br /><br /> UQ = vincolo UNIQUE|  
|schema_id|**int**|ID dello schema che contiene l'oggetto.<br /><br /> Per tutti gli oggetti di sistema con ambito schema inclusi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questo valore sarà sempre disponibile in (schema_id('sys'), schema_id('INFORMATION_SCHEMA'))|  
|parent_object_id|**int**|ID dell'oggetto a cui appartiene l'oggetto.<br /><br /> 0 = non è un oggetto figlio.|  
|tipo|**Char(2)**|Tipo di oggetto:<br /><br /> AF = funzione di aggregazione (CLR)<br /><br /> C = vincolo CHECK<br /><br /> D = DEFAULT (vincolo o valore autonomo)<br /><br /> F = vincolo FOREIGN KEY<br /><br /> FN = funzione scalare SQL<br /><br /> FS = funzione scalare di assembly (CLR)<br /><br /> FT = funzione valutata a livello di tabella assembly (CLR)<br /><br /> IF = funzione SQL inline valutata a livello di tabella<br /><br /> IT = tabella interna<br /><br /> P = stored procedure SQL<br /><br /> PC = stored procedure di assembly (CLR)<br /><br /> PG = guida di piano<br /><br /> PK = vincolo PRIMARY KEY<br /><br /> R = regola (tipo obsoleto, autonoma)<br /><br /> RF = procedura-filtro-replica<br /><br /> S = tabella di base di sistema<br /><br /> SN = sinonimo<br /><br /> SQ = coda di servizio<br /><br /> TA = trigger DML assembly (CLR)<br /><br /> TF = funzione valutata a livello di tabella SQL<br /><br /> TR = trigger DML SQL<br /><br /> TT = tipo tabella<br /><br /> U = tabella (definita dall'utente)<br /><br /> UQ = vincolo UNIQUE<br /><br /> V = vista<br /><br /> X = stored procedure estesa|  
|type_desc|**nvarchar(60)**|Descrizione del tipo di oggetto. AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|Data di creazione dell'oggetto.|  
|modify_date|**datetime**|Data dell'ultima modifica apportata all'oggetto mediante un'istruzione ALTER. Se l'oggetto è una tabella o una vista, modify_date viene modificata anche quando si crea o si modifica un indice cluster nella tabella o nella vista.|  
|is_ms_shipped|**bit**|Oggetto creato da un interno [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente.|  
|is_published|**bit**|L'oggetto viene pubblicato.|  
|is_schema_published|**bit**|Viene pubblicato solo lo schema dell'oggetto.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Oggetto viste del catalogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
