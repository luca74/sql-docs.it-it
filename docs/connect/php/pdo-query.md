---
title: 'PDO:: query | Documenti Microsoft'
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
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0ca9c3ffb50dc24d70f4db143d665a20794f65d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esegue una query SQL e restituisce un set di risultati come oggetto PDOStatement.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>Parametri  
*$statement*: istruzione SQL da eseguire.  
  
*$fetch_style*: istruzioni facoltative sull'esecuzione della query. Per altre informazioni, vedere le sezione Osservazioni. $*fetch_style* in PDO:: query può essere sostituito da $*fetch_style* in PDO:: Fetch.  
  
## <a name="return-value"></a>Valore restituito  
Se la chiamata ha esito positivo, PDO::query restituisce un oggetto PDOStatement. Se la chiamata non riesce, PDO::query genera un oggetto PDOException oppure restituisce false, a seconda dell'impostazione di PDO::ATTR_ERRMODE.  
  
## <a name="exceptions"></a>Eccezioni  
PDOException.  
  
## <a name="remarks"></a>Osservazioni  
Una query eseguita con PDO:: query può eseguire un'istruzione preparata o direttamente, a seconda dell'impostazione di PDO:: sqlsrv_attr_direct_query. Per altre informazioni, vedere [Esecuzione di istruzioni diretta e preparata nel driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  
  
PDO:: sqlsrv_attr_query_timeout influisce anche sul comportamento di PDO:: exec; per altre informazioni, vedere [PDO:: SetAttribute](../../connect/php/pdo-setattribute.md).  
  
È possibile specificare le opzioni seguenti per $*fetch_style*.  
  
|style|Description|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|Richiede i dati della colonna specificata. La prima colonna della tabella è la colonna 0.|  
|Fetch_class, '*classname*', matrice ( *arglist* )|Crea un'istanza di una classe e assegna i nomi di colonna alle proprietà della classe. Se il costruttore della classe accetta uno o più parametri, è anche possibile passare *arglist*.|  
|PDO::FETCH_CLASS, '*classname*'|Assegna i nomi delle colonne alle proprietà di una classe esistente.|  
  
Eseguire una chiamata a PDOStatement::closeCursor per rilasciare le risorse di database associate all'oggetto PDOStatement prima di eseguire una nuova chiamata a PDO::query.  
  
È possibile chiudere un oggetto PDOStatement impostandolo su null.  
  
Se non vengono recuperati tutti i dati di un set di risultati, la chiamata successiva a PDO::query avrà esito positivo.  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
Questo esempio mostra diverse query.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
