---
title: Stimare le dimensioni di un database | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d2d986d7e899e630429f431f040addb9076f081a
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="estimate-the-size-of-a-database"></a>Stima delle dimensioni di un database
  Durante la progettazione di un database potrebbe essere necessario stimare le dimensioni che il database può raggiungere quando viene riempito di dati. La stima delle dimensioni del database può consentire di determinare la configurazione hardware necessaria per raggiungere gli obiettivi seguenti:  
  
-   Ottenere il livello di prestazioni necessario per eseguire correttamente le applicazioni.  
  
-   Assegnare la quantità di spazio su disco appropriata per l'archiviazione dei dati e degli indici.  
  
 La stima delle dimensioni del database consente inoltre di determinare se è necessario ottimizzare la struttura del database. Ad esempio, si potrebbe determinare che le dimensioni del database stimate sono troppo grandi per implementarlo nell'organizzazione e che è necessaria una maggiore normalizzazione. Al contrario, le dimensioni potrebbero essere inferiori a quanto previsto e ciò consentirebbe di denormalizzare il database per ottimizzare le prestazioni delle query.  
  
 Per stimare le dimensioni del database, è possibile stimare le dimensioni di ogni singola tabella e quindi sommare i valori ottenuti. Le dimensioni di una tabella dipendono dalla presenza o meno di indici e dal tipo di indici.  
  
## <a name="in-this-section"></a>Argomenti della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Stima delle dimensioni di una tabella](../../relational-databases/databases/estimate-the-size-of-a-table.md)|Definisce i passaggi e i calcoli necessari per stimare la quantità di spazio necessaria per archiviare i dati in una tabella e gli indici associati.|  
|[Stima delle dimensioni di un heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|Definisce i passaggi e i calcoli necessari per stimare la quantità di spazio necessaria per archiviare i dati in un heap, ovvero in una tabella per cui non è disponibile un indice cluster.|  
|[Stima delle dimensioni di un indice cluster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|Definisce i passaggi e i calcoli necessari per stimare la quantità di spazio necessaria per archiviare i dati in un indice cluster.|  
|[Stima delle dimensioni di un indice non cluster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|Definisce i passaggi e i calcoli necessari per stimare la quantità di spazio necessaria per archiviare i dati in un indice non cluster.|  
  
  