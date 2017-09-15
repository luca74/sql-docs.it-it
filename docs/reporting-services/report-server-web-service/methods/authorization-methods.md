---
title: Metodi di autorizzazione | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], reports
- authorization [Reporting Services]
- reports [Reporting Services], security
- tasks [Reporting Services]
- roles [Reporting Services], methods
ms.assetid: 45e9cf2c-facf-4801-9482-c855403f42a8
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: eb327018c69059a27f7ff21a8f487f2a4eb6f306
ms.contentlocale: it-it
ms.lasthandoff: 08/12/2017

---
# <a name="authorization-methods"></a>Metodi di autorizzazione
  È possibile utilizzare questi metodi per gestire attività, ruoli e criteri nel server di report.  
  
|Metodo|Azione|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|Aggiunge un nuovo ruolo al database del server di report. Questo metodo può essere applicato solo in modalità nativa.|  
|<xref:ReportService2010.ReportingService2010.DeleteRole%2A>|Elimina un ruolo dal database del server di report. Questo metodo può essere applicato solo in modalità nativa.|  
|<xref:ReportService2010.ReportingService2010.GetPermissions%2A>|Restituisce le autorizzazioni utente associate a un particolare elemento nel database del server di report o in una raccolta di SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|Restituisce i criteri associati a un particolare elemento nel database del server di report o in una raccolta di SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|Restituisce le proprietà dei metadati dei ruoli e una raccolta di attività associate.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPermissions%2A>|Restituisce le autorizzazioni di sistema dell'utente. Questo metodo può essere applicato solo in modalità nativa.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|Restituisce i criteri di sistema, inclusi i gruppi e i ruoli ai quali sono associati. Questo metodo può essere applicato solo in modalità nativa.|  
|<xref:ReportService2010.ReportingService2010.InheritParentSecurity%2A>|Elimina i criteri associati a un particolare elemento nel database del server di report e imposta i criteri di sicurezza per l'elemento in modo che corrispondano a quelli dell'elemento padre.|  
|<xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>|Restituisce un valore booleano che indica se il protocollo Secure Socket Layer (SSL) è obbligatorio per l'utilizzo dell'endpoint <xref:ReportService2010>.|  
|<xref:ReportService2010.ReportingService2010.ListRoles%2A>|Restituisce i nomi e le descrizioni dei ruoli gestiti dal server di report.|  
|<xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>|Restituisce un elenco di metodi SOAP (Simple Object Access Protocol) nell'endpoint <xref:ReportExecution2005> che richiedono una connessione protetta quando vengono richiamati. Il **SecureConnectionLevel** impostazione del server di report viene utilizzata per determinare quali metodi vengono restituiti.|  
|<xref:ReportService2010.ReportingService2010.ListTasks%2A>|Restituisce le attività gestite dal server di report.|  
|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|Imposta i criteri associati a un elemento specificato.|  
|<xref:ReportService2010.ReportingService2010.SetRoleProperties%2A>|Imposta le proprietà dei metadati dei ruoli e associa un set di attività a un ruolo. Questo metodo può essere applicato solo in modalità nativa.|  
|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|Imposta i criteri di sistema che definiscono i gruppi e i ruoli associati. Questo metodo può essere applicato solo in modalità nativa.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di applicazioni mediante il servizio Web e .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servizio Web ReportServer](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Metodi del servizio Web ReportServer](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Riferimento tecnico &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  