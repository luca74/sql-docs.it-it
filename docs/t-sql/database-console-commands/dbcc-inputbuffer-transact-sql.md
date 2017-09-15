---
title: DBCC INPUTBUFFER (Transact-SQL) | Documenti Microsoft
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
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba54322c814911babe19e172a2cfafc4f00011a7
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Visualizza l'ultima istruzione inviata da un client a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *session_id*  
 ID della sessione associata a ogni connessione principale attiva.  
  
 *request_id*  
 Richiesta esatta (batch) da cercare nella sessione corrente.  
 La query seguente restituisce *request_id*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
 con  
 Consente di specificare opzioni.  
  
 NO_INFOMSGS  
 Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.  
  
## <a name="result-sets"></a>Set di risultati  
L'istruzione DBCC INPUTBUFFER restituisce un set di righe che include le colonne seguenti.
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar (30)**|Tipo di evento. Potrebbe trattarsi di **RPC Event** o **evento del linguaggio**. L'output sarà **No Event** quando è non stato rilevato alcun ultimo evento.|  
|**Parametri**|**smallint**|0 = Testo<br /><br /> 1 -  *n*  = parametri|  
|**EventInfo**|**nvarchar(4000)**|Per un **EventType** di RPC, **EventInfo** contiene solo il nome della routine. Per un **EventType** del linguaggio, vengono visualizzati solo i primi 4000 caratteri dell'evento.|  
  
Se, ad esempio, l'ultimo evento del buffer è DBCC INPUTBUFFER(11), DBCC INPUTBUFFER restituisce il set di risultati seguente.
  
```sql
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede uno dei seguenti:
-   Utente deve essere un membro del **sysadmin** ruolo predefinito del server.  
-   L'utente deve disporre di autorizzazione VIEW SERVER STATE.  
-   *session_id* deve essere lo stesso ID di sessione in cui viene eseguito il comando. Per determinare l'ID di sessione, eseguire la query seguente:  
  
```sql
SELECT @@spid;  
```
  
In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Premium richiede l'autorizzazione VIEW DATABASE STATE nel database. In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Standard e Basic richiede il [!INCLUDE[ssSDS](../../includes/sssds-md.md)] account amministratore.
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene eseguito `DBCC INPUTBUFFER` in una seconda connessione durante una transazione di lunga durata su una connessione precedente.
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)
  
  
