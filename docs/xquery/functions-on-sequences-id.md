---
title: Funzione ID (XQuery) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 341693aa368bc92e5176570711541ab6c217cb88
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-sequences---id"></a>Funzioni per le sequenze - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce la sequenza di nodi elemento con valori xs: ID corrispondenti ai valori di uno o più valori xs: IDREF specificati *$arg*.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Uno o più valori xs:IDREF.  
  
## <a name="remarks"></a>Osservazioni  
 Il risultato della funzione è una sequenza di elementi dell'istanza XML, nell'ordine in cui ricorrono nel documento, con un valore xs:ID uguale a uno o più valori xs:IDREF nell'elenco di valori xs:IDREF candidati.  
  
 Se il valore xs:IDREF non corrisponde ad alcun elemento, la funzione restituisce la sequenza vuota.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo di [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] database.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. Recupero di elementi basati sul valore dell'attributo IDREF  
 Nell'esempio seguente viene utilizzato fn:id per recuperare gli elementi <`employee`>, basati sull'attributo IDREF manager. In questo esempio, l'attributo manager è un attributo di tipo IDREF, mentre l'attributo eid è un attributo di tipo ID.  
  
 Per un valore di attributo specifico di gestione di **ID** funzione trova il <`employee`> elemento il cui valore di attributo di tipo ID corrisponde il valore IDREF di input. In altre parole, per un dipendente specifico, il **ID** funzione restituisce il relativo responsabile.  
  
 Tale caso è illustrato nell'esempio seguente:  
  
-   Viene creata una raccolta di XML Schema.  
  
-   Un oggetto tipizzato **xml** variabile creata tramite la raccolta di XML schema.  
  
-   La query recupera l'elemento con un valore dell'attributo ID a cui fa riferimento il **manager** attributo IDREF di <`employee`> elemento.  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 La query restituisce il valore "Dave", che indica che Dave è il responsabile di Joe.  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. Recupero di elementi basati sul valore dell'attributo IDREFS OrderList  
 Nell'esempio seguente, l'attributo OrderList dell'elemento <`Customer`> è un attributo di tipo IDREFS. che elenca gli ID degli ordini del cliente specifico. Per ogni ID di un ordine, è disponibile un elemento figlio <`Order`> di <`Customer`> che indica il valore dell'ordine.  
  
 L'espressione di query, `data(CustOrders:Customers/Customer[1]/@OrderList)[1]`, recupera il primo valore dall'elenco IDRES relativo al primo cliente. Questo valore viene quindi passato al **ID** (funzione). La funzione trova quindi il <`Order`> elemento il cui valore di attributo OrderID corrispondente all'input di **ID** (funzione).  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non supporta la versione di due argomenti di **ID**.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] richiede il tipo di argomento di **ID** per essere un sottotipo di xs: IDREF *.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni per le sequenze](http://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
