---
title: /= (assegnazione di divisione) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /=_TSQL
- /=
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, /=
- assignment operators, /=
- augmented operators, /=
- /= (divide equals)
ms.assetid: 9ab25d1e-5c98-4dd7-b2cd-9f49499c86e7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b32481d1595c7414ca3a364e2cd3984d39c69cc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="-division-assignment-transact-sql"></a>/= (assegnazione di divisione) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Esegue la divisione tra due numeri e imposta un valore sul risultato dell'operazione. Ad esempio, se una variabile @x è uguale a 34, a `@x /= 2` viene assegnato il valore originale di @x, quindi viene diviso per 2 e @x viene impostata sul nuovo valore (17).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
expression /= expression  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Qualsiasi [espressione](../../t-sql/language-elements/expressions-transact-sql.md) valida di un qualsiasi tipo di dati della categoria numerica, ad eccezione del tipo di dati **bit**.  
  
## <a name="result-types"></a>Tipi restituiti  
 Restituisce il tipo di dati dell'argomento con la priorità più alta. Per altre informazioni, vedere [Precedenza dei tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Per altre informazioni, vedere [&#40;Divisione&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-transact-sql.md).  

## <a name="examples"></a>Esempi  
L'esempio seguente imposta una variabile su 17. L'operatore `/=` viene quindi usato per impostare la variabile sulla metà del valore originale.  
```sql  
DECLARE @myVariable decimal(5,2);
SET @myVariable = 17.5;
SET @myVariable /= 2;
SELECT @myVariable AS ResultVariable;  
```
  
[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]  
|ResultVariable | 
|--- |
|8,75 |

## <a name="see-also"></a>Vedere anche  
 [Operatori composti &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operatori &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
