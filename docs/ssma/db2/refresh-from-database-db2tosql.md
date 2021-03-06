---
title: Aggiornamento dal Database (DB2ToSQL) | Documenti Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 421c86c9b8b61c95d5221c7ca28af9762a530778
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="refresh-from-database-db2tosql"></a>Aggiornamento dal Database (DB2ToSQL)
Il **aggiornamento dal Database** la finestra di dialogo consente di selezionare gli oggetti da aggiornare dal database di DB2. Le righe nella finestra di dialogo sono codificate con colori in base allo stato dei metadati:  
  
-   Se i metadati dell'oggetto sono stato modificato in locale e nel database di DB2, la riga blu.  
  
-   Se i metadati dell'oggetto sono stato modificato nel database di DB2, ma non in SSMA, la riga è gialla.  
  
-   Se i metadati dell'oggetto sono stato modificato in locale, ma non nel database di DB2, la riga è verde.  
  
-   Se l'oggetto è nuovo in database DB2, la riga è rosa.  
  
È possibile specificare le impostazioni di aggiornamento oggetto predefinite nel **impostazioni progetto** la finestra di dialogo. Per altre informazioni, vedere [impostazioni del progetto di&#40;sincronizzazione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Per l'accesso di **aggiornamento dal Database** nella finestra di dialogo scelta di un oggetto in Visualizzatore metadati DB2 e fare clic su **aggiornamento dal Database**.  
  
## <a name="options"></a>Opzioni  
**Comprimi (-)**  
Comprimere tutti i gruppi di oggetti per nascondere singoli oggetti.  
  
**Espansione (+)**  
Espandere tutti i gruppi di oggetti per visualizzare i singoli oggetti.  
  
**Mostra/Nascondi oggetti uguali**  
Nasconde gli oggetti nell'elenco se l'oggetto di metadati sono lo stesso nel database di DB2 in SSMA.  
  
**Aggiornamento dal Database (clic sul pulsante freccia)**  
Utilizzare il pulsante freccia per specificare che i metadati per gli oggetti selezionati devono essere aggiornati in SSMA.  
  
**Eseguire l'operazione non aggiornato dal Database (pulsante) X**  
Utilizzare il pulsante X per specificare che i metadati per gli oggetti selezionati non devono essere aggiornati in SSMA.  
  
**Legenda**  
Consente di visualizzare un **legenda** la finestra di dialogo. La legenda contiene il mapping tra i colori di riga e gli stati di metadati.  
  
Per mantenere il **legenda** la finestra di dialogo in cima il **aggiornamento dal Database** la finestra di dialogo, seleziona il **visualizzare in primo piano** casella di controllo.  
  
