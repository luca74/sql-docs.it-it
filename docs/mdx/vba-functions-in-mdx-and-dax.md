---
title: Funzioni VBA in MDX e DAX | Documenti Microsoft
ms.custom: 
ms.date: 01/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 420452fd-9507-4093-8857-71d3e70d96cc
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 6356a6c841072490e10f9c32933606010ce0b9f9
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2018
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funzioni VBA in MDX e DAX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Questo documento contiene un riferimento incrociato di tutte le funzioni VBA disponibili in [le funzioni di Visual Basic](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) che sono supportate in MDX; inoltre, l'elenco include una nota quando si verifica l'equivalenza funzionale con il linguaggio DAX .  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Riferimenti a funzioni di Visual Basic, Applications Edition  
  
|Nome funzione|Supported|Note|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Array|Non supportato||  
|Asc|Solo MDX||  
|AscW|Solo MDX||  
|Atn|Solo MDX||  
|CallByName|Non supportato||  
|CBool|Solo MDX||  
|CByte|Solo MDX||  
|CCur|Solo MDX||  
|CDate|Solo MDX||  
|CDbl|Solo MDX||  
|CDec|Solo MDX||  
|Choose|Solo MDX||  
|Chr|Solo MDX||  
|CInt|Solo MDX||  
|CLng|Solo MDX||  
|CLngLng|Non supportato||  
|CLngPtr|Non supportato||  
|Command|Non supportato||  
|Cos|Solo MDX||  
|CreateObject|Non supportato||  
|CSng|Solo MDX||  
|CStr|Solo MDX||  
|CurDir|Non supportato||  
|CVar|Solo MDX||  
|CVErr|Non supportato||  
|Data|Solo MDX|**Avviso** DAX viene implementata una funzione diversa con lo stesso nome, la funzione DATE (Year, Month, Day), utilizzata per generare un valore di tipo date dagli argomenti specificati|  
|DateAdd|Solo MDX|**Avviso** DAX viene implementata una funzione diversa con lo stesso nome, la funzione DATEADD (\<date >, < number_of_intervals >,\<intervallo >) (funzione), utilizzato per scorrere le date specificate da un numero di intervalli specificati|  
|DateDiff]|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|Funzione DateValue]|DAX, MDX||  
|Day|DAX, MDX||  
|DDB|Solo MDX||  
|Dir|Non supportato||  
|DoEvents|Non supportato||  
|Environ|Non supportato||  
|EOF|Non supportato||  
|Errore|Non supportato||  
|Exp|DAX, MDX||  
|FileAttr|Non supportato||  
|FileDateTime|Non supportato||  
|FileLen|Non supportato||  
|Filter|Non supportato|**Avviso** MDX viene implementata una funzione diversa con lo stesso nome, la funzione FILTER (Set_Expression, Logical_Expression) restituisce il set risultante dal filtraggio di un set specificato in base a una condizione di ricerca dagli argomenti specificati<br /><br /> **Avviso** DAX viene implementata una funzione diversa con lo stesso nome, il filtro (\<tabella >,\<filtro >) restituisce una tabella che rappresenta un subset di un'altra tabella o espressione dagli argomenti specificati|  
|Fix|Solo MDX||  
|Format (Visual Basic, Applications Edition)|DAX, MDX||  
|FormatCurrency|Non supportato||  
|FormatDateTime|Non supportato||  
|FormatNumber|Non supportato||  
|FormatPercent|Non supportato||  
|FreeFile|Non supportato||  
|FV|Solo MDX||  
|GetAllSettings|Non supportato||  
|GetAttr|Non supportato||  
|GetObject|Non supportato||  
|GetSetting|Non supportato||  
|Hex|Solo MDX||  
|Ora|DAX, MDX||  
|Iif|Solo MDX|**Avviso** DAX viene implementata una funzione simile, con il nome: IF (logical_test, value_if_true, value_if_false) (funzione).|  
|IMEStatus|Non supportato||  
|Input|Non supportato||  
|InputBox|Non supportato||  
|InStr|Solo MDX||  
|InStrRev|Non supportato||  
|Int|DAX, MDX||  
|IPmt|Solo MDX||  
|IRR|Solo MDX||  
|IsArray|Solo MDX||  
|Solo IsDateMDX||  
|IsEmpty|Solo MDX||  
|IsError|DAX, MDX||  
|IsMissing|Solo MDX||  
|IsNull|Solo MDX||  
|IsNumeric|Solo MDX||  
|IsObject|Non supportato||  
|Join|Non supportato||  
|LBound|Non supportato||  
|LCase|Solo MDX||  
|Left|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Non supportato||  
|LOF|Non supportato||  
|File di log|Solo MDX|**Importante** DAX viene implementata una funzione diversa con lo stesso nome, la funzione LOG (number, base). Viene restituito il logaritmo di un numero nella base specificata dagli argomenti specificati.|  
|LTrim|Solo MDX||  
|MacID|Non supportato||  
|MacScript|Non supportato||  
|Mid|DAX, MDX||  
|Minuto|DAX, MDX||  
|MIRR|Solo MDX||  
|Month|DAX, MDX||  
|MonthName|Non supportato||  
|MsgBox|Non supportato||  
|Adesso|DAX, MDX||  
|NPer]|Solo MDX||  
|NPV|Solo MDX||  
|Oct|Solo MDX||  
|Partition|Solo MDX||  
|Pmt|Solo MDX||  
|PPmt|Solo MDX||  
|PV|Solo MDX||  
|QBColor|Solo MDX||  
|replica|Solo MDX||  
|Sostituisci|Non supportato||  
|RGB|Solo MDX||  
|Right|DAX, MDX||  
|Rnd|Solo MDX||  
|Arrotondamento|DAX, MDX||  
|RTrim|Solo MDX||  
|Secondo|DAX, MDX||  
|Seek|Non supportato||  
|Sgn|DAX, MDX||  
|Shell|Non supportato||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Space|Solo MDX||  
|Spc|Non supportato||  
|divisione|Non supportato||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|String]|Solo MDX||  
|StrReverse|Non supportato||  
|Opzione|Solo MDX||  
|SYD|Solo MDX||  
|Scheda|Non supportato||  
|Tan|Solo MDX||  
|Time|Non supportato||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Trim]|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|Non supportato||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|Non supportato||  
|Giorno feriale|DAX, MDX||  
|WeekdayName|Non supportato||  
|Year|DAX, MDX||  
  
  
