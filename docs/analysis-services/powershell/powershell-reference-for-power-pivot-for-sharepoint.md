---
title: Guida di riferimento di PowerShell per PowerPivot per SharePoint | Documenti Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c01735a8-f919-48ad-8d74-35d75a18f821
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39567e2b212761ac2dd726a1f8f33893a83f245c
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>Informazioni di riferimento su PowerShell per Power Pivot per SharePoint

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  In questa sezione vengono elencati i cmdlet di PowerShell utilizzati per configurare o amministrare un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Per altre informazioni sull'abilitazione dei cmdlet e la visualizzazione della Guida integrata, vedere [Configurazione di Power Pivot con Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  

>[!NOTE] 
>In questo articolo può contenere esempi e informazioni non aggiornate. Usare il cmdlet Get-Help per la versione più recente.
  
## <a name="cmdlet-list"></a>Elenco di cmdlet  
 Per visualizzare un elenco di cmdlet dal prompt di PowerShell:  
  
1.  Aprire una shell di gestione di SharePoint usando l'opzione **Esegui come amministratore** .  
  
2.  Immettere il comando seguente: `Get-help *powerpivot*`  
  
|Cmdlet|Versioni supportate|  
|------------|------------------------|  
|[Cmdlet Get-PowerPivotServiceApplication](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Get-PowerPivotSystemService](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Get-PowerPivotSystemServiceInstance](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet New-PowerPivotServiceApplication](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet New-PowerPivotSystemServiceInstance](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Remove-PowerPivotServiceApplication](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Remove-PowerPivotSystemServiceInstance](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Set-PowerPivotServiceApplication](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Set-PowerPivotSystemService](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Update-PowerPivotSystemService](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
  
 Nota: i cmdlet seguenti funzionano solo con SharePoint 2010, non supportato da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  
