---
title: '&gt;(Maggiore di) (Transact-SQL) | Documenti Microsoft'
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Greater
- Than
- '> (Greater Than)'
- '>_TSQL'
- Greater Than
- '>'
dev_langs:
- TSQL
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: 50a7b098-a3fb-4df6-ae42-1272d6346338
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 20d07527184cd767723198509bff3b55b0562595
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="gt-greater-than-transact-sql"></a>&gt;(Maggiore di) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Confronta due espressioni (operatore di confronto) in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando si confrontano due espressioni diverse da Null, il risultato è TRUE se il valore dell'operando di sinistra è maggiore del valore di quello di destra. In caso contrario, il risultato è FALSE. Se uno o entrambi gli operandi sono NULL, vedere l'argomento [SET ANSI_NULLS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
expression > expression  
```  
  
## <a name="arguments"></a>Argomenti  
 *espressione*  
 È qualsiasi [espressione](../../t-sql/language-elements/expressions-transact-sql.md). È necessario che il tipo di dati di entrambe le espressioni possa essere convertito in modo implicito. La conversione dipende dalle regole di [precedenza dei tipi di dati](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 **Boolean**  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using--in-a-simple-query"></a>A. Utilizzando > in una query semplice  
 L'esempio seguente restituisce tutte le righe nella tabella `HumanResources.Department` che dispongono di un valore in `DepartmentID` maggiore di 13.  
  
```  
--Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID > 13  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
14           Facilities and Maintenance  
15           Shipping and Receiving  
16           Executive  
  
(3 row(s) affected)  
  
```  
  
### <a name="b-using--to-compare-two-variables"></a>B. Utilizzando > per confrontare due variabili  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------  
TRUE  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [IIF &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operatori &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  