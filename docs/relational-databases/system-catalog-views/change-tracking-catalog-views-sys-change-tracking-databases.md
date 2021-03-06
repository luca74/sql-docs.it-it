---
title: Sys. change_tracking_databases (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- change_tracking_databases
- sys.change_tracking_databases_TSQL
- sys.change_tracking_databases
- change_tracking_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.change_tracking_databases
- change tracking [SQL Server], sys.change_tracking_databases
ms.assetid: bb233baa-2991-4904-a0eb-3772b81121a4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2eb40072144b58a09c107f2f9c56a9342ed72e9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="change-tracking-catalog-views---syschangetrackingdatabases"></a>Modificare le viste del catalogo di rilevamento - Sys. change_tracking_databases
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni database con il rilevamento delle modifiche abilitato.  

|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID del database. È univoco all'interno dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_auto_cleanup_on|**bit**|Indica se i dati di rilevamento delle modifiche vengono rimossi automaticamente una volta trascorso il periodo di memorizzazione configurato:<br /><br /> 0 = Off<br /><br /> 1 = On|  
|retention_period|**int**|Se si utilizza la rimozione automatica, il periodo di memorizzazione specifica per quanto tempo i dati di rilevamento delle modifiche verranno conservati nel database.|  
|retention_period_units_desc|**nvarchar(60)**|Specifica la descrizione del periodo memorizzazione:<br /><br /> Minutes<br /><br /> Ore<br /><br /> Giorni|  
|retention_period_units|**tinyint**|Unità di tempo relativa al periodo di memorizzazione:<br /><br /> 1 = Minuti<br /><br /> 2 = Ore<br /><br /> 3 = Giorni|  
  
## <a name="permissions"></a>Permissions  
 Gli stessi controlli dell'autorizzazione vengono effettuati per sys.change_tracking_databases, così come per sys.databases. Se il chiamante di sys.change_tracking_databases non è il proprietario del database, le autorizzazioni minime necessarie per visualizzare la riga corrispondente sono ALTER ANY DATABASE o VIEW ANY DATABASE a livello di server, oppure l'autorizzazione CREATE DATABASE nel database master o corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le viste del catalogo di rilevamento &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [Rilevare le modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
