---
title: getBlob (metodo) (lang) (SQLServerResultSet) | Documenti Microsoft
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
apiname: SQLServerResultSet.getBlob (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 9f730d45-b54a-4961-950e-f4447f7225e1
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f99791ca535b7c143c982f18af2709b8bbf1d625
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="getblob-method-javalangstring-sqlserverresultset"></a>getBlob (metodo) (lang) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del nome della colonna designata nella riga corrente di questo [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) oggetto come oggetto Blob nel linguaggio di programmazione Java.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Blob getBlob(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *colName*  
  
 Oggetto **stringa** che contiene il nome della colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Un oggetto Blob.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getBlob viene specificato dal metodo getBlob nell'interfaccia Java.SQL. ResultSet.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getBlob &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
