---
title: PredictTimeSeries (DMX) | Documenti Microsoft
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
ms.topic: language-reference
f1_keywords:
- PredictTimeSeries
dev_langs:
- DMX
helpviewer_keywords:
- time series algorithms [Analysis Services]
- time series [Analysis Services]
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- PredictTimeSeries function
ms.assetid: 85c596be-a7f4-499b-8d36-7e67c2647b6c
caps.latest.revision: 56
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b1b631ab035bf4c444aa1c6b449eaa87e3305c91
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce i valori futuri stimati per una serie temporale. I dati di una serie temporale sono continui e possono essere archiviati in una tabella nidificata o di case. Il **PredictTimeSeries** funzione restituisce sempre una tabella nidificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>Argomenti  
 *\<tabella di riferimento di colonna >*,  *\<colonna scalare perchè >*  
 Specifica il nome della colonna da stimare. La colonna può contenere dati scalari o tabulari.  
  
 *n*  
 Specifica il numero dei prossimi passaggi da stimare. Se non è stato specificato un valore per  *n* , il valore predefinito è 1.  
  
 *n*non può essere 0. La funzione restituisce un errore se non viene indicata almeno una stima.  
  
 *avvio di n, n-end*  
 Specifica un intervallo di passaggi della serie temporale.  
  
 *n-inizio* deve essere un numero intero e non può essere 0.  
  
 *n-end* deve essere un numero intero maggiore di *n-inizio*.  
  
 *\<query di origine >*  
 Definisce i dati esterni utilizzati per l'esecuzione di stime.  
  
 REPLACE_MODEL_CASES | EXTEND_MODEL_CASES  
 Indica come gestire i nuovi dati.  
  
 REPLACE_MODEL_CASES specifica che i punti dati nel modello devono essere sostituiti con i nuovi dati. Tuttavia, le stime sono basate sugli schemi nel modello di data mining esistente.  
  
 EXTEND_MODEL_CASES specifica che i nuovi dati devono essere aggiunti al set di dati di training originale. Stime future vengono eseguite sul set di dati composto solo dopo che i nuovi dati sono stati utilizzati.  
  
 È possibile utilizzare questi argomenti solo quando i dati nuovi sono aggiunti mediante un'istruzione PREDICTION JOIN. Se si utilizza una query PREDICTION JOIN e non si specifica un argomento, l'impostazione predefinita è EXTEND_MODEL_CASES.  
  
## <a name="return-type"></a>Tipo restituito  
 Oggetto \< *espressione di tabella*>.  
  
## <a name="remarks"></a>Osservazioni  
 L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series non supporta la stima cronologica quando i dati nuovi sono aggiunti mediante l'istruzione PREDICTION JOIN.  
  
 In un'istruzione PREDICTION JOIN, il processo di stima inizia sempre immediatamente dopo la fine della serie di training originale anche se si aggiungono dati nuovi. Pertanto, il  *n*  parametro e *n-inizio* i valori dei parametri devono essere un numero intero maggiore di 0.  
  
> [!NOTE]  
>  La lunghezza dei dati nuovi non influisce sul punto iniziale di stima. Pertanto, per aggiungere dati nuovi ed eseguire anche stime nuove, accertarsi di impostare il punto di inizio della stima su un valore maggiore della lunghezza dei dati nuovi oppure estendere il punto finale della stima in base alla lunghezza dei dati nuovi.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come eseguire stime in base a un modello Time Series esistente:  
  
-   Nel primo esempio è illustrato come eseguire un numero specifico di stime in base al modello corrente.  
  
-   Nel secondo esempio viene mostrato come utilizzare il parametro REPLACE_MODEL_CASES per applicare gli schemi nel modello specificato a un nuovo set di dati.  
  
