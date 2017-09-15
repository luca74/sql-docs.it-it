---
title: Aggiungere elementi esistenti a un progetto | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a84052767f74ae790328cff5755398e3ea0afbe0
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="add-existing-items-to-a-project"></a>Aggiunta di elementi esistenti a un progetto
È possibile aggiungere nuovi elementi a un progetto per estendere la funzionalità dell'applicazione. Un elemento esistente può essere una query o un file esterno. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] sono presenti due tipi di progetto: progetto script di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e progetto script di Analysis Services. I file di query che è possibile aggiungere varieranno a seconda del tipo di progetto. È possibile aggiungere, ad esempio, una query [!INCLUDE[tsql](../../includes/tsql_md.md)] (un file con estensione sql) a un progetto script di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , ma non a un progetto script di Analysis Services. Per associare ulteriori estensioni di file a un tipo di progetto, vedere [Procedura: Associazione di estensioni di file a un editor di codice](http://msdn.microsoft.com/en-us/193630f4-93de-4950-8f36-68702531f925).  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>Per aggiungere una query o un file esterno esistente a un progetto  
  
1.  In Esplora soluzioni selezionare un progetto di destinazione.  
  
2.  Nel menu **Progetto** fare clic su **Aggiungi elemento esistente**.  
  
    **Cerca in**  
    Utilizzare questo elenco per individuare i file o le cartelle da aggiungere al progetto. Per i servizi Web XML e le applicazioni Web ASP.NET, i file si trovano nel server Web.  
  
    **Desktop**  
    Consente di visualizzare i file e le cartelle che si trovano sul desktop.  
  
    **Progetti**  
    Consente di visualizzare i file e le cartelle nella posizione predefinita **Progetti** .  
  
    **Risorse del computer**  
    Consente di visualizzare il contenuto della cartella **Risorse del computer** .  
  
    **Nome file**  
    Questa opzione consente di applicare un filtro alle cartelle e ai file visualizzati. Immettere il nome completo o parziale del file in base al quale applicare il filtro. Utilizzare un asterisco (`*`) come carattere jolly.  
  
    > [!NOTE]  
    > Per spostarsi su percorsi Web e di rete, immettere l'URL o il percorso di rete nella casella **Nome file** . Se, ad esempio, si digita **http://mywebsite** verranno visualizzati i file disponibili nel percorso Web mywebsite, mentre se si digita **\\\myserver\myshare** verranno visualizzati i file disponibili nel percorso myshare del server myserver.  
  
    **Tipo file**  
    Questa opzione consente di applicare un filtro ai file in base all'estensione. In ogni prodotto vengono elencati i filtri predefiniti dei tipi di file più comuni.  
  
    **Aggiungi**  
    Utilizzare questo pulsante a discesa per aggiungere l'elemento al progetto e aprirlo nell'editor predefinito.  
  
    -   **Aggiungi**  
  
        Consente di copiare l'elemento esistente nella cartella del progetto memorizzata sul disco e di aggiungerlo sotto il progetto selezionato in Esplora soluzioni. Le modifiche apportate all'elemento non si rifletteranno su quello presente nella posizione originale. Si tratta dell'editor predefinito per il tipo di file.  
  
    -   **Aggiungi come collegamento**  
  
        Consente di aggiungere il file selezionato al progetto e di aprirlo nell'editor predefinito per il tipo di file. Il file selezionato originariamente viene aperto, ma non copiato nella cartella del progetto.  
  
3.  Se vengono aggiunti file di query, nella finestra di dialogo di connessione verrà visualizzato un messaggio in cui si chiede di specificare una connessione per la query. Se non si desidera associare una connessione alla query, fare clic su **Annulla** nella finestra di dialogo di connessione.  
  
4.  Il file verrà aggiunto alla cartella **Query** o **File esterni** del progetto.  
  
## <a name="see-also"></a>Vedere anche  
[Esplora soluzioni](../../ssms/solution/solution-explorer.md)  
[Aggiunta di nuovi elementi a un progetto](../../ssms/solution/add-new-items-to-a-project.md)  
[Rimozione o eliminazione di un elemento o di un progetto](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
