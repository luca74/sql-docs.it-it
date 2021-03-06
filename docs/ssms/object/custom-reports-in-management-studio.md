---
title: Report personalizzati in Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be381dfcba80135f5c76694ab2f19f2942e0f5a8
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="custom-reports-in-management-studio"></a>Report personalizzati in Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] molti nodi di Esplora oggetti contengono un set di report standard creati da [!INCLUDE[msCoName](../../includes/msconame_md.md)]. In tali report viene fornito un riepilogo delle informazioni relative ai server generalmente necessarie. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] Service Pack 2, gli amministratori possono eseguire report personalizzati creati in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
## <a name="implementation"></a>Implementazione  
I report personalizzati vengono archiviati come file di definizione di report con estensione rdl e vengono creati mediante il linguaggio RDL (Report Definition Language). Il linguaggio RDL contiene informazioni sul layout e il recupero dei dati per un report in formato XML RDL è uno schema aperto. Gli sviluppatori possono estendere RDL con attributi ed elementi aggiuntivi. Nei report può essere eseguita qualsiasi istruzione [!INCLUDE[tsql](../../includes/tsql_md.md)] valida.  
  
Se Esplora oggetti è connesso a un server, i report personalizzati possono essere eseguiti nel contesto della selezione corrente di Esplora oggetti, a condizione che facciano riferimento ai parametri di report di tale nodo. Un report può pertanto utilizzare il contesto corrente, ad esempio il database corrente, oppure un contesto consistente, ad esempio specificando un database designato all'interno dell'istruzione [!INCLUDE[tsql](../../includes/tsql_md.md)] contenuta nel report personalizzato.  
  
## <a name="running-a-custom-report"></a>Esecuzione di un report personalizzato  
È possibile eseguire un report personalizzato in [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] nei modi seguenti:  
  
-   Fare clic con il pulsante destro del mouse su un nodo in Esplora oggetti, scegliere **Report** e quindi fare clic su **Report personalizzati**. Nella finestra di dialogo **Apri file** individuare una cartella contenente file con estensione rdl e aprire il file di report appropriato.  
  
-   Fare clic con il pulsante destro del mouse su un nodo in Esplora oggetti, scegliere **Report**, **Report personalizzati**e infine selezionare un report personalizzato nell'elenco degli ultimi file usati.  
  
## <a name="limitations"></a>Limitazioni  
Quando si utilizzano report personalizzati, tenere presenti le limitazioni seguenti:  
  
-   Per impedire l'esecuzione indesiderata di malware, non è possibile configurare [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] per l'esecuzione automatica di un report anche se il file system è configurato per l'associazione dei file con estensione rdl a [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]. I report non possono essere eseguiti a livello di codice in [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] né dalla riga di comando tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
-   È possibile eseguire report personalizzati in un contesto che non produce i valori previsti. È possibile, ad esempio, eseguire un report relativo alla replica nel contesto di un database non interessato dalla replica oppure eseguire un report utilizzando un account utente che non dispone dell'autorizzazione per accedere alle informazioni necessarie per generare un report accurato. L'autore del report personalizzato è responsabile della validità della struttura del report e del relativo contesto.  
  
-   Non è possibile aggiungere un report personalizzato all'elenco dei report standard.  
  
-   Il codice elaborato dal report può influire sulle prestazioni del server.  
  
-   I report personalizzati non supportano sottoreport.  
  
-   Il testo del comando per ogni query all'interno del report non deve essere definito tramite un'espressione.  
  
-   Qualsiasi parametro di query utilizzato in un comando (query) può fare riferimento soltanto a un singolo parametro di report e non può utilizzare operatori di espressione.  
  
-   Per i comandi dei report (query) sono supportati soltanto i tipi di comando Text e Stored Procedure.  
  
-   Il framework del report non contiene alcun parametro di escape per le query. Gli autori delle query devono verificare che le query non siano soggette ad attacchi intrusivi nel codice SQL.  
  
## <a name="managing-custom-reports"></a>Gestione dei report personalizzati  
In presenza di numerosi report personalizzati, è consigliabile organizzare tali report utilizzando cartelle del file system con autorizzazioni del file system NTFS appropriate.  
  
## <a name="permissions"></a>Autorizzazioni  
I report personalizzati vengono eseguiti utilizzando le autorizzazioni dell'utente corrente. Per impedire che le query eseguite dal report vengano modificate da utenti malintenzionati, è consigliabile impostare le autorizzazioni per la cartella del file system contenente i file di report in modo da limitare l'accesso.  
  
Sia l'utente che l'account utilizzato dal servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] necessitano dell'accesso in lettura alla cartella del file system contenente i file di report.  
  
In un report è possibile incorporare qualsiasi comando [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] valido, ma il comando non verrà eseguito.  
  
> [!CAUTION]  
> In un report può essere incorporata ed eseguita qualsiasi istruzione [!INCLUDE[tsql](../../includes/tsql_md.md)] valida. L'esecuzione di un report con un account utente che dispone di privilegi elevati consente di eseguire tutte le istruzioni incorporate senza problemi.  
  

  
## <a name="see-also"></a>Vedere anche  
[Aggiunta di un report personalizzato a Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[Visualizzazione di avvisi relativi all'esecuzione di report personalizzati](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[Usare report personalizzati con proprietà dei nodi di Esplora oggetti](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
