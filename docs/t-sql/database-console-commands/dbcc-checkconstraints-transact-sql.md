---
title: L'istruzione DBCC CHECKCONSTRAINTS (Transact-SQL) | Documenti Microsoft
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
- DBCC CHECKCONSTRAINTS
- DBCC_CHECKCONSTRAINTS_TSQL
- CHECKCONSTRAINTS
- CHECKCONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKCONSTRAINTS statement
- consistency [SQL Server], constraints
- checking constraint consistency
- constraints [SQL Server], consistency checks
- integrity [SQL Server], constraints
ms.assetid: da6c9cee-6687-46e8-b504-738551f9068b
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c5a15f6f5af19cd0e5da400dd4deb2cfa0d4cc4
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkconstraints-transact-sql"></a>DBCC CHECKCONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Controlla l'integrità di un vincolo specificato oppure di tutti i vincoli di una tabella specificata nel database corrente.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DBCC CHECKCONSTRAINTS  
[   
    (   
    table_name | table_id | constraint_name | constraint_id   
    )  
]  
    [ WITH   
    [ { ALL_CONSTRAINTS | ALL_ERRORMSGS } ]  
    [ , ] [ NO_INFOMSGS ]   
    ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *TABLE_NAME* | *table_id* | *constraint_name* | *constraint_id*  
 Tabella o vincolo da controllare. Quando *table_name* o *table_id* è specificato, vengono controllati tutti i vincoli abilitati in tale tabella. Quando *constraint_name* o *constraint_id* è specificato, solo tale vincolo viene controllato. Se non si specifica un identificatore di tabella o un identificatore di vincolo, vengono controllati tutti i vincoli abilitati in tutte le tabelle del database corrente.  
 Un nome di vincolo identifica in modo univoco la tabella a cui appartiene. Per altre informazioni, vedere [Identificatori del database](../../relational-databases/databases/database-identifiers.md).  
  
 con  
 Consente di specificare opzioni.  
  
 ALL_CONSTRAINTS  
 Controlla tutti i vincoli abilitati e disabilitati della tabella se viene specificato il nome della tabella o se vengono controllate tutte le tabelle. In caso contrario, viene controllato solo il vincolo abilitato. ALL_CONSTRAINTS non ha alcun effetto quando viene specificato un nome di vincolo.  
  
 ALL_ERRORMSGS  
 Restituisce tutte le righe che violano i vincoli della tabella controllata. Per impostazione predefinita vengono restituite le prime 200 righe.  
  
 NO_INFOMSGS  
 Disattiva tutti i messaggi informativi.  
  
## <a name="remarks"></a>Osservazioni  
DBCC CHECKCONSTRAINTS consente di creare ed eseguire una query per ottenere tutti i vincoli FOREIGN KEY e CHECK di una tabella.
  
Una query di chiave esterna, ad esempio, presenta il seguente formato:
  
```sql
SELECT <columns>  
FROM <table_being_checked> LEFT JOIN <referenced_table>  
    ON <table_being_checked.fkey1> = <referenced_table.pkey1>   
    AND <table_being_checked.fkey2> = <referenced_table.pkey2>  
WHERE <table_being_checked.fkey1> IS NOT NULL   
    AND <referenced_table.pkey1> IS NULL  
    AND <table_being_checked.fkey2> IS NOT NULL  
    AND <referenced_table.pkey2> IS NULL  
```  
  
I dati della query vengono archiviati in una tabella temporanea. Dopo che tutte le tabelle o tutti i vincoli richiesti sono stati controllati, viene restituito il set di risultati.
L'istruzione DBCC CHECKCONSTRAINTS controlla l'integrità dei vincoli FOREIGN KEY e CHECK, ma non l'integrità delle strutture di dati su disco di una tabella. Questi controlli struttura di dati possono essere eseguiti tramite [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
  
**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
Se *table_name* o *table_id* specificato e viene abilitata per il controllo delle versioni di sistema, DBCC CHECKCONSTRAINTS esegue inoltre controlli di coerenza sui dati temporali per la tabella specificata. Quando *NO_INFOMSGS* non viene specificato, questo comando restituisce ogni violazione coerenza nell'output in una riga separata. Il formato dell'output sarà ([pkcol1], [pkcol2]...) = (\<pkcol1_value >, \<pkcol2_value >...) E \<qual è il record della tabella temporale >.
  
|Controlla|Informazioni aggiuntive nell'output se il controllo non riuscito|  
|-----------|-----------------------------------------------|  
|PeriodEndColumn ≥ PeriodStartColumn (corrente)|[sys_end] = '{0}' e MAX(DATETIME2) = "9999-12-31 23:59:59.99999'|  
|PeriodEndColumn ≥ PeriodStartColumn (corrente, cronologia)|[sys_start] = '{0}' e [sys_end] = '\\{1 \\}'|  
|PeriodStartColumn < current_utc_time (corrente)|[sys_start] = '{0}' e SYSUTCTIME|  
|PeriodEndColumn < current_utc_time (cronologia)|[sys_end] = '{0}' e SYSUTCTIME|  
|Si sovrappone|(sys_start1, sys_end1), (sys_start2, sys_end2) per due record di sovrapposizione.<br /><br /> Se sono presenti più di 2 record sovrapposti, output includerà più righe di ogni coppia di sovrapposizioni di visualizzazione.|  
  
Non è possibile specificare constraint_name o constraint_id per eseguire verifiche di coerenza temporale solo.
  
## <a name="result-sets"></a>Set di risultati  
DBCC CHECKCONSTRAINTS restituisce un set di righe con le colonne seguenti.
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|Nome tabella|**varchar**|Nome della tabella.|  
|Constraint Name|**varchar**|Nome del vincolo violato.|  
|Where|**varchar**|Assegnazioni di valori di colonna che identificano una o più righe che violano il vincolo.<br /><br /> È possibile utilizzare il valore di questa colonna in una clausola WHERE di un'istruzione SELECT che esegue una query per individuare le righe che violano il vincolo.|  
  
## <a name="permissions"></a>Permissions  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o al ruolo predefinito del database **db_owner** .
  
## <a name="examples"></a>Esempi  
  
### <a name="a-checking-a-table"></a>A. Controllo di una tabella  
Nell'esempio seguente viene controllata l'integrità dei vincoli della tabella `Table1` del database `AdventureWorks`.
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (Col1 int, Col2 char (30));  
GO  
INSERT INTO Table1 VALUES (100, 'Hello');  
GO  
ALTER TABLE Table1 WITH NOCHECK ADD CONSTRAINT chkTab1 CHECK (Col1 > 100);  
GO  
DBCC CHECKCONSTRAINTS(Table1);  
GO  
```  
  
### <a name="b-checking-a-specific-constraint"></a>B. Controllo di un vincolo specifico  
Nell'esempio seguente viene controllata l'integrità del vincolo `CK_ProductCostHistory_EndDate`.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKCONSTRAINTS ('Production.CK_ProductCostHistory_EndDate');  
GO  
```  
  
### <a name="c-checking-all-enabled-and-disabled-constraints-on-all-tables"></a>C. Controllo di tutti i vincoli abilitati e disabilitati in tutte le tabelle  
 Nell'esempio seguente viene controllata l'integrità di tutti i vincoli abilitati e disabilitati di tutte le tabelle nel database corrente.  
  
```sql  
DBCC CHECKCONSTRAINTS WITH ALL_CONSTRAINTS;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
