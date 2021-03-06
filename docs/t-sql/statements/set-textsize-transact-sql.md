---
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5ecffd26c600d3a224824aa9a64ce347cd2f9fbc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Specifica la dimensione dei dati **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **text**, **ntext** e **image** restituiti da un'istruzione SELECT.  
  
> [!IMPORTANT]  
>  I tipi di dati **ntext**, **text** e **image** verranno rimossi in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di utilizzare questi tipi di dati in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni che attualmente li utilizzano. Usare in alternativa **nvarchar(max)**, **varchar(max)**e **varbinary(max)** .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>Argomenti  
 *number*  
 Lunghezza in byte dei dati **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **text**, **ntext** o **image**. *number* è un intero con un valore massimo di 2147483647 (2 GB).  Il valore -1 indica dimensioni illimitate. Il valore 0 reimposta le dimensioni sul valore predefinito (4 KB).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 e versioni successive) e ODBC Driver per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificano automaticamente `-1` (illimitate) al momento della connessione.  
  
 **Driver di versioni precedenti a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:**  Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (versione 9) per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impostano automaticamente l'opzione TEXTSIZE su 2147483647 al momento della connessione.  
  
## <a name="remarks"></a>Remarks  
 L'impostazione dell'opzione SET TEXTSIZE influisce sulla funzione @@TEXTSIZE.  
  
 L'opzione TEXTSIZE viene impostata in fase di esecuzione, non in fase di analisi.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **public** .  
  
## <a name="see-also"></a>Vedere anche  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
