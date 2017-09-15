---
title: "Importazione di un dominio da un file DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Importazione di un dominio da un file DQS
  In questo argomento viene descritto come importare un dominio da un file DQS in una Knowledge Base esistente in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Un file di dati DQS viene creato esportando un dominio o una Knowledge Base dall'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . I file di dati DQS sono crittografati, pertanto non è possibile visualizzarne il contenuto.  
  
 L'utilizzo di un file di dati DQS per l'esportazione di un dominio da una Knowledge Base e per l'importazione in un'altra semplifica il processo di generazione delle informazioni e consente di risparmiare tempo e impegno. La procedura permette di condividere un dominio e le relative informazioni con altri utenti, consentendo in tal modo anche ad essi un notevole risparmio di tempo. È possibile importare un singolo dominio o un dominio composito contenente più domini singoli. Un file DQS contenente un singolo dominio include tutti i dati del dominio stesso tra cui i dati di proprietà, valori e regole, tranne le informazioni sui dati di riferimento con mapping. Un file DQS che contiene un dominio composito include tutti i dati di tale dominio, compresi i dati dei domini singoli contenuti al suo interno, nonché le proprietà, i valori, le relazioni e le regole CD del dominio composito stesso, tranne i dati di riferimento con mapping. Verranno importati sia i dati pubblicati che quelli non pubblicati.  
  
 Quando si importa un dominio, il nome del dominio corrisponde al nome del dominio esportato originalmente, a meno che il nome esista già, in qual caso DQS aggiungerà il suffisso "1" al nome. Ciò avviene qualora si importi un dominio composito contenente un dominio singolo con lo stesso nome di un dominio esistente.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per importare un dominio da un file DQS, è necessario avere già esportato un dominio singolo o composito (contenente più domini singoli) nel file DQS. Il file DQS deve contenere solo un dominio. È inoltre necessario avere creato e aperto una Knowledge Base in cui importare il dominio.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per importare un dominio da un file DQS è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Import"></a> Importazione di un dominio da un file DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Client Data Quality](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire una Knowledge Base nell'attività Gestione dominio.  
  
3.  Fare clic sull'icona **Importa dominio da file di dati** .  
  
4.  Nel **Importa da File di dati** la finestra di dialogo, passare alla cartella che si desidera importare il file, selezionare il file (con estensione DQS) e quindi fare clic su **aprire**.  
  
5.  Nella finestra di dialogo **Importa dominio** fare clic su **OK**.  
  
    > [!NOTE]  
    >  L'operazione di importazione riuscirà solo se il file DQS da importare contiene solo un singolo dominio o un dominio composito (contenente più domini).  
  
6.  Verificare che il dominio importato venga visualizzato nell'elenco **Domini** . Se è stato importato un dominio composito, verificare che sia il dominio composito che i singoli domini in esso contenuti siano visualizzati nell'elenco **Domini** .  
  
##  <a name="FollowUp"></a> Completamento: Dopo avere importato un dominio da un file DQS  
 Dopo avere importato un dominio da un file DQS, è possibile aggiungere informazioni al dominio o utilizzarlo per progetti di pulizia o di individuazione delle corrispondenze, secondo il contenuto del dominio. Per ulteriori informazioni, vedere [eseguire l'individuazione delle informazioni](../data-quality-services/perform-knowledge-discovery.md), [gestione di un dominio](../data-quality-services/managing-a-domain.md), [la gestione di un dominio composito](../data-quality-services/managing-a-composite-domain.md), [creare un criterio di corrispondenza](../data-quality-services/create-a-matching-policy.md), [la pulizia dei dati](../data-quality-services/data-cleansing.md), o [corrispondenza dei dati](../data-quality-services/data-matching.md).  
  
  