---
title: sys.dm_tran_active_snapshot_database_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_snapshot_database_transactions_TSQL
- dm_tran_active_snapshot_database_transactions
- sys.dm_tran_active_snapshot_database_transactions
- dm_tran_active_snapshot_database_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_snapshot_database_transactions dynamic management view
ms.assetid: 55b83f9c-da10-4e65-9846-f4ef3c0c0f36
caps.latest.revision: 55
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7e488c7c8bff4dda22c5c0a3488b56723fc0726
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmtranactivesnapshotdatabasetransactions-transact-sql"></a>sys.dm_tran_active_snapshot_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  In un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa vista a gestione dinamica restituisce una tabella virtuale per tutte le transazioni attive che generano versioni di riga o che potrebbero accedervi. Le transazioni vengono incluse in una o più delle situazioni seguenti:  
  
-   Quando l'opzione di database ALLOW_SNAPSHOT_ISOLATION o READ_COMMITTED_SNAPSHOT oppure entrambe le opzioni sono impostate su ON:  
  
    -   È presente una riga per ogni transazione in esecuzione nel livello di isolamento dello snapshot o nel livello di isolamento Read-committed che utilizza il controllo delle versioni delle righe.  
  
    -   È presente una riga per ogni transazione che provoca la creazione di una versione di riga nel database corrente. Ad esempio, la transazione genera una versione di riga mediante l'aggiornamento o l'eliminazione di una riga nel database corrente.  
  
-   Quando si attiva un trigger, è presente una riga per la transazione nel cui ambito il trigger viene eseguito.  
  
-   Quando una procedura di indicizzazione online è in esecuzione, è presente una riga per la transazione che crea l'indice.  
  
-   Quando è abilitata una sessione MARS (Multiple Active Results Sets), è presente una riga per ogni transazione che accede alle versioni di riga.  
  
 Questa vista a gestione dinamica non include transazioni di sistema.  
  
> [!NOTE]  
>  Per chiamare questo metodo dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilizzare il nome **sys.dm_pdw_nodes_tran_active_snapshot_database_transactions**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.dm_tran_active_snapshot_database_transactions  
```  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|Numero di identificazione univoco assegnato alla transazione. L'ID transazione viene principalmente utilizzato per identificare la transazione nelle operazioni di blocco.|  
|**transaction_sequence_num**|**bigint**|Numero di sequenza di una transazione, ovvero un numero di sequenza univoco assegnato a una transazione al momento dell'avvio. Alle transazioni che non generano record di versione o che non utilizzano analisi di snapshot non verrà assegnato alcun numero di sequenza.|  
|**commit_sequence_num**|**bigint**|Numero di sequenza che indica quando la transazione termina (commit o arresto). Per le transazioni attive il valore è NULL.|  
|**is_snapshot**|**int**|0 = Non si tratta di una transazione di isolamento dello snapshot.<br /><br /> 1 = Si tratta di una transazione di isolamento dello snapshot.|  
|**session_id**|**int**|ID della sessione che ha avviato la transazione.|  
|**first_snapshot_sequence_num**|**bigint**|Numero di sequenza più basso delle transazioni attive nel momento in cui è stato eseguito uno snapshot. Al momento dell'esecuzione, una transazione snapshot esegue uno snapshot di tutte le transazioni attive in quel momento. Per le transazioni non snapshot, il valore di questa colonna è 0.|  
|**max_version_chain_traversed**|**int**|Lunghezza massima della catena delle versioni attraversata per trovare la versione consistente dal punto di vista transazionale.|  
|**average_version_chain_traversed**|**real**|Numero medio di versioni di riga nelle catene delle versioni attraversate.|  
|**elapsed_time_seconds**|**bigint**|Tempo trascorso dal momento in cui la transazione ha acquisito il relativo numero di sequenza.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo che utilizza questo tipo di distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], richiede `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], richiede il `VIEW DATABASE STATE` autorizzazione per il database.   

