---
title: Fare riferimento alla raccolta di XML Schema predefinita (sys) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sys XML schema collections [SQL Server]
- schema collections [SQL Server], predefined
- predefined XML schema collections [SQL Server]
- XML schema collections [SQL Server], predefined
- built-in XML schema collections [SQL Server]
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8140cdb2a53142fd48765bd4747fe3aa25244fd
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="reference-the-built-in-xml-schema-collection-sys"></a>Riferimento alla raccolta di XML Schema predefinita (sys)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Per ogni database creato è disponibile una raccolta di XML Schema **sys** predefinita nello schema relazionale **sys** . Tale raccolta riserva questi schemi predefiniti, ai quali è possibile accedere da qualsiasi altra raccolta XML Schema creata dall'utente. I prefissi utilizzati negli schemi predefiniti sono significativi in XQuery. L'unico prefisso riservato è **xml** .  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = http://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = http://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 Si noti che lo spazio dei nomi **sqltypes** contiene componenti ai quali è possibile fare riferimento da qualsiasi raccolta di XML Schema creata dall'utente. È possibile scaricare lo schema **sqltypes** da questo [sito Web Microsoft](http://go.microsoft.com/fwlink/?linkid=31850). I componenti predefiniti sono:  
  
-   I tipi XSD  
  
-   Gli attributi XML **lang**, **base**e **space**  
  
-   I componenti dello spazio dei nomi **sqltypes**  
  
 La query seguente restituisce i componenti predefiniti ai quali è possibile fare riferimento da una raccolta XML Schema creata dall'utente:  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 Nell'esempio seguente viene illustrato come viene fatto riferimento a tali componenti in uno schema utente. `CREATE XML SCHEMA COLLECTION` consente di creare una raccolta di XML Schema che fa riferimento al `varchar` tipo definito nello spazio dei nomi `sqltypes` . e inoltre all'attributo `lang` definito nello spazio dei nomi `xml` .  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 Si noti quanto segue:  
  
-   Non è possibile modificare XML Schema con questi spazi dei nomi in nessuna raccolta XML Schema definita dall'utente. Ad esempio, la raccolta XML Schema seguente genera un errore perché aggiunge un componente allo spazio dei nomi protetto `sqltypes` :  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   Non è possibile utilizzare la raccolta XML Schema `sys` nelle colonne, variabili o parametri di tipo `xml` . Il codice seguente, ad esempio, restituisce un errore:  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   La serializzazione di questi schemi predefiniti non è supportata. Il codice seguente, ad esempio, restituisce un errore:  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 Il codice seguente rappresenta un altro esempio nel quale viene creata una raccolta XML Schema che utilizza il tipo `varchar` definito nello spazio dei nomi `sqltypes`:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 Come illustrato nell'esempio seguente, è possibile creare una variabile `XML` tipizzata, assegnarvi un'istanza XML e verificare che il valore del tipo di elemento <`root`> corrisponda a un tipo `varchar`.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 L'espressione `instance of sqltypes:varchar?`restituisce TRUE, perché il valore dell'elemento <`root`> è di un tipo derivato da **varchar** in base allo schema associato alla variabile `@var`.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolte di XML Schema &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
