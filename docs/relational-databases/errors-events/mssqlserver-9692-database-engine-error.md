---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e493fd5094abc25c1ff3c26edd3c6b6dc0ebc7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9692|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SB2_CANT_LISTEN_PORT_IN_USE|  
|Testo del messaggio|Il trasporto di protocollo %S_MSG non può restare in attesa sulla porta %d perché è in uso da un altro processo.|  
  
## <a name="explanation"></a>Spiegazione  
Un altro programma in esecuzione nel computer sta utilizzando la porta TCP indicata.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire **netstat -aon** per determinare quale programma sta usando la porta. Disabilitare l'applicazione oppure specificare una porta diversa per Service Broker.  
  
