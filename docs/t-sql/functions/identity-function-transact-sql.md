---
title: IDENTITY (funzione) (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 43d42425842def7572cf7961a89cae355e6b78ae
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="identity-function-transact-sql"></a>IDENTITY (funzione) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Viene usato solo in un'istruzione SELECT con un INTO *tabella* clausola per inserire una colonna identity in una nuova tabella. Pur essendo simili, la funzione IDENTITY e la proprietà IDENTITY utilizzata con CREATE TABLE e ALTER TABLE non sono equivalenti.  
  
> [!NOTE]  
>  Per creare un numero a incremento automatico da usare in più tabelle o da chiamare dalle applicazioni senza fare riferimento ad alcuna tabella, vedere [Numeri di sequenza](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
## <a name="arguments"></a>Argomenti  
 *data_type*  
 Tipo di dati della colonna Identity. Tipi di dati validi per una colonna identity sono tutti tipi di dati della categoria di tipi di dati integer, ad eccezione di **bit** tipo di dati, o **decimale** tipo di dati.  
  
 *valore di inizializzazione*  
 Valore intero da assegnare alla prima riga della tabella. Ogni riga successiva viene assegnato il successivo valore identity, è uguale all'ultimo valore IDENTITY più il *incremento* valore. Se non si specifica *valore di inizializzazione* né *incremento* viene specificato, sia impostata su 1.  
  
 *incremento*  
 Valore intero per aggiungere il *valore di inizializzazione* valore per le righe successive nella tabella.  
  
 *column_name*  
 Nome della colonna da inserire nella nuova tabella.  
  
## <a name="return-types"></a>Tipi restituiti  
 Restituisce lo stesso come *data_type*.  
  
## <a name="remarks"></a>Osservazioni  
 Poiché questa funzione crea una colonna in una tabella, nell'elenco di selezione è necessario specificare un nome per la colonna in uno dei modi seguenti:  
  
```  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
  
```  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono inserite tutte le righe della tabella `Contact` del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] in una nuova tabella denominata `NewContact`. La funzione IDENTITY viene utilizzata per assegnare i numeri di identificazione nella tabella `NewContact` a partire da 100 anziché da 1.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;proprietà&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [Selezionare @local_variable &#40; Transact-SQL &#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [Sys. identity_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  