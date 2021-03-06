---
title: Puntatori statici ODBC | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 049eb6998407ad02ca91565d9b26d0a0bf9b37eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-static-cursors"></a>Puntatori statici ODBC
Un cursore statico è uno in cui il set di risultati sembra essere statico. Non è in genere rilevare le modifiche apportate all'appartenenza, nella disposizione o valori di set di risultati dopo l'apertura del cursore. Si supponga, ad esempio, un cursore statico recupera una riga e un'altra applicazione, quindi aggiorna tale riga. Se un cursore statico recupera nuovamente la riga, i valori rilevati sono identiche, nonostante le modifiche apportate da altre applicazioni.  
  
 I cursori statici rilevano i propri aggiornamenti, eliminazioni e inserimenti, anche non è necessario eseguire questa operazione. Se un cursore statico particolare rileva le modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**. I cursori statici rilevano mai altri Aggiorna, Elimina e inserisce.  
  
 La matrice di stato di riga specificata dall'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR per ogni riga. Restituisce SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED per le righe aggiornate, eliminate o inserite dal cursore, presupponendo che il cursore è possibile rilevare le modifiche.  
  
 I cursori statici vengono in genere implementati dal blocco di righe nel set di risultati o eseguendo una copia dello snapshot, il risultato impostare. Anche se il blocco di righe è relativamente semplice, ha lo svantaggio di ridurre significativamente la concorrenza. Creazione di una copia consente maggiore concorrenza e consente il cursore tenere traccia dei propri aggiornamenti, eliminazioni e inserisce modificando la copia. Tuttavia, una copia è più costosa da verificare e può far divergere dai dati sottostanti, come i dati viene modificati da altri utenti.
