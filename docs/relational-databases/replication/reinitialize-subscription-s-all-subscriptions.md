---
title: Reinizializza sottoscrizioni - Tutte le sottoscrizioni | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.reinit.all.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: e1122018-9f74-43e3-8489-7eae33ff23d9
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c59e203ad41b511bb82c066d11575006711965d9
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="reinitialize-subscriptions---all-subscriptions"></a>Reinizializza sottoscrizioni - Tutte le sottoscrizioni
  La finestra di dialogo **Reinizializza sottoscrizioni** consente di contrassegnare per la reinizializzazione tutte le sottoscrizioni di una pubblicazione. La reinizializzazione include l'applicazione di uno snapshot a ogni Sottoscrittore, eseguita dall'agente di distribuzione per le sottoscrizioni di pubblicazioni transazionali e dall'agente di merge per le sottoscrizioni a pubblicazioni di tipo merge.  
  
## <a name="options"></a>Opzioni  
 **Usa lo snapshot corrente**  
 Selezionare questa opzione per applicare lo snapshot corrente a ogni Sottoscrittore alla successiva esecuzione dell'agente di distribuzione o dell'agente di merge per la sottoscrizione. Se non sono disponibili snapshot validi, questa opzione non può essere selezionata.  
  
 **Usa un nuovo snapshot**  
 Selezionare questa opzione per reinizializzare tutte le sottoscrizioni con un nuovo snapshot. Lo snapshot può essere applicato a ogni Sottoscrittore solo dopo essere stato generato dall'agente snapshot. Se l'agente snapshot è impostato per l'esecuzione in base a una pianificazione, le sottoscrizioni non verranno reinizializzate fino al completamento della successiva esecuzione pianificata dell'agente snapshot.  
  
 Per avviare l'agente snapshot immediatamente, selezionare **Genera il nuovo snapshot ora** .  
  
 **Carica le modifiche non sincronizzate prima della reinizializzazione**  
 Solo per la replica di tipo merge. Selezionare questa opzione per caricare le modifiche in sospeso dai database di sottoscrizione prima che i dati nei Sottoscrittori vengano sovrascritti con uno snapshot.  
  
 Se si aggiunge, elimina o modifica un filtro con parametri, le modifiche in sospeso nel Sottoscrittore non possono essere caricate nel server di pubblicazione durante la reinizializzazione. Per caricare le modifiche in sospeso, sincronizzare tutte le sottoscrizioni prima di modificare il filtro.  
  
 **Contrassegna per la reinizializzazione**  
 Selezionare questa opzione per contrassegnare ogni sottoscrizione per la reinizializzazione. Dopo aver verificato la disponibilità di uno snapshot valido, alla successiva esecuzione dell'agente di distribuzione o dell'agente di merge per la sottoscrizione viene applicato lo snapshot nel Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Reinizializzare le sottoscrizioni](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  