---
title: Creare un progetto Data Quality | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.dqproject.newdqproject.f1
helpviewer_keywords:
- create,data quality project
- data quality project,create
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 585accdc7848b22001406dc46ff7bf2de7e83cdf
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2018
---
# <a name="create-a-data-quality-project"></a>Creare un progetto Data Quality
  In questo argomento viene descritto come creare un progetto Data Quality mediante il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Un progetto Data Quality viene utilizzato per eseguire l'attività di pulizia o di corrispondenza in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario disporre di una Knowledge Base pertinente da utilizzare nel progetto Data Quality per l'attività di pulizia e di corrispondenza.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per creare un progetto Data Quality, è necessario disporre del ruolo dqs_kb_editor o dqs_kb_operator nel database DQS_MAIN.  
  
##  <a name="Create"></a> Creare un progetto Data Quality  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Nuovo progetto Data Quality**.  
  
3.  Nella schermata **Nuovo progetto Data Quality** :  
  
    1.  Nella casella **Nome** digitare un nome per il nuovo progetto Data Quality.  
  
    2.  Nella casella **Descrizione** digitare una descrizione per il nuovo progetto Data Quality (facoltativo).  
  
    3.  Nell'elenco **Usa Knowledge Base** fare clic per selezionare una Knowledge Base da utilizzare per il progetto Data Quality. Nell'area **Dettagli Knowledge Base: <Nome_Knowledge_Base>** sul lato destro vengono visualizzati i nomi di dominio disponibili nella knowledge base selezionata.  
  
    4.  Nell'area **Seleziona attività** fare clic su un'attività che si desidera eseguire utilizzando questo progetto Data Quality:  
  
        -   **Pulizia**: selezionare questa attività per pulire i dati di origine.  
  
        -   **Corrispondenza**: selezionare questa attività per eseguire una corrispondenza. Questa attività è disponibile solo se la Knowledge Base selezionata per il progetto Data Quality contiene i criteri di corrispondenza.  
  
4.  Fare clic su **Crea** per creare un progetto Data Quality.  
  
##  <a name="FollowUp"></a> Completamento: fasi successive alla creazione di un progetto Data Quality  
 Dopo avere creato un progetto Data Quality, viene visualizzata una procedura guidata che è possibile utilizzare per eseguire l'attività selezionata: pulizia o corrispondenza. Per altre informazioni sulle attività di pulizia e corrispondenza, vedere [Pulizia dei dati](../data-quality-services/data-cleansing.md) e [Corrispondenza di dati](../data-quality-services/data-matching.md).  
  
  
