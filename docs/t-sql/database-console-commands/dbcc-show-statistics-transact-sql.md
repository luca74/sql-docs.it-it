---
title: DBCC SHOW_STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHOW_STATISTICS_TSQL
- DBCC SHOW_STATISTICS
- SHOW_STATISTICS
- DBCC_SHOW_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], densities
- histograms [SQL Server]
- statistical information [SQL Server], viewing statistics objects
- current distribution statistics
- query optimization statistics [SQL Server], histograms
- DBCC SHOW_STATISTICS statement
- distribution statistics
- statistical information [SQL Server], densities
- statistics objects
- statistical information [SQL Server], histograms
- query optimization statistics [SQL Server], viewing statistics objects
- statistical information [SQL Server], distribution
- densities [SQL Server]
- displaying distribution statistics
ms.assetid: 12be2923-7289-4150-b497-f17e76a50b2e
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 66f00526254a3592c3bb980ecf22c390b88cb687
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-showstatistics-transact-sql"></a>DBCC SHOW_STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

DBCC SHOW_STATISTICS consente di visualizzare le statistiche relative all'ottimizzazione delle query correnti per una tabella o una vista indicizzata. L'utilizzo delle statistiche consente a Query Optimizer di stimare la cardinalità o il numero di righe nel risultato di una query e di creare un piano di query di qualità elevata. Query Optimizer potrebbe ad esempio utilizzare le stime relative alla cardinalità per scegliere l'operatore Index Seek anziché l'operatore Index Scan nel piano di query, evitando un'operazione di analisi dell'indice che utilizza un numero elevato di risorse e migliorando di conseguenza le prestazioni delle query.
  
Query Optimizer archivia le statistiche relative a una tabella oppure a una vista indicizzata in un oggetto statistiche. Per una tabella, l'oggetto statistiche viene creato in un indice oppure in un elenco di colonne della tabella. L'oggetto statistiche è costituito da un'intestazione con metadati relativi alle statistiche, un istogramma con la distribuzione dei valori nella prima colonna chiave dell'oggetto stesso e un vettore di densità per misurare la correlazione tra colonne. Nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] è possibile calcolare le stime relative alla cardinalità con qualsiasi dato contenuto nell'oggetto statistiche.
  
DBCC SHOW_STATISTICS consente di visualizzare l'intestazione, l'istogramma e il vettore di densità in base ai dati archiviati nell'oggetto statistiche. La sintassi consente inoltre di specificare una tabella o una vista indicizzata con un nome di colonna, un nome di statistiche o un nome di indice di destinazione. In questo argomento vengono descritte le modalità di visualizzazione delle statistiche e di interpretazione dei risultati visualizzati.
  
Per altre informazioni, vedere [Statistics](../../relational-databases/statistics/statistics.md).
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```
-- Syntax for SQL Server and Azure SQL Database  
  
DBCC SHOW_STATISTICS ( table_or_indexed_view_name , target )   
[ WITH [ NO_INFOMSGS ] < option > [ , n ] ]  
< option > :: =  
    STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM  
```  
  
