---
title: Escludere una regola di business (Master Data Services) | Microsoft Docs
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
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 6d6ae880dffcf2bf01e9a1f3444c9cc775994216
ms.contentlocale: it-it
ms.lasthandoff: 09/07/2017

---
# <a name="exclude-a-business-rule-master-data-services"></a>Escludere una regola business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]escludere una regola di business quando non si vuole eliminarla in modo permanente, ma non si vuole convalidare i dati rispetto a essa.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-exclude-a-business-rule"></a>Per escludere una regola business  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Regole business** selezionare un modello nell'elenco a discesa **Modello** .  
  
4.  Nell'elenco a discesa **Entità** selezionare un'entità.  
  
5.  Nell'elenco a discesa **Tipi di membri** selezionare un tipo di membro.  
  
6.  Nella griglia selezionare la riga per la regola di business che si vuole escludere e quindi fare clic su **Modifica**.  
  
7.  Selezionare la casella di controllo **Esclusa** .  
  
8.  Fare clic su **Salva**.  
  
9. Fare clic su **Pubblica tutto**.  
  
10. Nella finestra di dialogo di conferma fare clic su **OK**. Il valore nella colonna **Stato della regola di business** è **Esclusa** e la colonna **Esclusa** è impostata su **Sì**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una regola business &#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)   
 [Creare e pubblicare una regola di business &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regole di business &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  