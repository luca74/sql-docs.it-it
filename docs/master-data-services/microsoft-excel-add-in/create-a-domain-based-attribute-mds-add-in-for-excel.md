---
title: Creare un attributo basato su dominio (componente aggiuntivo MDS per Excel) | Documenti Microsoft
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f67b43f772e9693f5abbb396b6987527a5220a1d
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>Creare un attributo basato su dominio (componente aggiuntivo MDS per Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]gli amministratori possono creare un attributo basato su dominio per vincolare i valori in una colonna a un set di valori specifico.  
  
 I valori possono essere già presenti nel foglio di lavoro oppure possono derivare da un'entità esistente.  
  
> [!NOTE]  
>  Se gli utenti digitano un valore nella colonna vincolata, anziché selezionarlo nell'elenco, gli errori vengono visualizzati nella colonna **$InputStatus$** al momento della pubblicazione.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione di accesso alle aree funzionali **Amministrazione sistema** e **Visualizzatore** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   Il modello e l'entità devono esistere già.  
  
### <a name="to-perform-this-procedure"></a>Per eseguire questa procedura:  
  
1.  In Excel caricare l'entità contenente la colonna (attributo) che si desiderare vincolare. Per altre informazioni, vedere [Esportare dati in Excel da Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
2.  Fare clic su una cella nella colonna che si desidera vincolare.  
  
3.  Nel gruppo **Compila modello** fare clic su **Proprietà attributi**.  
  
4.  Nella finestra di dialogo **Proprietà attributi** scegliere **Elenco vincolato (basato su dominio)** nell'elenco **Tipo di attributo**.  
  
5.  Nell'elenco **Popola l'attributo con valori di** :  
  
    -   Per usare valori del foglio di lavoro, scegliere **colonna selezionata**. Verranno create una nuova entità e una nuova tabella di gestione con i valori dalla colonna selezionata.  
  
    -   Per utilizzare valori di un'entità esistente, scegliere il nome dell'entità.
    
    Se sono presenti più di 50 entità, è possibile filtrare e cercare per un'entità. In caso contrario, selezionare un'entità dall'elenco a discesa.  
  
6.  Se si sceglie **colonna selezionata** nel passaggio precedente, nella casella **Nome nuova entità** digitare un nome per la nuova entità. Il nome può corrispondere a quello della colonna (attributo).  
  
7.  Scegliere **OK**. In ogni cella nella colonna è ora presente un elenco di valori tra cui gli utenti possono scegliere.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Per aggiungere ed eliminare valori nell'elenco vincolato, caricare l'entità su cui l'attributo è basato. Per altre informazioni sul caricamento delle entità, vedere [Esportare dati in Excel da Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi basati su dominio &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)   
 [Creare un'entità &#40; Il componente aggiuntivo MDS per Excel &#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)   
 [Compilazione di un modello &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  