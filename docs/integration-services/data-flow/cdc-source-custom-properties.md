---
title: "Proprietà personalizzate dell'origine CDC | Documenti Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 106f7ecb0798682b26c806ea9c2d943524dd87d4
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source-custom-properties"></a>Proprietà personalizzate dell'origine CDC
  Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine CDC. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Description|  
|-------------------|---------------|-----------------|  
|Connessione|ADO.Net Connection|Connessione ADO.NET al database CDC di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'accesso alle tabelle delle modifiche.|  
|StateVariable|String|Variabile del pacchetto di stringhe SSIS che gestisce lo stato CDC dell'esecuzione CDC corrente.|  
|CdcProcessingMode|Integer (enumerazione)|Questa modalità determina il modo in cui viene gestita l'elaborazione. Le opzioni possibili sono **All**, **All with old values**, **Net**, **Net with update mask**e **Net with merge**.<br /><br /> Le modalità il cui nome inizia con All restituiscono tutte le modifiche, mentre quelle il cui nome inizia con Net restituiscono solo le modifiche delta.<br /><br /> Le tabelle senza una chiave primaria possono accettare solo i valori ALL.<br /><br /> **NET with Update Mask** aggiunge colonne booleane con il modello di nome **_ $\<nome colonna >\__Changed** che indicano le colonne modificate nella finestra corrente riga modificata.<br /><br /> Per altre informazioni sui valori per questa proprietà, vedere [Editor origine CDC &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).|  
|CaptureInstance|String|Nome dell'istanza di acquisizione CDC con la tabella CDC da leggere. Una tabella di origine acquisita può contenere una o due istanze acquisite per gestire la transizione senza problemi della definizione di tabella mediante modifiche dello schema. Se per la tabella di origine in corso di acquisizione sono definite più istanze di acquisizione, selezionare l'istanza di acquisizione che si desidera utilizzare a questo punto. Il nome di istanza di acquisizione predefinito per una tabella [schema]. [tabella] è \<schema > _\<tabella >, ma che i nomi delle istanze di acquisizione effettivi in uso potrebbero essere diversi. La tabella effettiva che viene letto dal è la tabella CDC **cdc.\< istanza di acquisizione > CT**.|  
|ReprocessingIndicator|Boolean|Valore che specifica se aggiungere la colonna **__$reprocessing** . Questa colonna di output speciale consente allo sviluppatore di SSIS di gestire gli errori di consistenza in modo diverso quando si utilizza l'intervallo di elaborazione iniziale.<br /><br /> Se il valore è **true**, viene aggiunta la colonna  **__$reprocessing** .<br /><br /> Il valore di questa colonna è **true** quando l'intervallo di elaborazione CDC si sovrappone all'intervallo di elaborazione iniziale (intervallo di LSN che corrisponde al periodo di caricamento iniziale) o quando un intervallo di elaborazione CDC viene rielaborato a causa di un errore in un'esecuzione precedente. Questa colonna indicatore consente agli sviluppatori di SSIS di gestire gli errori in modo diverso durante la rielaborazione delle modifiche. Azioni quali l'eliminazione di una riga non esistente e l'inserimento non riuscito su una chiave duplicata, ad esempio, possono essere ignorate.<br /><br /> Il valore predefinito è **false**.|  
|CommandTimeout|Valore intero|Questo valore indica il timeout (in secondi) da usare quando si comunica con il database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Questo valore viene utilizzato quando il tempo di risposta dal database è molto lento e il valore predefinito (30 secondi) non è sufficiente.|  
  
 Per altre informazioni sull'origine CDC, vedere [Origine CDC](../../integration-services/data-flow/cdc-source.md).  
  
  