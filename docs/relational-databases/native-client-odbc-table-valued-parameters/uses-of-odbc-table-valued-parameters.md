---
title: Utilizzi dei parametri con valori di tabella ODBC | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 050d0e33419b2f73fba8e5e7fd011d786fcb9f21
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2018
---
# <a name="uses-of-odbc-table-valued-parameters"></a>Utilizzi dei parametri con valori di tabella in ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In questo argomento vengono illustrati gli scenari utente principali relativi all'utilizzo di parametri con valori di tabella in ODBC:  
  
-   Parametro con valori di tabella con buffer a più righe completamente associati (invio di dati come TVP con tutti i valori in memoria)  
  
-   Parametro con valori di tabella con flusso di righe (invio di dati come TVP mediante data-at-execution)  
  
-   Recupero dei metadati del parametro con valori di tabella dal catalogo di sistema  
  
-   Recupero di metadati del parametro con valori di tabella per un'istruzione preparata  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>Parametro con valori di tabella con buffer a più righe completamente associati (invio di dati come TVP con tutti i valori in memoria)  
 Se utilizzato con buffer a più righe completamente associati, tutti i valori del parametro sono disponibili in memoria. È tipico, ad esempio, di una transazione OLTP nella quale i parametri con valori di tabella possono essere assemblati in una singola stored procedure. Senza parametri con valori di tabella, risulta necessario generare dinamicamente un batch complesso con più istruzioni o effettuare più chiamate al server.  
  
 Il parametro con valori di tabella stesso viene associato tramite [SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328) insieme agli altri parametri. Dopo avranno associati tutti i parametri, l'applicazione imposta l'attributo lo stato attivo del parametro, SQL_SOPT_SS_PARAM_FOCUS, su ogni parametro con valori di tabella e chiama la funzione SQLBindParameter per le colonne del parametro con valori di tabella.  
  
 Il tipo di server per un parametro con valori di tabella è un nuovo tipo specifico per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_SS_TABLE. Il tipo C dell'associazione per SQL_SS_TABLE deve essere sempre SQL_C_DEFAULT. Non vengono trasferiti dati per il parametro associato al parametro con valori di tabella; viene utilizzato per passare i metadati delle tabelle e per controllare il modo in cui passare i dati nelle colonne che costituiscono il parametro con valori di tabella.  
  
 La lunghezza del parametro con valori di tabella è impostata sul numero di righe inviate al server. Il *ColumnSize* parametro di SQLBindParameter per un parametro con valori di tabella specifica il numero massimo di righe che può essere inviato; rappresenta la dimensione della matrice dei buffer delle colonne. *ParameterValuePtr* è il buffer del parametro, per un parametro con valori di tabella in SQLBindParameter. *ParameterValuePtr* e l'identificatore associato *BufferLength* vengono utilizzati per passare il nome del tipo del parametro con valori di tabella quando necessario. Il nome del tipo non è necessario per le chiamate alle stored procedure, mentre è necessario per le istruzioni SQL.  
  
 Quando in una chiamata a SQLBindParameter viene specificato un nome di tipo di parametro con valori di tabella, deve sempre essere specificato come valore Unicode, anche in applicazioni che vengono compilate come applicazioni ANSI. Quando si specifica un nome di tipo di parametro con valori di tabella tramite SQLSetDescField, è possibile utilizzare un valore letterale conforme al modo in cui che l'applicazione viene compilata. In Gestione driver ODBC verrà eseguita la conversione Unicode necessaria.  
  
 I metadati per parametri con valori di tabella e le colonne di parametri con valori di tabella possono essere modificati singolarmente e in modo esplicito utilizzando SQLGetDescRec, SQLSetDescRec, SQLGetDescField e SQLSetDescField. Tuttavia, l'overload di SQLBindParameter è generalmente più comodo e non richiede l'accesso descrittore esplicita nella maggior parte dei casi. Questo approccio è coerenza con la definizione di SQLBindParameter per altri tipi di dati, ad eccezione del fatto che per un parametro con valori di tabella sono leggermente diversi campi di descrizione interessato.  
  
 Un'applicazione utilizza talvolta un parametro con valori di tabella con le istruzioni SQL dinamiche ed è necessario fornire il nome del tipo del parametro con valori di tabella. Se questo è il caso e il parametro con valori di tabella non è definito nello schema predefinito corrente per la connessione, è necessario impostare SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME utilizzando SQLSetDescField. Poiché le definizioni del tipo di tabella e i parametri con valori di tabella devono risiedere nello stesso database, SQL_CA_SS_TYPE_CATALOG_NAME non deve essere impostato se l'applicazione utilizza parametri con valori di tabella. In caso contrario, SQLSetDescField segnalerà un errore.  
  
 Codice di esempio per questo scenario è nella procedura `demo_fixed_TVP_binding` in [utilizzare parametri &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>Parametro con valori di tabella con flusso di righe (invio di dati come TVP mediante data-at-execution)  
 In questo scenario l'applicazione fornisce le righe al driver nel modo in cui vengono richieste, le quali vengono poi trasferite al server. In questo modo si evita di dovere memorizzare tutte le righe nel buffer di memoria. Tale condizione è rappresentativa negli scenari di inserimento/aggiornamento bulk. Le prestazioni dei parametri con valori di tabella sono a metà tra le matrici di parametri e la copia bulk. La programmazione dei parametri con valori di tabella è semplice quanto quella delle matrici di parametri, ma offre una maggiore flessibilità sul lato server.  
  
 Il parametro con valori di tabella e le relative colonne vengono associate come descritto nella sezione precedente, Parametro con valori di tabella con buffer a più righe completamente associati, impostando però l'indicatore della lunghezza del parametro con valori di tabella su SQL_DATA_AT_EXEC. Il driver risponde a SQLExecute o SQLExecuteDirect nel modo consueto per i parametri data-at-execution, ovvero restituendo SQL_NEED_DATA. Quando il driver è pronto per accettare i dati per un parametro con valori di tabella, SQLParamData restituisce il valore di *ParameterValuePtr* in SQLBindParameter.  
  
 Un'applicazione utilizza SQLPutData per un parametro con valori di tabella per indicare la disponibilità dei dati per le colonne che costituiscono parametri con valori di tabella. Quando viene chiamato SQLPutData per un parametro con valori di tabella, *DataPtr* deve essere sempre null e *StrLen_or_Ind* deve essere 0 o un numero minore o uguale alla dimensione della matrice specificata per valori di tabella buffer di parametri (il *ColumnSize* parametro di SQLBindParameter). 0 significa che non ci sono più righe per il parametro con valori di tabella e il driver procederà con l'elaborazione fino al successivo parametro effettivo della procedura. Quando *StrLen_or_Ind* è diverso da 0, il driver elaborerà le colonne che costituiscono il parametro con valori di tabella nello stesso modo come parametri associati al parametro non – con valori di tabella: ogni colonna di parametri con valori di tabella è possibile specificare i dati effettivi lunghezza, SQL_NULL_DATA, oppure è possibile specificare dati durante l'esecuzione tramite il buffer di lunghezza/indicatore. Colonna di parametri con valori di tabella i valori possono essere passati da chiamate ripetute a SQLPutData come di consueto quando deve essere passati in parti un carattere o un valore binario.  
  
 Una volta elaborate tutte le colonne del parametro con valori di tabella, il driver torna al parametro con valori di tabella per elaborare ulteriori righe di dati del parametro con valori di tabella. Pertanto, per i parametri con valori di tabella data-at-execution il driver non segue la solita analisi sequenziale dei parametri associati. Un parametro con valori di tabella associato verrà eseguito il polling fino a quando non viene chiamato SQLPutData con *StrLen_Or_IndPtr* uguale a 0, nel momento in cui il driver ignora le colonne di parametri con valori di tabella e si sposta al successivo parametro effettivo della stored procedura.  Quando SQLPutData passa un valore dell'indicatore maggiore o uguale a 1, il driver elabora le righe e colonne di parametri con valori di tabella in ordine sequenziale fino a quando non sono presenti valori per tutte le righe associate e le colonne. Dopodiché il driver torna al parametro con valori di tabella. Tra la ricezione di token per il parametro con valori di tabella da SQLParamData e SQLPutData (hstmt, NULL, n) di chiamata per un parametro con valori di tabella, l'applicazione deve impostare dati di colonna che costituiscono parametri con valori di tabella e l'indicatore del contenuto del buffer per il righe successive da passare al server.  
  
 Codice di esempio per questo scenario è nella routine `demo_variable_TVP_binding` in [utilizzare parametri &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>Recupero dei metadati del parametro con valori di tabella dal catalogo di sistema  
 Quando un'applicazione chiama SQLProcedureColumns per una routine con parametri con valori di tabella, DATA_TYPE viene restituito come SQL_SS_TABLE e TYPE_NAME è il nome del tipo di tabella per il parametro con valori di tabella. Due colonne aggiuntive vengono aggiunti al set di risultati restituito da SQLProcedureColumns: SS_TYPE_CATALOG_NAME restituisce il nome del catalogo in cui è definito il tipo di tabella del parametro con valori di tabella e SS_TYPE_SCHEMA_NAME restituisce il nome dello schema in cui il in cui è definito il tipo di tabella del parametro con valori di tabella. In conformità con la specifica ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME vengono visualizzati prima di tutte le colonne specifiche del driver che sono state aggiunte nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dopo tutte le colonne richieste da ODBC stesso.  
  
 Le nuove colonne verranno popolate non solo per i parametri con valori di tabella, ma anche per i parametri del tipo CLR definito dall'utente. Le colonne esistenti dello schema e del catalogo dei parametri UDT verranno ancora popolate, ma la disponibilità di colonne comuni per lo schema e il catalogo da utilizzare per i tipi di dati semplificherà in futuro lo sviluppo di applicazioni. Notare che le raccolte di XML Schema sono piuttosto diverse e non sono incluse in questa modifica.  
  
 Un'applicazione utilizza SQLTables per determinare i nomi dei tipi di tabella esattamente come che avviene per le tabelle persistenti, tabelle di sistema e viste. Viene introdotto un nuovo tipo di tabella, TABLE TYPE, per consentire a un'applicazione di identificare i tipi di tabella associati ai parametri con valori di tabella. I tipi di tabella e le tabelle normali utilizzano spazi dei nomi diversi. È pertanto possibile utilizzare lo stesso nome per un tipo di tabella e una tabella effettiva. A tale scopo è stato introdotto un nuovo attributo dell'istruzione, SQL_SOPT_SS_NAME_SCOPE. Questo attributo specifica se SQLTables e altre funzioni di catalogo che accettano un nome di tabella come parametro devono interpretare il nome della tabella come nome di una tabella effettiva o il nome di un tipo di tabella.  
  
 Un'applicazione utilizza SQLColumns per determinare le colonne per un tipo di tabella nello stesso modo delle tabelle persistenti, ma è necessario prima impostare SQL_SOPT_SS_NAME_SCOPE per indicare che funziona con i tipi di tabella anziché le tabelle effettive. SQLPrimaryKeys utilizzabile anche con i tipi di tabella, utilizzando di nuovo SQL_SOPT_SS_NAME_SCOPE.  
  
 Codice di esempio per questo scenario è nella routine `demo_metadata_from_catalog_APIs` in [utilizzare parametri &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>Recupero di metadati del parametro con valori di tabella per un'istruzione preparata  
 In questo scenario, un'applicazione utilizza SQLNumParameters e SQLDescribeParam per recuperare i metadati per i parametri con valori di tabella.  
  
 Il campo IPD SQL_CA_SS_TYPE_NAME viene utilizzato per recuperare il nome del tipo per il parametro con valori di tabella. I campi IPD SQL_CA_SS_TYPE_SCHEMA_NAME e SQL_CA_SS_TYPE_CATALOG_NAME vengono utilizzati per recuperare rispettivamente il catalogo e lo schema.  
  
 Le definizioni del tipo di tabella e i parametri con valori di tabella devono essere nello stesso database. SQLSetDescField segnalerà un errore se un'applicazione imposta SQL_CA_SS_TYPE_CATALOG_NAME quando si utilizzano parametri con valori di tabella.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME possono inoltre essere utilizzati per recuperare il catalogo e lo schema associati ai parametri del tipo CLR definito dall'utente. SQL_CA_SS_TYPE_CATALOG_NAME and SQL_CA_SS_TYPE_SCHEMA_NAME sono le alternative agli attributi esistenti specifici del tipo per il catalogo e lo schema per i tipi CLR UDT.  
  
 Un'applicazione utilizza SQLColumns per recuperare i metadati della colonna per un parametro con valori di tabella in questo scenario, in quanto SQLDescribeParam restituisce i metadati per le colonne di una colonna di parametri con valori di tabella.  
  
 Codice di esempio per questo caso di utilizzo è nella routine `demo_metadata_from_prepared_statement` in [utilizzare parametri &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Table-Valued parametri &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
