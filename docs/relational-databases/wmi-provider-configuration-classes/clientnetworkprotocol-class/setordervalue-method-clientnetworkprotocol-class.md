---
title: Metodo SetOrderValue (classe ClientNetworkProtocol) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SetOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26da8fd19277dd1170b811e4337785a3fb7557cd
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2018
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>Metodo SetOrderValue (classe ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Seleziona il protocollo con il valore dell'ordine specificato dall'elenco di protocolli del client.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## <a name="parts"></a>Parti  
 *oggetto*  
 Oggetto della [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal client di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Description|  
|---------------|-----------------|  
|*OrderValue*|Valore u**int32** che imposta il valore dell'ordine.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà-protocolli client (scheda ordine)](http://technet.microsoft.com/library/ms187884.aspx)  
  
  
