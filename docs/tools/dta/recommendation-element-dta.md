---
title: Elemento Recommendation (DTA) | Documenti Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: affac3964b25761341c5ac39e3987a107636fae1
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="recommendation-element-dta"></a>Elemento Recommendation (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Contiene informazioni sugli indici ipotetici che fanno parte di una configurazione specificata dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuno|  
|**Valore predefinito**|Nessuno|  
|**Occorrenza**|Facoltativa. Può essere usato una volta per ogni elemento **Table** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TABLE per Schema &#40; DTA &#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**Elementi figlio**|[Elemento Create &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> Elemento **Drop**. Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](http://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Osservazioni  
 Questo elemento appartiene al nome **RecommendationTypecomplexType** nell'XML Schema dell'Ottimizzazione guidata motore di database. Viene utilizzato per specificare indici per una configurazione ipotetica. Non confondere l'elemento **Recommendation** con altri tipi che possono essere usati per specificare il partizionamento (**RecommendationPType**) o le visualizzazioni (**RecommendationViewType**). Per informazioni su questi altri tipi di elemento **Recommendation** , vedere l' [XML Schema di Ottimizzazione guidata motore di database](http://go.microsoft.com/fwlink/?linkid=43100).  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
