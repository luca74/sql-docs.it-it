---
title: DBCC CLEANTABLE (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
caps.latest.revision: 53
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7152b7241d97953fdeddf343dbeea60ed8d7ff5f
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Recupera lo spazio delle colonne a lunghezza variabile eliminate nelle tabelle o viste indicizzate.
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name* | *database_id* | 0  
 Database a cui appartiene la tabella in cui recuperare lo spazio. Se si specifica 0, viene utilizzato il database corrente. I nomi di database devono seguire le regole per [identificatori](../../relational-databases/databases/database-identifiers.md).  
  
 *TABLE_NAME* | *table_id* | *view_name*| *view_id*  
 Tabella o vista indicizzata in cui recuperare lo spazio.  
  
 *batch_size*  
 Numero di righe elaborate per transazione. Se si omette l'argomento o si specifica 0, l'istruzione elabora l'intera tabella in una sola transazione.  
  
 WITH NO_INFOMSGS  
 Disattiva tutti i messaggi informativi.  
  
## <a name="remarks"></a>Osservazioni  
DBCC CLEANTABLE recupera lo spazio dopo l'eliminazione di una colonna a lunghezza variabile. Una colonna a lunghezza variabile può essere uno dei seguenti tipi di dati: **varchar**, **nvarchar**, **varchar (max)**, **nvarchar (max)**, **varbinary**, **varbinary (max)**, **testo**, **ntext**, **immagine**,  **sql_variant**, e **xml**. Questo comando non consente di recuperare spazio dopo l'eliminazione di colonne a lunghezza fissa.
Se le colonne eliminate erano archiviate all'interno di righe, DBCC CLEANTABLE recupera lo spazio dall'unità di allocazione IN_ROW_DATA della tabella. Se le colonne erano archiviate all'esterno di righe, lo spazio viene recuperato dall'unità di allocazione ROW_OVERFLOW_DATA o LOB_DATA a seconda del tipo di dati della colonna eliminata. Se l'operazione di recupero di spazio da una pagina ROW_OVERFLOW_DATA o LOB_DATA restituisce una pagina vuota, DBCC CLEANTABLE rimuove tale pagina.
DBCC CLEANTABLE viene eseguita come una o più transazioni. Se non si specificano le dimensioni di batch, il comando elabora l'intera tabella in una sola transazione e per la tabella viene acquisito un blocco esclusivo durante l'operazione. Per tabelle di grandi dimensioni, la lunghezza della singola transazione e lo spazio del log necessario potrebbero risultare eccessivi. Se si specificano le dimensioni del batch, il comando viene eseguito in una serie di transazioni, ognuna con il numero di righe specificato. Non è possibile eseguire DBCC CLEANTABLE come una transazione all'interno di un'altra transazione.
Questa operazione viene registrata completamente.
L'istruzione DBCC CLEANTABLE non è supportata per l'utilizzo in tabelle di sistema, tabelle temporanee o nella parte dell'indice columnstore con ottimizzazione per la memoria xVelocity di una tabella.
  
## <a name="best-practices"></a>Procedure consigliate  
Non eseguire DBCC CLEANTABLE come attività di manutenzione di routine. Utilizzare invece DBCC CLEANTABLE dopo aver apportato modifiche significative alle colonne a lunghezza variabile di una tabella o di una vista indicizzata, se è necessario recuperare immediatamente lo spazio inutilizzato. In alternativa, è possibile ricompilare gli indici sulla tabella o sulla vista. Questa operazione richiede tuttavia molte risorse.
  
## <a name="result-sets"></a>Set di risultati  
DBCC CLEANTABLE restituisce:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
 Chiamante deve essere proprietario della tabella o vista indicizzata o essere un membro del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database, o **db_ddladmin** ruolo predefinito del database.  
  
## <a name="examples"></a>Esempi  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. Utilizzo di DBCC CLEANTABLE per il recupero di spazio  
Nell'esempio seguente viene eseguito DBCC CLEANTABLE per la tabella `Production.Document` del database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. Utilizzo di DBCC CLEANTABLE e verifica dei risultati  
Nell'esempio seguente viene creata e popolata una tabella con più colonne a lunghezza variabile. Due colonne vengono quindi eliminate e viene eseguito DBCC CLEANTABLE per recuperare lo spazio inutilizzato. Viene eseguita una query per verificare i conteggi delle pagine e i valori relativi allo spazio utilizzato prima e dopo l'esecuzione del comando DBCC CLEANTABLE.
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [Sys. allocation_units &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  