## <a name="remarks"></a>Osservazioni  
 **DM tran_active_snapshot_database_transactions** segnala le transazioni che vengono assegnate un numero di sequenza della transazione (XSN). Il numero XSN viene assegnato quando la transazione accede per la prima volta all'archivio delle versioni. Negli esempi viene illustrato cosa accade quando si assegna un numero XSN a una transazione in un database abilitato per l'isolamento dello snapshot o l'isolamento Read-committed che utilizza il controllo delle versioni delle righe:  
  
-   Se una transazione viene eseguita nel livello di isolamento serializzabile, il numero XSN viene assegnato quando la transazione esegue per la prima volta un'istruzione, ad esempio un'operazione UPDATE, che provoca la creazione di una versione di riga.  
  
-   Se una transazione viene eseguita nel livello di isolamento dello snapshot, il numero XSN viene assegnato al momento dell'esecuzione di una qualsiasi istruzione DML (Data Manipulation Language), inclusa un'operazione SELECT.  
  
 Per ogni transazione avviata in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] i relativi numeri di sequenza vengono incrementati in modo seriale.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato uno scenario di test in cui quattro transazioni simultanee, ognuna identificata da un numero di sequenza della transazione (XSN), vengono eseguite in un database con le opzioni ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT impostate su ON. Vengono eseguite le transazioni seguenti:  
  
-   XSN-57 è un'operazione di aggiornamento con isolamento serializzabile.  
  
-   XSN-58 è uguale a XSN-57.  
  
-   XSN-59 è un'operazione di selezione nel livello di isolamento dello snapshot.  
  
-   XSN-60 è uguale a XSN-59.  
  
 Viene eseguita la query seguente.  
  
```  
SELECT   
    transaction_id,  
    transaction_sequence_num,  
    commit_sequence_num,  
    is_snapshot session_id,  
    first_snapshot_sequence_num,  
    max_version_chain_traversed,  
    average_version_chain_traversed,  
    elapsed_time_seconds  
  FROM sys.dm_tran_active_snapshot_database_transactions;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_id  transaction_sequence_num  commit_sequence_num  
--------------  ------------------------  -------------------  
9295            57                        NULL  
9324            58                        NULL  
9387            59                        NULL  
9400            60                        NULL  
  
is_snapshot  session_id   first_snapshot_sequence_num  
-----------  -----------  ---------------------------  
0            54           0  
0            53           0  
1            52           57  
1            51           57  
  
max_version_chain_traversed  average_version_chain_traversed  
---------------------------  -------------------------------  
0                            0  
0                            0  
1                            1  
1                            1  
  
elapsed_time_seconds  
--------------------  
419  
397  
359  
333  
```  
  
 Le informazioni seguenti valutano i risultati di **Sys.dm tran_active_snapshot_database_transactions**:  
  
-   XSN-57: Poiché questa transazione non è in esecuzione con isolamento dello snapshot, il `is_snapshot` valore e `first_snapshot_sequence_num` sono `0`. `transaction_sequence_num` indica che alla transazione è stato assegnato un numero di sequenza della transazione, poiché una o entrambe le opzioni di database ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT sono impostate su ON.  
  
-   XSN-58: questa transazione non viene eseguita nel livello di isolamento dello snapshot e si applicano le stesse informazioni di XSN-57.  
  
-   XSN-59: si tratta della prima transazione attiva in esecuzione nel livello di isolamento dello snapshot. Questa transazione legge i dati di cui è stato eseguito il commit prima di XSN-57, come indicato da `first_snapshot_sequence_num`. L'output di questa transazione mostra inoltre che la catena massima delle versioni attraversata per una riga è pari a `1` e che è stata attraversata in media `1` versione per ogni riga a cui è stato eseguito l'accesso. Ciò significa che le transazioni XSN-57, XSN-58 e XSN-60 non hanno modificato righe e non ne hanno eseguito il commit.  
  
-   XSN-60: si tratta della seconda transazione eseguita nel livello di isolamento dello snapshot. L'output restituisce le stesse informazioni di XSN-59.  
  
## <a name="see-also"></a>Vedere anche  
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative alle transazioni &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


