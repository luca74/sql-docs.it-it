---
title: IsNull (tipo di dati geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c07ddb41209c507845da7e790035ab54ed1044f1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="isnull-geography-data-type"></a>IsNull (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Proprietà che specifica se l'istanza **geography** è Null. Restituisce 'TRUE' se l'istanza è Null. In caso contrario, restituisce 0.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull` può essere usato per verificare se un'istanza **geography** è Null. Questa verifica potrebbe produrre risultati piuttosto confusi, poiché restituisce 0 se l'istanza è diversa da Null, ma restituisce Null se l'istanza è Null.  
  
 Questo metodo viene usato principalmente dall'infrastruttura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È consigliabile usare il predicato T-SQL IS NULL per verificare se un'istanza **geography** è Null. Per altre informazioni sul predicato T-SQL IS NULL, vedere [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze geografiche](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
