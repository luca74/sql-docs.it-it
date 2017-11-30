---
title: Viste della replica (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b73dfed7709b76d20856fe03648a7e0c6db0d258
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="replication-views-transact-sql"></a>Viste della replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Queste viste contengono informazioni utilizzate dalla replica in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le viste consentono di semplificare l'accesso ai dati in [tabelle di sistema di replica](../../relational-databases/system-tables/replication-tables-transact-sql.md). Le viste vengono create in un database utente quando questo viene abilitato come database di pubblicazione o sottoscrizione. Tutti gli oggetti di replica vengono rimossi da un database utente quando questo viene rimosso dalla topologia di replica. Il metodo preferito per l'accesso ai metadati di replica è tramite [Stored procedure di replica](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
> [!IMPORTANT]  
>  Gli utenti non devono modificare direttamente le viste di sistema.  
  
## <a name="replication-views"></a>Viste della replica  
 Di seguito è riportato un elenco delle viste di sistema utilizzate dalla replica, raggruppate per database.  
  
### <a name="replication-views-in-the-msdb-database"></a>Viste della replica nel database msdb  
  
|||  
|-|-|  
|[MSdatatype_mappings &#40; Transact-SQL &#41;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[sysdatatypemappings &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>Viste della replica nel database di distribuzione  
  
|||  
|-|-|  
|[IHextendedArticleView &#40; Transact-SQL &#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles &#40; Vista di sistema &#41; &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[IHextendedSubscriptionView &#40; Transact-SQL &#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[sysextendedarticlesview &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[IHsyscolumns &#40; Transact-SQL &#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications &#40;System View&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[MSdistribution_status &#40; Transact-SQL &#41;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions &#40;System View&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns &#40; Vista di sistema &#41; &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>Viste della replica nel database di pubblicazione  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40; Transact-SQL &#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>Viste della replica nel database di sottoscrizione  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40; Transact-SQL &#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  