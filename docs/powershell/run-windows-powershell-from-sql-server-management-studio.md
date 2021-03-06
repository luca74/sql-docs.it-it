---
title: Eseguire Windows PowerShell da SQL Server Management Studio| Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: "11"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 762d038aba38b2cbcb8906b729179aca6a6f7835
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2018
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Esecuzione di Windows PowerShell da SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

È possibile avviare sessioni di Windows PowerShell da **Esplora oggetti** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] avvia Windows PowerShell, carica il modulo **SqlServer** e imposta il contesto del percorso al nodo associato nell'albero di **Esplora oggetti**.  
  

> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).



Quando si specifica l'esecuzione di PowerShell per un oggetto in **Esplora oggetti**, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] inizia una sessione di Windows PowerShell in cui sono stati caricati e registrati gli snap-in PowerShell di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Il percorso della sessione è preimpostato sulla posizione dell'oggetto su cui si è fatto clic con il pulsante destro del mouse in Esplora oggetti. Ad esempio, facendo clic con il pulsante destro del mouse sull'oggetto del database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] in Esplora oggetti e selezionando **Avvia PowerShell**, il percorso di PowerShell viene impostato come segue:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>Esecuzione di PowerShell  
 **Per eseguire PowerShell da SQL Server Management Studio**  
  
1.  Aprire **Esplora oggetti**.  
  
2.  Passare al nodo corrispondente all'oggetto desiderato.  
  
3.  Fare clic con il pulsante destro del mouse sull'oggetto e selezionare **Avvia PowerShell**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Quando viene aperto da [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], PowerShell non viene eseguito con privilegi di amministratore, che possono impedire determinate attività quali le chiamate a WMI.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
