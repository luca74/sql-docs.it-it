---
title: Celle (Analysis Services - dati multidimensionali) del cubo | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6542727b42e98fa73f2e485f0bf88426c442df2d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Celle del cubo (Analysis Services - Dati multidimensionali)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Un cubo è composto di celle organizzate per gruppi di misure e dimensioni. Una cella rappresenta l'intersezione logica univoca in un cubo di un membro da ogni dimensione del cubo. Ad esempio, il cubo descritto nella figura seguente contiene un gruppo di due misure organizzato in base a tre dimensioni, denominate Source, Route e Time.  
  
 ![Diagramma del cubo che identifica una singola cella](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro5.gif "diagramma del cubo che identifica una singola cella")  
  
 La cella ombreggiata rappresenta l'intersezione dei membri seguenti:  
  
-   Il membro air della dimensione Route.  
  
-   Il membro Africa della dimensione Source.  
  
-   Il membro 4th quarter della dimensione Time.  
  
-   La misura Packages.  
  
## <a name="leaf-and-nonleaf-cells"></a>Celle foglia e non foglia  
 È possibile ottenere il valore della cella in un cubo in uno dei modi seguenti. Nell'esempio precedente, il valore nella cella può essere recuperato direttamente dalla tabella dei fatti del cubo, perché tutti i membri utilizzati per identificare tale cella sono *i membri foglia*. Un membro foglia non ha membri figlio in termini gerarchici e generalmente fa riferimento a un unico record nella tabella della dimensione. Questo tipo di cella viene considerato un *cella foglia*.  
  
 Tuttavia, una cella può essere inoltre individuata tramite *membri non foglia*. Un membro non foglia è un membro che ha uno o più membri figlio. In questo caso, il valore della cella viene generalmente derivato dall'aggregazione dei membri figlio associati al membro non foglia. Ad esempio, l'intersezione dei membri e delle dimensioni seguenti fa riferimento a una cella il cui valore viene fornito dall'aggregazione:  
  
-   Il membro air della dimensione Route.  
  
-   Il membro Africa della dimensione Source.  
  
-   Il membro 2nd half della dimensione Time.  
  
-   Il membro Packages.  
  
 Il membro 2nd half della dimensione Time è un membro non foglia. È pertanto necessario aggregare tutti i valori associati, come illustrato nella figura seguente.  
  
 ![le celle di quarter 3 ° e 4 per membro 2nd half](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro6.gif "3 ° e 4 celle trimestre per membro 2nd half")  
  
 Supponendo che le aggregazioni dei membri 3rd quarter e 4th quarter siano somme, il valore della cella specificata è 400, che corrisponde al totale di tutte le celle foglia ombreggiate nella figura precedente. Poiché il valore della cella viene derivato dall'aggregazione delle altre celle, la cella specificata viene considerata un *cella non foglia*.  
  
 I valori della cella derivati per i membri che utilizzano rollup personalizzati e gruppi di membri, oltre a membri personalizzati, vengono gestiti in modo simile. I valori della cella derivati per i membri calcolati, tuttavia, vengono basati completamente sull'espressione MDX (Multidimensional Expressions) utilizzata per definire il membro calcolato. In alcuni casi, ciò potrebbe non interessare alcun dato effettivo delle celle. Per ulteriori informazioni, vedere [operatori di Rollup personalizzati nelle dimensioni padre-figlio](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md), [definire formule personalizzate](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md), e [calcoli](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
## <a name="empty-cells"></a>Celle vuote  
 Non è necessario che tutte le celle di un cubo contengano un valore. In un cubo possono esistere intersezioni prive di dati, che vengono chiamate celle vuote. Questo tipo di celle è frequente nei cubi, dato che non tutte le intersezioni degli attributi delle dimensioni con una misura contengono un record corrispondente nella tabella dei fatti. Il rapporto tra le celle vuote in un cubo per il numero totale di celle in un cubo viene spesso definito il *densità* di un cubo.  
  
 Ad esempio, la struttura del cubo visualizzata nel diagramma seguente è simile a quella degli altri esempi presentati in questo argomento. Tuttavia, in questo esempio, non vi sono spedizioni aree per l'Africa nel terzo trimestre o per l'Australia nel quarto trimestre. Nella tabella dei fatti non sono presenti dati che supportano le intersezioni di queste dimensioni e misure e pertanto le celle corrispondenti a queste intersezioni sono vuote.  
  
 ![Diagramma del cubo che identifica le celle vuote](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro7.gif "diagramma del cubo che identifica le celle vuote")  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una cella vuota è una cella con qualità speciali. Dato che le celle vuote possono distorcere i risultati di cross join, conteggi e così via, molte funzioni MDX consentono di ignorare le celle vuote a scopo di calcolo. Per ulteriori informazioni, vedere [espressioni multidimensionali &#40; MDX &#41; Riferimento](../../mdx/multidimensional-expressions-mdx-reference.md), e [i concetti chiave per MDX &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>Sicurezza  
 L'accesso ai dati delle celle viene gestito in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a livello di ruolo e può essere controllato con efficacia utilizzando espressioni MDX. Per ulteriori informazioni, vedere [concedere l'accesso personalizzato alla dimensione dei dati &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md), e [concedere l'accesso personalizzato a una cella di dati &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Archiviazione dei cubi &#40; Analysis Services - dati multidimensionali &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [Le aggregazioni e progettazione di aggregazioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
