---
title: Descrizione XML del flusso di lavoro personalizzato (Master Data Services) | Documenti Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ca6f208bab4ed0b7932d3bd5f7e9a911b8b2c8af
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---xml-description"></a>Creare un flusso di lavoro personalizzato - descrizione XML
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] il metodo <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> viene chiamato da SQL Server MDS Workflow Integration Service all'avvio di un flusso di lavoro. Questo metodo riceve i metadati e i dati sull'elemento che ha attivato la regola business del flusso di lavoro come blocco di XML. Ad esempio di codice che implementa un gestore del flusso di lavoro, vedere [personalizzato del flusso di lavoro esempio &#40; Master Data Services &#41; ](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 Nell'esempio seguente viene illustrato il possibile aspetto del codice XML inviato al gestore del flusso di lavoro:  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 Nella tabella seguente vengono descritti alcuni dei tag contenuti nel codice XML:  
  
|Tag|Description|  
|---------|-----------------|  
|\<Tipo >|Il testo immesso nella **tipo flusso di lavoro** casella di testo in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] per identificare l'assembly del flusso di lavoro personalizzato da caricare.|  
|\<SendData >|Un valore booleano controllato dal **Includi dati membro nel messaggio** nella casella di controllo [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Il valore 1 indica che il \<MemberData > sezione non verrà inviati; in caso contrario il \<MemberData > sezione non viene inviata.|  
|< Server_URL >|Il testo immesso nella **sito flusso di lavoro** casella di testo in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|< Action_ID >|Il testo immesso nella **nome flusso di lavoro** casella di testo in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|\<MemberData >|Contiene i dati del membro che ha attivato l'azione del flusso di lavoro. Questo è incluso solo se il valore di \<SendData > è 1.|  
|\<Immettere*xxx*>|Questo set di tag contiene i metadati sulla creazione del membro, ad esempio il momento e l'autore della creazione.|  
|\<LastChg*xxx*>|Questo set di tag contiene i metadati sull'ultima modifica apportata al membro, ad esempio il momento e l'autore dell'esecuzione della modifica.|  
|\<Nome >|Primo attributo del membro modificato. Questo membro di esempio contiene solo gli attributi Name e Code.|  
|\<Codice >|Attributo successivo del membro modificato. Se il membro di esempio contiene più attributi, essi vengono specificati dopo questo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un flusso di lavoro personalizzato &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [Esempio di flusso di lavoro personalizzato &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  