-   Nel terzo esempio è illustrato come utilizzare il parametro EXTEND_MODEL_CASES per aggiornare un modello di data mining con nuovi dati.  
  
 Per ulteriori informazioni sull'utilizzo di modelli time series, vedere l'esercitazione di data mining, [lezione 2: compilazione di uno Scenario di previsione &#40; esercitazione intermedia sul Data Mining &#41;](http://msdn.microsoft.com/library/9a988156-c900-4c22-97fa-f6b0c1aea9e2) e [esercitazione su DMX stima serie tempo](http://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
> [!NOTE]  
>  È possibile che vengano restituiti risultati diversi dal modello utilizzato. I risultati degli esempi seguenti sono forniti solo per illustrare il formato del risultato.  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>Esempio 1: Stima di un numero di intervalli di tempo  
 L'esempio seguente usa il **PredictTimeSeries** funzione per restituire una stima per i prossimi tre intervalli temporali e limita i risultati per la serie M200 nelle aree Europa e Pacifico. In questo modello specifico, l'attributo stimabile è Quantity, pertanto è necessario utilizzare `[Quantity]` come primo argomento alla funzione PredictTimeSeries.  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 Risultati previsti:  
  
|Model Region|t.$TIME|t.Quantity|  
|------------------|-------------|----------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|  
|M200 Europe|8/25/2008 12:00:00 AM|142|  
|M200 Europe|9/25/2008 12:00:00 AM|152|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 In questo esempio è stata utilizzata la parola chiave FLATTENED per rendere più semplice la lettura dei risultati.  Se non si utilizza la parola chiave FLATTENED e viene restituito invece un set di righe gerarchico, questa query restituisce due colonne. La prima colonna contiene il valore per [ModelRegion] e la seconda colonna contiene una tabella nidificata con due colonne: $TIME, che mostra gli intervalli di tempo stimati e Quantity, che contiene i valori stimati.  
  
### <a name="example-2-adding-new-data-and-using-replacemodelcases"></a>Esempio 2: Aggiunta di dati nuovi e utilizzo di REPLACE_MODEL_CASES  
 Si supponga di trovare dati non corretti per una particolare area e di voler utilizzare gli schemi nel modello per modificare le stime in modo che riflettano i nuovi dati. In alternativa, si potrebbe scoprire che un'altra area dispone di tendenze più affidabili e desiderare di applicare il modello più affidabile ai dati da un'area diversa.  
  
 In questo scenario, è possibile utilizzare il parametro REPLACE_MODEL_CASES e specificare un nuovo set di dati da impiegare come dati della cronologia. In tal modo, le proiezioni saranno basate sugli schemi nel modello specificato, ma continueranno uniformemente dalla fine dei nuovi punti dati. Per una descrizione completa di questo scenario, vedere [avanzate stime basate su serie temporali &#40; esercitazione intermedia sul Data Mining Data &#41;](http://msdn.microsoft.com/library/b614ebdb-07ca-44af-a0ff-893364bd4b71).  
  
 Nella seguente query PREDICTION JOIN è illustrata la sintassi per la sostituzione di dati e l'esecuzione delle nuove stime. Per i dati della sostituzione, l'esempio recupera il valore delle colonne Amount e Quantity e moltiplica ogni valore per due:  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 Le tabelle seguenti confrontano i risultati della stima.  
  
 Stime originali:  
  
||||  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 Stime aggiornate:  
  
||||  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|91|  
|M200 Pacific|8/25/2008 12:00:00 AM|89|  
|M200 Pacific|9/25/2008 12:00:00 AM|84|  
  
### <a name="example-3-adding-new-data-and-using-extendmodelcases"></a>Esempio 3: Aggiunta di dati nuovi e utilizzo di EXTEND_MODEL_CASES  
 Esempio 3 viene illustrato l'utilizzo del *EXTEND_MODEL_CASES* opzione per fornire nuovi dati, che viene aggiunto alla fine di una serie di dati esistente. Anziché sostituire i punti dati esistenti, i nuovi dati vengono aggiunti nel modello.  
  
 Nell'esempio seguente, i nuovi dati vengono forniti nell'istruzione SELECT che segue NATURAL PREDICTION JOIN. È possibile fornire più righe di nuovo input con questa sintassi, ma ogni nuova riga di input deve disporre di un timestamp univoco:  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 Poiché la query utilizza la *EXTEND_MODEL_CASES* opzione [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esegue le azioni seguenti per le stime:  
  
-   Aumenta la dimensione totale dei case di training aggiungendo i due nuovi mesi di dati al modello.  
  
-   Avvia le stime alla fine dei dati del case precedenti. Pertanto, le prime due stime rappresentano i nuovi dati di vendita effettivi che sono stati appena aggiunti al modello.  
  
-   Restituisce stime nuove per i tre intervalli di tempo rimanenti in base al modello appena espanso.  
  
 Nella tabella seguente sono elencati i risultati della query dell'esempio 2. Notare che i primi due valori restituiti per M200 Europa corrispondono esattamente ai nuovi valori forniti. Questo comportamento avviene per motivi strutturali. Per avviare stime dopo la fine dei nuovi dati, è necessario specificare intervallo temporale di inizio e di fine. Per un esempio di come eseguire questa operazione, vedere [lezione 5: estendere il modello Time Series](http://msdn.microsoft.com/library/7aad4946-c903-4e25-88b9-b087c20cb67d).  
  
 Inoltre, notare che non sono stati forniti i nuovi dati per l'area Pacifico. Pertanto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restituisce nuove stime per tutti e cinque gli intervalli di tempo,  
  
 Quantità: M200 Europe. EXTEND_MODEL_CASES:  
  
|$TIME|Quantity|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 Quantità: M200 Pacific. EXTEND_MODEL_CASES:  
  
|$TIME|Quantity|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>Esempio 4: Restituzione di statistiche in una stima basata su serie temporali  
 Il **PredictTimeSeries** funzione non supporta *INCLUDE_STATISTICS* come parametro. Tuttavia, è possibile utilizzare la query seguente per visualizzare le statistiche di stima relative a una query di serie temporale. Questo approccio può essere utilizzato anche nel caso di modelli con colonne della tabella nidificate.  
  
 In questo modello specifico, l'attributo stimabile è Quantity, pertanto è necessario utilizzare `[Quantity]` come primo argomento alla funzione PredictTimeSeries. Se nel modello viene utilizzato un attributo stimabile diverso, è possibile sostituire un nome della colonna diverso.  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 Risultati dell'esempio:  
  
|Model Region|t.$TIME|t.PREDICTION|t.VARIANCE|t.STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|11.6050581415597|3.40661975300439|  
|M200 Europe|8/25/2008 12:00:00 AM|142|10.678201866621|3.26775180615374|  
|M200 Europe|9/25/2008 12:00:00 AM|152|9.86897842568614|3.14149302493037|  
|M200 North America|7/25/2008 12:00:00 AM|163|1.20434529288162|1.20434529288162|  
|M200 North America|8/25/2008 12:00:00 AM|178|1.65031343900634|1.65031343900634|  
|M200 North America|9/25/2008 12:00:00 AM|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  In questo esempio è stata utilizzata la parola chiave FLATTENED per rendere più semplice la presentazione dei risultati in una tabella. Tuttavia, se il provider supporta i set di righe gerarchici, è possibile omettere la parola chiave FLATTENED. Se si omette la parola chiave FLATTENED, la query restituisce due colonne, la prima colonna contenente il valore che identifica la serie di dati `[Model Region]` e la seconda colonna contenente la tabella di statistiche nidificata.  
  
## <a name="see-also"></a>Vedere anche  
 [Data Mining Extensions &#40; DMX &#41; Riferimento (funzione)](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Tempo Series Model Query Examples](../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Stimare &#40; DMX &#41;](../dmx/predict-dmx.md)  
  
  
