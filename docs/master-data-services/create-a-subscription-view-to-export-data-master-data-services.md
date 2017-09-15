---
title: Creare una vista sottoscrizioni per esportare i dati (Master Data Services) | Documenti Microsoft
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
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4934e49ef7b8e4f6b56439dd3b414fc93d5af832
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-subscription-view-to-export-data-master-data-services"></a>Creare una vista sottoscrizioni per esportare i dati (Master Data Services)
  Creare una vista sottoscrizioni per esportare dati di Master Data Services nei sistemi di sottoscrizione Si sta creando una vista dei dati nel database di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Gestione integrazione**. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-and-edit-a-subscription-view"></a>Per creare e modificare una vista sottoscrizioni  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]fare clic su **Gestione integrazione**.  
  
2.  Dalla barra dei menu, scegliere **Crea viste**.  
  
3.  Nella pagina **Viste sottoscrizioni** fare clic su **Aggiungi** per creare una vista o fare clic su **Modifica** per modificare una vista. Viene visualizzato un pannello sulla destra.  
  
4.  Digitare un nome per la vista nella casella **Nome** del riquadro **Crea vista sottoscrizioni** .  
  
     Digitare un altro nome per la vista nella casella **Nome** del riquadro **Modifica vista sottoscrizioni** .  
  
5.  Dall'elenco **Modello** , selezionare un modello.  
  
6.  Selezionare **Includi membri eliminati temporaneamente**per includere nella vista i membri eliminati temporaneamente.  
  
7.  Selezionare **Versione** o **Flag versione** in **Opzioni versione**, quindi selezionare una voce nell'elenco corrispondente.  
  
    > [!TIP]  
    >  Creare una vista sottoscrizioni basata su un flag di versione. Quando si blocca una versione, è possibile riassegnare il flag a una versione aperta senza aggiornare la vista sottoscrizioni.  
  
8.  Selezionare **Entità** o **Gerarchia derivata** in **Origini dati** , quindi selezionare una voce nell'elenco corrispondente.  
  
9. Selezionare un formato di vista sottoscrizioni dall'elenco **Formato** .  
  
10. Se si sceglie **Livelli espliciti** o **Livelli derivati** dall'elenco **Formato** , digitare il numero di livelli della gerarchia da includere nella vista.  
  
11. Fare clic su **Salva**.  
  
## <a name="view-information"></a>Visualizzare informazioni  
 Per ogni vista creata, viene aggiunta alla griglia una riga con dieci colonne. La tabella seguente descrive le colonne.  
  
|Colonna|Description|  
|------------|-----------------|  
|Stato|Stato della vista.<br /><br /> Quando fa clic su **salvare**, ![icona per l'aggiornamento dello stato](../master-data-services/media/mds-statusicon-updating.png "icona per l'aggiornamento dello stato") immagine, che indica che la vista sta aggiornando.<br /><br /> Se si verificano errori durante la creazione o la modifica di una vista, la ![icona di stato di errore](../master-data-services/media/mds-statusicon-error.png "icona di stato di errore") immagine consente di visualizzare.<br /><br /> In caso contrario, lo stato è OK e ![icona per lo stato OK](../master-data-services/media/mds-statusicon-ok.png "icona per lo stato OK") immagine consente di visualizzare.|  
|Nome|Nome della vista sottoscrizioni.|  
|Modello|Nome del modello.|  
|Versione|Nome della versione.|  
|Flag versione|Nome del flag di versione.|  
|Gerarchia derivata|Nome della gerarchia derivata.|  
|Entità|Nome dell'entità.|  
|Formato|Specifica il tipo di dati nella vista.|  
|Level|Specifica il numero di livelli nella vista, che viene usato solo per i formati di vista di livello esplicito o derivato|  
|Includi membri eliminati|Indica se nella vista sono inclusi i membri eliminati temporaneamente.|  
  
 Quando si fa clic su una vista, vengono visualizzate le informazioni seguenti.  
  
-   **Creata da**: nome dell'utente che ha creato la vista.  
  
-   **Il**: data e ora di creazione della vista.  
  
-   **Aggiornata da**: nome dell'ultimo utente che ha aggiornato la vista.  
  
-   **Il**: data e ora dell'ultimo aggiornamento della vista.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica: Esportazione di dati &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Eliminare una vista sottoscrizioni &#40; Master Data Services &#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [Creare un Flag di versione &#40; Master Data Services &#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  