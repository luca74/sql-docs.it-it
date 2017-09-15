---
title: Quali sono le funzioni di database SQL di Microsoft? | Microsoft Docs
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- built-in functions [SQL Server]
- function [SQL Server] See functions [SQL Server]
- functions [Transact-SQL]
- functions [SQL Server], about functions
- scalar functions
- functions [SQL Server]
ms.assetid: 17186213-5ab5-40b0-b470-b660af1ec44c
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53a2a1be1099b2224b14f8c8d856b7ae07d42ac6
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="what-are-the-sql-database-functions"></a>Quali sono le funzioni di database SQL?
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Informazioni sulle categorie di funzioni predefinite che è possibile utilizzare con i database SQL. È possibile utilizzare le funzioni predefinite o creare funzioni definite dall'utente.
  
## <a name="aggregate-functions"></a>Funzioni di aggregazione

Le funzioni di aggregazione eseguono un calcolo su un set di valori e restituiscono un singolo valore. Sono consentiti nella clausola HAVING di un'istruzione SELECT o elenco di selezione. È possibile utilizzare un'aggregazione in combinazione con la clausola GROUP BY per calcolare l'aggregazione in categorie di righe. Utilizzare la clausola OVER per calcolare l'aggregazione in un intervallo specifico di valore. La clausola OVER non può seguire le aggregazioni GROUPING o GROUPING_ID.

Tutte le funzioni di aggregazione sono deterministiche, ovvero che restituiscono sempre lo stesso valore quando vengono eseguite negli stessi valori di input. Per ulteriori informazioni, vedere [funzioni deterministiche e non](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). |

## <a name="analytic-functions"></a>Funzioni analitiche
Le funzioni analitiche calcolano un valore di aggregazione basato su un gruppo di righe. Tuttavia, a differenza delle funzioni di aggregazione, funzioni analitiche possono restituire più righe per ogni gruppo. È possibile utilizzare le funzioni analitiche per calcolare le medie mobili, totali, percentuali, parziali o i primi N risultati all'interno di un gruppo.

## <a name="ranking-functions"></a>Funzioni di rango
Le funzioni di rango restituiscono un valore di rango per ogni riga di una partizione. In base alla funzione utilizzata, è possibile che venga assegnato lo stesso valore a più righe. Le funzioni di rango non sono deterministiche.

## <a name="rowset-functions"></a>Funzioni rowset
Funzioni rowset restituiscono un oggetto che può essere utilizzato come riferimenti a tabelle in un'istruzione SQL.

## <a name="scalar-functions"></a>Funzioni scalari
Sono applicate a un singolo valore e restituiscono un singolo valore. È possibile usare le funzioni scalari in tutte le posizioni in cui sono consentite espressioni.

### <a name="categories-of-scalar-functions"></a>Categorie di funzioni scalari
  
|Categoria di funzioni|Description|  
|-----------------------|-----------------|  
|[Funzioni di configurazione](configuration-functions-transact-sql.md)|Restituiscono informazioni sulla configurazione corrente.|  
|[Funzioni di conversione](conversion-functions-transact-sql.md)|Supportano l'esecuzione del cast e la conversione del tipo di dati.|  
|[Funzioni di cursore](cursor-functions-transact-sql.md)|Restituiscono informazioni sui cursori.|  
|[Data e ora i tipi e funzioni](date-and-time-data-types-and-functions-transact-sql.md)|Eseguono operazioni su valori di input di data e ora e restituiscono valori stringa, numerici o di data e ora.|  
|[Funzioni JSON](json-functions-transact-sql.md)|Convalidare, eseguire query o modificare i dati JSON.|  
|[Funzioni logiche](http://msdn.microsoft.com/library/5b2b4546-951b-462d-91d5-e41fc5acd6f9)|Eseguono operazioni logiche.|  
|[Funzioni matematiche](mathematical-functions-transact-sql.md)|Eseguono calcoli in base ai valori di input specificati come parametri per le funzioni e restituiscono valori numerici.|  
|[Funzioni dei metadati](metadata-functions-transact-sql.md)|Restituiscono informazioni sul database e sugli oggetti di database.|  
|[Funzioni di sicurezza](security-functions-transact-sql.md)|Restituiscono informazioni sugli utenti e sui ruoli.|  
|[Funzioni stringa](string-functions-transact-sql.md)|Eseguire operazioni su una stringa (**char** o **varchar**) valore di input e restituiscono un valore stringa o numerica.|  
|[Funzioni di sistema](../../relational-databases/system-functions/system-functions-for-transact-sql.md)|Eseguono operazioni e restituiscono informazioni su valori, oggetti e impostazioni in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Funzioni statistiche di sistema](system-statistical-functions-transact-sql.md)|Restituiscono informazioni statistiche sul sistema.|  
|[Funzioni di immagine e testo](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|Eseguono operazioni su valori di input o colonne di testo o immagini e restituiscono informazioni sul valore.|  
  
## <a name="function-determinism"></a>Determinismo delle funzioni  
 Le funzioni predefinite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere deterministiche o non deterministiche. Sono deterministiche quando restituiscono sempre lo stesso risultato ogni volta che vengono chiamate con un set specifico di valori di input. Sono invece non deterministiche se restituiscono valori diversi per ogni chiamata con un set specifico di valori di input. Per ulteriori informazioni, vedere [funzioni deterministiche e non](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)  
  
## <a name="function-collation"></a>Regole di confronto per le funzioni  
 Le funzioni che accettano una stringa di caratteri come input e restituiscono una stringa di caratteri come output usano per l'output le regole di confronto della stringa di input.  
  
 Le funzioni che accettano input di dati non di tipo carattere e restituiscono una stringa di caratteri usano per l'output le regole di confronto predefinite del database corrente.  
  
 Le funzioni che accettano input composti da più stringhe di caratteri e restituiscono una stringa di caratteri impostano le regole di confronto per l'output in base alle regole sulla precedenza delle regole di confronto. Per ulteriori informazioni, vedere [precedenza delle regole di confronto &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [Funzioni deterministiche e non deterministiche](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)   
 [Tramite le Stored procedure &#40; MDX &#41;](../../mdx/using-stored-procedures-mdx.md)  
  
  