---
title: decimal e numeric (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 614025c21f0f021a4b1ad3a193afec8f5115b845
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal e numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipi di dati numerici con precisione e scala fisse. Decimal e numeric sono sinonimi e possono essere usati in modo intercambiabile.
  
## <a name="arguments"></a>Argomenti  
**decimal**[ **(***p*[ **,***s*] **)**] e **numeric**[ **(***p*[ **,***s*] **)**]  
Numeri con precisione e scala fisse. Se viene utilizzata la precisione massima, i valori validi sono compresi nell'intervallo da - 10^38 +1 a 10^38 - 1. I sinonimi ISO per **decimal** sono **dec** e **dec(***p*, *s***)**. Dal punto di vista funzionale, **numeric** equivale a **decimal**.
  
p (precisione)  
Numero massimo totale di cifre decimali che verranno archiviate, sia a destra sia a sinistra del separatore decimale. La precisione deve essere un valore compreso tra 1 e la precisione massima di 38. La precisione predefinita è 18.
  
> [!NOTE]  
>  Informatica supporta solo 16 cifre significative, indipendentemente dalla precisione e dalla scala specificate.  
  
*s* (scala)  
Numero massimo di cifre decimali che verranno archiviate a destra del separatore decimale. Questo numero viene sottratto da *p* per determinare il numero massimo di cifre a sinistra del separatore decimale. Numero massimo di cifre decimali che è possibile archiviare a destra del separatore decimale. La scala deve essere un valore compreso tra 0 e *p*. È possibile specificare la scala solo se viene specificata la precisione. La scala predefinita è 0. Di conseguenza, 0 <= *s* \<= *p*. Le dimensioni massime di archiviazione variano a seconda della precisione.
  
|Precisione|Byte per l'archiviazione|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (connesso tramite il connettore Informatica di SQL Server PDW) supporta solo 16 cifre significative, indipendentemente dalla precisione e dalla scala specificate.  
  
## <a name="converting-decimal-and-numeric-data"></a>Conversione dei dati di tipo decimal e numeric
Per i tipi di dati **decimal** e **numeric**, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ogni combinazione specifica di precisione e scala viene considerata un tipo di dati diverso. **decimal(5,5)** e **decimal(5,0)** sono ad esempio considerati tipi di dati diversi.
  
Nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] una costante con separatore decimale viene convertita automaticamente in un valore di tipo **numeric** in base ai valori di precisione e scala minimi necessari. Ad esempio, la costante 12.345 viene convertita in un valore **numeric** con precisione 5 e scala 3.
  
La conversione da **decimal** o **numeric** in **float** o **real** può determinare una perdita di precisione. La conversione da **int**, **smallint**, **tinyint**, **float**, **real**, **money** o **smallmoney** in **decimal** o **numeric** può determinare un overflow.
  
Per impostazione predefinita, quando si converte un numero in un valore **decimal** o **numeric** con precisione e scala inferiori, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene applicato l'arrotondamento. Se l'opzione SET ARITHABORT è impostata su ON, in caso di overflow viene segnalato un errore in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La diminuzione di precisione e scala nelle operazioni di conversione non è sufficiente per generare un errore.
  
Quando si convertono i valori float o reali in valori decimali o numerici, il valore decimale non conterrà mai più di 17 decimali. I valori float < 5E-18 verranno convertiti sempre come 0.
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene creata una tabella usando i tipi di dati **decimal** e **numeric**.  I valori vengono inseriti in ogni colonna e i risultati vengono restituiti utilizzando un'istruzione SELECT.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vedere anche
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
