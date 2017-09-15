---
title: SET FORCEPLAN (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df0bb88faa940a54f3b3eb14c34998b1982879c6
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quando FORCEPLAN è impostato su ON, Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elabora un join nello stesso ordine delle tabelle nella clausola FROM di una query. L'impostazione di FORCEPLAN su ON determina inoltre l'utilizzo forzato di un nested loop join, a meno che altri tipi di join non siano necessari per la costruzione di un piano per la query o siano richiesti con hint di join o hint per la query.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>Osservazioni  
 L'opzione SET FORCEPLAN sostanzialmente sostituisce la logica utilizzata in Query Optimizer per l'elaborazione di un'istruzione SELECT [!INCLUDE[tsql](../../includes/tsql-md.md)]. I dati restituiti dall'istruzione SELECT sono gli stessi, indipendentemente dall'impostazione. L'unica differenza è la modalità in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elabora le tabelle per soddisfare la query.  
  
 È inoltre possibile utilizzare gli hint di Query Optimizer in query che hanno effetto sulla modalità di elaborazione dell'istruzione SELECT in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 L'opzione SET FORCEPLAN viene applicata in fase di esecuzione, non in fase di analisi.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per l'opzione SET FORCEPLAN vengono assegnate per impostazione predefinita a tutti gli utenti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguito il join di quattro tabelle. L'impostazione dell'opzione `SHOWPLAN_TEXT` è abilitata in modo che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisca le informazioni sulla diversa modalità di elaborazione della query dopo l'abilitazione di `SET FORCE_PLAN`.  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  
