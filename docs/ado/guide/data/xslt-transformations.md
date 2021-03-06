---
title: Le trasformazioni XSLT | Documenti Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7dc90399ec31c921bfebbd342bbc082365dc238d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="xslt-transformations"></a>Trasformazioni XSLT
XSLT può essere applicato per il codice XML generato per trasformarlo in un altro formato. Comprendere il formato XML in ADO consente di sviluppare modelli XSLT che è possono trasformare in un formato di facile utilizzo.  
  
 Ad esempio, si conosce che ogni riga del Recordset viene salvato come elemento z: riga all'interno dell'elemento di dati: rs. Analogamente, ogni campo del Recordset viene salvato come coppia attributo-valore per questo elemento.  
  
## <a name="remarks"></a>Osservazioni  
 Il seguente script XSLT può essere applicato per il codice XML visualizzato nella sezione precedente per trasformarlo in una tabella HTML da visualizzare nel browser:  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 Lo script XSLT converte il flusso XML generato dal metodo Save ADO in una tabella HTML che visualizza ogni campo del Recordset insieme a un'intestazione di tabella. Le righe e intestazioni della tabella vengono inoltre assegnate diversi tipi di carattere e colori.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
