---
title: Metodo (SQLServerDataSource) getServerPreparedStatementDiscardThreshold | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ab3592fdaa20290a163e88d2d4b9d057a2f55a2
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold metodo (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il valore di **serverPreparedStatementDiscardThreshold** proprietà di connessione. Questa impostazione Controlla preparato in sospeso quanti Ignora istruzione azioni (sp_unprepare) possono essere in attesa per ogni connessione prima che venga eseguita una chiamata per pulire l'handle in sospeso nel server. Quando l'impostazione è < = 1 unprepare azioni vengono eseguite immediatamente in chiusura istruzione preparata. Se questo valore è impostato su 1 > queste chiamate sono raggruppate per evitare l'overhead della chiamata sp_unprepare troppo spesso.

  
## <a name="syntax"></a>Sintassi  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce il **int** valore il **serverPreparedStatementDiscardThreshold** proprietà di connessione.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successivo.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
