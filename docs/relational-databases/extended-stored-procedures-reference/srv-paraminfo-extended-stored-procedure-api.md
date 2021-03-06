---
title: srv_paraminfo (API Stored procedure estesa) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- srv_paraminfo
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16ca2d41922461768b8edba1e12724e4bc852b15
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="srvparaminfo-extended-stored-procedure-api"></a>srv_paraminfo (API Stored procedure estesa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] In alternativa, usare l'integrazione con CLR.  
  
 Restituisce informazioni su un parametro. Questa funzione sostituisce le funzioni seguenti: [srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md), [srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md), [srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md) e [srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md). **srv_paraminfo** supporta i tipi di dati in [Tipi di dati](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md) e i dati di lunghezza zero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_paraminfo (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbType  
,  
ULONG *  
pcbMaxLen  
,  
ULONG *  
pcbActualLen  
,  
BYTE *  
pbData  
,  
BOOL *  
pfNull  
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Handle per una connessione client.  
  
 *n*  
 Numero ordinale del parametro da impostare. Il primo parametro è 1.  
  
 *pbType*  
 Tipo di dati del parametro.  
  
 *pcbMaxLen*  
 Indicatore di misura relativo alla lunghezza massima del parametro.  
  
 *pcbActualLen*  
 Indicatore di misura relativo alla lunghezza effettiva del parametro. Il valore 0 (\**pcbActualLen* == 0) indica dati di lunghezza zero se **pfNull* è impostato su FALSE.  
  
 *pbData*  
 Puntatore al buffer per i dati di parametro. Se *pbData* non è NULL, l'API Stored procedure estesa scrive \**pcbActualLen* byte di dati in \**pbData*. Se *pbData* è NULL, viene scritto alcun dato per \**pbData* ma la funzione restituisce \**pbType*, \**pcbMaxLen*, \**pcbActualLen*, e **pfNull*. La memoria per questo buffer deve essere gestita dall'applicazione.  
  
 *pfNull*  
 Puntatore a un flag null. **pfNull* viene impostato su TRUE se il valore del parametro è NULL.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Se le informazioni sul parametro vengono ottenute correttamente, viene restituito SUCCEED; in caso contrario, FAIL. Viene restituito FAIL se non esiste una stored procedure remota corrente e in assenza del parametro della stored procedure remota in posizione *n*.  
  
## <a name="remarks"></a>Osservazioni  
 **Nota sulla sicurezza** È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento per i programmatori delle stored procedure estese](../../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
  
  
