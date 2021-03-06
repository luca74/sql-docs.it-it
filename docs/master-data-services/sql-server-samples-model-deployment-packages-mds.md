---
title: 'Esempi di SQL Server: pacchetti di distribuzione di modelli (MDS) | Microsoft Docs'
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Master Data Services
- campione
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b37258b7d39b022bb6982c54a9ed14b557af86cc
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>Esempi di SQL Server: pacchetti di distribuzione di modelli (MDS)
  Quando viene installato [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]vengono inclusi anche pacchetti di modelli di esempio. Il percorso predefinito dei pacchetti di modelli di esempio è unità\<>\Programmi\Microsoft SQL Server\130\Master Data Services\Samples\Packages.  
  
 Per istruzioni su come distribuire i pacchetti di modelli di esempio, vedere [Distribuzione di modelli di esempio e dati](../master-data-services/master-data-services-installation-and-configuration.md#deploySample). I pacchetti di modelli di esempio vengono distribuiti con lo [strumento MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]  
>  **Aggiornamenti di esempio in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
>   
>  I pacchetti di esempio sono stati aggiornati per supportare le nuove funzionalità seguenti.  
>   
>  -   Visualizzare le relazione molti-a-molti.  
>   
>      Per altre informazioni, vedere [Relazione M2M nel modello di esempio](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample).  

> -   Valori consentiti dai vincoli per attributi basati su dominio.  
>   
>      Per altre informazioni, vedere [Creare un attributo basato su dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
> -   Richiedere l'approvazione delle modifiche delle entità.  
>   
>      Per altre informazioni, vedere [Approvazione necessaria &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md).  
> -   Usare gli operatori Not ed Else nelle regole di business  
>   
>      Per altre informazioni, vedere [Esempi di regole di business](../master-data-services/business-rule-examples-master-data-services.md).  
> -   Implementare l'indice personalizzato  
>   
>      Per altre informazioni, vedere [Indice personalizzato &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
 

 
 In Master Data Services, un pacchetto è un file XML contenente una struttura di modello distribuibile e, facoltativamente, i dati del modello. Usare i pacchetti di modelli per spostare copie dei modelli da un ambiente MDS a un altro o per creare nuovi modelli nell'ambiente [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
