---
title: Associazione di dati relazionali all'interno di dati XML | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87dca9b5bcd70335a6121b1be1e49f4cc352826e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>Associazione di dati relazionali all'interno di dati XML
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  È possibile specificare [metodi con tipo di dati xml](../../t-sql/xml/xml-data-type-methods.md) per una variabile o colonna con tipo di dati **xml**. Ad esempio il [Metodo query&#40;&#41; &#40;tipo di dati xml&#41;](../../t-sql/xml/query-method-xml-data-type.md) esegue la query XQuery specificata in un'istanza XML. Quando si creano dati XML in questo modo, è possibile inserirvi un valore di una colonna di tipo non XML o di una variabile Transact-SQL. Questo processo viene definito associazione di dati relazionali all'interno di dati XML.  
  
 Nel Motore di database di SQL Server sono disponibili le pseudofunzioni seguenti che consentono di associare dati relazionali non XML all'interno di dati XML:  
  
-   [Funzione sql:column&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md) Consente di usare i valori di una colonna relazionale nell'espressione XQuery o XML DML.  
  
-   [Funzione sql:variable&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md) . Consente di utilizzare il valore di una variabile SQL nell'espressione XQuery o XML DML.  
  
 È possibile usare queste funzioni con i metodi con tipo di dati **xml** quando si vuole esporre un valore relazionale all'interno di dati XML.  
  
 Non è possibile usare queste funzioni per fare riferimento a dati di colonne o variabili di tipo **xml**, CLR definito dall'utente, datetime, smalldatetime, **text**, **ntext**, **sql_variant** e **image**.  
  
 Inoltre, questo tipo di associazione è destinata a scopi di sola lettura, ovvero non è possibile scrivere dati nelle colonne che utilizzano queste funzioni. Ad esempio, sql:variable("@x")="*some expression"* non è consentita.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Esempio: query tra domini tramite sql:variable()  
 Questo esempio illustra come **sql:variable()** può consentire a un'applicazione di impostare i parametri di una query. Il codice ISBN viene passato usando una variabile SQL @isbn. Sostituendo la costante con **sql:variable()** è possibile usare la query per cercare qualsiasi codice ISBN, non solo gli elementi con codice ISBN uguale a 0-7356-1588-2.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** ha un uso analogo e offre vantaggi aggiuntivi. Per migliorare l'efficienza è possibile utilizzare indici sulla colonna, in base a quanto stabilito dallo strumento Query Optimizer basato sui costi. Nella colonna calcolata può inoltre essere archiviata una proprietà promossa.  
  
## <a name="see-also"></a>Vedere anche  
 [metodi con tipo di dati xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
