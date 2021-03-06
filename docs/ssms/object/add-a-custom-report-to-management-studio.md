---
title: Aggiungere un report personalizzato a Management Studio | Microsoft Docs
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
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b682c71e77188ea46cea5f85590953c17d61bda
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="add-a-custom-report-to-management-studio"></a>Aggiunta di un report personalizzato a Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Questo argomento descrive come creare un report semplice di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] salvato come file con estensione rdl e quindi aggiungere tale file a [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] come report personalizzato. [!INCLUDE[ssRS](../../includes/ssrs_md.md)] consente di creare una vasta gamma di sofisticati report. Per creare un report in base a questo argomento, è necessario che nel computer sia installato [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] . Per eseguire un report personalizzato mediante [!INCLUDE[ssRS](../../includes/ssrs_md.md)] non è necessario installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
 
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>Per creare un report semplice salvato come file con estensione rdl  
  
1.  Fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**e fare clic su **SQL Server Data Tools**.  
  
2.  Scegliere **Nuovo** dal menu **File**e quindi fare clic su **Progetto**.  
  
3.  Nell'elenco **Tipi progetto** fare clic su **Progetti Business Intelligence**.  
  
4.  Nell'elenco **Modelli** fare clic su **Creazione guidata progetto server di report**.  
  
5.  In **Nome**digitare **ReportConnessioni**e fare clic su **OK**.  
  
6.  Nella pagina introduttiva di **Creazione guidata report** fare clic su **Avanti**.  
  
7.  Nella casella Nome della pagina **Selezione origine dati** digitare un nome per la connessione a [!INCLUDE[ssDE](../../includes/ssde_md.md)]e fare clic su **Modifica**.  
  
8.  Nella casella **Nome server** della finestra di dialogo **Proprietà connessione** digitare il nome dell'istanza di [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
9. Nella casella **Selezionare o immettere un nome di database** digitare il nome di uno dei database presenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ad esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)], e fare clic su **OK**.  
  
10. Nella pagina **Selezione origine dati** fare clic su **Avanti**.  
  
11. Nella casella **Stringa query** della pagina **Progettazione query** digitare l'istruzione [!INCLUDE[tsql](../../includes/tsql_md.md)] seguente, che elenca le connessioni correnti a [!INCLUDE[ssDE](../../includes/ssde_md.md)]e fare clic su **Avanti**. Nella casella Stringa query della Creazione guidata report non è possibile immettere parametri di report. La creazione di report personalizzati più complessi dovrà essere eseguita manualmente.  
  
    **SELECT session_id, net_transport FROM sys.dm_exec_connections;**  
  
12. Nella pagina **Selezione tipo di report** selezionare **Tabulare**e fare clic su **Fine**.  
  
13. Nella pagina **Completamento procedura guidata** digitare **ReportConnessioni** nella casella **Nome report**e fare clic su **Fine** per creare e salvare il report.  
  
14. Chiudere [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio_md.md)].  
  
15. Copiare **ReportConnessioni.rdl** in una cartella creata nel server di database per i report personalizzati.  
  
### <a name="to-add-a-report-to-management-studio"></a>Per aggiungere un report a Management Studio  
  
-   In [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]fare clic con il pulsante destro del mouse su un nodo in Esplora oggetti, scegliere **Report**e fare clic su **Report personalizzati**. Nella finestra di dialogo **Apri file** individuare la cartella dei report personalizzati, selezionare il file **ReportConnessioni.rdl** e fare clic su **Apri**.  
  
    Alla prima apertura di un nuovo report personalizzato da un nodo di Esplora oggetti, tale report verrà aggiunto all'elenco degli ultimi elementi usati in **Report personalizzati** nel menu di scelta rapida del nodo. Analogamente, alla prima apertura, anche un report standard verrà aggiunto all'elenco degli ultimi elementi usati in **Report personalizzati**. Se viene eliminato un file di un report personalizzato, alla successiva selezione dell'elemento verrà visualizzato un messaggio che chiederà di eliminare la relativa voce dall'elenco degli ultimi elementi utilizzati.  
  
    1.  Per modificare il numero dei file visualizzati nell'elenco degli ultimi elementi usati, scegliere **Opzioni** dal menu **Strumenti** , espandere la cartella **Ambiente** e fare clic su **Generale**.  
  
    2.  Modificare il numero in **Display files in recently used list**(Visualizza file nell'elenco degli ultimi file usati).  
  
## <a name="see-also"></a>Vedere anche  
[Report personalizzati in Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
[Utilizzo di report personalizzati con proprietà dei nodi di Esplora oggetti](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
[Visualizzazione di avvisi relativi all'esecuzione di report personalizzati](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[SQL Server Reporting Services](http://msdn.microsoft.com/en-us/b8d18d3d-9db0-43e7-8286-7b46cc3a37ed)  
  
