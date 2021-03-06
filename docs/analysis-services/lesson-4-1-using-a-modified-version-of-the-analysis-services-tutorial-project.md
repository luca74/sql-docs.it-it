---
title: Utilizzando una versione modificata dell'analisi di servizi progetto Tutorial | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 685aa217-de1b-4df2-bf22-095228c40775
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 90a1b92087d0f753fdd637830bc4dd4c86d601a3
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/19/2018
---
# <a name="lesson-4-1---using-a-modified-version-of-the-analysis-services-tutorial-project"></a>Lezione 4-1-utilizzo di una versione modificata del progetto Analysis Services Tutorial
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Le lezioni rimanenti di questa esercitazione sono basate su una versione migliorata del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial completato nelle prime tre lezioni. Altre tabelle e calcoli denominati sono stati aggiunti alla vista origine dati **Adventure Works DW 2012** ; sono state aggiunte altre dimensioni al progetto e al cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. Infine, è stato aggiunto un secondo gruppo di misure contenente le misure di una seconda tabella dei fatti. Il progetto migliorato consente di approfondire la conoscenza delle tecniche per l'aggiunta di funzionalità alla propria applicazione di Business Intelligence senza la necessità di tornare su informazioni già acquisite.  
  
Per continuare l'esercitazione è necessario scaricare, estrarre, caricare ed elaborare la versione migliorata del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.  Utilizzare le istruzioni riportate in questa lezione per verificare di avere eseguito tutti i passaggi.  
  
## <a name="downloading-and-extracting-the-project-file"></a>Download ed estrazione del file di progetto  
  
1.  [Fare clic qui](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) per accedere alla pagina di download in cui si trovano i progetti di esempio usati in questa esercitazione. I progetti dell'esercitazione sono inclusi nel **adventure-works-multidimensionale-esercitazione-projects.zip** scaricare.  
  
2.  Fare clic su **adventure-works-multidimensionale-esercitazione-projects.zip** per scaricare il pacchetto che contiene i progetti per questa esercitazione.  
  
    Per impostazione predefinita, nella cartella Downloads viene salvato un file con estensione ZIP. È necessario spostare il file ZIP in un percorso più breve, ad esempio creare una cartella C:\Tutorials per archiviare i file.  È quindi possibile estrarre i file contenuti nel file ZIP. Se si tenta di decomprimere i file dalla cartella Downloads il cui percorso è più lungo, si otterrà solo la Lezione 1.  
  
3.  Creare una sottocartella al livello dell'unità radice, ad esempio C:\Tutorial, o a un livello immediatamente inferiore.  
  
4.  Spostare il **adventure-works-multidimensionale-esercitazione-projects.zip** file nella sottocartella.  
  
5.  Fare clic con il pulsante destro del mouse sul file e scegliere **Estrai tutto**.  
  
6.  Passare alla cartella **Lesson 4 Start** per trovare il file **Analysis Services Tutorial.sln** .  
  
## <a name="loading-and-processing-the-enhanced-project"></a>Caricamento ed elaborazione del progetto migliorato  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Chiudi soluzione** dal menu **File** per chiudere i file che non verranno usati.  
  
2.  Scegliere **Apri** dal menu **File** e fare clic su **Progetto/Soluzione**.  
  
3.  Passare al percorso in cui sono stati estratti i file di progetto dell'esercitazione.  
  
    Trovare la cartella denominata **Lesson 4 Start**, quindi fare doppio clic sul file Analysis Services Tutorial.sln.  
  
4.  Distribuire la versione migliorata del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial nell'istanza locale di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]o in un'altra istanza e verificare che l'elaborazione venga completata correttamente.  
  
## <a name="understanding-the-enhancements-to-the-project"></a>Informazioni sui miglioramenti apportati al progetto  
La versione migliorata del progetto è diversa dalla versione del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial completata nelle prime tre lezioni. Le differenze verranno descritte nelle sezioni seguenti. Leggere attentamente queste informazioni prima di passare alle lezioni rimanenti dell'esercitazione.  
  
