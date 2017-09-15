---
title: Origine OData | Documenti Microsoft
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 1e0ef2b7cca9509a58aeadca3903e8aec3b7b9b9
ms.contentlocale: it-it
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source"></a>Origine OData
Usare il componente di origine OData in un pacchetto SSIS per utilizzare i dati da un servizio Protocollo OData (Open Data). Il componente supporta i protocolli OData v3 e v4.  
  
-   Per il protocollo OData V3, il componente supporta i formati di dati ATOM e JSON.  
  
-   Per il protocollo OData V4, il componente supporta il formato dati JSON.  

L'origine OData include il supporto per le origini dati seguenti:
-   Microsoft Dynamics AX Online e Microsoft Dynamics CRM Online
-   Elenchi di SharePoint. Per visualizzare tutti gli elenchi in un server SharePoint, utilizzare il seguente URL: http://\<server > / _vti_bin/ListData.svc. Per ulteriori informazioni sulle convenzioni per l'URL di SharePoint, vedere la pagina relativa all' [interfaccia REST di SharePoint Foundation](http://msdn.microsoft.com/library/ff521587.aspx).
  
## <a name="odata-format-and-performance"></a>Formato OData e prestazioni
 La maggior parte dei servizi OData possono restituire risultati in più formati. È possibile specificare il formato del set di risultati tramite l'utilizzo di `$format` opzione di query. I formati quali JSON e JSON Light sono più efficienti di ATOM o XML e possono garantire prestazioni migliori quando si trasferiscono grandi quantità di dati. Nella tabella seguente vengono forniti i risultati dei test di esempio. Come si può notare, si verifica un miglioramento delle prestazioni del 30-53% quando si passa dal formato ATOM a JSON e un miglioramento del 67% quando si passa da ATOM al nuovo formato JSON Light, disponibile in WCF Data Services 5.1.  
  
|Righe|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 secondi|74 secondi|68 secondi|  
|1000000|1110 secondi|853 secondi|665 secondi|  
  
## <a name="related-topics-in-this-section"></a>Argomenti correlati in questa sezione  
  
-   [Esercitazione: uso dell'origine OData](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Modificare la query di origine OData in fase di esecuzione](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Proprietà dell'origine OData](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>Editor origine OData (pagina Connessione)
  Usare la pagina **Connessione** della finestra di dialogo **Editor origine OData** per selezionare la gestione connessione OData per l'origine OData. In questa pagina è inoltre possibile specificare una raccolta o un percorso della risorsa, nonché tutte le opzioni query per scegliere i dati che devono essere recuperati dall'origine OData. 
  
### <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione OData**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 Dopo aver selezionato o creato una gestione connessione, la finestra di dialogo mostra la versione del protocollo OData che la gestione connessione sta usando.  
  
 **Nuova**  
 Creare una nuova gestione connessione usando la finestra di dialogo **Editor gestione connessione OData** .  
  
 **Usa percorso risorsa o raccolta**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Description|  
|------------|-----------------|  
|Collection|Recuperare i dati dall'origine OData utilizzando il nome di una raccolta.|  
|Percorso risorsa|Recuperare i dati dall'origine OData utilizzando un percorso della risorsa.|  
  
 **Opzioni query**  
 Specificare le opzioni per la query. Esempio: `$top=5` 
  
 **URL feed**  
 Consente di visualizzare le proprietà di sola lettura in base alle opzioni selezionate nella finestra di dialogo URL del feed.  
  
 **Anteprima**  
 Vengono visualizzati in anteprima i risultati tramite la finestra di dialogo **Anteprima** . L'**anteprima** supporta la visualizzazione di un massimo di 20 righe.  
  
### <a name="dynamic-options"></a>Opzioni dinamiche  
  
#### <a name="use-collection-or-resource-path--collection"></a>Usa percorso risorsa o raccolta = Raccolta  
 **Collection**  
 Selezionare una raccolta dall'elenco a discesa.  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>Usa percorso risorsa o raccolta = Percorso risorsa  
 **Resource path**  
 Digitare un percorso della risorsa. Ad esempio: Dipendenti  
  
## <a name="odata-source-editor-columns-page"></a>Editor origine OData (pagina Colonne)
  Usare la pagina **Colonne** della finestra di dialogo **Editor origine OData** per selezionare le colonne esterne (di origine) da includere nell'output ed eseguirne il mapping alle colonne di output.  
  
### <a name="options"></a>Opzioni  
 **Colonne esterne disponibili**  
 Viene visualizzato l'elenco delle colonne di origine disponibili nell'origine dati. Utilizzare le caselle di controllo nell'elenco per aggiungere colonne alla tabella, o rimuoverne, nella parte inferiore della pagina. Le colonne selezionate vengono aggiunte all'output.  
  
 **Colonna esterna**  
 Vengono visualizzate le colonne di origine selezionate per essere incluse nell'output.  
  
 **Colonna di output**  
 Consente di specificare un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
## <a name="odata-source-editor-error-output-page"></a>Editor origine OData (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **Editor origine OData** per selezionare le opzioni di gestione degli errori e impostare le proprietà delle colonne di output degli errori.  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Vengono visualizzate le colonne esterne (di origine) selezionate nella pagina **Gestione connessione** della finestra di dialogo **Editor origine OData** .  
  
 **Errore**  
 Consente di specificare l'azione da eseguire in caso di errori, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Argomenti correlati:** [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Troncamento**  
 Consente di specificare l'azione da eseguire in caso di troncamenti, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Description**  
 Consente di visualizzare la descrizione dell'errore.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di specificare l'azione che dovrà interessare tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione connessione OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  