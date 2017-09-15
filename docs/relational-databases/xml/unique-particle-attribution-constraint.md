---
title: Vincolo di attribuzione di particelle univoche | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e8b99a18280070f3960e6e9259e36144e22889c2
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="unique-particle-attribution-constraint"></a>Vincolo di attribuzione di particelle univoche
  In XSD i modelli di contenuto complessi sono soggetti alla regola del vincolo di attribuzione di particelle univoche (UPA, Unique Particle Attribution). Tale regola prevede che ogni elemento in un documento dell'istanza corrisponda in modo non ambiguo a una particella `<xsd:element>` o `<xsd:any>` nel relativo modello di contenuto padre. Ogni schema che contiene un tipo con un modello di contenuto potenzialmente ambiguo viene rifiutato.  
  
 Le cause di ambiguità più comuni sono la presenza di caratteri jolly `<xsd:any>` e le particelle con intervalli di occorrenze variabili, ad esempio minOccurs < maxOccurs. Il modello di contenuto seguente, ad esempio, è ambiguo perché un elemento <`e1`> può corrispondere sia all'elemento `<xsd:element>` che all'elemento `<xsd:any>`.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Anche il modello di contenuto seguente è ambiguo:  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Mentre un documento come `<root><e1/><e2/><e1/></root>` può essere convalidato senza ambiguità, questo non è possibile per un documento quale `<root><e1/><e1/></root>` , perché non è chiaro a quale `<xsd:element>` corrisponda il secondo `<e1/>` . Anche se alcuni documenti possono essere convalidati senza ambiguità, lo schema verrà rifiutato a causa delle ambiguità potenziali.  
  
 Si noti che, affinché un modello di contenuto sia valido, deve essere possibile convalidare in modo non ambiguo tutte le istanze, senza eseguire ricerche look-ahead. Si consideri, ad esempio, il modello di contenuto seguente.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Per un documento quale `<root><e1/><e3/></root>`, la sequenza `<e1/><e3/>` corrisponde esattamente al secondo elemento `<xsd:sequence>`. Poiché tuttavia l'elemento `<xsd:element>` a cui corrisponde `<e1/>` non può essere determinato senza eseguire ricerche look-ahead a `<e3/>`, il modello di contenuto viola la regola del vincolo UPA.  
  
## <a name="finding-more-information"></a>Per ulteriori informazioni  
 Il documento seguente è pubblicato dal World Wide Web Consortium (W3C) e contiene la descrizione tecnica del vincolo di attribuzione di particelle univoche (informazioni in lingua inglese):  
  
 "XML Schema Part 1: Structures Second Edition, W3C Proposed Edited Recommendation":  
  
-   Section 3.8.6: Constraints on Model Group Schema Components  
  
-   Appendix H: Analysis of the Unique Particle Attribution Constraint (non-normative)  
  
 Il documento è disponibile all'indirizzo [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?linkid=48881).  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolte di XML Schema &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  