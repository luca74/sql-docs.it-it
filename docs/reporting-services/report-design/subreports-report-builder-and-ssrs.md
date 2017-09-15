---
title: Sottoreport (Generatore Report e SSRS) | Documenti Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab5bea3a-109e-4c25-92d9-494df7c52dd8
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8deb7c183ab46007fb0d4c4aee17762676963c4d
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="subreports-report-builder-and-ssrs"></a>Sottoreport (Generatore report e SSRS)
  Un sottoreport è un elemento del report in cui viene visualizzato un altro report all'interno del corpo del report principale. A livello concettuale, un sottoreport in un report è simile a un frame in una pagina Web. Un sottoreport viene utilizzato per incorporare un report in un altro report. Qualsiasi report può essere utilizzato come sottoreport. Il report visualizzato come sottoreport è archiviato in un server di report, solitamente nella stessa cartella del report padre. È possibile progettare il report padre per il passaggio di parametri al sottoreport. Un sottoreport può essere ripetuto all'interno di aree dati, utilizzando un parametro per filtrare i dati in ogni istanza del sottoreport.  
  
> [!NOTE]  
>  Se si utilizza un sottoreport in un'area dati Tablix, il sottoreport e i relativi parametri verranno elaborati per ogni riga dell'area dati nell'area dati. Se le righe sono numerose, è consigliabile valutare l'opportunità di utilizzare un report drill-through.  
  
 ![rs_Subreport](../../reporting-services/report-design/media/rs-subreport.gif "rs_Subreport")  
  
 In questa illustrazione, le informazioni di contatto visualizzate nel report Sales Order principale provengono da un sottoreport Contacts.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-subreports-and-nested-data-regions"></a>Sottoreport e aree dati nidificate  
 Se i sottoreport vengono utilizzati per visualizzare gruppi separati di dati, è consigliabile prendere in considerazione l'utilizzo delle aree dati, ovvero tabelle, matrici o grafici. È possibile che le prestazioni dei report che utilizzano solo le aree dati risultino migliori di quelle dei report che includono sottoreport.  
  
 Utilizzare le aree dati per annidare gruppi di dati dalla stessa origine dati all'interno di un'unica area dati. I sottoreport sono utili per annidare gruppi di dati da diverse origini dati all'interno di un'unica area dati, riutilizzare un sottoreport in più report padre o visualizzare un report autonomo all'interno di un altro report. È possibile, ad esempio, creare un catalogo di prodotti e sottoprodotti inserendo più sottoreport nel corpo di un altro report.  
  
 Le aree dati offrono invece un livello di funzionalità e flessibilità analogo a quello dei sottoreport, ma con prestazioni migliori. Poiché infatti ogni istanza di un sottoreport viene elaborata dal server di report come report distinto, le prestazioni possono risultare rallentate. Per altre informazioni, vedere [Aree dati annidate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md).  
  
## <a name="using-parameters-in-subreports"></a>Utilizzo di parametri nei sottoreport  
 Per passare parametri dal report padre al sottoreport, definire un parametro di report nel report utilizzato come sottoreport. Quando si inserisce il sottoreport nel report padre, è possibile selezionare il parametro di report e un valore da passare dal report padre al parametro di report nel sottoreport.  
  
> [!NOTE]  
>  Il parametro che si seleziona nel sottoreport è un parametro di report, non un parametro di query.  
  
 È possibile inserire un sottoreport nel corpo principale del report o in un'area dati. Se si inserisce un sottoreport in un'area dati, il sottoreport verrà ripetuto per ogni istanza del gruppo o riga dell'area dati. Per passare un valore dal gruppo o dalla riga al sottoreport, nella proprietà del valore del sottoreport utilizzare un'espressione di campo per il campo contenente il valore che si desidera passare al parametro del sottoreport.  
  
 Per ulteriori informazioni sull'utilizzo dei sottoreport, vedere [aggiungere un sottoreport e i parametri &#40; Generatore report e SSRS &#41; ](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md).  
  
## <a name="specifying-subreport-names-and-locations"></a>Specifica di nomi e percorsi dei sottoreport  
 È possibile progettare un report principale per specificare un sottoreport in una cartella diversa nello stesso server di report.  
  
 La sintassi utilizzata per specificare il sottoreport dipende dalla modalità del server di report, ovvero nativa o integrata SharePoint. Per altre informazioni, vedere [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 In Generatore report, per visualizzare in anteprima un sottoreport in un report principale, entrambi i report devono trovarsi nello stesso server di report oppure è necessario specificare il percorso completo del sottoreport.  
  
## <a name="see-also"></a>Vedere anche  
 [Drill-through, drill-down, sottoreport e aree dati nidificate &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  