```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

DBCC SHOW_STATISTICS ( table_name , target )   
    [ WITH {STAT_HEADER | DENSITY_VECTOR | HISTOGRAM } [ ,...n ] ]  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *table_or_indexed_view_name*  
 Nome della tabella o della vista indicizzata per la quale visualizzare le informazioni statistiche.  
  
 *table_name*  
 Nome della tabella contenente la statistica da visualizzare. La tabella non può essere una tabella esterna.  
  
 *destinazione*  
 Nome dell'indice, delle statistiche o della colonna per cui visualizzare le informazioni statistiche. L'oggetto *target* è racchiuso tra parentesi quadre, virgolette singole, virgolette doppie o viene inserito senza virgolette. Se l'oggetto *target* è il nome di un indice o di statistiche esistenti in una tabella o in una vista indicizzata, vengono restituite le relative informazioni statistiche. Se *target* è il nome di una colonna esistente e per tale colonna sono presenti statistiche create automaticamente, vengono restituite le informazioni relative a tali statistiche. Se per una colonna specificata in target non sono presenti statistiche create automaticamente, viene restituito il messaggio di errore 2767.  
 In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], *target* non può essere un nome di colonna.  
  
 NO_INFOMSGS  
 Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.  
  
 STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM [ **,***n* ]  
 Specificando una o più opzioni tra quelle disponibili è possibile limitare i set di risultati restituiti dall'istruzione all'opzione o alle opzioni specificate. Se non si specifica alcuna opzione, vengono restituite tutte le informazioni statistiche.  
  
 STATS_STREAM è [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Set di risultati  
Nella tabella seguente vengono descritte le colonne restituite nel set di risultati quando si specifica l'opzione STAT_HEADER.
  
|Nome colonna|Description|  
|-----------------|-----------------|  
|nome|Nome dell'oggetto statistiche.|  
|Updated|Data e ora dell'ultimo aggiornamento delle statistiche. La funzione [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) rappresenta un metodo alternativo per il recupero di queste informazioni. Per altre informazioni, vedere la sezione [Osservazioni](#Remarks) più avanti nella pagina.|  
|Righe|Numero totale di righe della tabella o della vista indicizzata al momento dell'ultimo aggiornamento delle statistiche. Se le statistiche vengono filtrate o corrispondono a un indice filtrato, il numero di righe potrebbe essere inferiore al numero di righe della tabella. Per altre informazioni, vedere [Statistiche](../../relational-databases/statistics/statistics.md).|  
|Rows Sampled|Numero totale di righe campionate per i calcoli statistici. Se Rows Sampled < Rows, l'istogramma e i risultati relativi alla densità visualizzati vengono stimati in base alle righe campionate.|  
|Passaggi|Numero di intervalli nell'istogramma. Ogni intervallo comprende un insieme di valori di colonna seguiti da un valore di colonna pari al limite superiore. Gli intervalli dell'istogramma vengono definiti nella prima colonna chiave delle statistiche. Il numero massimo di intervalli è 200.|  
|Density|Valore calcolato come 1/ *valori distinct* per tutti i valori nella prima colonna chiave dell'oggetto statistiche, ad eccezione dei valori limite dell'istogramma. Tale valore Density non viene utilizzato da Query Optimizer e viene visualizzato per compatibilità con le versioni precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|Average Key Length|Numero medio di byte per valore per tutte le colonne chiave nell'oggetto statistiche.|  
|String Index|Il valore Yes indica che l'oggetto statistiche contiene statistiche di riepilogo delle stringhe per migliorare le stime relative alla cardinalità per i predicati della query che utilizzano l'operatore LIKE, ad esempio `WHERE ProductName LIKE '%Bike'`. Le statistiche di riepilogo delle stringhe vengono archiviate separatamente rispetto all'istogramma e vengono create nella prima colonna chiave dell'oggetto statistiche quando tale colonna è di tipo **char**, **varchar**, **nchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **text** o **ntext**.|  
|Espressione filtro|Predicato per il subset di righe della tabella incluso nell'oggetto statistiche. NULL = statistiche non filtrate. Per altre informazioni sui predicati di filtro, vedere [Creare indici filtrati](../../relational-databases/indexes/create-filtered-indexes.md). Per altre informazioni sulle statistiche filtrate, vedere [Statistiche](../../relational-databases/statistics/statistics.md).|  
|Unfiltered Rows|Numero totale di righe nella tabella prima dell'applicazione dell'espressione di filtro. Se l'espressione di filtro è NULL, Unfiltered Rows è uguale a Rows.|  
|Persisted Sample Percent|Percentuale di campionamento persistente usata per gli aggiornamenti delle statistiche che non specificano in modo esplicito una percentuale di campionamento. Se il valore è zero, non viene impostata alcuna percentuale di campionamento persistente per la statistica.<br /><br /> **Si applica a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4| 
  
Nella tabella seguente vengono descritte le colonne restituite nel set di risultati quando si specifica l'opzione DENSITY_VECTOR.
  
|Nome colonna|Description|  
|-----------------|-----------------|  
|All Density|Il valore Density viene calcolato come 1/ *valori distinct*. Nei risultati la densità viene visualizzata per ogni prefisso di colonna dell'oggetto statistiche, una riga per ogni densità. Un valore distinct è un elenco distinto dei valori delle colonne per riga e per prefisso di colonna. Se l'oggetto statistiche contiene, ad esempio, le colonne chiave (A, B, C), i risultati restituiscono la densità degli elenchi di valori distinct in ognuno di tali prefissi di colonna, ovvero (A), (A, B) e (A, B, C). Utilizzando il prefisso (A, B, C), ciascuno di questi elenchi è un elenco di valori distinct, ovvero (3, 5, 6), (4, 4, 6), (4, 5, 6), (4, 5, 7). Utilizzando il prefisso (A, B) agli stessi valori di colonna sono associati gli elenchi di valori distinct (3, 5), (4, 4) e (4, 5).|  
|Average Length|Lunghezza media, in byte, per archiviare un elenco di valori di colonna per il prefisso di colonna. Se per ogni valore presente nell'elenco (3, 5, 6), ad esempio, sono necessari 4 byte, la lunghezza media è di 12 byte.|  
|Colonne|Nomi delle colonne nel prefisso per cui sono visualizzati i valori di All Density e Average Length.|  
  
Nella tabella seguente vengono descritte le colonne restituite nel set di risultati quando si specifica l'opzione HISTOGRAM.
  
|Nome colonna|Description|  
|---|---|
|RANGE_HI_KEY|Valore di colonna pari al limite superiore per un intervallo dell'istogramma. Il valore di colonna viene denominato anche valore chiave.|  
|RANGE_ROWS|Numero stimato di righe il cui valore di colonna è compreso in un intervallo dell'istogramma, escluso il limite superiore.|  
|EQ_ROWS|Numero stimato di righe il cui valore di colonna è uguale al limite superiore dell'intervallo dell'istogramma.|  
|DISTINCT_RANGE_ROWS|Numero stimato di righe con un valore distinct di colonna compreso in un intervallo dell'istogramma, escluso il limite superiore.|  
|AVG_RANGE_ROWS|Numero medio di righe con valori di colonna duplicati compresi in un intervallo dell'istogramma, escluso il limite superiore (RANGE_ROWS / DISTINCT_RANGE_ROWS per DISTINCT_RANGE_ROWS > 0).| 
  
## <a name="Remarks"></a> Osservazioni 

La data di aggiornamento delle statistiche viene archiviata nell'[oggetto BLOB di statistiche](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics) insieme all'[istogramma](#histogram) e al [vettore di densità](#density), non nei metadati. Quando non viene letto alcun dato per generare i dati delle statistiche, il BLOB di statistiche non viene creato e la data non è disponibile. La colonna *updated* è NULL. È il caso delle statistiche filtrate per le quali il predicato non restituisce alcuna riga o delle nuove tabelle vuote.
  
## <a name="histogram"></a> Istogramma  
Un istogramma misura la frequenza di occorrenza per ogni valore distinct in un set di dati. Query Optimizer calcola un istogramma nei valori di colonna nella prima colonna chiave dell'oggetto statistiche, selezionando i valori di colonna tramite il campionamento statistico delle righe o un'analisi completa di tutte le righe della tabella o della vista. Se l'istogramma viene creato da un set campionato di righe, i totali archiviati per numero di righe e numero di valori distinct sono stime e non è necessario che siano numeri interi.
  
Per creare l'istogramma, Query Optimizer ordina i valori di colonna, calcola il numero di valori che corrispondono a ogni valore distinct di colonna, quindi aggrega i valori di colonna in un massimo di 200 intervalli contigui dell'istogramma. Ogni intervallo comprende un insieme di valori di colonna seguiti da un valore di colonna pari al limite superiore. Nell'insieme sono inclusi tutti i possibili valori di colonna compresi tra i valori limite, esclusi questi ultimi. Il minore tra i valori di colonna ordinati costituisce il limite superiore per il primo intervallo dell'istogramma.
  
Nel diagramma seguente viene illustrato un istogramma con sei intervalli. L'area a sinistra del primo valore limite superiore è il primo intervallo.
  
![](../../relational-databases/system-dynamic-management-views/media/a0ce6714-01f4-4943-a083-8cbd2d6f617a.gif "a0ce6714-01f4-4943-a083-8cbd2d6f617a")
  
Per ogni intervallo dell'istogramma:
-   La riga in grassetto rappresenta il valore limite superiore (RANGE_HI_KEY) e il relativo numero di occorrenze (EQ_ROWS).  
-   L'area a tinta unita a sinistra di RANGE_HI_KEY rappresenta l'insieme di valori di colonna e il numero medio di occorrenze di ciascun valore (AVG_RANGE_ROWS) di colonna. Il valore AVG_RANGE_ROWS per il primo intervallo dell'istogramma è sempre 0.  
-   Le linee punteggiate rappresentano i valori campionati utilizzati per stimare il numero complessivo dei valori distinct nell'insieme (DISTINCT_RANGE_ROWS) e il numero complessivo dei valori nell'insieme (RANGE_ROWS). Query Optimizer utilizza RANGE_ROWS e DISTINCT_RANGE_ROWS per calcolare AVG_RANGE_ROWS e non archivia i valori campionati.  
  
Query Optimizer definisce gli intervalli dell'istogramma in base al relativo significato statistico e utilizza un algoritmo per il calcolo della differenza massima per ridurre al minimo il numero di intervalli nell'istogramma, aumentando contemporaneamente la differenza tra i valori limite. Il numero massimo di intervalli è 200. Il numero di intervalli dell'istogramma può essere minore del numero di valori distinct, anche per le colonne con un numero di punti limite inferiore a 200. A una colonna con 100 valori distinct, ad esempio, può essere associato un istogramma con un numero di punti limite inferiore a 100.
  
## <a name="density"></a> Vettore di densità  
Per ottimizzare le stime relative alla cardinalità per query che restituiscono più colonne della stessa tabella o vista indicizzata, Query Optimizer utilizza le densità. Il vettore di densità contiene una densità per ogni prefisso di colonna nell'oggetto statistiche. Se in un oggetto statistiche, ad esempio, sono presenti le colonne chiave `CustomerId`, `ItemId` e `Price`, la densità viene calcolata per ognuno dei prefissi di colonna seguenti.
  
|Prefisso di colonna|Densità calcolata su|  
|---|---|
|(CustomerId)|Righe con valori corrispondenti per CustomerId|  
|(CustomerId, ItemId)|Righe con valori corrispondenti per CustomerId e ItemId|  
|(CustomerId, ItemId, Price)|Righe con valori corrispondenti per CustomerId, ItemId e Price|  
  
## <a name="restrictions"></a>Restrictions  
 DBCC SHOW_STATISTICS non fornisce statistiche per gli indici spaziali o columnstore ottimizzati in memoria xVelocity.  
  
## <a name="permissions-for-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>Autorizzazioni per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e per il [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
Per visualizzare l'oggetto statistiche, l'utente deve essere il proprietario della tabella oppure un membro del ruolo predefinito del server `sysadmin` o del ruolo predefinito del database `db_owner` o `db_ddladmin`.
  
Tramite [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 vengono modificate le restrizioni alle autorizzazioni e gli utenti che hanno l'autorizzazione SELECT possono usare questo comando. Affinché le autorizzazioni SELECT siano sufficienti per eseguire il comando, sono richiesti i requisiti seguenti:
-   Gli utenti devono disporre delle autorizzazioni su tutte le colonne nell'oggetto statistiche  
-   Gli utenti devono disporre dell'autorizzazione su tutte le colonne in una condizione di filtro, se esistente  
-   La tabella non può avere criteri di sicurezza a livello di riga.  
  
Per disabilitare questo comportamento, utilizzare il traceflag 9485.
  
## <a name="permissions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Autorizzazioni per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC SHOW_STATISTICS richiede l'autorizzazione SELECT per la tabella o l'appartenenza a uno degli elementi seguenti:
-   ruolo predefinito del server sysadmin  
-   ruolo predefinito del database db_owner  
-   ruolo predefinito del database db_ddladmin  
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Limitazioni e restrizioni per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC SHOW_STATISTICS consente di visualizzare le statistiche archiviate nel database shell a livello di nodo di controllo. Non vengono visualizzate le statistiche create automaticamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui nodi di calcolo.
  
DBCC SHOW_STATISTICS non è supportato per le tabelle esterne.
  
## <a name="examples-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>Esempi: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
### <a name="a-returning-all-statistics-information"></a>A. Restituzione di tutte le informazioni statistiche  
Nell'esempio seguente vengono visualizzate tutte le informazioni statistiche per l'indice `AK_Address_rowguid` della tabella `Person.Address` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);  
GO  
```  
  
### <a name="b-specifying-the-histogram-option"></a>B. Specifica dell'opzione HISTOGRAM  
In questo modo le informazioni statistiche visualizzate per Customer_LastName vengono limitate ai dati HISTOGRAM.
  
```sql
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName) WITH HISTOGRAM;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="c-display-the-contents-of-one-statistics-object"></a>C. Visualizzare il contenuto di un oggetto statistiche  
 Nell'esempio seguente viene visualizzato il contenuto delle statistiche Customer_LastName per la tabella DimCustomer.  
  
```sql
-- Uses AdventureWorks  
--First, create a statistics object  
CREATE STATISTICS Customer_LastName   
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName);  
GO  
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName);  
GO  
```  
  
Nei risultati vengono visualizzati l'intestazione, il vettore di densità e parte dell'istogramma.
  
![Risultati di DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/media/aps-sql-dbccshow-statistics.JPG "Risultati di DBCC SHOW_STATISTICS")
  
## <a name="see-also"></a>Vedere anche  
[Statistiche](../../relational-databases/statistics/statistics.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)  
[DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)  
[sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)  
[sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)  
[STATS_DATE &#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
[sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
[sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
