---
title: Risultati dei messaggi di SQL Server | Documenti Microsoft
description: risultati dei messaggi di SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08c47b78d764e62d3e13f55b8a9aa1081d234782
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="sql-server-message-results"></a>Risultati dei messaggi di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Nell'esempio [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzioni non generano Driver OLE DB per i set di righe di SQL Server o un conteggio delle righe interessate quando eseguita:  
  
-   PRINT  
  
-   RAISERROR con gravità minore o uguale a 10  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Queste istruzioni restituiscono uno o più messaggi informativi o determinano la restituzione da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di messaggi informativi in sostituzione dei risultati del conteggio o del set di righe. Dopo l'esecuzione, il Driver OLE DB per SQL Server restituisce S_OK e i messaggi sono disponibili per il Driver OLE DB per il consumer di SQL Server.  
  
 Il Driver OLE DB per SQL Server restituisce S_OK e include uno o più messaggi informativi disponibili dopo l'esecuzione di molte [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzioni o all'esecuzione del consumer di un Driver OLE DB per la funzione membro di SQL Server.  
  
 Il Driver OLE DB per i consumer di SQL Server che consente la specifica dinamica del testo della query deve verificare le interfacce di errore dopo ogni esecuzione della funzione membro indipendentemente dal valore del codice restituito, la presenza o assenza di un insieme restituito **IRowset** oppure **IMultipleResults** riferimento all'interfaccia o un conteggio delle righe interessate.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](../../oledb/ole-db-errors/errors.md)  
  
  
