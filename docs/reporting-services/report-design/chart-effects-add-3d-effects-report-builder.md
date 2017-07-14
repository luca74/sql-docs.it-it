---
title: Aggiunta di effetti 3D a un grafico (Generatore Report e SSRS) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9625d8-6557-4a4d-8123-eefa7c066ff5
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7170699a3f0cbb26dd2376a8805978fe792223f0
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="chart-effects---add-3d-effects-report-builder"></a>Grafico effetti - aggiunta di effetti 3D (Generatore Report)
  Gli effetti tridimensionali (3D) possono essere usati per fornire profondità e aggiungere un impatto visivo ai grafici impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Ad esempio, se si desidera evidenziare una particolare sezione di un grafico a torta esplosa, è possibile ruotare e modificare la prospettiva del grafico in modo che si noti prima di tutto tale sezione. Quando al grafico vengono applicati effetti 3D, tutti i colori delle sfumature e gli stili di tratteggio vengono disabilitati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-apply-3d-effects-to-a-range-area-line-scatter-or-polar-chart"></a>Per applicare effetti 3D a un grafico a intervallo, ad area, a linee, a dispersione o polare  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi nell'area del grafico e quindi scegliere **Effetti 3D**. Verrà visualizzata la finestra di dialogo **Proprietà area grafico** .  
  
2.  In **Opzioni 3D**selezionare l'opzione **Abilita 3D** .  
  
3.  (Facoltativo) In **Opzioni 3D**è possibile impostare un'ampia varietà di proprietà relative alle opzioni degli angoli e delle scene 3D. Per altre informazioni su queste proprietà, vedere [Effetti 3D, smussature e altri effetti in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md).  
  
4.  Scegliere **OK**.  
  
## <a name="to-apply-3d-effects-to-a-funnel-chart"></a>Per applicare effetti 3D a un grafico a imbuto  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi nell'area del grafico e quindi scegliere **Effetti 3D**. Verrà visualizzata la finestra di dialogo **Proprietà area grafico** .  
  
2.  In **Opzioni 3D**selezionare l'opzione **Abilita 3D** . Scegliere **OK**.  
  
3.  (Facoltativo) Per personalizzare l'aspetto visivo del grafico a imbuto, è possibile aprire il riquadro Proprietà e modificare le proprietà specifiche di questo tipo di grafico.  
  
    1.  Aprire il riquadro Proprietà.  
  
    2.  Nell'area di progettazione fare clic in un punto qualsiasi dell'imbuto. Le proprietà della serie del grafico a imbuto verranno visualizzate nel riquadro Proprietà.  
  
    3.  Nella sezione **Generale** espandere il nodo **CustomAttributes** .  
  
    4.  Per la proprietà **Funnel3DDrawingStyle** , selezionare se l'imbuto verrà visualizzato con una forma circolare o quadrata.  
  
    5.  Per la proprietà **Funnel3DRotationAngle** , impostare un valore compreso tra -10 e 10. Questa opzione determinerà il grado di inclinazione che verrà visualizzato nel grafico a imbuto 3D.  
  
## <a name="to-apply-3d-effects-to-a-pie-chart"></a>Per applicare effetti 3D a un grafico a torta  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi nell'area del grafico, quindi scegliere Effetti 3D. Verrà visualizzata la finestra di dialogo **Proprietà area grafico** .  
  
2.  In **Opzioni 3D**selezionare l'opzione **Abilita 3D** . Scegliere **OK**.  
  
3.  (Facoltativo) In **Rotazione**digitare un valore intero che rappresenta la rotazione orizzontale del grafico a torta.  
  
4.  (Facoltativo) In **Inclinazione**digitare un valore intero che rappresenta la rotazione di inclinazione verticale del grafico a torta.  
  
5.  Scegliere **OK**.  
  
## <a name="to-apply-3d-effects-to-a-bar-or-column-chart"></a>Per applicare effetti 3D a un grafico a barre o a un istogramma  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi nell'area del grafico e quindi scegliere **Effetti 3D**. Verrà visualizzata la finestra di dialogo **Proprietà area grafico** .  
  
2.  Selezionare l'opzione **Abilita 3D** . Scegliere **OK**.  
  
3.  (Facoltativo) Selezionare l'opzione **Abilita clustering serie** . Se il grafico contiene più serie di barre o colonne, con questa opzione le serie verranno visualizzate come cluster. Per impostazione predefinita, più serie di barre o colonne vengono visualizzate affiancate.  
  
4.  Scegliere **OK**.  
  
5.  (Facoltativo) Per aggiungere effetti di cilindro a un grafico a barre o a un istogramma, effettuare le operazioni seguenti:  
  
    1.  Aprire il riquadro Proprietà.  
  
    2.  Nell'area di progettazione fare clic su una delle barre della serie. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
    3.  Nella sezione **Generale** espandere il nodo **CustomAttributes** .  
  
    4.  Per la proprietà **DrawingStyle** , specificare il valore **Cilindro** .  
  
## <a name="see-also"></a>Vedere anche  
 [Effetti 3D, smussature e altri effetti in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md)   
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  