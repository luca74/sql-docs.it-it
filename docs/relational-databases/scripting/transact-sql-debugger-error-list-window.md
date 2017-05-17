---
title: Finestra Elenco errori (Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ErrorList
dev_langs:
- TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aa7ebae3445240303352026f7cdb99a06b2d61ca
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---error-list-window"></a>Debugger Transact-SQL - Finestra Elenco errori
  La finestra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Error List** displays the syntax and semantic errors that are generated from the IntelliSense code in the [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor.  
  
## <a name="features-of-the-error-list"></a>Caratteristiche della finestra Elenco errori  
 In **Elenco errori** sono disponibili le funzionalità seguenti:  
  
-   Durante la modifica degli script, in **Elenco errori** vengono visualizzati gli errori e gli avvisi prodotti da IntelliSense nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   È possibile fare doppio clic su una voce del messaggio di errore per attivare la scheda del file script che ha generato l'errore e spostarsi nella posizione dello stesso.  
  
-   È possibile filtrare le voci e le colonne di informazioni che si desidera visualizzare per ogni voce.  
  
-   Dopo avere corretto un errore, la relativa voce viene rimossa da **Elenco errori**.  
  
-   Quando si chiude la scheda di un file script [!INCLUDE[tsql](../../includes/tsql-md.md)] , gli errori relativi al file vengono rimossi da **Elenco errori**.  
  
## <a name="working-with-the-error-list"></a>Utilizzo dell'elenco degli errori  
 Per visualizzare **Elenco errori**, eseguire una delle operazioni seguenti:  
  
-   Scegliere **Elenco errori** dal menu **Visualizza**.  
  
-   Utilizzare i tasti di scelta rapida CTRL+\\, CTRL+E.  
  
 Dopo avere aperto **Elenco errori**, è possibile personalizzare la visualizzazione eseguendo le azioni seguenti:  
  
-   Per ordinare l'elenco, fare clic sull'intestazione di una colonna. Per ordinare nuovamente l'elenco in base a un'altra colonna, fare clic sull'intestazione di un'altra colonna tenendo premuto il tasto MAIUSC.  
  
-   Per selezionare le colonne da visualizzare e quelle da nascondere, scegliere **Mostra colonne** dal menu di scelta rapida.  
  
-   Per modificare l'ordine di visualizzazione delle colonne, trascinare l'intestazione di una colonna verso sinistra o verso destra.  
  
 **Elenco errori** non offre collegamenti a informazioni aggiuntive su errori specifici.  
  
## <a name="transact-sql-errors-in-management-studio"></a>Errori Transact-SQL in Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mostra gli errori relativi agli script [!INCLUDE[tsql](../../includes/tsql-md.md)] nelle seguenti posizioni:  
  
-   **Elenco errori** contiene tutti gli errori semantici e di sintassi individuati da IntelliSense nell'editor del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . L'elenco degli errori viene aggiornato dinamicamente durante la modifica di script [!INCLUDE[tsql](../../includes/tsql-md.md)] e comprende tutti gli errori individuati dall'editor in ogni script [!INCLUDE[tsql](../../includes/tsql-md.md)] . L'editor non arresta l'analisi di un file dopo avere rilevato errori in uno script. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]IntelliSense non supporta tutti gli elementi della sintassi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] nell'editor [!INCLUDE[tsql](../../includes/tsql-md.md)] . **Elenco errori** contiene solo gli errori della sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] supportata da IntelliSense.  
  
-   La scheda **Messaggi** nella parte inferiore della finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] visualizza tutti gli errori e messaggi restituiti da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] durante l'esecuzione di uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Questo elenco non subisce modifiche se non viene eseguito nuovamente lo script. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] arresta l'analisi di un batch dopo l'individuazione di uno o due errori di compilazione; pertanto la scheda **Messaggi** potrebbe non elencare tutti gli errori presenti in uno script.  
  
 Talvolta gli errori sono elencati in entrambe le posizioni. Ad esempio, in un file script potrebbe essere presente un errore di sintassi elencato in **Elenco errori**. Se lo script viene eseguito prima di correggere l'errore, il parser [!INCLUDE[ssDE](../../includes/ssde-md.md)] può rilevare la stessa condizione e restituire un'altra copia del messaggio di errore nella scheda **Messaggi** .  
  
> [!NOTE]  
>  **Elenco errori** visualizza solo gli errori dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , non gli errori degli editor MDX, DMX o XML/A. Questi errori vengono visualizzati nella scheda **Messaggi** dei rispettivi editor.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 All'apertura di **Elenco errori** le informazioni sono visualizzate nelle colonne seguenti:  
  
 **Ordine predefinito**  
 Visualizza un valore intero che indica l'ordine in cui le voci sono state generate.  
  
 **Descrizione**  
 Visualizza il testo della voce di errore. Le descrizioni più lunghe vengono suddivise in più righe.  
  
 **File**  
 Visualizza il nome del file script che ha generato l'errore.  
  
 **Linea**  
 Visualizza un numero intero che indica la riga del codice che contiene l'errore.  
  
 **Colonna**  
 Visualizza un numero intero che indica la posizione dell'errore nella riga del codice.  
  
 **Progetto**  
 Visualizza il nome del progetto che comprende il file script.  
  
  