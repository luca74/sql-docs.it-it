---
title: Visualizzare lo stato di un database con mirroring (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- states [SQL Server], database mirroring
- database mirroring [SQL Server], states
ms.assetid: 544f4194-253e-4c57-96ca-31c16301434f
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d1b428ba4fd0196c3b279b905475bc4bad06cd85
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="view-the-state-of-a-mirrored-database-sql-server-management-studio"></a>Visualizzazione dello stato di un database con mirroring (SQL Server Management Studio)
  Durante una sessione di mirroring del database, è possibile visualizzare lo stato nella pagina **Mirroring** della finestra di dialogo **Proprietà database** .  
  
### <a name="to-view-the-status-of-a-database-mirroring-session"></a>Per visualizzare lo stato di una sessione di mirroring del database  
  
1.  Dopo aver attivato la connessione all'istanza del server principale, in Esplora oggetti fare clic sul nome del server per espandere l'albero.  
  
2.  Espandere **Database**e selezionare il database per il mirroring.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Server mirror**. Viene visualizzata la pagina **Mirroring** della finestra di dialogo **Proprietà database** .  
  
4.  In seguito all'avvio del mirroring, nel pannello **Stato** verrà visualizzato lo stato della sessione di mirroring del database nel momento in cui si è selezionata la pagina **Mirroring** o si è fatto clic sul pulsante **Aggiorna** . Gli stati possibili sono indicati di seguito:  
  
    |Stati|Spiegazione|  
    |------------|-----------------|  
    |\<vuoto>|Non esiste alcuna sessione di mirroring del database e non ci sono attività da segnalare nella pagina **Mirroring** .|  
    |In sospeso|Il database principale è in esecuzione, ma non viene inviato alcun log al server mirror. La copia mirror del database non è disponibile.|  
    |Nessuna connessione|L'istanza del server principale non può connettersi ai partner o all'istanza del server di controllo del mirroring (se disponibile).|  
    |Sincronizzazione in corso|La posizione del contenuto del database mirror precede quella del database principale. L'istanza del server principale invia record di log all'istanza del server mirror, che applica le modifiche al database mirror per eseguirne il rollforward.<br /><br /> All'avvio della sessione di mirroring del database, i database mirror e principale sono in stato di sincronizzazione.|  
    |Failover|Nell'istanza del server principale è iniziato un failover manuale (inversione di ruolo), che non è stato ancora accettato dal server mirror.|  
    |Sincronizzato|Il database mirror contiene gli stessi dati del database principale. I failover manuale e automatico sono possibili *solo* in stato sincronizzato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Stati di mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
  