---
title: 'Esercitazione: Ottimizzazione guidata motore di Database | Documenti Microsoft'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
- tutorials [Database Engine Tuning Advisor]
ms.assetid: 3b54cbbe-d8c6-424d-92f1-aa58179f4da8
caps.latest.revision: "38"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0c6068064e47e571f143070bfd853c6df4e913d4
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="tutorial-database-engine-tuning-advisor"></a>Esercitazione: Strumento Ottimizzazione guidata motore di database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Benvenuti nell'esercitazione di ottimizzazione guidata motore di Database. Ottimizzazione guidata motore di database che esamina il modo in cui vengono elaborate le query nei database specificati e offre indicazioni su come migliorare le prestazioni di elaborazione attraverso la modifica delle strutture di database, ad esempio indici, viste indicizzate e partizionamento.  
  
Ottimizzazione guidata motore di database ha due interfacce utente, vale a dire un'interfaccia utente grafica (GUI) e l'utilità del prompt dei comandi **dta** . L'interfaccia utente grafica consente di visualizzare rapidamente i risultati delle sessioni di ottimizzazione, mentre con l'utilità **dta** è possibile incorporare con semplicità la funzionalità dello strumento Ottimizzazione guidata motore di database in script per l'ottimizzazione automatica. Lo strumento Ottimizzazione guidata motore di database, inoltre, può utilizzare input in formato XML, che garantisce un maggiore controllo sul processo di ottimizzazione.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
In questa esercitazione verrà illustrato come navigare nell'interfaccia utente grafica dello strumento Ottimizzazione guidata motore di database ed eseguire alcune semplici attività usando sia la GUI che l'utilità **dta** . Questa esercitazione contiene le lezioni seguenti:  
  
[Lezione 1: Navigazione di base in Ottimizzazione guidata motore di Database](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
In questa lezione sarà possibile acquisire familiarità con la GUI dello strumento Ottimizzazione guidata motore di database e ottenere informazioni su come impostare il layout e le opzioni di visualizzazione.  
  
[Lezione 2: Utilizzo di ottimizzazione guidata motore di Database](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
In questa lezione verranno descritte le procedure per eseguire alcune semplici attività di ottimizzazione utilizzando la GUI dello strumento Ottimizzazione guidata motore di database.  
  
[Lezione 3: Utilizzo dell'utilità del prompt dei comandi dta](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
In questa lezione verranno descritte le procedure per avviare l'utilità del prompt dei comandi **dta** e per eseguire alcune semplici comandi per l'ottimizzazione.  
  
## <a name="requirements"></a>Requisiti  
Questa esercitazione è destinata agli amministratori di database che non hanno familiarità con l'interfaccia utente grafica dello strumento Ottimizzazione guidata motore di database o con l'utilità del prompt dei comandi **dta** , ma che hanno tuttavia esperienza in merito ai concetti e alle strutture relativi ai database, quali indici e viste indicizzate.  
  
È necessario installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o una versione successiva, con i database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database di esempio, vedere la pagina relativa all' [installazione dei database di esempio e degli esempi di SQL Server](http://sqlserversamples.codeplex.com).  
  
## <a name="after-you-finish-this-tutorial"></a>Al termine di questa esercitazione  
Al termine di questa esercitazione, per ulteriori informazioni sullo strumento Ottimizzazione guidata motore di database, è possibile consultare gli argomenti seguenti:  
  
-   [Ottimizzazione guidata motore di database](../../relational-databases/performance/database-engine-tuning-advisor.md) per le descrizioni sull'uso di questo strumento in determinate attività.  
  
-   [Utilità dta](../../tools/dta/dta-utility.md) per materiale di riferimento sull'utilità del prompt dei comandi e sul file XML facoltativo disponibile per usare l'utilità.  
  
## <a name="next-lesson"></a>Lezione successiva  
[Lezione 1: Navigazione di base in Ottimizzazione guidata motore di Database](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
  
  
  
