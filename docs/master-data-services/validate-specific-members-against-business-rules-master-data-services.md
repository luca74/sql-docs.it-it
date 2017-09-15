---
title: Convalidare membri specifici rispetto alle regole Business (Master Data Services) | Documenti Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ca1beaf471a1adfb91ec4fa66c32e0bde3c6514
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Convalidare membri specifici rispetto a regole business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] è opportuno applicare selettivamente regole business quando si desidera aggiornare o convalidare subset di membri rispetto a regole business.  
  
> [!NOTE]  
>  Per applicare le regole di business a tutti i membri in una versione di un modello, vedere [Validate a Version against Business Rules &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** .  
  
-   È necessario disporre almeno dell'autorizzazione **Update** per l'oggetto modello al quale vengono applicate le regole di business.  
  
### <a name="to-apply-business-rules-selectively"></a>Per applicare regole business selettivamente  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare un modello nell'elenco **Modello** .  
  
2.  Nell'elenco a discesa **Versione** selezionare una versione.  
  
3.  Fare clic sulla scheda **Esplora** .  
  
4.  Scegliere **Entità** dalla barra dei menu, quindi fare clic sul nome dell'entità contenente i membri a cui applicare le regole.  
  
5.  Fare clic su **Applica regole**. Le regole business sono applicate solo ai membri visualizzati nella griglia.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare una versione rispetto a regole Business &#40; Master Data Services &#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Le regole di business &#40; Master Data Services &#41;](../master-data-services/business-rules-master-data-services.md)  
  
  