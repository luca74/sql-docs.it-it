---
title: Configurazione dell'archiviazione per le tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: 
ms.date: 10/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e787ac4b1106857a2571dd56c0d352495e8056b
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2018
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configurazione dell'archiviazione per le tabelle con ottimizzazione per la memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È necessario configurare la capacità di archiviazione e le operazioni di input/output al secondo (IOPS).  
  
## <a name="storage-capacity"></a>Capacità di archiviazione  
 Usare le informazioni in [Stimare i requisiti di memoria delle tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) per stimare le dimensioni in memoria delle tabelle ottimizzate per la memoria durevoli del database. Poiché gli indici non vengono mantenuti per le tabelle ottimizzate per la memoria, non includere le dimensioni degli indici. Una volta determinata la dimensione, è necessario fornire uno spazio libero su disco quattro volte superiore alla dimensione delle tabelle in memoria durevoli.  
  
## <a name="storage-iops"></a>IOPS di archiviazione  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] consente di aumentare notevolmente la velocità effettiva del carico di lavoro. Pertanto, è importante verificare che le operazioni di IO non rappresentino un collo di bottiglia.  
  
-   Quando si esegue la migrazione delle tabelle basate su disco nelle tabelle ottimizzate per la memoria, verificare che il log delle transazioni sia in un supporto di archiviazione che supporti l'attività aumentata del log delle transazioni. Ad esempio, se il supporto di archiviazione supporta le operazioni del log delle transazioni a 100 MB/sec e le tabelle ottimizzate per la memoria restituiscono prestazioni cinque volte superiori, anche il supporto di archiviazione del log delle transazioni deve essere in grado di supportare un incremento di cinque volte delle prestazioni, per impedire all'attività del log delle transazioni di diventare un collo di bottiglia.  
  
-   Le tabelle ottimizzate per la memoria sono persistenti nei file di checkpoint distribuiti in uno o più contenitori. In genere è necessario eseguire il mapping di ogni contenitore al relativo dispositivo di archiviazione, che consente di aumentare la capacità di archiviazione e migliorare gli IOPS. È necessario assicurarsi che le operazioni di IOPS sequenziali del supporto di archiviazione possano supportare fino a 3 volte la velocità effettiva del log delle transazioni. Le operazioni di scrittura nei file di checkpoint sono di 256 KB per i file di dati e di 4 KB per file differenziali.
  
     - Ad esempio, se le tabelle ottimizzate per la memoria generano 500 MB/sec di attività nel log delle transazioni, l'archiviazione per le tabelle ottimizzate per la memoria deve supportare IOPS da 1,5 GB/sec. La necessità di supportare fino a 3 volte la velocità effettiva del log delle transazioni deriva dall'analisi che le coppie di file di dati e differenziali vengono prima scritti con dati iniziali e quindi devono essere letti e riscritti come parte di un'operazione di merge.  
  
- Un altro fattore per stimare gli IOPS per l'archiviazione è il tempo di recupero per le tabelle ottimizzate per la memoria. I dati delle tabelle durevoli devono essere letti in memoria prima che un database viene reso disponibile alle applicazioni. In genere, il caricamento dei dati nelle tabelle ottimizzate per la memoria può essere eseguito alla velocità delle operazioni di IOPS. Pertanto se l'archiviazione totale per le tabelle ottimizzate per la memoria durevoli è di 60 GB e si desidera essere in grado di caricare i dati in 1 minuto, le operazioni di IOPS per l'archiviazione devono essere impostati su 1 GB/sec.  
  
-   I file di checkpoint vengono in genere distribuiti in modo uniforme in tutti i contenitori, se lo spazio disponibile lo consente. Con SQL Server 2014 è necessario eseguire il provisioning di un numero dispari di contenitori per ottenere una distribuzione uniforme. A partire dalla versione 2016, sia un numero pari che un numero dispari di contenitori permette una distribuzione uniforme.
  
## <a name="encryption"></a>Crittografia  
 In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]lo spazio di archiviazione per le tabelle ottimizzate per la memoria viene crittografato come parte dell'abilitazione di Transparent Data Encryption nel database. Per altre informazioni sulla crittografia trasparente del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md). In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] i file di checkpoint non vengono crittografati, anche se TDE è abilitata nel database.
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
