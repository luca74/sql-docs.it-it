---
title: Spazio su disco per il log delle transazioni per operazioni sugli indici | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7fcf3131776066e183f0b6f031dce00d143bdeca
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="transaction-log-disk-space-for-index-operations"></a>Spazio su disco per il log delle transazioni per operazioni sugli indici
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Le operazioni sugli indici su larga scala possono generare carichi di dati di grandi dimensioni che possono causare un rapido riempimento del log delle transazioni. Per garantire la possibilità di esecuzione del rollback dell'operazione sull'indice, non è possibile troncare il log delle transazioni fino al completamento dell'operazione sull'indice. Durante tale operazione è tuttavia possibile eseguire il backup del log. Nel log delle transazioni deve pertanto esserci spazio sufficiente per archiviare sia le transazioni dell'operazione sull'indice che eventuali transazioni utente simultanee per la durata dell'operazione sull'indice. Questo è valido sia per le operazioni sugli indici online che non offline. Poiché durante un'operazione sull'indice offline non è possibile accedere alle tabelle sottostanti, il numero di transazioni utente potrebbe essere basso e il log potrebbe non aumentare in modo eccessivamente rapido. Le operazioni sugli indici online non impediscono attività utente simultanee e pertanto le operazioni sugli indici su larga scala in combinazione con transazioni utente simultanee significative possono causare un aumento continuo del log delle transazioni senza che sia possibile troncarlo.  
  
## <a name="recommendations"></a>Indicazioni  
 Quando si eseguono operazioni sugli indici su larga scala, considerare i consigli seguenti:  
  
1.  Verificare di avere eseguito il backup del log delle transazioni e di averlo troncato prima di eseguire operazioni sugli indici online su larga scala e verificare che nel log vi sia spazio sufficiente per archiviare le transazioni utente e di indice previste.  
  
2.  Valutare l'opportunità di impostare l'opzione SORT_IN_TEMPDB su ON per l'operazione sull'indice. In questo modo, è possibile separare le transazioni di indice dalle transazioni utente simultanee. Le transazioni di indice verranno archiviate nel log delle transazioni di **tempdb** e le transazioni utente simultanee verranno archiviate nel log delle transazioni del database utente. In questo modo, il log delle transazioni del database utente può essere troncato durante l'operazione sull'indice, se necessario. Se, inoltre, il log del database **tempdb** non si trova nello stesso disco del log del database utente, i due log non useranno lo stesso spazio su disco.  
  
    > [!NOTE]  
    >  Verificare che nel database **tempdb** e nel log delle transazioni vi sia spazio su disco sufficiente per gestire l'operazione sull'indice. Il log delle transazioni di **tempdb** non può essere troncato prima del termine dell'operazione sull'indice.  
  
3.  Utilizzare un modello di recupero del database che consenta la registrazione minima dell'operazione sull'indice. In questo modo, sarà possibile ridurre la dimensione del log e impedire che il relativo spazio venga riempito.  
  
4.  Non eseguire l'operazione sull'indice online in una transazione esplicita. Il log non verrà troncato fino al termine della transazione esplicita.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Requisiti di spazio su disco per operazioni DLL sugli indici](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Esempio di spazio su disco per gli indici](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
