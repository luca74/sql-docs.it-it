---
title: Requisiti per aggregazioni CLR definite dall'utente | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a46a1a0e60c7fbe667904388a4c1c8cae93ab827
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="clr-user-defined-aggregates---requirements"></a>CLR aggregazioni definite dall'utente, requisiti
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Un tipo in un assembly di common language runtime (CLR) può essere registrato come una funzione di aggregazione definita dall'utente, purché implementi il contratto di aggregazione necessario. Questo contratto è costituito il **SqlUserDefinedAggregate** metodi del contratto di aggregazione e di attributo. Il contratto di aggregazione include il meccanismo per salvare lo stato intermedio dell'aggregazione e il meccanismo per accumulare nuovi valori, costituito da quattro metodi: **Init**, **Accumulate**,  **Merge**, e **terminare**. Quando si sono soddisfatti questi requisiti, sarà in grado di sfruttare appieno le aggregazioni definite dall'utente in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nelle sezioni seguenti di questo argomento sono disponibili altre informazioni dettagliate su come creare e utilizzare aggregazioni definite dall'utente. Per un esempio, vedere [le funzioni di aggregazione Invoking CLR User-Defined](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Per ulteriori informazioni, vedere [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Metodi di aggregazione  
 La classe registrata come aggregazione definita dall'utente deve supportare i metodi di istanza seguenti. Tali metodi vengono utilizzati da Query Processor per calcolare l'aggregazione:  
  
|Metodo|Sintassi|Description|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|Query Processor utilizza questo metodo per inizializzare il calcolo dell'aggregazione. Questo metodo viene richiamato una volta per ogni gruppo aggregato da Query Processor. Query Processor può scegliere di riutilizzare la stessa istanza della classe di aggregazione per il calcolo delle aggregazioni di più gruppi. Il **Init** metodo deve eseguire qualsiasi la pulizia necessaria rispetto agli utilizzi precedenti di questa istanza e abilitarlo per avviare nuovamente un nuovo calcolo di aggregazione.|  
|**Si accumulano**|`public void Accumulate ( input-type value[, input-type value, ...]);`|Uno o più parametri che rappresentano i parametri della funzione. *INPUT_TYPE* deve essere gestito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati equivalente a nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati specificato da *input_sqltype* nel **CREATE AGGREGATE** istruzione . Per ulteriori informazioni, vedere [Mapping dei dati di parametro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> Per i tipi definiti dall'utente (UDT, User-Defined Type), il tipo di input coincide con il tipo definito dall'utente. Query Processor utilizza questo metodo per accumulare i valori di aggregazione. Il metodo viene richiamato una volta per ogni valore nel gruppo aggregato. Query processor chiama sempre questo solo dopo la chiamata di **Init** metodo nell'istanza specificata della classe di aggregazione. L'implementazione di questo metodo deve aggiornare lo stato dell'istanza per riflettere l'accumulazione del valore dell'argomento passato.|  
|**Merge**|`public void Merge( udagg_class value);`|Questo metodo può essere utilizzato per unire un'altra istanza di questa classe di aggregazione all'istanza corrente. Query Processor utilizza questo metodo per unire più calcoli parziali di un'aggregazione.|  
|**Terminare**|`public return_type Terminate();`|Questo metodo completa il calcolo di aggregazione e restituisce il risultato dell'aggregazione. Il *return_type* deve essere gestito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati che è l'equivalente gestito di *return_sqltype* specificato nella **CREATE AGGREGATE** istruzione. Il *return_type* può anche essere un tipo definito dall'utente.|  
  
### <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 I parametri con valori di tabella, ovvero tipi di tabella definiti dall'utente passati in una procedura o in una funzione, consentono di passare in modo efficiente più righe di dati al server. Pur essendo caratterizzati da funzionalità simili alle matrici di parametri, i parametri con valori di tabella offrono più flessibilità e una maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] Consentono inoltre di ottenere prestazioni potenzialmente migliori. I parametri con valori di tabella consentono inoltre di ridurre il numero di round trip al server. Anziché inviare più richieste al server, ad esempio con un elenco di parametri scalari, è possibile inviare i dati al server sotto forma di parametro con valori di tabella. Un tipo di tabella definito dall'utente non può essere passato come parametro con valori di tabella a una stored procedure gestita o a una funzione in esecuzione nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], né può essere restituito dalle stesse. I parametri con valori di tabella, inoltre, non possono essere utilizzati nell'ambito di una connessione di contesto. È tuttavia possibile utilizzare un parametro con valori di tabella con SqlClient in stored procedure o funzioni gestite eseguite nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se utilizzato in una connessione diversa da una connessione di contesto. La connessione può essere stabilita con lo stesso server che esegue la funzione o la procedura gestita. Per ulteriori informazioni su TVP, vedere [utilizzare parametri &#40; motore di Database &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Aggiornamento della descrizione del **Accumulate** (metodo), che ora accetta più di un parametro.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Richiamo di funzioni di aggregazione definita dall'utente CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  