---
title: PDO::exec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3708ab788738ea523f2f879efbcac5eb584614e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara ed esegue un'istruzione SQL in una sola chiamata di funzione, restituendo il numero di righe interessate dall'istruzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>Parametri  
*$statement*: stringa contenente l'istruzione SQL da eseguire.  
  
## <a name="return-value"></a>Valore restituito  
Valore intero che segnala il numero di righe interessate.  
  
## <a name="remarks"></a>Osservazioni  
Se *$statement* contiene più istruzioni SQL, il numero delle righe interessate viene segnalato solo per l'ultima istruzione.  
  
PDO::exec non restituisce risultati per un'istruzione SELECT.  
  
Gli attributi seguenti influiscono sul comportamento di PDO::exec:  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
Per altre informazioni, vedere [PDO::setAttribute](../../connect/php/pdo-setattribute.md). 
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
Questo esempio elimina le righe di Table1 contenenti 'xxxyy' in col1. L'esempio quindi segnala il numero di righe eliminate.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
