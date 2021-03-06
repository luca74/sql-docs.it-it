---
title: Sys. Configurations (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38f44fb8d174d3fa32bea9d97e079fce0c3d1afc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ciascun valore di un'opzione di configurazione valida per l'intero server impostata nel sistema.  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|ID univoco del valore di configurazione.|  
|**name**|**nvarchar(35)**|Nome dell'opzione di configurazione.|  
|**valore**|**sql_variant**|Valore configurato per l'opzione.|  
|**minimum**|**sql_variant**|Valore minimo dell'opzione di configurazione.|  
|**maximum**|**sql_variant**|Valore massimo dell'opzione di configurazione.|  
|**value_in_use**|**sql_variant**|Valore corrente dell'opzione.|  
|**Descrizione**|**nvarchar(255)**|Descrizione dell'opzione di configurazione.|  
|**is_dynamic**|**bit**|1 = La variabile viene applicata quando viene eseguita l'istruzione RECONFIGURE.|  
|**is_advanced**|**bit**|1 = la variabile viene visualizzata solo quando il **Mostra advancedoption** è impostata.|  
  
 Per un elenco di tutte le opzioni di configurazione di server, vedere [opzioni di configurazione del Server &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Per le opzioni di configurazione a livello di database, vedere [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Per configurare Soft-NUMA, vedere [Soft-NUMA &#40; SQL Server &#41; ](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo a livello di Server Configuration &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
