---
title: Esecuzione di query su un modello tabulare | Documenti Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: b01d45d9-4598-4ded-9a9e-e3419cc3df8e
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1968b025d87d76cf8e1cf2417e13dd6027a252d3
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="querying-a-tabular-model"></a>Esecuzione di query su un modello tabulare
  La query di uno sviluppatore su un modello tabulare produce il recupero dei dati dal database tabulare. Per portare a termine questo obiettivo vi sono due opzioni: utilizzare le query della tabella in DAX o utilizzare MDX e recuperare i dati come se stessero arrivando da un cubo. Tuttavia, a seconda della modalità sottostante del modello tabulare è possibile che l'utilizzo venga limitato alle sole query della tabella DAX. La modalità DirectQuery richiede l'utilizzo di query delle tabelle DAX.  
  
## <a name="querying-with-adomdnet"></a>Query con ADOMD.Net  
 L'utilizzo di ADOMD.Net per eseguire una query su un modello tabulare è semplice e flessibile; è possibile inviare istruzioni MDX o espressioni di query tabulari da DAX al server per ottenere risultati.  
  
 Nel codice seguente vengono mostrate le modalità per passare le istruzioni di query a un modello tabulare e ricevere i risultati  
  
```csharp  
//Function: tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
//   - arg: qry, the tabular query or MDX expression to be evaluated  
//   - arg: cnx, an active and opened ADOMD connection to the database where 'qry' is to be evaluated  
//  
// This function takes a query or mdx expression -qry-, a connection -cnx-  
// and runs the query it against a Tabular Model using ADOMD.net  
//  
// Important note:  
//    If the MDX query contains more than 2 axes (ON COLUMNS, ON ROWS), each axis will come as a new column  
//    If the (All) value of the members in any axis have not been defined, a blank cell is returned. This might be misleading  
//    if the model also has missing values... which are also represented with blank cells.  
private DataTable tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
{  
    ADOMD.AdomdDataAdapter currentDataAdapter = new ADOMD.AdomdDataAdapter(qry, cnx);  
    DataTable tabularResults = new DataTable();  
    currentDataAdapter.Fill(tabularResults);  
    return tabularResults;  
}  
  
```  
  
### <a name="example"></a>Esempio  
 Se il codice sopra riportato viene utilizzato con l'espressione MDX seguente:  
  
```  
SELECT { [Measures].[Internet Total Sales], [Measures].[Reseller Total Sales], [Measures].[Total Sales] } ON COLUMNS  
     , NON EMPTY [Product Category].[Product Category Name].MEMBERS ON ROWS "  
     , NON EMPTY [Date].[Calendar Year].members ON 2 \n"  
FROM [Model]  
  
```  
  
 Rispetto al modello di esempio 'Adventure Works DW Tabulare Denali CTP3' è necessario ricevere i seguenti valori come la tabella risultante:  
  
|Calendar Year|Product Category Name|Internet Total Sales|Reseller Total Sales|Total Sales|  
|-------------------|---------------------------|--------------------------|--------------------------|-----------------|  
|||$     29,358,677.22|$     80,450,596.98|$   109,809,274.20|  
||Accessories|$           700,759.96|$           571,297.93|$        1,272,057.89|  
||Bikes|$     28,318,144.65|$     66,302,381.56|$     94,620,526.21|  
||Clothing|$           339,772.61|$        1,777,840.84|$        2,117,613.45|  
||Components||$     11,799,076.66|$     11,799,076.66|  
|2001||$        3,266,373.66|$        8,065,435.31|$     11,331,808.96|  
|2001|Accessories||$              20,235.36|$              20,235.36|  
|2001|Bikes|$        3,266,373.66|$        7,395,348.63|$     10,661,722.28|  
|2001|Clothing||$              34,376.34|$              34,376.34|  
|2001|Components||$           615,474.98|$           615,474.98|  
|2002||$        6,530,343.53|$     24,144,429.65|$     30,674,773.18|  
|2002|Accessories||$              92,735.35|$              92,735.35|  
|2002|Bikes|$        6,530,343.53|$     19,956,014.67|$     26,486,358.20|  
|2002|Clothing||$           485,587.15|$           485,587.15|  
|2002|Components||$        3,610,092.47|$        3,610,092.47|  
|2003||$        9,791,060.30|$     32,202,669.43|$     41,993,729.72|  
|2003|Accessories|$           293,709.71|$           296,532.88|$           590,242.59|  
|2003|Bikes|$        9,359,102.62|$     25,551,775.07|$     34,910,877.69|  
|2003|Clothing|$           138,247.97|$           871,864.19|$        1,010,112.16|  
|2003|Components||$        5,482,497.29|$        5,482,497.29|  
|2004||$        9,770,899.74|$     16,038,062.60|$     25,808,962.34|  
|2004|Accessories|$           407,050.25|$           161,794.33|$           568,844.58|  
|2004|Bikes|$        9,162,324.85|$     13,399,243.18|$     22,561,568.03|  
|2004|Clothing|$           201,524.64|$           386,013.16|$           587,537.80|  
|2004|Components||$        2,091,011.92|$        2,091,011.92|  
  
 Se l'espressione MDX viene sostituita con questa espressione di query della tabella DAX:  
  
```  
DEFINE  
   MEASURE 'Product Category'[Internet Sales] = SUM( 'Internet Sales'[Sales Amount])  
   MEASURE 'Product Category'[Reseller Sales] = SUM('Reseller Sales'[Sales Amount]) \n"  
   EVALUATE ADDCOLUMNS('Product Category', \"Internet Sales - All Years\", 'Product Category'[Internet Sales], \"Reseller Sales - All Years\", 'Product Category'[Reseller Sales])  
  
```  
  
 e inviata al server utilizzando il codice esempio qui sopra, rispetto al modello di esempio 'Adventure Works DW Tabulare Denali CTP3' si dovrebbero ricevere i seguenti valori come la tabella risultante:  
  
|Product Category Id|Product Category Alternate Id|Product Category Name|Internet Sales|Reseller Sales|  
|-------------------------|-----------------------------------|---------------------------|--------------------|--------------------|  
|4|4|Accessories|$        700,759.96|$        571,297.93|  
|1|1|Bikes|$  28,318,144.65|$  66,302,381.56|  
|3|3|Clothing|$        339,772.61|$    1,777,840.84|  
|2|2|Components||$  11,799,076.66|  
  
  