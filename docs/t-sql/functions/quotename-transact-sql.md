---
title: QUOTENAME (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f4e40797fc49e8a70b01162fc6959ad60475e8b
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una stringa Unicode a cui sono stati aggiunti i delimitatori per rendere la stringa di input un identificatore delimitato valido di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>Argomenti  
 '*character_string*'  
 Stringa di dati di tipo carattere Unicode. *character_string* è **sysname** ed è limitato a 128 caratteri. In caso di input maggiori di 128 caratteri, viene restituito NULL.  
  
 '*le virgolette*'  
 Stringa di un solo carattere da utilizzare come delimitatore. Può essere una virgoletta singola ( **'** ), una parentesi quadra sinistra o destra ( **[]** ), o un segno di virgolette doppie ( **"** ). Se *le virgolette* viene omesso, vengono utilizzate le parentesi quadre.  
  
## <a name="return-types"></a>Tipi restituiti  
 **nvarchar (258)**  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono utilizzati la stringa di caratteri `abc[]def` e i caratteri `[` e `]` per creare un identificatore delimitato di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido.  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 Si noti che nella stringa `abc[]def` la parentesi quadra chiusa è doppia a indicare un carattere di escape.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente vengono utilizzati la stringa di caratteri `abc def` e i caratteri `[` e `]` per creare un identificatore delimitato di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido.  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni stringa &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

