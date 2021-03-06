---
title: Alcune repliche di disponibilità sono disconnesse | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc3af26fd507ef52e13ca29fa72b4dc6640c0dbd
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="some-availability-replicas-are-disconnected"></a>Alcune repliche di disponibilità sono disconnesse
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato di connessione delle repliche di disponibilità|  
|**Problema**|Alcune repliche di disponibilità sono disconnesse.|  
|**Category**|**Avviso**|  
|**Facet**|gruppo di disponibilità|  
  
## <a name="description"></a>Description  
 Questi criteri consentono di eseguire il rollup dello stato di connessione di tutte le repliche di disponibilità e di verificare tutte le repliche di disponibilità che sono disconnesse. I criteri sono in uno stato non integro quando una replica di disponibilità è disconnessa. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili in [Alcune repliche di disponibilità sono disconnesse](http://go.microsoft.com/fwlink/p/?LinkId=220855) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 In questo gruppo di disponibilità, almeno una replica secondaria non è connessa alla replica primaria. Lo stato è DISCONNESSO.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare lo stato dei criteri della replica di disponibilità per trovare quella disconnessa e risolvere il problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il dashboard Always On &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
