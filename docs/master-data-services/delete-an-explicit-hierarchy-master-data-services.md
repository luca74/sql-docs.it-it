---
title: Eliminare una gerarchia esplicita (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
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
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97194db5e215df90d4260cb7f96d55c7bc008fa0
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>Eliminare una gerarchia esplicita (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eliminare una gerarchia esplicita quando non è più necessaria.  
  
> [!WARNING]  
>  Quando si elimina una gerarchia esplicita, vengono eliminati anche tutti i membri consolidati in essa contenuti. Se si eliminano tutte le gerarchie esplicite per un'entità, vengono eliminate anche tutte le raccolte dell'entità e quest'ultima non è più abilitata per le raccolte e le gerarchie esplicite.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-an-explicit-hierarchy"></a>Per eliminare una gerarchia esplicita  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Gestisci modelli** selezionare un modello dalla griglia, quindi fare clic su **Entità**.  
  
3.  Dalla griglia nella pagina **Gestisci entità** selezionare la riga per l'entità che contiene la gerarchia esplicita da eliminare.  
  
4.  Fare clic su **Gerarchie esplicite**.  
  
5.  Nella pagina **Gestisci gerarchie esplicite** fare clic sulla gerarchia esplicita che si vuole eliminare.  
  
6.  Fare clic su **Modifica**.  
  
7.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una gerarchia esplicita &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Gerarchie esplicite &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
