---
title: O (DMX) | Documenti Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- DMX
helpviewer_keywords:
- OR operator
ms.assetid: 727a38a9-7f75-4963-8e8a-aa703c129d30
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41cdd1638dc31eefa9cb034db33ef9d30162d617
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Operatore logico che esegue la disgiunzione logica di due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione DMX (Data Mining Extensions) valida che restituisce un valore numerico.  
  
 *Expression2*  
 Espressione DMX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce TRUE se uno o entrambi gli argomenti restituiscono TRUE, FALSE in caso contrario.  
  
## <a name="remarks"></a>Osservazioni  
 Per consentire all'operatore di eseguire la disgiunzione logica, entrambi gli argomenti vengono gestiti come valori booleani, per cui 0 equivale a FALSE e tutti gli altri valori a TRUE. Se uno o entrambi gli argomenti restituiscono TRUE, l'operatore restituirà TRUE. Se *Expression1* restituisce TRUE e *Expression2* restituisce FALSE, l'operatore restituisce TRUE.  
  
 La tabella seguente illustra come viene eseguita la disgiunzione logica.  
  
|Valore di Expression1|Valore di Expression2|Valore restituito|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Vedere anche  
 [Data Mining Extensions &#40; DMX &#41; Riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Logica operatori &#40; DMX &#41;](../dmx/operators-logical.md)   
 [Operatori &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
