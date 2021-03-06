---
title: Creare una Query sul contenuto su un modello di Data Mining | Documenti Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- content queries [DMX]
ms.assetid: a0ce837a-89ed-46cf-9ce1-801ccb75fa04
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 77cca4b8462befde098dc522067b44131a009fc8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-content-query-on-a-mining-model"></a>Creare una query sul contenuto di un modello di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]È possibile eseguire una query contenuto del modello di data mining a livello di programmazione tramite AMO o XML/A, ma è più facile creare query mediante DMX. È anche possibile creare query sui set di righe dello schema di data mining stabilendo una connessione all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e creando una query tramite le viste a gestione dinamica fornite da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Nelle procedure riportate di seguito viene illustrato come creare le query su un modello di data mining utilizzando DMX e come eseguire una query sui set di righe dello schema di data mining.  
  
 Per un esempio di come creare una query simile con XMLA, vedere [Creare una query di data mining usando XMLA](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>Esecuzione di una query sul contenuto del modello di data mining utilizzando DMX  
  
#### <a name="to-create-a-dmx-model-content-query"></a>Per creare una query del contenuto del modello DMX  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  Nel riquadro **Esplora modelli** fare clic sull'icona del cubo per modificare l'elenco e visualizzare i modelli di Analysis Services.  
  
3.  Nell'elenco di categorie del modello, espandere **DMX**, **Contenuto del modello**e quindi fare doppio clic su **Query contenuto**.  
  
4.  Nella finestra di dialogo **Connetti a Analysis Services** selezionare l'istanza che contiene il modello di data mining su cui eseguire la query e fare clic su **Connetti**.  
  
     Il modello **Query contenuto** si apre nell'editor del codice adatto. Nel riquadro dei metadati sono elencati i modelli disponibili nel database corrente. Per modificare il database, selezionare un altro database nell'elenco **Database disponibili** .  
  
5.  Immettere il nome di un modello di data mining nella riga, `FROM` [*\<modello di data mining, name, MyModel >*]`.CONTENT`. Se nel nome del modello di data mining sono inclusi spazi, tale nome deve essere racchiuso tra parentesi.  
  
     Se non si vuole digitare il nome, è possibile selezionare un modello di data mining in **Esplora oggetti** e trascinarlo nel modello.  
  
6.  Nella riga, `SELECT`  *\<Seleziona elenco, expr, \* >* , digitare i nomi delle colonne nel set di righe dello schema del contenuto del modello data mining.  
  
     Per visualizzare un elenco di colonne che è possibile restituire nelle query del contenuto del modello di data mining, vedere [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
7.  Facoltativamente, digitare una condizione nella clausola WHERE del modello per limitare le righe restituite a nodi o valori specifici.  
  
8.  Fare clic su **Esegui**.  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>Esecuzione di una query sui set di righe dello schema di data mining  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>Per creare una query sul set di righe dello schema di data mining  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], sulla barra degli strumenti **Nuova query** fare clic su **Query DMX di Analysis Services**o **Query MDX di Analysis Services**.  
  
2.  Nella finestra di dialogo **Connetti ad Analysis Services** selezionare l'istanza che contiene gli oggetti su cui eseguire la query e fare clic su **Connetti**.  
  
     Il modello **Query contenuto** si apre nell'editor del codice adatto. Nel riquadro dei metadati sono elencati gli oggetti disponibili nel database corrente. Per modificare il database, selezionare un altro database nell'elenco **Database disponibili** .  
  
3.  Nell'editor di query digitare quanto segue:  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  Fare clic su **Esegui**.  
  
     Nel riquadro Risultati verrà visualizzato il contenuto del modello.  
  
    > [!NOTE]  
    >  Per visualizzare un elenco di tutti i set di righe dello schema su cui è possibile eseguire una query nell'istanza corrente, utilizzare la query `SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS. In alternativa, per un elenco di set di righe dello schema specifici del data mining, vedere [Set di righe dello schema di data mining](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Set di righe dello schema di data mining](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
