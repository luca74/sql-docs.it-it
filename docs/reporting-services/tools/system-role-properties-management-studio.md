---
title: "Proprietà ruolo del sistema (Management Studio) | Documenti Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68038228fd6fb7b2af8dd6f1bb5ae50b7f63daac
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="system-role-properties-management-studio"></a>Proprietà ruolo a livello di sistema (Management Studio)
  La pagina Ruoli a livello di sistema consente di visualizzare le definizioni di ruolo a livello di sistema attualmente definite per il server di report. Una definizione di ruolo a livello di sistema contiene una raccolta denominata di attività eseguite in relazione all'intero sito, anziché a un singolo elemento. Le definizioni di ruolo vengono assegnate a un utente o a gruppi per creare un'assegnazione di ruolo. Le attività indicate nella definizione di ruolo specificano le operazioni consentite per un utente o un gruppo.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]sono disponibili due predefinite definizioni di ruolo di sistema: **amministratore di sistema** e **utente sistema**. Tali definizioni di ruolo possono essere personalizzate modificando l'elenco di attività oppure è possibile creare nuovi ruoli a livello di sistema per supportare combinazioni di attività diverse. Le modifiche apportate a una definizione di ruolo vengono propagate a tutte le assegnazioni di ruolo che includono tale definizione.  
  
> [!NOTE]  
>  Le assegnazioni di ruolo a livello di sistema vengono utilizzate solo in un server di report in esecuzione in modalità nativa. Se il server di report è configurato per l'integrazione con SharePoint, questa pagina non è disponibile.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare il nome della definizione di ruolo a livello di sistema.  
  
 **Description**  
 Consente di visualizzare una descrizione della definizione di ruolo a livello di sistema. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]la descrizione viene visualizzata solo in questa pagina. Gli utenti che visualizzano questo elemento tramite Gestione report potrebbero vedere questa descrizione durante l'esplorazione della gerarchia di cartelle.  
  
 **Attività**  
 Elenca tutte le attività di sistema che è possibile selezionare per la definizione di ruolo. È possibile aggiungere o rimuovere elementi dall'elenco di attività predefinite per specificare il modo in cui gli utenti accedono a un determinato elemento tramite questo ruolo. Non è possibile creare nuove attività, né modificare quelle esistenti.  
  
 **Description**  
 Offre informazioni su ogni attività. Non è possibile modificare le descrizioni delle attività.  
  
## <a name="see-also"></a>Vedere anche  
 [Server di report in Management Studio F1 Help](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Attività a livello di sistema](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)   
 [Attività e autorizzazioni](../../reporting-services/security/tasks-and-permissions.md)   
 [Ruoli predefiniti](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  