---
title: Metodo getSendStringParametersAsUnicode (SQLServerDataSource) | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.getSendStringParametersAsUnicode
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7eb3b6f95939250d2eccf7edaaa06aace8d743f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>Metodo getSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un **booleano** valore che indica se l'invio di parametri di stringa al server in formato UNICODE è abilitato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se i parametri string vengono inviati al server in formato UNICODE. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà sendStringParametersAsUnicode è impostata su **true**, vale a dire il valore predefinito, i parametri string vengono inviati al server in formato UNICODE. Se sendStringParametersAsUnicode è impostata su **false**, i parametri di stringa vengono inviati al server in formato ASCII/MBCS, non in formato UNICODE. Se non è impostata, getSendStringParametersAsUnicode restituisce il valore predefinito di **true**.  
  
 Per ulteriori informazioni sulla proprietà di connessione sendStringParametersAsUnicode, vedere [impostando le proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
