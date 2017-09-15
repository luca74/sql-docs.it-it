---
title: Configurare il Set di campi predefinito per i report di Power View (SSAS tabulare) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- ql12.asvs.bidtoolset.deffieldset.f1
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc0a2fd4178189a072a9b194e502ae1c58de3f92
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="power-view---configure-default-field-set-for-reports"></a>Power View: configurare i Set di campi predefinito per i report
  Un set di campi predefiniti è un elenco predefinito di colonne e misure che vengono aggiunte automaticamente all'area di disegno di un report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] quando si seleziona la tabella nell'elenco dei campi del report. I creatori del modello tabulare possono creare un set di campi predefinito per eliminare passaggi ridondanti per i creatori di report che utilizzano il modello. Ad esempio, se è noto che la maggior parte degli autori del report che utilizza le informazioni di contatto dei clienti desidera vedere sempre il nome di un contatto, il numero telefonico principale, un indirizzo di posta elettronica e il nome dell'azienda, è possibile pre-selezionare tali colonne in modo che vengano sempre aggiunte all'area di disegno del report quando l'autore fa clic sulla tabella Customer Contact.  
  
> [!NOTE]  
>  Un set di campi predefinito si applica solo a un modello tabulare utilizzato come modello di dati in [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. I set di campi predefiniti non sono supportati nei report pivot di Excel.  
  
## <a name="creating-a-default-field-set"></a>Creazione di un set di campi predefinito  
 È possibile determinare quali campi vengono eventualmente inclusi per impostazione predefinita ogni volta che viene selezionata una tabella specifica in [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. È possibile inoltre determinare l'ordine di visualizzazione dei campi nell'elenco. Per specificare un set di campi predefinito, è necessario impostare le proprietà del report nel progetto del modello tabulare.  
  
#### <a name="to-add-a-default-field-set"></a>Per aggiungere un set di campi predefinito  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sulla tabella (scheda) per la quale si sta configurando un elenco di campi predefiniti.  
  
2.  Nella finestra **Proprietà** fare clic su **Fare clic per modificare** nella proprietà **Set di campi predefiniti**.  
  
3.  Nella finestra di dialogo Set di campi predefinito selezionare uno o più campi. È possibile scegliere qualsiasi campo nella tabella, incluse le misure. Tenere premuto il tasto MAIUSC per selezionare un intervallo o il tasto CTRL per selezionare singoli campi.  
  
4.  Fare clic su **Aggiungi** per aggiungerli al set di campi predefiniti.  
  
5.  Utilizzare i pulsanti Su e Giù per specificare un ordine nell'elenco di campi. I campi verranno aggiunti al report nell'ordine definito per il set di campi.  
  
6.  Ripetere questi passaggi per le altre tabelle della cartella di lavoro.  
  
## <a name="next-step"></a>Passaggio successivo  
 Dopo aver creato un set di campi predefinito, è possibile influire ulteriormente sulla progettazione dei report specificando etichette e immagini predefinite, un comportamento del gruppo predefinito o indicando se le righe contenenti lo stesso valore vengono raggruppate in una riga o elencate individualmente. Per altre informazioni, vedere [Configurare le proprietà Comportamento tabella per i report Power View &#40;SSAS tabulare&#41;](../../analysis-services/tabular-models/power-view-configure-table-behavior-properties-for-reports.md).  
  
  