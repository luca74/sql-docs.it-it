---
title: Grafico di tipi (Generatore Report e SSRS) | Documenti Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7b23da886ccf8fc76cbe8e86a722e4e9a8f3e656
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---

# <a name="chart-types-report-builder-and-ssrs"></a>Tipi di grafico (Generatore report e SSRS)

È importante scegliere un tipo di grafico appropriato per il tipo di dati da visualizzare. Tale scelta risulta infatti fondamentale per una corretta interpretazione dei dati visualizzati nel grafico. Se ad esempio il set di dati contiene un numero di punti dati particolarmente elevato rispetto alla dimensioni del grafico, è opportuno rappresentarlo in un grafico ad area, a linee o a dispersione. Per informazioni dettagliate sulla preparazione dei dati in base al tipo di grafico selezionato, vedere [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>Scelta del tipo di grafico  
 A ogni tipo di grafico sono associate caratteristiche univoche per agevolare la visualizzazione del set di dati. Per visualizzare i dati, è possibile usare qualsiasi tipo di grafico, tuttavia la lettura dei dati risulterà facilitata se si sceglie un tipo di grafico adatto ai dati, basato su quanto si intende visualizzare nel report. Nella tabella seguente sono riepilogate le caratteristiche dei grafici che rendono un grafico più o meno appropriato a seconda di un determinato set di dati.  
  
 È possibile modificare il tipo di grafico dopo averlo creato. Per ulteriori informazioni, vedere [modificare un tipo di grafico &#40; Generatore report e SSRS &#41; ](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md).  
  
 Molti esempi di questi tipi di grafici sono disponibili come report di esempio. Per ulteriori informazioni sul download di report di esempio, vedere [report di Generatore Report e progettazione Report di esempio](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
|Tipo di grafico|Visualizzazione di dati proporzionali|Visualizzazione di dati azionari|Visualizzazione di dati lineari|Visualizzazione di dati multivalore|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[Grafici ad aree &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||  
|[Grafici a barre &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||  
|[Barre dei dati](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||  
|[Istogrammi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||  
|[Grafici a linee &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||  
|[Grafici a torta &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||||  
|[Grafici polari &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||||  
|[Grafici a intervalli &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)|||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|  
|[Grafici a dispersione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/scatter-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||  
|[Grafici con forme &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||||  
|[Grafici sparkline](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|  
|[Grafici azionari &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/stock-charts-report-builder-and-ssrs.md)||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")||![Disponibile](../../reporting-services/report-data/media/greencheck.gif "disponibili")|  

## <a name="next-steps"></a>Passaggi successivi

[Grafici](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Punti dati vuoti e Null nei grafici](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
[Aggiungere un grafico a un Report](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  

Ulteriori domande? [Provare a porre il forum di Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)