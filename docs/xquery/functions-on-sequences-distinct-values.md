---
title: Funzione DISTINCT-values (XQuery) | Documenti Microsoft
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4355506371dfbb5db0b6baea519d96ea5ddab6a9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-sequences---distinct-values"></a>Funzioni per le sequenze - valori distinct
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove valori duplicati dalla sequenza specificata da *$arg*. Se *$arg* è una sequenza vuota, la funzione restituisce una sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Sequenza di valori atomici.  
  
## <a name="remarks"></a>Osservazioni  
 Tutti i tipi di valori atomizzati passati a **DISTINCT** devono essere sottotipi dello stesso tipo di base. Tipi di base accettati sono i tipi che supportano il **eq** operazione. Tra questi tipi sono inclusi i tre tipi di base numerici predefiniti, ovvero i tipi di base di data/ora xs:string, xs:boolean e xdt:untypedAtomic. Per i valori di tipo xdt:untypedAtomic viene eseguito il cast a xs:string. In presenza di una combinazione di questi tipi o nel caso in cui vengano passati altri valori di altri tipi, viene restituito un errore statico.  
  
 Il risultato di **DISTINCT** riceve il tipo di base dei tipi passati, ad esempio xs: String nel caso di xdt: untypedAtomic, con la cardinalità originale. Se l'input è una sequenza vuota calcolata in modo statico, la sequenza vuota è implicita e viene restituito un errore statico.  
  
 I valori di tipo xs:string vengono confrontati con le regole di confronto dei punti di codice Unicode predefinite XQuery.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Utilizzo della funzione distinct-values() per rimuovere valori duplicati dalla sequenza  
 In questo esempio, un'istanza XML che contiene i numeri di telefono viene assegnata a un **xml** variabile di tipo. Espressione XQuery specificata su tale variabile utilizza il **DISTINCT** funzione per compilare un elenco di numeri di telefono che non contengono duplicati.  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 Risultato:  
  
```  
111-111-1111 222-222-2222    
```  
  
 Nella query seguente, una sequenza di numeri (1, 1, 2) viene passata al **DISTINCT** (funzione). La funzione rimuove quindi il duplicato dalla sequenza e restituisce gli altri due.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 La query restituisce 1 2.  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **DISTINCT** funzione esegue il mapping di valori interi a xs: decimal.  
  
-   Il **DISTINCT** funzione solo supporta i tipi indicati in precedenza e non supporta la combinazione di tipi di base.  
  
-   Il **DISTINCT** funzione su valori xs: Duration non è supportata.  
  
-   Non è supportata l'opzione sintattica che fornisce le regole di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
