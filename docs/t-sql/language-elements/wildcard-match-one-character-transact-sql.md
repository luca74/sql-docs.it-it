---
title: _ (Carattere jolly per corrispondenze di singoli caratteri) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 01bc0c4c006ae55395d752a0377575fa680dffaa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (carattere jolly per corrispondenze di singoli caratteri) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Usare il carattere di sottolineatura _ per individuare singoli caratteri in un'operazione di confronto stringhe con criteri di ricerca, ad esempio `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Esempi  

## <a name="a-simple-example"></a>A: Esempio semplice   

L'esempio seguente restituisce tutti i nomi di database che iniziano con la lettera `m` e la cui terza lettera è la lettera `d`. Il carattere di sottolineatura specifica che il secondo carattere del nome può essere qualsiasi lettera. I database `model` e `msdb` soddisfano questi criteri. Il database `master` non li soddisfa.

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
È possibile che altri database soddisfino questi criteri.

È possibile usare più caratteri di sottolineatura per rappresentare più caratteri. La modifica del criterio `LIKE` in modo da includere due caratteri di sottolineatura `'m__%` determinerà l'inclusione del database master nel risultato.

### <a name="b-more-complex-example"></a>B: Esempio più complesso
 Nell'esempio seguente viene usato l'operatore _ per trovare tutte le persone nella tabella `Person` con un nome composto da tre lettere che termina con `an`.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: Escape del carattere di sottolineatura   
L'esempio seguente restituisce i nomi dei ruoli predefiniti del database come `db_owner` e `db_ddladmin`, ma restituisce anche l'utente `dbo`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

Il carattere di sottolineatura nella posizione di terzo carattere viene considerato come un carattere jolly e non viene applicato alcun filtro per restituire solo le entità che iniziano con le lettere `db_`. Racchiudere il carattere di sottolineatura tra parentesi quadre `[_]`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Ora l'utente `dbo` è escluso.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Vedere anche  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Caratteri jolly per la corrispondenza)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Caratteri jolly per la corrispondenza)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; (Caratteri jolly per la mancata corrispondenza dei caratteri)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
