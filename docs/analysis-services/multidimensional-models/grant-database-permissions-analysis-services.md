---
title: Concedere le autorizzazioni di database (Analysis Services) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b05b035f530318759f0b2eb4b20bd9bd5edd4d01
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="grant-database-permissions-analysis-services"></a>Concedere le autorizzazioni per il database (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Se si affronta l'amministrazione del database di Analysis Services avendo già esperienza con i database relazionali, il primo aspetto da comprendere è che, per quanto riguarda l'accesso ai dati, il database non è l'oggetto principale a protezione diretta in Analysis Services.  
  
 La struttura di query primaria in Analysis Services è rappresentata da un cubo (o un modello tabulare), con le autorizzazioni utente impostate per specifici oggetti. A differenza del motore di database relazionale, in cui gli account di accesso al database e le autorizzazioni utente (spesso **db_datareader**) vengono impostati nel database stesso, un database di Analysis Services è per lo più un contenitore per gli oggetti query principali in un modello di dati. Se l'obiettivo immediato è consentire l'accesso ai dati per un cubo o un modello tabulare, per ora è possibile ignorare le autorizzazioni di database e passare direttamente all'argomento: [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Le autorizzazioni di database in Analysis Services consentono di eseguire funzioni amministrative, che in senso lato equivalgono all'autorizzazione del database Controllo completo, mentre in un contesto più specifico consentono di delegare le operazioni di elaborazione. I livelli di autorizzazione per un database di Analysis Services sono specificati nel riquadro **Generale** della finestra di dialogo **Crea ruolo** , illustrata nella figura seguente e descritta di seguito.  
  
 In Analysis Services non ci sono account di accesso. È sufficiente creare i ruoli e assegnare gli account di Windows nel riquadro **Appartenenza** . Tutti gli utenti, compresi gli amministratori, si connettono ad Analysis Services con un account di Windows.  
  
 ![Ruolo di finestra di dialogo con autorizzazioni create database](../../analysis-services/multidimensional-models/media/ssas-permsdbrole.png "ruolo finestra di dialogo con autorizzazioni Create database")  
  
 Esistono tre tipi di autorizzazioni specificate a livello di database.  
  
 **Controllo completo (amministratore)** : si tratta di un'autorizzazione omnicomprensiva che conferisce ampi poteri in un database di Analysis Services come, ad esempio, la possibilità di elaborare o eseguire query su qualsiasi oggetto all'interno del database e di gestire la sicurezza dei ruoli. L'autorizzazione Controllo completo consente di eseguire le stesse funzioni di un amministratore di database. Quando si seleziona **Controllo completo**, **Elaborazione database** e **Lettura definizione** , anche le autorizzazioni vengono selezionate e non possono essere rimosse.  
  
> [!NOTE]  
>  Agli amministratori del server (membri del ruolo di amministratore del server) viene assegnata implicitamente l'autorizzazione Controllo completo per ogni database del server.  
  
 **Elaborazione database** : questa autorizzazione viene usata per delegare l'elaborazione a livello di database. L'amministratore può ripartire questa attività creando un ruolo che consenta a un'altra persona o servizio di richiamare le operazioni di elaborazione per un oggetto del database. In alternativa, è anche possibile creare i ruoli che consentono l'elaborazione in oggetti specifici. Per altre informazioni, vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) .  
  
 **Lettura definizione** : questa autorizzazione concede la possibilità di leggere i metadati degli oggetti, senza però visualizzare i dati associati. In genere, questa autorizzazione viene usata nei ruoli creati per un'elaborazione dedicata, offrendo la possibilità di usare strumenti quali [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per elaborare un database in modo interattivo. Senza **Lettura definizione**, l'autorizzazione **Elaborazione database** è valida solo in scenari con script. Per automatizzare l'elaborazione, ad esempio tramite SSIS o un'altra utilità di pianificazione, è possibile creare un ruolo con l'autorizzazione **Elaborazione database** ma privo di **Lettura definizione**. In caso contrario, provare a usare insieme le due proprietà nello stesso ruolo per supportare sia l'elaborazione automatica che interattiva tramite gli strumenti di SQL Server che visualizzano il modello di dati in un'interfaccia utente.  
  
## <a name="full-control-administrator-permissions"></a>Autorizzazioni Controllo completo (amministratore)  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], per amministratore di database si intende un'identità utente di Windows assegnata a un ruolo che include le autorizzazioni Controllo completo (amministratore). Un amministratore di database può eseguire qualsiasi attività all'interno del database, tra cui:  
  
-   Elaborazione di oggetti  
  
-   Lettura di dati e metadati per tutti gli oggetti del database, compresi cubi, dimensioni, gruppi di misure, prospettive e modelli di data mining  
  
-   Creazione o modifica dei ruoli di database mediante l'aggiunta di utenti o autorizzazioni, compresa la possibilità di aggiungere utenti a ruoli con autorizzazioni Controllo completo  
  
-   Eliminazione di ruoli di database o dell'appartenenza a ruoli  
  
-   Registrazione di assembly (o stored procedure) per il database  
  
 Si noti che un amministratore di database non può aggiungere o eliminare database dal server né concedere diritti di amministratore ad altri database sullo stesso server. Tale privilegio appartiene solo agli amministratori del server. Vedere [Concedere i diritti di amministratore del server a un'istanza di Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) per altre informazioni su questo livello di autorizzazione.  
  
 Poiché tutti i ruoli sono definiti dall'utente, è consigliabile creare un ruolo dedicato a tale scopo, ad esempio un ruolo denominato "dbadmin", e quindi assegnare in modo appropriato gli account utente e di gruppo di Windows.  
  
#### <a name="create-roles-in-ssms"></a>Creare ruoli in SSMS  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], aprire la cartella **Database** , selezionare un database e fare clic con il pulsante destro del mouse su **Ruoli** | **Nuovo ruolo**.  
  
2.  Nel riquadro **Generale** immettere un nome, ad esempio DBAdmin.  
  
3.  Selezionare la casella di controllo **Controllo completo (amministratore)** per il cubo. Si noti che **Elaborazione database** e **Lettura definizione** vengono selezionate automaticamente. Entrambe le autorizzazioni vengono sempre incluse nei ruoli con **Controllo completo**.  
  
4.  Nel riquadro **Appartenenza** immettere gli account utente e di gruppo di Windows che si connettono ad Analysis Services con questo ruolo.  
  
5.  Fare clic su **OK** per completare la creazione del ruolo.  
  
## <a name="process-database"></a>Elaborazione database  
 Quando si definisce un ruolo che concede le autorizzazioni di database, è possibile ignorare l'autorizzazione **Controllo completo** e scegliere solo **Elaborazione database**. Tale autorizzazione, impostata a livello di database, consente l'elaborazione in tutti gli oggetti all'interno del database. Per altre informazioni, vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>Lettura definizione  
 L'impostazione delle autorizzazioni **Lettura definizione**a livello di database produce un effetto a catena sugli altri oggetti all'interno del database, analogamente all'autorizzazione **Elaborazione database** . Se si vogliono impostare le autorizzazioni Lettura definizione a un livello più granulare, è necessario deselezionare Lettura definizione come proprietà del database nel riquadro Generale. Per altre informazioni, vedere [Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere i diritti di amministratore del server a un'istanza di Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Concedere le autorizzazioni di elaborazione &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  
