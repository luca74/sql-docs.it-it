---
title: Proprietà RecordCount (ADO) | Documenti Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6ee9d1ea1c4e996c9608bc1ce76ff3f1baa7c62
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2018
---
# <a name="recordcount-property-ado"></a>Proprietà RecordCount (ADO)

Indica il numero di record in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.
  
## <a name="return-value"></a>Valore restituito

Restituisce un **lungo** valore che indica il numero di record di **Recordset**.
  
## <a name="remarks"></a>Osservazioni

Utilizzare il **RecordCount** sono di proprietà per individuare il numero di record un **Recordset** oggetto. La proprietà restituisce -1 quando ADO non è possibile determinare il numero di record o se il tipo di cursore o provider non supporta **RecordCount**. Lettura di **RecordCount** proprietà in una classe chiusa **Recordset** causa un errore.

#### <a name="bookmarks-or-approximate-positioning"></a>Posizionamento approssimato o i segnalibri

Se l'oggetto Recordset *does* supporta entrambi i segnalibri o approssimativo di posizionamento, questa proprietà restituisce il numero esatto di record del recordset. Questa proprietà restituisce il numero esatto indipendentemente dal fatto il Recordset è stato completamente popolato.

Se l'oggetto Recordset non invece *non* supporta i segnalibri o posizionamento approssimativo, accedere a questa proprietà potrebbe essere un numero significativo sulle risorse. Esaurire le risorse si verifica perché tutti i record devono recuperati e conteggiate per restituire un valore RecordCount accurato.

- **adBookmark** correlate ai segnalibri.
- **adApproxPosition** si riferisce al posizionamento approssimativo.

> [!NOTE]
> In ADO 2.8 e versioni precedenti, il provider SQLOLEDB recupera tutti i record quando viene utilizzato un cursore sul lato server, nonostante il fatto che restituisce **True** per entrambi **supporta (adApproxPosition)** e **Supporta (adBookmark)**.
  
Il tipo di cursore: il **Recordset** oggetto influisce sulla possibilità di determinare il numero di record. Il **RecordCount** proprietà restituirà -1 per un cursore forward-only; il conteggio effettivo per un valore statico o keyset cursore; e -1 o il conteggio effettivo per un cursore dinamico, a seconda dell'origine dati.
  
## <a name="applies-to"></a>Si applica a

[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche

[Esempio di proprietà RecordCount (VB) e di filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Esempio di proprietà RecordCount (VC + +) e di filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[Proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
