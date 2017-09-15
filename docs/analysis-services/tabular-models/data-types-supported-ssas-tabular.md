---
title: Tipi di dati supportati (SSAS tabulare) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a60cc3c2782abed53a8064f80bcdbe01921826cc
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="data-types-supported-ssas-tabular"></a>Tipi di dati supportati (SSAS tabulare)
  In questo articolo vengono descritti i tipi di dati che possono essere utilizzati nei modelli tabulari e viene illustrata la conversione implicita dei tipi di dati quando i dati vengono calcolati o utilizzati in una formula DAX (Data Analysis Expressions).  
  
 In questo articolo sono contenute le sezioni seguenti:  
  
-   [Tipi di dati utilizzati nei modelli tabulari](#bkmk_data_types)  
  
-   [Conversione implicita ed esplicita del tipo di dati nelle formule DAX](#bkmk_implicit)  
  
-   [Gestione di valori blank, stringhe vuote e valori zero](#bkmk_hand_blanks)  
  
##  <a name="bkmk_data_types"></a> Tipi di dati utilizzati nei modelli tabulari  
 Sono supportati i tipi di dati indicati di seguito. Quando si importano i dati o si utilizza un valore in una formula, anche se nell'origine dati originale è contenuto un tipo di dati diverso, viene eseguita la conversione dei dati in uno dei tipi seguenti. Anche per i valori risultanti dalle formule vengono utilizzati questi tipi di dati.  
  
 In generale, questi tipi di dati vengono implementati per consentire l'esecuzione di calcoli accurati nelle colonne calcolate e le stesse restrizioni si applicano al resto dei dati nei modelli per garantire coerenza.  
  
 I formati utilizzati per i numeri, la valuta, le date e le ore devono seguire il formato delle impostazioni locali specificato nel client in uso per l'utilizzo dei dati del modello. È possibile utilizzare le opzioni di formattazione nel modello per controllare la modalità di visualizzazione del valore.  
  
||||  
|-|-|-|  
|**Tipo di dati nel modello**|**Tipi di dati in DAX**|**Description**|  
|Numero intero|Valore intero a 64 bit (otto byte)*<br /><br /> Nota:<br />         Le formule DAX non supportano i tipi di dati troppo piccoli per contenere il valore minimo indicato nella descrizione.|Numeri senza cifre decimali. I numeri interi possono essere positivi o negativi ma devono essere numeri interi compresi tra -9.223.372.036.854.775.808 (-2^63) e 9.223.372.036.854.775.807 (2^63-1).|  
|Numero decimale|Numero reale a 64 bit (otto byte)*<br /><br /> Nota:<br />         Le formule DAX non supportano i tipi di dati troppo piccoli per contenere il valore minimo indicato nella descrizione.|I numeri reali sono numeri che possono avere cifre decimali e coprono un ampio intervallo di valori:<br /><br /> Valori negativi compresi tra -1,79E +308 e -2,23E -308<br /><br /> Zero<br /><br /> Valori positivi compresi tra 2,23E -308 e 1,79E + 308<br /><br /> Tuttavia, il numero di cifre significative è limitato a 17 cifre decimali.|  
|Boolean|Boolean|Valore True o False.|  
|Text|String|Stringa di dati di tipo carattere Unicode. Può trattarsi di stringhe, numeri o date rappresentati in un formato di testo.|  
|Data|Date/time|Date e ore in una rappresentazione di data e ora valida.<br /><br /> Le date valide sono tutte le date successive al 1 marzo del 1900.|  
|Currency|Currency|Il tipo di dati currency consente valori compresi tra -922.337.203.685.477,5808 e 922.337.203.685.477,5807 con quattro cifre decimali di precisione fissa.|  
|N/D|Vuoto|Un tipo di dati blank in DAX rappresenta e sostituisce i valori Null di SQL. È possibile creare un tipo di dati blank utilizzando la funzione BLANK, nonché verificare la presenza di tipi di dati blank utilizzando la funzione logica ISBLANK.|  
  
 \* Se si prova a importare dati con valori numerici molto grandi, l'importazione potrebbe non riuscire con l'errore seguente:  
  
 Errore di database in memoria: il '\<nome colonna >' colonna del '\<nome tabella >' tabella contiene un valore, ' 1.7976931348623157 e + 308' che non è supportata. L'operazione è stata annullata.  
  
 Questo errore si verifica perché in Progettazione modelli viene utilizzato questo valore per rappresentare valori Null. I valori nell'elenco seguente sono sinonimi del già menzionato valore Null:  
  
||  
|-|  
|Valore|  
|9223372036854775807|  
|-9223372036854775808|  
|1,7976931348623158e+308|  
|2,2250738585072014e-308|  
  
 È necessario rimuovere il valore dai dati e ritentare l'importazione.  
  
> [!NOTE]  
>  Non è possibile importare da una colonna **varchar(max)** con una lunghezza di stringa superiore a 131.072 caratteri.  
  
### <a name="table-data-type"></a>Tipo di dati tabella  
 In DAX viene inoltre usato un tipo di dati *table* . Questo tipo di dati viene utilizzato da DAX in numerose funzioni, ad esempio aggregazioni e calcoli della funzionalità di Business Intelligence per le gerarchie temporali. Alcune funzioni richiedono un riferimento a una tabella e altre restituiscono una tabella che può quindi essere utilizzata come input per altre funzioni. In alcune funzioni che richiedono una tabella come input è possibile specificare un'espressione che restituisce una tabella. Per alcune funzioni è necessario un riferimento a una tabella di base. Per informazioni sui requisiti di funzioni specifiche, vedere [Riferimento alle funzioni DAX](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
##  <a name="bkmk_implicit"></a> Conversione implicita ed esplicita del tipo di dati nelle formule DAX
  
 Ogni funzione DAX prevede requisiti specifici relativi ai tipi di dati utilizzati come input e output. Alcune funzioni, ad esempio, richiedono numeri interi per determinati argomenti e date per altri. Altre funzioni richiedono testo o tabelle.  
  
 Se i dati nella colonna specificata come argomento non sono compatibili con il tipo di dati richiesto dalla funzione, in molti casi in DAX viene restituito un errore. Quando possibile, tuttavia, in DAX viene eseguito un tentativo di conversione implicita dei dati nel tipo di dati richiesto. Esempio:  
  
-   È possibile digitare un numero, ad esempio "123", come stringa. Tramite DAX la stringa verrà analizzata e si tenterà di specificarla come tipo di dati numerico.  
  
-   È possibile aggiungere TRUE + 1 e ottenere il risultato 2, in quanto TRUE viene convertito in modo implicito nel numero 1 e viene eseguita l'operazione 1+1.  
  
-   Se si aggiungono valori in due colonne e un valore è rappresentato come testo ("12"), mentre l'altro come numero (12), in DAX la stringa viene convertita in modo implicito in un numero e quindi viene eseguita la somma per ottenere un risultato numerico. L'espressione seguente restituisce 44: = "22" + 22  
  
-   Se si tenta di concatenare due numeri, questi verranno visualizzati come stringhe e quindi concatenati dal componente aggiuntivo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . L'espressione seguente restituisce "1234": = 12 & 34  
  
 Nella tabella seguente vengono riepilogate le conversioni implicite dei tipi di dati eseguite nelle formule. In generale, il comportamento della progettazione dei modelli semantici è analogo a quello di Microsoft Excel, in quanto vengono eseguite conversioni implicite ogni volta che è possibile, quando necessario per l'operazione specificata.  
  
### <a name="table-of-implicit-data-conversions"></a>Tabella delle conversioni implicite dei dati  
 Il tipo di conversione eseguito è determinato dall'operatore, che esegue il cast dei valori necessari prima di eseguire l'operazione richiesta. In queste tabelle sono elencati gli operatori e viene indicata la conversione eseguita per ogni tipo di dati nella colonna quando viene abbinato con il tipo di dati nella riga con cui avviene l'intersezione.  
  
> [!NOTE]  
>  I tipi di dati di testo non sono inclusi in queste tabelle. Quando un numero viene rappresentato in un formato di testo, in alcuni casi, tramite Progettazione modelli viene eseguito un tentativo di determinare il tipo di numero e rappresentarlo come numero.  
  
#### <a name="addition-"></a>Addizione (+)  
  
||||||  
|-|-|-|-|-|  
|Operatore (+)|INTEGER|Currency|REAL|Date/time|  
|INTEGER|INTEGER|Currency|REAL|Date/time|  
|Currency|Currency|Currency|REAL|Date/time|  
|REAL|REAL|REAL|REAL|Date/time|  
|Date/time|Date/time|Date/time|Date/time|Date/time|  
  
 Se, ad esempio, in un'operazione di addizione viene utilizzato un numero reale in combinazione con dati di valuta, entrambi i valori vengono convertiti nel tipo REAL e il risultato viene restituito come tipo REAL.  
  
#### <a name="subtraction--"></a>Sottrazione (-)  
 Nella tabella seguente l'intestazione di riga rappresenta il minuendo (lato sinistro) mentre l'intestazione di colonna il sottraendo (lato destro).  
  
||||||  
|-|-|-|-|-|  
|Operatore (-)|INTEGER|Currency|REAL|Date/time|  
|INTEGER|INTEGER|Currency|REAL|REAL|  
|Currency|Currency|Currency|REAL|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|Date/time|Date/time|Date/time|Date/time|Date/time|  
  
 Se, ad esempio, in un'operazione di sottrazione viene utilizzata una data con qualsiasi altro tipo di dati, entrambi i valori vengono convertiti in date e anche il valore restituito è una data.  
  
> [!NOTE]  
>  I modelli tabulari supportano inoltre l'operatore unario, - (segno negativo), ma questo operatore non consente di modificare il tipo di dati dell'operando.  
  
#### <a name="multiplication-"></a>Moltiplicazione (*)  
  
||||||  
|-|-|-|-|-|  
|Operatore (*)|INTEGER|Currency|REAL|Date/time|  
|INTEGER|INTEGER|Currency|REAL|INTEGER|  
|Currency|Currency|REAL|Currency|Currency|  
|REAL|REAL|Currency|REAL|REAL|  
  
 Se, ad esempio, un intero viene combinato con un numero reale in un'operazione di moltiplicazione, entrambi i numeri vengono convertiti in numeri reali e anche il valore restituito è di tipo REAL.  
  
#### <a name="division-"></a>Divisione (/)  
 Nella tabella seguente l'intestazione di riga rappresenta il numeratore mentre l'intestazione di colonna il denominatore.  
  
||||||  
|-|-|-|-|-|  
|Operatore (/)<br /><br /> (Riga/Colonna)|INTEGER|Currency|REAL|Date/time|  
|INTEGER|REAL|Currency|REAL|REAL|  
|Currency|Currency|REAL|Currency|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|Date/time|REAL|REAL|REAL|REAL|  
  
 Se, ad esempio, un intero viene combinato con un valore di valuta in un'operazione di divisione, entrambi i valori vengono convertiti in numeri reali e anche il risultato è un numero reale.  
  
#### <a name="comparison-operators"></a>Operatori di confronto  
È supportato solo un set limitato di combinazioni di tipo di dati misti per operazioni di confronto. Per altre informazioni, vedere [Guida di riferimento agli operatori DAX](https://msdn.microsoft.com/library/ee634237.aspx).  
  
## <a name="bkmk_hand_blanks"></a> Gestione di valori blank, stringhe vuote e valori zero  
 Nella tabella seguente vengono riepilogate le differenze tra DAX e Microsoft Excel per quanto riguarda la gestione dei valori blank.  
  
||||  
|-|-|-|  
|Espressione|DAX|Excel|  
|BLANK + BLANK|Vuoto|0 (zero)|  
|BLANK +5|5|5|  
|BLANK * 5|Vuoto|0 (zero)|  
|5/BLANK|Infinito|Errore|  
|0/BLANK|Non un numero (NaN, Not a Number)|Errore|  
|BLANK/BLANK|Vuoto|Errore|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|Vuoto|Errore|  
|BLANK AND BLANK|Vuoto|Errore|  
  
 Per informazioni dettagliate sulla gestione dei valori vuoti da parte di una funzione o un operatore specifico, vedere i singoli argomenti per ogni funzione DAX nella sezione [Riferimento alle funzioni DAX](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
## <a name="see-also"></a>Vedere anche  
 [Origini dati &#40;SSAS tabulare&#41;](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Importare dati &#40;SSAS tabulare&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  