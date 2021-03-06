---
title: Codici restituiti | Documenti Microsoft
description: Codici restituiti
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
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37efa9ce4a80cb9d90b3cddccefab243ef3a90ea
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="return-codes"></a>Codici restituiti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Al livello più elementare, una funzione membro può avere esito positivo o negativo. A un livello più approfondito, una funzione può avere esito positivo, ma tale esito potrebbe non corrispondere alle previsioni dello sviluppatore dell'applicazione.  
  
 Per ulteriori informazioni sui codici restituiti OLE DB, vedere [codici restituiti (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando un Driver OLE DB per la funzione membro di SQL Server viene restituito S_OK, la funzione ha avuto esito positivo.  
  
 Quando un Driver OLE DB per la funzione membro di SQL Server non restituisce S_OK, le macro OLE/COM HRESULT FAILED e IS_ERROR possono determinare l'esito positivo o negativo complessivo di una funzione.  
  
 Se FAILED o IS_ERROR restituisce TRUE, il Driver OLE DB per il consumer di SQL Server ha la certezza che l'esecuzione della funzione membro non è riuscita. Se FAILED o IS_ERROR restituisce FALSE e il valore HRESULT non sia uguale a S_OK, il Driver OLE DB per SQL Server consumer è garantito la funzione ha esito positivo in un certo senso. Il consumer può recuperare informazioni dettagliate su questa restituzione "esito positivo con informazioni" dal Driver OLE DB per le interfacce di errore di SQL Server. Inoltre, nel caso in cui una funzione non riesce chiaramente (la macro FAILED restituisce TRUE), informazioni dettagliate sull'errore è disponibile nel Driver OLE DB per le interfacce di errore di SQL Server.  
  
 Il Driver OLE DB per i consumer di SQL Server verifica in genere il valore restituito HRESULT DB_S_ERRORSOCCURRED "esito positivo con informazioni". Le funzioni membro che restituiscono DB_S_ERRORSOCCURRED definiscono in genere uno o più parametri che forniscono al consumer i valori di stato. Nessuna informazione di errore potrebbe essere disponibile per il consumer siano quelle restituite nei parametri con valori di stato, è necessario implementare la logica dell'applicazione per recuperare i valori di stato quando sono disponibili.  
  
 Il Driver OLE DB per le funzioni membro di SQL Server non restituiscono il codice di esito positivo S_FALSE. Tutti i Driver OLE DB per le funzioni membro di SQL Server restituiscono sempre S_OK per indicare l'esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](../../oledb/ole-db-errors/errors.md)  
  
  