### <a name="data-source-view"></a>Vista origine dati  
Nella vista origine dati del progetto migliorato è inclusa un'ulteriore tabella dei fatti e quattro tabelle delle dimensioni aggiuntive del database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
Si noti che con dieci tabelle nella vista origine dati, il diagramma <All Tables> risulta molto pieno. Di conseguenza, risulta difficile individuare sia le relazioni tra le tabelle che tabelle specifiche. Per risolvere questo problema, le tabelle vengono organizzate in due diagrammi logici, ovvero **Internet Sales** e **Reseller Sales** . Ogni diagramma è organizzato in base a una singola tabella dei fatti. La creazione di diagrammi logici consente di visualizzare e utilizzare un subset specifico delle tabelle in una vista origine dati anziché visualizzare sempre tutte le tabelle e le relative relazioni in un unico diagramma.  
  
#### <a name="internet-sales-diagram"></a>Diagramma Internet Sales  
Il diagramma **Internet Sales** contiene le tabelle relative alla vendita dei prodotti [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] direttamente ai clienti tramite Internet. Le tabelle del diagramma sono le quattro tabelle delle dimensioni e una sola tabella dei fatti aggiunte alla vista origine dati di **Adventure Works DW 2012** nella Lezione 1. Le tabelle sono le seguenti:  
  
-   **Geography**  
  
-   **Customer**  
  
-   **Data**  
  
-   **Product**  
  
-   **InternetSales**  
  
#### <a name="reseller-sales-diagram"></a>Diagramma Reseller Sales  
Il diagramma **Reseller Sales** contiene le tabelle relative alla vendita dei prodotti [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] da parte dei rivenditori. Nel diagramma sono incluse le seguenti sette tabelle delle dimensioni e una tabella dei fatti del database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
-   **Reseller**  
  
-   **Promotion**  
  
-   **SalesTerritory**  
  
-   **Geography**  
  
-   **Data**  
  
-   **Product**  
  
-   **Employee**  
  
-   **ResellerSales**  
  
Si noti che le tabelle **DimGeography**, **DimDate**e **DimProduct** sono usate sia nel diagramma **Internet Sales** sia nel diagramma **Reseller Sales** . È possibile collegare le tabelle delle dimensioni a più tabelle dei fatti.  
  
### <a name="database-and-cube-dimensions"></a>Dimensioni del database e del cubo  
Nel progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial sono incluse cinque nuove dimensioni del database e il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial contiene queste stesse cinque dimensioni come dimensioni del cubo. Tali dimensioni sono state definite in modo da avere attributi e gerarchie utente modificati utilizzando calcoli denominati, chiavi dei membri per la composizione e cartelle di visualizzazione. Nell'elenco seguente vengono descritte le nuove dimensioni.  
  
Dimensione Reseller  
La dimensione Reseller è basata sulla tabella **Reseller** della vista origine dati di **Adventure Works DW 2012** .  
  
Dimensione Promotion  
La dimensione Promotion è basata sulla tabella **Promotion** della vista origine dati di **Adventure Works DW 2012** .  
  
Dimensione Sales Territory  
La dimensione Sales Territory è basata sulla tabella **SalesTerritory** della vista origine dati di **Adventure Works DW 2012** .  
  
Dimensione Employee  
La dimensione Employee è basata sulla tabella **Employee** della vista origine dati di **Adventure Works DW 2012** .  
  
Dimensione Geography  
La dimensione Geography è basata sulla tabella **Geography** della vista origine dati di **Adventure Works DW 2012** .  
  
#### <a name="analysis-services-cube"></a>Cubo di Analysis Services  
Il cubo **Analysis Services Tutorial** contiene ora due gruppi di misure, ovvero il gruppo di misure originale basato sulla tabella **InternetSales** e un secondo gruppo di misure basato sulla tabella **ResellerSales** della vista origine dati di **Adventure Works DW 2012** .  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Definizione delle proprietà degli attributi padre in una gerarchia padre-figlio](../analysis-services/lesson-4-2-defining-parent-attribute-properties-in-a-parent-child-hierarchy.md)  
  
## <a name="see-also"></a>Vedere anche  
[Distribuzione di un progetto di Analysis Services](../analysis-services/lesson-2-5-deploying-an-analysis-services-project.md)  
  
