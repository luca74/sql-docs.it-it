---
title: Creazione di programmi SMO | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: cd8d9fa33596bd200816c7d2e65213646c9e8344
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="creating-smo-programs"></a>Creazione di programmi SMO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Programmazione generale degli [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) oggetti include le aree comuni che condividono tutti gli oggetti, quali l'esecuzione di metodi, proprietà di impostazione e modifica delle raccolte.  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Connessione a un'istanza di SQL Server](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|Il programma SMO più semplice che stabilisce una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Vengono illustrate l'autenticazione di Windows e l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e vengono forniti esempi di connessione a un'istanza locale e a un'istanza remota di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Disconnessione da un'istanza di SQL Server](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|Programma che illustra come eseguire la disconnessione dall'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Chiamata di metodi](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|In questa sezione viene descritto l'approccio generale alla chiamata dei metodi. Viene illustrato l'utilizzo dei parametri e la gestione delle tabelle di dati restituite in un oggetto <xref:System.Data.DataTable>. Viene fornito un esempio di come chiamare un costruttore di oggetto e come chiamare il **Clone** metodo.|  
|[Impostazione delle proprietà - SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|In questa sezione viene illustrato come impostare diversi tipi di proprietà, come impostare e ottenere le proprietà degli oggetti e, attraverso gli esempi forniti, come impostare le proprietà dell'oggetto al momento della creazione e come  scorrere tutte le proprietà di un oggetto.|  
|[Uso delle raccolte](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|Vari programma che illustrano le tecniche utilizzate con le raccolte di oggetti. Viene spiegato come fare riferimento a un oggetto tramite le raccolte e, attraverso gli esempi forniti, come scorrere i membri di una raccolta.|  
|[Gestione degli eventi SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|In questa sezione viene descritto come impostare e gestire eventi in SMO e viene fornito un esempio su come impostare un gestore eventi e una sottoscrizione di eventi.|  
|[Gestione delle eccezioni SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|In questa sezione viene illustrato come intercettare le eccezioni in SMO attraverso esempi di intercettazioni e di visualizzazione di un'eccezione interna.|  
|[Uso dei tipi di dati](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|In questa sezione viene illustrato come utilizzare i diversi tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], come costruire un oggetto datatype con la specifica nel costruttore di oggetti e viene fornito un esempio di creazione di un oggetto datatype tramite il costruttore predefinito.|  
|[Uso di transazioni](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|In questa sezione viene illustrato come implementare l'elaborazione delle transazioni in un programma SMO e vengono forniti esempi di utilizzo delle transazioni in questo tipo di programmi.|  
|[Uso della modalità di acquisizione](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|In questa sezione viene illustrato come registrare l'output del programma SMO. Nell'esempio il programma SMO viene registrato sotto forma di istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] inviate all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per un'esecuzione successiva.|  
  
  