---
title: Metodo (SQLServerResultSet) getStatement | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dea981b-b4fd-4f8d-954f-e686124627e2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 129fcea59f7ff9555203fe7ced9b51fabade1d83
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="getstatement-method-sqlserverresultset"></a>getStatement (metodo) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) oggetto che ha generato questo [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Statement getStatement()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Un oggetto SQLServerStatement.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getStatement viene specificato dal metodo getStatement nell'interfaccia Java.SQL. ResultSet.  
  
 Se il set di risultati è stato generato un altro modo, ad esempio da un [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) , questo metodo restituisce null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  