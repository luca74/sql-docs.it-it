---
title: StructureColumn (DMX) | Documenti Microsoft
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
- StructureColumn
dev_langs:
- DMX
helpviewer_keywords:
- StructureColumn function
ms.assetid: 57557536-4bfa-4fa7-bf7a-fb8722ca200d
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 24b7869462815e6d636572a093a332ecce6dc02c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il valore della colonna della struttura corrispondente al case specificato oppure il valore di tabella relativo a una tabella nidificata nel case specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>Argomenti  
 nome-colonna-struttura.  
 Nome della colonna della struttura di data mining di un case o di una tabella nidificata.  
  
## <a name="result-type"></a>Tipo di risultato  
 Il tipo restituito dipende dal tipo della colonna a cui fa riferimento il \<nome colonna della struttura > parametro. Ad esempio, se la colonna della struttura di data mining a cui viene fatto riferimento contiene un valore scalare, la funzione restituisce un valore scalare.  
  
 Se la colonna della struttura di data mining alla quale viene fatto riferimento è una tabella nidificata, la funzione restituisce un valore di tabella. Il valore di tabella restituito può essere utilizzato nella clausola FROM di un'istruzione sub-SELECT.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione è polimorfica e può essere utilizzata in qualunque posizione in un'istruzione che consente espressioni, comprese un elenco di espressioni SELECT, un'espressione di condizione WHERE e un'espressione ORDER BY.  
  
 Il nome della colonna nella struttura di data mining è un valore stringa e di conseguenza deve essere racchiuso tra virgolette singole: ad esempio, `StructureColumn('` **colonna 1**`')`. Nel caso in cui siano presenti più colonne con lo stesso nome, il nome è risolto nel contesto dell'istruzione SELECT che lo racchiude.  
  
 I risultati restituiti da una query tramite il **StructureColumn** funzione sono interessate dalla presenza di eventuali filtri nel modello. ovvero il filtro del modello controlla i case inclusi nel modello di data mining. Una query nella colonna della struttura può pertanto restituire solo i case utilizzati nel modello di data mining. Per un esempio di codice che illustra l'effetto dei filtri del modello di data mining sia in tabelle del case che in tabelle nidificate, vedere la sezione Esempi di questo argomento.  
  
 Per ulteriori informazioni su come usare questa funzione in un'istruzione DMX SELECT, vedere [modello SELECT FROM &#60; &#62;. DMX casi &#40; &#41; ](../dmx/select-from-model-cases-dmx.md) o [struttura SELECT FROM &#60; &#62;. CASI](../dmx/select-from-structure-cases.md).  
  
## <a name="error-messages"></a>messaggi di errore  
 Se l'utente non dispone di autorizzazioni drill-through sulla struttura di data mining padre, viene generato l'errore di sicurezza seguente:  
  
 L'utente '%{user/} non dispone dell'autorizzazione per eseguire il drill-through nella struttura di data mining padre del modello di data mining '%{model/}'.  
  
 Se il nome della colonna della struttura specificato non è valido, viene generato il messaggio di errore seguente:  
  
 Impossibile trovare la colonna della struttura di data mining '%{structure-column-name/}' nella struttura di data mining padre '%{structure/}' del contesto corrente (riga %{line/}, colonna %{column/}).  
  
## <a name="examples"></a>Esempi  
 Per questi esempi sarà utilizzata la struttura di data mining riportata di seguito. Si noti che la struttura di data mining contiene due colonne di tabelle nidificate, `Products` e `Hobbies`. La tabella nidificata nella colonna `Hobbies` contiene una singola colonna che viene utilizzata come chiave per la tabella nidificata. La tabella nidificata nella colonna `Products` è una tabella nidificata complessa con una colonna chiave e altre colonne utilizzate per l'input. Negli esempi seguenti viene illustrato come progettare una struttura di data mining per includere colonne diverse, anche se un modello potrebbe non utilizzare tutte le colonne. Alcune di queste colonne potrebbero non essere utili a livello di modello per la generalizzazione dei modelli, ma rivelarsi molto indicate per il drill-through.  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 Creare quindi un modello di data mining basato sulla struttura appena creata utilizzando il codice di esempio seguente:  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>Esempio di query 1: Restituzione di una colonna dalla struttura di data mining  
 Nella query di esempio seguente vengono restituite le colonne `CustomerName` e `Age`, definite come parte del modello di data mining. Tuttavia la query restituisce anche la colonna `Age`, che fa parte della struttura ma non è inclusa nel modello di data mining.  
  
```  
SELECT CustomerName, Age, StructureColumn(‘Occupation’) FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 Si noti che per limitare i case ai clienti di età superiore ai 30 anni il filtro delle righe viene applicato a livello del modello. Pertanto, questa espressione non restituisce case inclusi nei dati della struttura ma non utilizzati dal modello. Poiché la condizione di filtro utilizzata per creare il modello, `EXISTS (Products)`, limita i case solo ai clienti che hanno acquistato prodotti, nella struttura ci potrebbero essere case che non vengono restituiti dalla query.  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>Esempio di query 2: Applicazione di un filtro alla colonna della struttura  
 Nella query di esempio seguente, oltre alle colonne del modello `CustomerName` e `Age` e alla tabella nidificata `Products`, viene restituito il valore della colonna `Quantity` nella tabella nidificata che non fa parte del modello.  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn(‘Quantity’) FROM Products) FROM MA.CASES   
WHERE StructureColumn(‘Occupation’) = ‘Architect’  
```  
  
 Si noti che, in questo esempio viene applicato un filtro alla colonna della struttura per limitare i case ai clienti con occupazione 'Architect' (`WHERE StructureColumn(‘Occupation’) = ‘Architect’`). Poiché la condizione di filtro del modello viene sempre applicata ai case al momento della creazione del modello, vengono inclusi nei case del modello solo i case con almeno una riga risultante nella tabella `Products`. Vengono pertanto applicati sia il filtro sulla tabella nidificata `Products` che il filtro sul case `(‘Occupation’)`.  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>Esempio di query 3: Selezione di colonne da una tabella nidificata  
 Nella query di esempio seguente vengono restituiti i nomi dei clienti che sono stati utilizzati come case di training dal modello. Per ogni cliente, la query restituisce anche una tabella nidificata contenente i dettagli dell'acquisto. Sebbene il modello include il `ProductName` colonna, il modello non utilizza il valore di `ProductName` colonna. Il modello controlla solo se il prodotto è stato acquistato al normale (`NOT``OnSale`) prezzo. Questa query non solo restituisce il nome del prodotto, ma anche la quantità acquistata che non è inclusa nel modello.  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 Si noti che non è possibile restituire la colonna `ProductName` o `Quantity` se non è attivato il drill-through nel modello di data mining.  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>Esempio di query 4: Applicazione di filtri e restituzione di colonne di tabella nidificata  
 Nella query di esempio seguente vengono restituite le colonne della tabella nidificata e del case incluse nella struttura di data mining ma non nel modello. Sul modello è già applicato un filtro relativo alla presenza di prodotti `OnSale`, ma questa query aggiunge un filtro nella colonna della struttura di data mining, `Quantity`:  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Data Mining Extensions &#40; DMX &#41; Riferimento (funzione)](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX funzioni &#40; &#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
