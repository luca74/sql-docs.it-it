---
title: Gli operatori nelle espressioni (Generatore Report e SSRS) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 35e702d0d1944cd5e7f2b7120da07e272f30cf70
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>Operatori nelle espressioni (Generatore report e SSRS)
  Un operatore è un simbolo che rappresenta le azioni applicate a uno o più termini di un'espressione. In un'espressione sono supportate le categorie di operatori seguenti: aritmetico, di confronto, di concatenazione, logico o bit per bit e di scorrimento bit.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>Aritmetico  
 Gli operatori aritmetici eseguono operazioni matematiche su due termini numerici in un'espressione.  
  
|Operatore|Description|  
|--------------|-----------------|  
|^|Eleva un numero alla potenza di un altro numero.|  
|*|Moltiplica due numeri.|  
|/|Divide due numeri e restituisce un risultato a virgola mobile.|  
|\|Divide due numeri e restituisce un risultato intero.|  
|Mod|Restituisce il resto intero di una divisione, ad esempio 7 Mod 5 = 2 perché il resto di 7 diviso 5 è 2.|  
|+|Somma due numeri.|  
|-|Restituisce la differenza tra due numeri o indica il valore negativo di un termine numerico.|  
  
### <a name="comparison"></a>Confronto  
 Gli operatori di confronto consentono di confrontare due espressioni.  
  
|Operatore|Description|  
|--------------|-----------------|  
|<|Minore di.|  
|\<=|Minore o uguale a.|  
|>|Maggiore di.|  
|>=|Maggiore o uguale a.|  
|=|Uguale a.|  
|<>|Diverso da.|  
|Simile a|Determina se una stringa di caratteri specifica corrisponde a un modello specificato. Il modello può contenere caratteri specifici e caratteri jolly. In una ricerca in base a un modello i normali caratteri devono corrispondere esattamente ai caratteri specificati nella stringa di caratteri del modello. I caratteri jolly tuttavia possono venire abbinati a frammenti arbitrari della stringa. L'utilizzo di caratteri jolly rende l'operatore LIKE più flessibile rispetto all'utilizzo degli operatori di confronto tra stringhe = e !=.<br /><br /> Nella tabella seguente sono elencati i caratteri che è possibile utilizzare come caratteri jolly:<br /><br /> %: qualsiasi stringa composta da zero o più caratteri.<br /><br /> _: qualsiasi carattere singolo.<br /><br /> [ ]: qualsiasi carattere singolo compreso nell'intervallo ([a-f]) o nel set ([aeiou]) specificato.<br /><br /> [^]: qualsiasi carattere singolo non compreso nell'intervallo ([^a-f]) o nel set ([^aeiou]) specificato|  
|Is|Confronta due riferimenti a oggetti.|  
  
### <a name="string-concatenation"></a>Concatenazione di stringhe  
 La concatenazione di stringhe aggiunge la seconda stringa alla prima in un'espressione. Per le altre operazioni con stringhe, utilizzare le funzioni predefinite.  
  
|Operatore|Description|  
|--------------|-----------------|  
|&|Concatena due stringhe|  
|+|Concatena due stringhe|  
  
### <a name="logical-and-bitwise"></a>Logico e bit per bit  
 Gli operatori logici e bit per bit eseguono modifiche logiche tra due termini interi in un'espressione.  
  
|Operatore|Description|  
|--------------|-----------------|  
|And|Esegue una congiunzione logica di due espressioni booleane oppure una congiunzione bit per bit di due espressioni numeriche.|  
|Not|Esegue una negazione logica di un'espressione booleana oppure una negazione bit per bit di un'espressione numerica.|  
|Oppure|Esegue una disgiunzione logica di due espressioni booleane oppure una disgiunzione bit per bit di due valori numerici.|  
|Xor|Esegue un'operazione di esclusione logica di due espressioni booleane oppure un'esclusione bit per bit di due espressioni numeriche.|  
|AndAlso|Esegue una congiunzione logica di due espressioni.|  
|OrElse|Esegue una disgiunzione logica di due espressioni.|  
  
### <a name="bit-shift"></a>Scorrimento di bit  
 Gli operatori bit per bit eseguono modifiche di bit tra due termini interi in un'espressione.  
  
|Operatore|Description|  
|--------------|-----------------|  
|<\<|Esegue uno scorrimento a sinistra aritmetico a sinistra in un modello di bit.|  
|>>|Esegue uno scorrimento a destra aritmetico in un modello di bit.|  
  
## <a name="see-also"></a>Vedere anche  
 [La finestra di dialogo espressione](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Espressioni &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati in espressioni &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Nella finestra di dialogo Espressione &#40; Generatore report &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  