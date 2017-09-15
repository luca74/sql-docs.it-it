---
title: I cursori scorrevoli e isolamento delle transazioni | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 192962491095f8c6b8fb212ab7789cb74b609897
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="scrollable-cursors-and-transaction-isolation"></a>I cursori scorrevoli e isolamento delle transazioni
Nella tabella seguente elenca i fattori che controllano la visibilità delle modifiche.  
  
|Modifiche apportate da:|Visibilità dipende da:|  
|----------------------|----------------------------|  
|Cursore|Tipo di cursore, implementazione dei cursori|  
|Altre istruzioni nella stessa transazione|Tipo di cursore|  
|Istruzioni in altre transazioni|Tipo di cursore, il livello di isolamento delle transazioni|  
  
 Questi fattori vengono visualizzati nella figura seguente.  
  
 ![Fattori che controllano la visibilità delle modifiche](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 Nella tabella seguente sono riepilogate le capacità di ogni tipo di cursore per rilevare le modifiche apportate da se stesso, da altre operazioni nella relativa transazione e da altre transazioni. La visibilità delle modifiche di quest'ultime varia a seconda del tipo di cursore e il livello di isolamento della transazione contenente il cursore.  
  
|Cursore type\action|Self|Proprietario<br /><br /> TXN|Othr<br /><br /> TXN<br /><br /> (RU[a])|Othr<br /><br /> TXN<br /><br /> (RC[a])|Othr<br /><br /> TXN<br /><br /> (RR[a])|Othr<br /><br /> TXN<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|Statico|||||||  
|Insert|Ad esempio [b]|No|No|No|No|No|  
|Update|Ad esempio [b]|No|No|No|No|No|  
|DELETE|Ad esempio [b]|No|No|No|No|No|  
|Gestito da keyset|||||||  
|Insert|Ad esempio [b]|No|No|No|No|No|  
|Update|Sì|Sì|Sì|Sì|No|No|  
|DELETE|Ad esempio [b]|Sì|Sì|Sì|No|No|  
|Dynamic|||||||  
|Insert|Sì|Sì|Sì|Sì|Sì|No|  
|Update|Sì|Sì|Sì|Sì|No|No|  
|DELETE|Sì|Sì|Sì|Sì|No|No|  
  
 [a] le lettere tra parentesi indicano il livello di isolamento della transazione contenente il cursore. il livello di isolamento della transazione (in cui è stata effettuata la modifica) è irrilevante.  
  
 RU: Read uncommitted  
  
 RC: Read commit  
  
 RR: Lettura ripetibile  
  
 S: serializzabile  
  
 [b] dipende dalla modalità di implementazione del cursore. Se il cursore è possibile rilevare le modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**.