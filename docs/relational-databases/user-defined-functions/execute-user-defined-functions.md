---
title: Eseguire funzioni definite dall'utente | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08287922d15adabd1128da2edbb1caa65bc3f85f
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="execute-user-defined-functions"></a>Eseguire funzioni definite dall'utente
  Eseguire una funzione definita dall'utente con Transact-SQL.
  

> **Nota:** per altre informazioni, vedere l'argomento sulle  [funzioni definite dall'utente](https://msdn.microsoft.com/library/ms191007.aspx) e [Create Function (Transact SQL)](https://msdn.microsoft.com/library/ms186755.aspx) . 
  
 
##  <a name="BeforeYouBegin"></a> Operazioni preliminari  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 In Transact-SQL è possibile specificare parametri tramite *valore* o*parameter_name*=*valore.* Un parametro non fa parte di una transazione. Se un parametro viene modificato in una transazione per la quale verrà eseguito il rollback, il valore del parametro non viene ripristinato al suo valore precedente. Il valore restituito al chiamante corrisponde sempre al valore specificato al termine del modulo.  
  
###  <a name="Security"></a> Sicurezza  
  
 Per eseguire l'istruzione [EXECUTE](https://msdn.microsoft.com/library/ms188332.aspx) non sono necessarie autorizzazioni specifiche. Sono tuttavia **obbligatorie** autorizzazioni per le entità a protezione diretta a cui si fa riferimento all'interno della stringa EXECUTE. Se, ad esempio, la stringa include un'istruzione [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) , il chiamante dell'istruzione EXECUTE deve avere l'autorizzazione INSERT per la tabella di destinazione. Le autorizzazioni vengono verificate non appena viene rilevata l'istruzione EXECUTE, anche se l'istruzione è inclusa in un modulo. Per altre informazioni, vedere [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
### <a name="example"></a>Esempio 
  
Questo esempio usa la funzione a valori scalari `ufnGetSalesOrderStatusText` disponibile nella maggior parte delle edizioni di `AdventureWorks`.  Lo scopo della funzione è di restituire un valore di testo per lo stato delle vendite da un numero intero specificato.  Modificare l'esempio passando i numeri interi da 1 a 7 al parametro **\@Status** .
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
