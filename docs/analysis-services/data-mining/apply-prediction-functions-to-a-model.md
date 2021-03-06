---
title: Applicare funzioni di stima a un modello | Documenti Microsoft
ms.custom: ''
ms.date: 03/02/2016
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
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ea29a1f9406014bf684d4c573ed2640bb7d0cf96
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="apply-prediction-functions-to-a-model"></a>Applicare le funzioni di stima a un modello
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Per creare una query di stima in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining, è innanzitutto necessario selezionare il modello di data mining su cui basare la query. È possibile selezionare qualsiasi modello di data mining esistente nel progetto corrente.  
  
 Dopo avere selezionato un modello, aggiungere una *funzione di stima* alla query. Una funzione di stima può essere usata per ottenere una stima, ma è anche possibile aggiungere funzioni di stima che restituiscono le statistiche correlate, come la probabilità del valore stimato, o le informazioni usate per generare la stima.  
  
 Le funzioni di stima possono restituire i tipi seguenti di valori:  
  
-   Nome dell'attributo di stima e valore che viene stimato.  
  
-   Statistiche sulla distribuzione e varianza dei valori stimati.  
  
-   Probabilità di un risultato specificato o di tutti i possibili risultati.  
  
-   Punteggi superiori o inferiori o valori.  
  
-   Valori associati a un nodo, un oggetto o un attributo specificato.  
  
 I tipi delle funzioni di stima disponibili dipendono dal tipo di modello di data mining usato. Ad esempio, le funzioni di stima applicate a modelli di albero delle decisioni possono restituire regole e descrizioni di nodo, mentre le funzioni di stima per modelli Time Series possono restituire l'intervallo e altre informazioni specifiche delle serie temporali.  
  
 Per un elenco delle funzioni di stima supportate per quasi tutti i tipi di modello, vedere [Funzioni di stima generali &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md).  
  
 Per alcuni esempi di come eseguire una query su un tipo specifico di modello di data mining, vedere l'argomento di riferimento sugli algoritmi in [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>Scegliere un modello di data mining da utilizzare per la stima  
  
1.  Da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul modello e scegliere **Compila query di stima**.  
  
     -oppure-  
  
     In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sulla scheda **Stima modello di data mining**e quindi scegliere **Seleziona modello** nella tabella  **Modello di data mining** .  
  
2.  Nella finestra di dialogo **Seleziona modello di data mining** selezionare un modello di data mining e quindi fare clic su **OK**.  
  
     È possibile scegliere qualsiasi modello all'interno del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] corrente. Per creare una query utilizzando un modello in un database diverso, è necessario aprire una nuova finestra Query nel contesto di quel database oppure aprire il file della soluzione che contiene tale modello.  
  
### <a name="add-prediction-functions-to-a-query"></a>Aggiungere funzioni di stima a una query  
  
1.  In **Generatore delle query di stima**configurare i dati di input usati per la stima, specificando i valori nella finestra di dialogo **Input query singleton** o eseguendo il mapping del modello a un'origine dati esterna.  
  
     Per altre informazioni, vedere [Scegliere ed eseguire il mapping di dati di input per una query di stima](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md).  
  
    > [!WARNING]  
    >  Non è necessario fornire input per generare stime. In assenza di input, l'algoritmo restituisce in genere il valore stimato più probabile attraverso tutti i possibili input.  
  
