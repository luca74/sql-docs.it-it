---
title: Elemento DTAInput (DTA) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 22a7b07a5dee4e826d2b438d384d44796ca23480
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="dtainput-element-dta"></a>Elemento DTAInput (DTA)
  Contiene la definizione dell'input XML per Ottimizzazione guidata motore di database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristiche|Descrizione|  
|---------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuno|  
|**Valore predefinito**|Nessuno|  
|**Occorrenza**|Facoltativo una volta per ogni elemento **DTAXML** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento DTAXML &#40; DTA &#41;](../../tools/dta/dtaxml-element-dta.md)|  
|**Elementi figlio**|[Elemento server &#40; DTA &#41;](../../tools/dta/server-element-dta.md)<br /><br /> [Elemento Workload &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)<br /><br /> [Elemento TuningOptions &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)<br /><br /> [Elemento Configuration &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)|  
  
## <a name="remarks"></a>Osservazioni  
 Questo è l'elemento radice della gerarchia dello schema di input di Ottimizzazione guidata motore di database. L'input in Ottimizzazione guidata motore di database può essere costituito da argomenti che specificano i server di cui si desidera ottimizzare i database, i carichi di lavoro, le opzioni di ottimizzazione o una configurazione specificata dall'utente.  
  
## <a name="example"></a>Esempio  
 Per un esempio d'uso dell'elemento **DTAInput**, vedere [Esempio di file di input XML semplice &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  