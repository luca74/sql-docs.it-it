---
title: MSSQLSERVER_3169 | Microsoft Docs
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
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abece55da39f2860cb15373ea0a44d21ee9d1ed0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3169"></a>MSSQLSERVER_3169
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3169|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|ND|  
|Testo del messaggio|Il backup del database è stato eseguito in un server che esegue la versione %ls. Tale versione è incompatibile con il server, che esegue la versione %ls. Ripristinare il database in un server che supporta il backup oppure utilizzare un backup compatibile con questo server.|  
  
## <a name="explanation"></a>Spiegazione  
Alcune caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] influiscono sulla struttura dei file di database. Quando si ripristina un database in un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile che il formato di file non sia compatibile con una versione diversa di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
Ad esempio, questo errore può verificarsi quando si usa il formato vardecimalstorage in una versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e successivamente si tenta di ripristinare i file di database in una versione precedente a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2.  
  
## <a name="user-action"></a>Azione dell'utente  
Verificare quale versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione nel server di origine. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fare clic con il pulsante destro del mouse sul server e quindi scegliere **Proprietà** oppure digitare **SELECT @@VERSION** in una finestra Query. Aprire il database utilizzando la versione originale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verificare quali caratteristiche sono attivate nel database originale nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modificare tali impostazioni in modo che funzionino con la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui il database verrà ripristinato.  
  
