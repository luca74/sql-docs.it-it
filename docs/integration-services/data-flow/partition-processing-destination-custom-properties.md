---
title: "Proprietà personalizzate della destinazione elaborazione partizione | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a4ed16b65d8f6c7096551f7a55382e97213c9da
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="partition-processing-destination-custom-properties"></a>Proprietà personalizzate della destinazione elaborazione partizione
  La destinazione elaborazione partizione include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione elaborazione partizione. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|Stringa di connessione a un progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, valore che indica come gestire gli errori di chiave duplicata. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **IgnoreError** (0).|  
|KeyErrorAction|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, valore che indica come gestire gli errori di chiave. I valori possibili sono **ConvertToUnknown** (0) e **DiscardRecord** (1). Il valore predefinito della proprietà è **ConvertToUnknown** (0).|  
|KeyErrorLimit|Valore intero|Quando UseDefaultConfiguration è **False**, limite massimo consentito di errori di chiave.|  
|KeyErrorLimitAction|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica l'azione da eseguire quando viene raggiunto il **KeyErrorLimit** . I valori possibili sono **StopLogging** (1) e **StopProcessing** (0). Il valore predefinito di questa proprietà è **StopProcessing** (0).|  
|KeyErrorLogFile|String|Quando UseDefaultConfiguration è **False**, il percorso e il nome del file di log degli errori.|  
|KeyNotFound|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica come gestire gli errori di chiave mancanti. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **ReportAndContinue** (1).|  
|NullKeyConvertedToUnknown|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, valore che indica come gestire le chiavi Null convertite nel valore sconosciuto. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **IgnoreError** (0).|  
|NullKeyNotAllowed|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica come gestire i valori Null non consentiti. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **ReportAndContinue** (1).|  
|ProcessType|Integer (enumerazione)|Tipo di elaborazione della partizione utilizzata dalla trasformazione. I valori possibili sono **ProcessAdd** (1) (incrementale), **ProcessFull** (0) e **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Boolean|Valore che specifica se la trasformazione utilizza la configurazione degli errori predefinita. Se questa proprietà è **False**, la trasformazione usa i valori delle proprietà personalizzate di gestione degli errori elencate in questa tabella, incluse KeyDuplicate, KeyErrorAction e così via.|  
  
 L'input e le colonne di input della destinazione elaborazione partizione non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione elaborazione partizione](../../integration-services/data-flow/partition-processing-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
