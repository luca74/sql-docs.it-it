---
title: Riferimenti al linguaggio di Integration Services | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9fe4120f8a5dc93517e8eb35b13e7fe5252be6b6
ms.contentlocale: it-it
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-language-reference"></a>Guida di riferimento al linguaggio Integration Services
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In questa sezione viene descritta l'API [!INCLUDE[tsql](../includes/tsql-md.md)] per l'amministrazione di progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] distribuiti in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gli oggetti, le impostazioni e i dati operativi vengono archiviati in un database definito catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Il nome predefinito di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] catalogo è SSISDB. Tra gli oggetti archiviati nel catalogo sono inclusi progetti, pacchetti, parametri, ambienti e cronologia operativa.  
  
 Nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] i relativi dati vengono archiviati in tabelle interne che non sono visibili agli utenti. Tuttavia, vengono esposte le informazioni necessarie tramite un set di viste pubbliche su cui è possibile eseguire una query. Inoltre, è disponibile un set di stored procedure utilizzabili per eseguire attività comuni nel catalogo.  
  
 In genere gli oggetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nel catalogo vengono gestiti aprendo [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Tuttavia, è anche possibile utilizzare le viste del database e chiamare direttamente le stored procedure oppure scrivere codice personalizzato con cui chiamare l'API gestita. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e l'API gestita eseguono query sulle viste e chiamano le stored procedure descritte in questa sezione per eseguire molte delle rispettive attività.  
  
## <a name="in-this-section"></a>Argomenti della sezione  
 [Viste &#40; catalogo di Integration Services &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 Eseguire una query sulle viste per controllare gli oggetti, le impostazioni e i dati operativi di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Stored procedure &#40; catalogo di Integration Services &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 Chiamare le stored procedure per aggiungere, rimuovere o modificare oggetti e impostazioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Funzioni &#40;Catalogo di Integration Services&#41;](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 Chiamare le funzioni per l'amministrazione di progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
  