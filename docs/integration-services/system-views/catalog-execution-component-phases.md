---
title: Catalog. execution_component_phases | Documenti Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: b3459ce6d7e9eb0b9580ffa54e3b87e16f3e8fb0
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Visualizza il tempo trascorso da un componente del flusso di dati in ogni fase di esecuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|Identificatore univoco (ID) della fase.|  
|execution_id|**bigint**|ID univoco per l'istanza di esecuzione.|  
|package_name|**nvarchar (260)**|Nome del primo pacchetto avviato durante l'esecuzione.|  
|task_name|**nvarchar(4000)**|Nome dell'attività del flusso di dati.|  
|subcomponent_name|**nvarchar(4000)**|Nome del componente del flusso di dati.|  
|fase|**nvarchar(128)**|Nome della fase di esecuzione.|  
|start_time|**DateTimeOffset(7)**|Ora di inizio della fase.|  
|end_time|**DateTimeOffset(7)**|Ora di fine della fase.|  
|execution_path|**nvarchar(max)**|Percorso di esecuzione dell'attività del flusso di dati.|  
  
## <a name="remarks"></a>Osservazioni  
 In questa vista viene visualizzata una riga per ogni fase di esecuzione di un componente del flusso di dati, ad esempio Convalida, Pre-esecuzione, Post-esecuzione, PrimeOutput e ProcessInput. In ogni riga viene visualizzata l'ora di inizio e di fine per una fase di esecuzione specifica.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa la vista Catalog. execution_component_phases per calcolare la quantità totale di tempo che un pacchetto specifico in esecuzione in tutte le fasi (**active_time**) e il tempo totale trascorso per il pacchetto (**total_time**).  
  
> [!WARNING]  
>  Nella vista catalog.execution_component_phases vengono fornite queste informazioni se il livello di registrazione dell'esecuzione del pacchetto è impostato su Prestazioni o Dettagliato. Per altre informazioni, vedere [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
```  
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per l'istanza di esecuzione  
  
-   L'appartenenza al **ssis_admin** ruolo del database  
  
-   L'appartenenza al **sysadmin** ruolo del server  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  