---
title: '| (OR bit per bit Inclusivo) (Espressione SSIS) | Documenti Microsoft'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 90a8167d52a50c569418af86d4f36526ad3482c0
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (OR inclusivo bit per bit) (espressione SSIS)
  Viene eseguita un'operazione con OR bit per bit su due valori integer. Confronta ogni bit del primo operando con il bit corrispondente del secondo operando. Se uno dei due bit ha valore 1, il bit del risultato verrà impostato su 1, altrimenti verrà impostato su 0 (0).  
  
 Entrambe le condizioni devono essere costituite da un valore con tipo di dati Integer con segno o da un valore con tipo di dati Integer senza segno.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression1, integer_ expression2*  
 Qualsiasi espressione valida con tipo di dati Integer con o senza segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Osservazioni  
 Se una delle due condizioni è Null, il risultato dell'espressione sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 Questo esempio esegue un'operazione con OR inclusivo bit per bit tra le variabili **NumberA** e **NumberB**. **NumberA** contiene 3 (00000011) e **NumberB** contiene 9 (00001001).  
  
```  
@NumberA | @NumberB  
```  
  
 L'espressione restituisce 11 (00001011).  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 Questo esempio esegue un'operazione con OR inclusivo bit per bit tra le colonne **ReorderPoint** e **SafetyStockLevel** .  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 Se **ReorderPoint** ha valore 10 e **SafetyStockLevel** ha valore 8, l'espressione restituirà 10 (00001010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 In questo esempio viene eseguita un'operazione con OR inclusivo bit per bit tra due valori integer.  
  
```  
3 | 5   
```  
  
 L'espressione restituisce 7 (00000111).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>Vedere anche  
 [&#124; &#124; &#40; OR logico &#41; &#40; Espressione SSIS &#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40; Bit per bit esclusivo &#41; &#40; Espressione SSIS &#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Associatività e precedenza operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40; Espressione SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  