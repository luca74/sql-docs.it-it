---
title: 'Invio di aggiornamenti: metodo UpdateBatch | Documenti Microsoft'
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
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 061435976bb08c644705e80c0d1d605ee944f304
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="sending-the-updates-updatebatch-method"></a>Invio di aggiornamenti: metodo UpdateBatch
Il codice seguente viene aperto un Recordset in modalità batch impostando la proprietà LockType su adLockBatchOptimistic e CursorLocation su adUseClient. Aggiunge due nuovi record e modifica il valore di un campo in un record esistente, salvare i valori originali e quindi chiama il metodo UpdateBatch per inviare di nuovo le modifiche all'origine dati.  
  
## <a name="remarks"></a>Osservazioni  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 Se si modifica il record corrente o aggiungendo un nuovo record quando si chiama il metodo UpdateBatch, ADO chiamerà automaticamente il metodo Update per salvare le modifiche in sospeso al record corrente prima di trasmettere le modifiche in blocco al provider.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
