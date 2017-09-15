---
title: Tipi di dati di intervallo | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1e19ac3f7c14326524ab7cbaa60f499c5d81e91
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="interval-data-types"></a>Tipi di dati di intervallo
Un intervallo è definito come la differenza tra due date e ore. Gli intervalli sono espressi in uno dei due modi diversi. Uno è un *anno-mese* intervallo espresso intervalli in termini di anni e un numero integrale di mesi. L'altro è un *diurno* intervallo che esprime gli intervalli in termini di giorni, minuti e secondi. Questi due tipi di intervalli sono distinti e non possono essere combinati, perché i mesi possono avere un numero di giorni.  
  
 Un intervallo è costituito da un set di campi. Non vi è un ordinamento implicito tra i campi. Ad esempio, in un intervallo di anno per mese, anno per primo, seguito da mese. Analogamente, nel giorno in minuti, i campi sono in ordine giorno, ora e minuto. Viene chiamato il primo campo in un tipo di intervallo di *iniziali* , campo o *significativo* campo. L'ultimo campo viene chiamato il *finali* campo.  
  
 In tutti gli intervalli, il campo iniziale non è vincolato dalle regole del calendario gregoriano. Ad esempio, in un intervallo per ora, minuto, al campo dell'ora non è vincolato per essere compreso tra 0 e 23 (inclusi), come avviene normalmente. I campi finali dopo il campo iniziale seguono i normali vincoli del calendario gregoriano. Per ulteriori informazioni, vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), più avanti in questa appendice.  
  
 Sono disponibili tipi di dati SQL intervallo 13 e 13 tipi di dati di intervallo C. Ognuno dei tipi di dati di intervallo C Usa la stessa struttura, SQL_INTERVAL_STRUCT, per contenere i dati di intervallo. (Per ulteriori informazioni, vedere la sezione successiva, [struttura intervallo C](../../../odbc/reference/appendixes/c-interval-structure.md).) Per ulteriori informazioni sui tipi di dati SQL, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md); per ulteriori informazioni sui tipi di dati C, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificatore di tipo|Classe|Description|  
|---------------------|-----------|-----------------|  
|MONTH|Anno-mese|Numero di mesi tra due date.|  
|YEAR|Anno-mese|Numero di anni tra due date.|  
|YEAR_TO_MONTH|Anno-mese|Numero di anni e mesi tra due date.|  
|DAY|Ora diurna|Numero di giorni tra due date.|  
|HOUR|Ora diurna|Numero di ore tra due data/ora.|  
|MINUTE|Ora diurna|Numero di minuti tra due data/ora.|  
|SECOND|Ora diurna|Numero di secondi tra due data/ora.|  
|DAY_TO_HOUR|Ora diurna|Numero di giorni/ore tra due data/ora.|  
|DAY_TO_MINUTE|Ora diurna|Numero di giorni/ore o minuti tra due data/ora.|  
|DAY_TO_SECOND|Ora diurna|Numero di giorni/ore/minuti/secondi tra due data/ora.|  
|HOUR_TO_MINUTE|Ora diurna|Numero di ore o minuti tra due data/ora.|  
|HOUR_TO_SECOND|Ora diurna|Numero di minuti/ore/secondi tra due data/ora.|  
|MINUTE_TO_SECOND|Ora diurna|Numero di minuti/secondi tra due data/ora.|  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Struttura di intervallo C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisione del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Lunghezza del tipo di dati intervallo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Valori letterali di intervallo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Override iniziale predefinita e la precisione in secondi per i tipi di dati di intervallo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)