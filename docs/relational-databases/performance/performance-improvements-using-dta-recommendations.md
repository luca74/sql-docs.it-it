---
title: Miglioramenti delle prestazioni mediante le indicazioni di Ottimizzazione guidata motore di database | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
caps.latest.revision: 3
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7722ff42ebc2e4e4515a3097a6b8d1106f5e1287
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="performance-improvements-using-dta-recommendations"></a>Miglioramenti delle prestazioni mediante le indicazioni di Ottimizzazione guidata motore di database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


---
Le prestazioni dei carichi di lavoro di data warehousing e analisi possono trarre vantaggio dagli indici **columnstore**, in particolare per le query che devono eseguire l'analisi di tabelle di grandi dimensioni. Gli indici **Rowstore** (albero B+-) sono particolarmente utili per le query che accedono a quantità relativamente piccole di dati durante la ricerca di un determinato valore o intervallo di valori. Poiché possono restituire righe ordinate, gli indici rowstore consentono anche di ridurre il costo dell'ordinamento nei piani di esecuzione delle query. Pertanto, la scelta della combinazione di indici rowstore e columnstore da compilare dipende dal carico di lavoro dell'applicazione.

A partire da SQL Server 2016, Ottimizzazione guidata motore di database può proporre una **combinazione di indici rowstore e columnstore** appropriata grazie all'analisi di uno specifico carico di lavoro del database. 

Per illustrare i vantaggi delle indicazioni di Ottimizzazione guidata motore di database relative alle prestazioni del carico di lavoro, abbiamo provato diversi carichi di lavoro reali dei clienti. Per ogni carico di lavoro dei clienti, Ottimizzazione guidata motore di database analizza le singole query e il carico di lavoro completo delle query. Consideriamo tre alternative:
  
  1. **Solo indici columnstore**: compilare solo gli indici columnstore per tutte le tabelle senza usare Ottimizzazione guidata motore di database. 
  2. **Ottimizzazione guidata motore di database (solo indici rowstore)**: eseguire Ottimizzazione guidata motore di database con l'opzione per fornire indicazioni solo per gli indici rowstore.
  3. **Ottimizzazione guidata motore di database (indici rowstore + columnstore)**: eseguire Ottimizzazione guidata motore di database con l'opzione per fornire indicazioni sia per gli indici rowstore che per gli columnstore.  
   
In ogni caso abbiamo implementato gli indici consigliati. Viene evidenziato il tempo di CPU (in millisecondi) come valore medio di più esecuzioni della query o del carico di lavoro. Nella figura seguente è riportato il tempo di CPU in millisecondi per i carichi di lavoro tra due diversi database dei clienti. Si noti che l'asse y (tempo di CPU) usa una scala logaritmica.   


![Prestazioni degli indici rowstore e columnstore in Ottimizzazione guidata motore di database](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**Necessario per progettazioni fisiche miste**: primo set di barre corrispondente a Cliente 1 Query 1. L'indicazione di Ottimizzazione guidata motore di database (rowstore + columnstore) che prevede un set di quattro indici columnstore e sei indici rowstore ha come risultato un tempo di CPU da 2,5 a 4 volte inferiore rispetto all'uso solo dell'indice columnstore e di Ottimizzazione guidata motore di database (solo rowstore). Questo esempio dimostra i vantaggi delle progettazioni fisiche miste costituite da indici rowstore e columnstore *anche per una singola query*. 

**Efficacia delle indicazioni relative agli indici rowstore**: il secondo e terzo set di barre, corrispondenti a Cliente 1 Query 2 e a Cliente 2 Query 1, sono casi in cui le query includono predicati del filtro selettivo che traggono vantaggio dagli indici rowstore adatti. Per entrambe queste query, Ottimizzazione guidata motore di database (solo rowstore) e Ottimizzazione guidata motore di database (rowstore + columnstore) consigliano l'uso solo degli indici rowstore. Questi esempi illustrano inoltre che, anche se Ottimizzazione guidata motore di database viene chiamato con l'opzione per consigliare gli indici columnstore, il relativo approccio basato sui costi fa sì che venga proposto un indice columnstore solo se effettivamente il carico di lavoro può trarne vantaggio.

**Efficacia delle indicazioni relative agli indici columnstore**: il quarto set di barre corrispondente a Cliente 2 Query 2 rappresenta un caso in cui la query esegue l'analisi di tabelle di grandi dimensioni e può trarre beneficio dagli indici columnstore. Ottimizzazione guidata motore di database (solo rowstore) genera un'indicazione il cui tempo di CPU è superiore rispetto a quando sono presenti gli indici columnstore. Ottimizzazione guidata motore di database (rowstore + columnstore) consiglia gli indici columnstore adatti, ottenendo prestazioni di esecuzione delle query corrispondenti a quelle in cui viene usata l'opzione basata solo su indici columnstore.

**Efficacia delle indicazioni per il carico di lavoro con più query**: il set finale di barre corrispondente al carico di lavoro completo per Cliente 2 illustra la capacità di Ottimizzazione guidata motore di database di analizzare più query nel carico di lavoro per consigliare un set appropriato di indici rowstore e columnstore al fine di migliorare il costo di esecuzione globale del carico di lavoro. Ottimizzazione guidata motore di database (rowstore + columnstore) consiglia quattro indici columnstore e decine di indici rowstore, ottenendo come risultato un rilevante miglioramento delle prestazioni per il carico di lavoro, se confrontato con l'opzione che prevede la compilazione solo di indici columnstore, nonché un miglioramento da 4 a 5 volte superiore se confrontato con Ottimizzazione guidata motore di database (solo rowstore).

In sintesi, gli esempi precedenti illustrano la capacità di Ottimizzazione guidata motore di database di sfruttare gli indici sia rowstore che columnstore supportati nel motore di database di SQL Server e di consigliare una combinazione appropriata di indici in grado di ridurre in modo significativo il tempo di CPU per il carico di lavoro. 

<a name="see-also"></a>Vedere anche
---
[Ottimizzazione guidata motore di database](../../relational-databases/performance/database-engine-tuning-advisor.md)

[Indicazioni relative agli indici columnstore in Ottimizzazione guidata motore di database](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[Guida agli indici columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)

[Indici columnstore per il data warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



