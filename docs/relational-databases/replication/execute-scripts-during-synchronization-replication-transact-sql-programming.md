---
title: Eseguire script durante la sincronizzazione (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: deef18b1b37375e659dd0412dd7b69f10b8a3bdf
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Esecuzione di script durante la sincronizzazione (programmazione Transact-SQL della replica)
  La replica supporta l'esecuzione di script su richiesta per i Sottoscrittori di pubblicazioni transazionali e di tipo merge. Con questa funzionalità lo script viene copiato nella directory di lavoro della replica e quindi viene applicato al Sottoscrittore tramite **sqlcmd** . Per impostazione predefinita, se si verifica un errore durante l'applicazione dello script per una sottoscrizione di una pubblicazione transazionale, l'agente di distribuzione verrà arrestato. È possibile specificare uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] da eseguire a livello di programmazione tramite le stored procedure di replica.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Per specificare uno script da eseguire per tutti i Sottoscrittori di una pubblicazione snapshot, transazionale o di tipo merge  
  
1.  Comporre e testare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] che verrà eseguito su richiesta.  
  
2.  Salvare il file script in un percorso in cui sia accessibile all'agente snapshot per la pubblicazione.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addscriptexec &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Specificare **@publication**, il nome del file script con il percorso UNC completo creato nel passaggio 2 per **@scriptfile**e uno dei valori seguenti per **@skiperror**:  
  
    -   **0** : l'agente arresterà l'esecuzione dello script se viene rilevato un errore.  
  
    -   **1** : l'agente registrerà gli errori e continuerà l'esecuzione dello script quando vengono rilevati errori.  
  
4.  Lo script specificato verrà eseguito in ogni Sottoscrittore la volta successiva che l'agente verrà eseguito per sincronizzare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare i dati](../../relational-databases/replication/synchronize-data.md)  
  
  