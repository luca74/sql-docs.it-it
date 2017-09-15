---
title: Creare e accedere alle tabelle in TempDB da stored procedure | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 72cc529d0e9dbbc13130d5abe7eaad2e97098bb0
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>Creare e accedere alle tabelle in TempDB da stored procedure
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  La creazione e l'accesso alle tabelle in TempDB dalle stored procedure compilate in modo nativo non è supportato. Usare invece tabelle con ottimizzazione per la memoria con DURABILITY=SCHEMA_ONLY o tipi di tabella e variabili di tabella. 

Per altre informazioni sull'ottimizzazione per la memoria degli scenari di tabella temporanea e variabile di tabella, vedere: [Faster temp table and table variable by using memory optimization](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)(Tabella temporanea e variabile di tabella più rapide con l'ottimizzazione per la memoria).
  
  L'esempio seguente mostra come usare una variabile di tabella **@OrderQuantityByProduct** di tipo **dbo.OrderQuantityByProduct**anziché una tabella temporanea con tre colonne (id, ProductID, Quantity):  
  
```tsql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Costrutti Transact-SQL non supportati da OLTP in memoria](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  