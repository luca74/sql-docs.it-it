---
title: Convalida (Master Data Services) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
caps.latest.revision: 12
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f442721e0e3d428b58e6bdd281af09193ebad867
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="validation-master-data-services"></a>Convalida (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], i dati sono convalidati per assicurare l'accuratezza. Una convalida viene eseguita automaticamente, mentre l'altra convalida è basata sulle regole business create dagli amministratori.  
  
## <a name="when-data-validation-occurs"></a>Quando viene eseguita la convalida dei dati  
 La convalida viene eseguita in momenti diversi ed è visualizzata in modo diverso nell'applicazione Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
|Tipo di convalida|Standard determinati da|Quando viene eseguita|Visualizzata nella interfaccia utente Web di Gestione dati master come|Visualizzata nel componente aggiuntivo per Excel come|I dati vengono salvati nel database MDS?|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|Convalida delle regole business|Un amministratore MDS|Automaticamente quando un utente aggiunge o modifica dati.<br /><br /> Manualmente quando un utente applica regole business.<br /><br /> Manualmente quando un amministratore nell'area funzionale **Gestione versioni** dell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] convalida una versione rispetto alle regole di business.|Errori di convalida|ValidationStatus|Sì|  
|Tipo di dati e convalida del contenuto|Un amministratore MDS, in caso di creazione di oggetti modello (ad esempio, la lunghezza di un attributo o il tipo di dati)|Automaticamente quando un utente aggiunge o modifica dati|Errori di input|InputStatus|No|  
|Tipo di dati e convalida del contenuto|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oppure [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Automaticamente quando un utente aggiunge o modifica dati|Errori di input|InputStatus|No|  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare regole business e pubblicarle, in modo che i dati vengano convalidati rispetto a tali regole.|[Creare e pubblicare una regola business &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Convalidare una versione di dati rispetto a regole business. Solo amministratori.|[Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|Convalidare un subset specifico di dati rispetto a regole business. Tutti gli utenti con l'autorizzazione per l'area funzionale **Visualizzatore** .|[Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Convalidare un subset specifico di dati rispetto a regole business. Tutti gli utenti con l'autorizzazione per l'area funzionale **Visualizzatore** e che usano [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].|[Applicare le regole di business &#40;componente aggiuntivo MDS per Excel&#41;](../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Regole business &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  