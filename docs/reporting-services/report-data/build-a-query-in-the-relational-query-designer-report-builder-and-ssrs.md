---
title: Compilare una query in Progettazione query relazionale (Generatore report e SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 166a38397f8af03d0d146c9fdd46388ad128376f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Compilare una query in Progettazione query relazionale (Generatore report e SSRS)
  Una finestra Progettazione query consente di specificare i dati da recuperare da un'origine dati esterna per un set di dati del report. Si utilizza la finestra Progettazione query quando si compila una query in una procedura guidata o si crea una query del set di dati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Un set di dati è basato su un'origine dati. Il tipo di origine dati e l'ambiente di creazione determinano la finestra Progettazione query da visualizzare quando si definisce la query del set di dati. Le funzionalità di Progettazione query variano in base all'origine dati sottostante. Per altre informazioni sui livelli dati, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34) o [Connessioni dati, origini dati e stringhe di connessione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 È possibile utilizzare una finestra Progettazione query per le attività seguenti:  
  
-   Esplorare i metadati per più schemi nell'origine dati esterna  
  
-   Specificare i campi da recuperare per il set di dati  
  
-   Specificare le relazioni tra due oggetti quali tabelle  
  
-   Specificare i filtri per limitare i dati prima che vengono recuperati come dati del report  
  
-   Indicare se creare parametri  
  
-   Specificare le aggregazioni per eseguire i calcoli nell'origine dati esterna  
  
 Dopo avere visualizzato una finestra Progettazione query, è possibile compilare una query nello stesso modo per un set di dati incorporato o un set di dati condiviso. Nelle procedure riportate di seguito viene utilizzata una query del set di dati incorporato.  
  
 Per altre informazioni, vedere [Interfaccia utente di Progettazione query relazionale &#40;Generatore report&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md).  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>Per compilare una query per un set di dati incorporato nella visualizzazione Struttura report  
  
1.  Aprire la finestra Progettazione query. Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sul set di dati e quindi scegliere **Query**.  
  
     Verrà visualizzata la finestra Progettazione query associata all'origine dati.  
  
2.  Nel riquadro Vista di database espandere le cartelle in cui viene visualizzata una vista gerarchica di oggetti dello schema di database quali tabelle, viste e stored procedure. Fare clic sulla casella scelta per selezionare tutti i campi per un oggetto o espandere il nodo per selezionare i singoli campi.  
  
     Quando si selezionano i campi dal riquadro Vista di database, le scelte vengono visualizzate nel riquadro **Seleziona campi** .  
  
     Se si selezionano campi da più tabelle di database correlate, utilizzare il riquadro Relazioni per visualizzare le relazioni tra tabelle rilevate dallo schema del database.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     L'elenco di campi del set di dati viene visualizzato nel riquadro dei dati del report.  
  
### <a name="to-specify-limits-for-a-query"></a>Per specificare i limiti per una query  
  
1.  In Progettazione query relazionale verificare di aver selezionato i campi e che questi vengano visualizzati nel riquadro **Campi selezionati** .  
  
2.  Nella barra degli strumenti del riquadro Filtri applicati fare clic su **Aggiungi filtro**. Verrà visualizzata una nuova riga del filtro.  
  
3.  In **Nome campo**fare clic per visualizzare l'elenco a discesa dei campi e quindi fare clic sul nome del campo in base al quale si vuole filtrare. Per filtrare ad esempio in base alla quantità, fare clic sul campo che contiene il numero di elementi.  
  
4.  In **Operatore**fare clic per visualizzare l'elenco a discesa degli operatori e quindi selezionare l'operatore di confronto da usare nel filtro.  
  
5.  In **Valore**digitare il valore in base al quale si vuole filtrare. Per filtrare ad esempio in base a una quantità maggiore di 100, digitare 100.  
  
6.  Selezionare l'opzione di parametro in questa riga per creare un parametro del set di dati per consentire a un utente di specificare un valore di filtro. Un parametro del report che corrisponde al parametro del set di dati viene creato automaticamente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 L'elenco di campi del set di dati viene visualizzato nel riquadro dei dati del report.  
  
### <a name="to-view-a-query-result-set"></a>Per visualizzare un set di risultati della query  
  
1.  Sulla barra degli strumenti di Progettazione query fare clic su **Esegui query (!)**.  
  
    > [!NOTE]  
    >  Nella finestra Progettazione query vengono utilizzate le credenziali della fase di progettazione per eseguire la query e recuperare il set di risultati. Per altre informazioni, vedere [Specifica di credenziali in Generatore report](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
 La query viene eseguita sull'origine dati e i dati di esempio vengono restituiti nel riquadro Risultati query.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [Finestre di progettazione query &#40;Generatore report&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)   
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Visualizzazione di progettazione set di dati condivisi &#40;Generatore report&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Strumenti di progettazione query in Reporting Services](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)  
  
  