2.  Fare clic sulla colonna **Origine** e scegliere un valore nell'elenco:  
  
    |||  
    |-|-|  
    |**\<Nome modello >**|Selezionare questa opzione per includere i valori del modello di data mining nell'output. È possibile aggiungere unicamente colonne stimabili.<br /><br /> Quando si aggiunge una colonna dal modello, il risultato restituito è l'elenco non distinto di valori in quella colonna.<br /><br /> Le colonne che si aggiungono tramite questa opzione sono incluse nella parte SELECT dell'istruzione DMX risultante.|  
    |**Prediction Function**|Selezionare questa opzione per esplorare un elenco di funzioni di stima.<br /><br /> I valori o le funzioni selezionate vengono aggiunte alla parte SELECT dell'istruzione DMX risultante.<br /><br /> L'elenco di funzioni di stima non è filtrato o vincolato dal tipo di modello selezionato. Pertanto, se non si sa con sicurezza se la funzione è supportata per il tipo di modello corrente, è possibile aggiungerla all'elenco e assicurarsi che non si verifichi alcun errore.<br /><br /> Gli elementi dell'elenco preceduti da $ (ad esempio, $AdjustedProbability) rappresentano le colonne della tabella annidata restituita quando si usa la funzione **PredictHistogram**. Si tratta di collegamenti che è possibile utilizzare per restituire una singola colonna e non una tabella nidificata.|  
    |**Espressione personalizzata**|Selezionare questa opzione per digitare un'espressione personalizzata e quindi assegnare un alias all'output.<br /><br /> L'espressione personalizzata viene aggiunta alla parte SELECT della query di stima DMX risultante.<br /><br /> Questa opzione è utile se si desidera aggiungere del testo per l'output con ogni riga, per chiamare funzioni VB o stored procedure personalizzate.<br /><br /> Per informazioni sull'uso di funzioni VBA e di Excel da DMX, vedere [Funzioni VBA in MDX e DAX](../../mdx/vba-functions-in-mdx-and-dax.md).|  
  
3.  Dopo avere aggiunto ogni funzione o espressione, passare alla vista DMX per vedere come la funzione viene aggiunta all'interno dell'istruzione DMX.  
  
    > [!WARNING]  
    >  Il Generatore delle query di stima non convalida l'istruzione DMX finché non si fa clic su **Risultati**. Spesso, l'espressione che viene prodotta dal generatore di query non è una DMX valida. Le cause tipiche sono una colonna che non è correlata alla colonna stimabile o il tentativo di stimare una colonna in una tabella nidificata che richiede un'istruzione sub-SELECT. A questo punto, è possibile passare a vista DMX e continuare a modificare l'istruzione.  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>Esempio: creare una query in un modello di clustering  
  
1.  Se non è disponibile un modello di clustering per la generazione di questa query di esempio, creare il modello [TM_Clustering] facendo riferimento a [Esercitazione di base sul data mining](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
2.  Da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul modello [TM_Clustering] e scegliere **Compila query di stima**.  
  
3.  Scegliere **Query singleton** dal menu **Modello di data mining**.  
  
4.  Nella finestra di dialogo **Input query singleton** impostare i valori seguenti come input:  
  
    -   Gender = M  
  
    -   Commute Distance = 5-10 miles  
  
5.  Nella griglia della query per **Origine**selezionare il modello di data mining TM_Clustering e aggiungere la colonna [Bike Buyer].  
  
6.  Per **Origine**selezionare **Funzione di stima**e quindi aggiungere la funzione **Cluster**.  
  
7.  Per **Origine**selezionare **Funzione di stima**, aggiungere la funzione **PredictSupport**e trascinare la colonna [Bike Buyer] del modello nella casella **Criteri/Argomento** . Digitare **Supporto** nella colonna **Alias** .  
  
     Copiare l'espressione che rappresenta la funzione di stima e il riferimento alla colonna dalla casella **Criteri/Argomento** .  
  
8.  Per **Origine**selezionare **Espressione personalizzata**, digitare un alias e quindi fare riferimento alla funzione CEILING di Excel usando la sintassi seguente:  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     Incollare il riferimento alla colonna come argomento alla funzione.  
  
     Ad esempio, l'espressione seguente restituisce il valore CEILING del valore di supporto:  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     Digitare CEILING nella colonna **Alias** .  
  
9. Fare clic su **Passa alla visualizzazione del testo della query** per esaminare l'istruzione DMX generata e quindi fare clic su **Passa alla visualizzazione dei risultati della query** per visualizzare l'output delle colonne restituito dalla query di stima.  
  
     Nella tabella seguente vengono illustrati i risultati previsti:  
  
    |Bike Buyer|$Cluster|Supporto|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|Cluster 8|954|953.948638926372|  
  
 Se si desidera aggiungere altre clausole nell'istruzione, ad esempio una clausola WHERE, non è possibile aggiungerle tramite la griglia, ma è necessario passare prima alla vista DMX.  
  
## <a name="see-also"></a>Vedere anche  
 [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
