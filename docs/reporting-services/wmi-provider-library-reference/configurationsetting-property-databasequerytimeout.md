---
title: "Proprietà DatabaseQueryTimeout (MSReportServer_ConfigurationSetting WMI) | Documenti Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- DatabaseQueryTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 67505da58ea80c15c6029d849af594e63340e863
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-property---databasequerytimeout"></a>Proprietà ConfigurationSetting - DatabaseQueryTimeout
  Specifica il numero di secondi di attesa prima che il server di report presuma che il comando non sia riuscito e che sia necessaria una quantità di tempo troppo elevata per l'esecuzione. Il server di report calcola il tempo di esecuzione della query rispetto al catalogo SQL e non rispetto a un'origine dati per il report. Proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Oggetto **integer** non firmato a 32 bit che rappresenta il numero di secondi concessi per l'esecuzione della query.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  