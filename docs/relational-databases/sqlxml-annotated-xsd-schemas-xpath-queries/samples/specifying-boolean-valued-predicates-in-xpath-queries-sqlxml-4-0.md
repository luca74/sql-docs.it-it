---
title: Specifica di predicati con valori booleani nelle query XPath (SQLXML 4.0) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- nested predicates
- successive predicates
- predicates [SQLXML]
- top-level predicates
- Boolean-valued predicates
- multiple predicates
ms.assetid: 5f6e7219-6911-4bca-a54b-56b95e0b43dd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 251563fb2c7bdee03efa1df2e52c37934b736dbc
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="specifying-boolean-valued-predicates-in-xpath-queries-sqlxml-40"></a>Specifica di predicati con valori booleani nelle query XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Negli esempi seguenti viene illustrato come specificare predicati con valori booleani nelle query XPath. Le query XPath di questi esempi vengono specificate sullo schema di mapping contenuto in SampleSchema1.xml. Per informazioni su questo schema di esempio, vedere [Schema XSD con annotazioni di esempio per gli esempi XPath &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-specify-multiple-predicates"></a>A. Specificare più predicati  
 Nella query XPath seguente vengono utilizzati più predicati per trovare informazioni sull'ordine per un ID ordine e un ID cliente specifici:  
  
```  
/child::Customer[attribute::CustomerID="1"]/child::Order[attribute::OrderID="Ord-43860"]  
```  
  
 È possibile specificare un collegamento all'asse `attribute` (@) e, poiché l'asse `child` è l'asse predefinito, può essere omesso dalla query:  
  
```  
/Customer[@CustomerID="1"]/Order[@SalesOrderID="Ord-43860"]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Per testare la query Xpath sullo schema di mapping  
  
1.  Copia il [schema codice di esempio](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello BooleanValuedPredicatesA.xml seguente e salvarlo nella directory in cui viene salvato il file SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="1"]/Order[@SalesOrderID="Ord-43860"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzando ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
     Il risultato è il seguente:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <Order SalesOrderID="Ord-43860" SalesPersonID="280" OrderDate="2001-08-01T00:00:00" DueDate="2001-08-13T00:00:00" ShipDate="2001-08-08T00:00:00">  
        <OrderDetail ProductID="Prod-729" UnitPrice="226.8571" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-738" UnitPrice="220.2496" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-753" UnitPrice="2576.3544" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-756" UnitPrice="1049.7528" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-758" UnitPrice="1049.7528" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-761" UnitPrice="503.3507" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-762" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-763" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-765" UnitPrice="503.3507" OrderQty="2" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-768" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
        <OrderDetail ProductID="Prod-770" UnitPrice="503.3507" OrderQty="1" UnitPriceDiscount="0" />   
      </Order>  
    </ROOT>  
    ```  
  
### <a name="b-specify-successive-and-nested-predicates"></a>B. Specificare predicati successivi e nidificati  
 Nella query seguente viene illustrato l'utilizzo di predicati successivi. La query restituisce tutti i  **\<cliente >** gli elementi figlio del nodo di contesto che hanno entrambi un **SalesPersonID** attributo con un valore 277 e un **TerritoryID**attributo con un valore di 3:  
  
```  
/child::Customer[attribute::SalesPersonID="277"][attribute::TerritoryID="3"]  
```  
  
 La query restituisce il  **\<cliente >** gli elementi che soddisfano entrambe le condizioni specificate nei predicati.  
  
 Un collegamento per il **attributo** asse (@) può essere specificato e poiché il **figlio** è l'asse predefinito, può essere omesso dalla query:  
  
```  
/Customer[@SalesPersonID="277"][@TerritoryID="3"]  
```  
  
 Nella query XPath seguente viene illustrato l'utilizzo di predicati nidificati. La query restituisce tutti i  **\<cliente >** gli elementi figlio del nodo di contesto che includono  **\<ordine >** gli elementi figlio con almeno un  **\<Ordine >** elemento che presenta un **SalesPersonID** attributo valore 2.  
  
```  
/Customer[Order[@SalesPersonID=2]]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Per testare la query Xpath sullo schema di mapping  
  
1.  Copia il [schema codice di esempio](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello nestedSuccessive.xml seguente e salvarlo nella directory in cui viene salvato il file SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
             /Customer[@SalesPersonID="277"][@TerritoryID="3"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzando ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito è riportato un risultato parziale:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="22" SalesPersonID="277" TerritoryID="3"   
            AccountNumber="22" CustomerType="S"   
            Orders="Ord-43874 Ord-44519 Ord-46989 Ord-48013 Ord-49130 Ord-50274 Ord-51807 Ord-57113 Ord-63162 Ord-69495">  
    <Order SalesOrderID="Ord-43874" SalesPersonID="277"   
           OrderDate="2001-08-01T00:00:00"   
           DueDate="2001-08-13T00:00:00"   
           ShipDate="2001-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-763" UnitPrice="503.3507"   
                   OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
    ...  
  </Customer>  
  <Customer CustomerID="39" SalesPersonID="277" TerritoryID="3"   
            AccountNumber="39" CustomerType="S"   
            Orders="Ord-47428 Ord-48367 Ord-49529 Ord-50742 Ord-53591 Ord-59051 Ord-65301 Ord-71912">    <Order SalesOrderID="Ord-47428" SalesPersonID="277"   
           OrderDate="2002-09-01T00:00:00"   
           DueDate="2002-09-13T00:00:00"   
           ShipDate="2002-09-08T00:00:00">  
      <OrderDetail ProductID="Prod-759" UnitPrice="563.7528" OrderQty="2" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-769" UnitPrice="563.7528" OrderQty="1" UnitPriceDiscount="0" />   
      ...  
    </Order>  
    ...  
  </Customer>  
  ...  
</ROOT>  
```  
  
### <a name="c-specify-a-top-level-predicate"></a>C. Specificare un predicato di livello superiore  
 La query seguente restituisce il  **\<cliente >** nodi elemento figlio del nodo di contesto con  **\<ordine >** gli elementi figlio. La query testa il percorso come predicato di livello superiore:  
  
```  
/child::Customer[child::Order]  
```  
  
 Il **figlio** è l'asse predefinito. È pertanto possibile specificare la query nel modo seguente:  
  
```  
/Customer[Order]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Per testare la query Xpath sullo schema di mapping  
  
1.  Copia il [schema codice di esempio](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello TopLevelPredicate.xml seguente e salvarlo nella directory in cui viene salvato il file SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzando ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito è riportato il risultato parziale:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" SalesPersonID="280" TerritoryID="1" AccountNumber="1" CustomerType="S" Orders="Ord-43860 Ord-44501 Ord-45283 Ord-46042">  
    <Order SalesOrderID="Ord-43860" SalesPersonID="280" OrderDate="2001-08-01T00:00:00" DueDate="2001-08-13T00:00:00" ShipDate="2001-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-729" UnitPrice="226.8571" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-738" UnitPrice="220.2496" OrderQty="1" UnitPriceDiscount="0" />   
      ...  
    </Order>  
    <Order SalesOrderID="Ord-44501" SalesPersonID="280" OrderDate="2001-11-01T00:00:00" DueDate="2001-11-13T00:00:00" ShipDate="2001-11-08T00:00:00">  
      <OrderDetail ProductID="Prod-725" UnitPrice="226.8571" OrderQty="3" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-726" UnitPrice="226.8571" OrderQty="2" UnitPriceDiscount="0" />   
      ...  
    </Order>    ...  
  </Customer>  
  ...  
</ROOT>  
```  
  
  
