---
title: Agente snapshot | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.snapshotagent.f1
helpviewer_keywords:
- Snapshot Agent dialog box
ms.assetid: b715e621-2cd5-4a15-8f58-a341aa8ef5e4
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bee5c0a544ae0cf33e22d43f1fca706d185b9e1a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="snapshot-agent"></a>agente snapshot
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Nella finestra di dialogo **Agente snapshot** vengono visualizzate informazioni dettagliate sull'agente snapshot, inclusi lo stato, la cronologia, i messaggi informativi e tutti quelli di errore.  
  
## <a name="options"></a>Opzioni  
 Scegliere le sessioni dell'agente snapshot da visualizzare dal menu **Visualizza** e quindi selezionare una specifica sessione nella griglia con etichetta **Sessioni dell'agente snapshot**. Nella griglia con etichetta **Azioni nella sessione selezionata**verranno visualizzate informazioni dettagliate sulla sessione selezionata. Se la sessione selezionata è terminata con un errore, verrà inoltre visualizzata l'area di testo con etichetta **Messaggio o dettagli errore della sessione selezionata** .  
  
 **Visualizza**  
 Consente di selezionare le sessioni dell'agente snapshot da visualizzare.  
  
 **Stato**  
 Stato dell'agente snapshot. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Ripetizione comando non riuscito  
  
-   Non in esecuzione  
  
-   Completato  
  
 **Start Time**  
 Ora di inizio della sessione.  
  
 **Ora fine**  
 Ora di fine della sessione. Se l'agente non è arrestato, questo campo è vuoto.  
  
 **Durata**  
 Periodo di tempo per cui l'agente snapshot è stato eseguito in questa sessione. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale della sessione se la sessione dell'agente è terminata.  
  
 **Messaggio di errore**  
 Se una sessione è terminata con un errore, in questo campo verrà visualizzato l'ultimo messaggio di errore registrato dall'agente snapshot. Se una sessione non è terminata con un errore, questo campo è vuoto.  
  
 **Messaggio azione**  
 Tutti i messaggi informativi e di errore registrati dall'agente snapshot durante la sezione selezionata.  
  
 **Ora azione**  
 Ora di esecuzione dell'azione descritta nella colonna **Messaggio azione** .  
  
 **Messaggio o dettagli errore della sessione selezionata**  
 Area visualizzata solo se per la sessione selezionata è visualizzato il valore **Errore** nella colonna **Stato** . In questa area di testo vengono visualizzate informazioni dettagliate sull'errore e viene indicato il comando di cui è stata tentata l'esecuzione quando si è verificato l'errore. Sono inoltre disponibili collegamenti a contenuto aggiuntivo correlato all'errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione &#40;Monitoraggio replica&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
