---
title: Metodo executeUpdate (SQLServerStatement) | Documenti Microsoft
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
apiname: SQLServerStatement.executeUpdate
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c0c1f5238ece3adb72f108061742034b3df159f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="executeupdate-method-sqlserverstatement"></a>Metodo executeUpdate (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esegue l'istruzione SQL specificata, che può essere un'istruzione INSERT, UPDATE o DELETE, oppure un'istruzione SQL che non restituisce nulla, ad esempio un'istruzione SQL DDL. A partire da [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Driver JDBC 3.0, il metodo executeUpdate restituirà il numero corretto di righe aggiornate in un'operazione di unione.  
  
## <a name="overload-list"></a>Elenco degli overload  
  
|Nome|Description|  
|----------|-----------------|  
|[executeUpdate (lang)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|Esegue l'istruzione SQL specificata, che può essere un'istruzione INSERT, UPDATE, DELETE o MERGE, oppure un'istruzione SQL che non restituisce nulla, ad esempio un'istruzione SQL DDL.|  
|[executeUpdate (lang. String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|Esegue l'istruzione SQL specificata e segnala il [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con il flag specificato se le chiavi generate automaticamente prodotte da questo [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) oggetto deve essere rese disponibile per il recupero.|  
|[executeUpdate (lang, int &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|Esegue l'istruzione SQL specificata e segnala al driver JDBC che le chiavi generate automaticamente indicate nella matrice specificata devono essere rese disponibili per il recupero.|  
|[executeUpdate (lang, lang &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|Esegue l'istruzione SQL specificata e segnala al driver JDBC che le chiavi generate automaticamente indicate nella matrice specificata devono essere rese disponibili per il recupero.|  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
