---
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b786414c1fdd53d21148ff7b682f0b030362afe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver5235"></a>MSSQLSERVER_5235
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|5235|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|Testo del messaggio|[EMERGENCY] DBCC DBCC_COMMAND_DETAILS eseguito da USER_NAME è stato terminato in modo anomalo a causa dello stato di errore ERROR_STATE. Tempo trascorso: HOURS ore MINUTES minuti SECONDS secondi.|  
  
## <a name="explanation"></a>Spiegazione  
Messaggio di riepilogo registrato da DBCC nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando si verifica una chiusura imprevista durante l'esecuzione del comando. Lo stato dell'errore riportato nel messaggio definisce il tipo di chiusura imprevista.  
  
Nella tabella seguente vengono elencati e definiti gli stati di errore.  
  
|Stato di errore|Definizione|  
|---------------|--------------|  
|Stato 1|L'istruzione è stata interrotta a causa di un danneggiamento irreversibile dei metadati. Insieme al messaggio sono presenti una o più istanze dell'errore 8930.|  
|Stato 2|L'istruzione è stata interrotta a causa di un errore di controllo interno. Insieme al messaggio sono presenti una o più istanze dell'errore 8967.|  
|Stato 3|I controlli delle tabelle di sistema del motore di archiviazione principali da parte della tabella di sistema di base non sono stati eseguiti correttamente. Insieme al messaggio sono presenti una o più istanze dell'errore [7984](../../relational-databases/errors-events/mssqlserver-7984-database-engine-error.md), 7985, [7986](~/relational-databases/errors-events/mssqlserver-7986-database-engine-error.md), [7987](~/relational-databases/errors-events/mssqlserver-7987-database-engine-error.md) o [7988](~/relational-databases/errors-events/mssqlserver-7988-database-engine-error.md).|  
|Stato 4|La correzione in modalità di emergenza di DBCC non è stata eseguita correttamente poiché non è stato possibile avviare il database dopo la ricompilazione del log delle transazioni. Insieme al messaggio è presente l'errore 7909.|  
|Stato 5|Durante l'esecuzione del comando si è verificata un'asserzione non riuscita o una violazione dell'accesso.|  
|Stato 6|Si è verificato un errore sconosciuto che ha causato l'interruzione imprevista del comando DBCC.|  
|Stato 7|Interruzione anomala a causa dell'errore nella replica (Always On).|  
  
## <a name="user-action"></a>Azione dell'utente  
Nella tabella seguente vengono illustrate le azioni utente appropriate agli stati di errore specificati.  
  
|Stato di errore|Azione utente|  
|---------------|---------------|  
|Stato 1|Eseguire un ripristino dal backup.|  
|Stato 2|Contattare il Servizio Supporto Tecnico Clienti [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|Stato 3|Eseguire un ripristino dal backup.|  
|Stato 4|Eseguire un ripristino dal backup.|  
|Stato 4|Contattare il Servizio Supporto Tecnico Clienti Microsoft.|  
|Stato 6|Eseguire di nuovo il comando. Se il problema persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.|  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-transact-sql.md)  
  
