---
title: Membri di dimensione (configurazione guidata dimensioni a modifica lenta) derivati | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b99116c19f5ec69fcf382069a1ca3c76ee65b3d6
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>Membri dimensione derivati (Configurazione guidata dimensioni a modifica lenta)
  Utilizzare la finestra di dialogo **Membri dimensione derivati** per specificare le opzioni per l'utilizzo di membri derivati. I membri derivati esistono quando una tabella dei fatti fa riferimento a membri della dimensione non ancora caricati. Dopo il caricamento dei dati relativi al membro derivato, sarà possibile aggiornare il record esistente anziché crearne uno nuovo.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Abilita supporto per membri derivati**  
 Se si sceglie di abilitare i membri derivati, è necessario selezionare una delle due opzioni seguenti.  
  
 **Tutte le colonne con un tipo di modifica sono Null**  
 Consente di specificare se immettere valori Null in tutte le colonne con un tipo di modifica nel nuovo record del membro derivato.  
  
 **Usa una colonna booleana per indicare se il record corrente è un membro derivato**  
 Consente di specificare se utilizzare una colonna booleana esistente per indicare se il record corrente è un membro derivato.  
  
 **Indicatore membro derivato**  
 Se si è scelto di utilizzare una colonna booleana per indicare membri derivati, come descritto in precedenza, selezionare la colonna nell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione degli output tramite configurazione guidata dimensioni a modifica lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  