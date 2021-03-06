---
title: Funzione SQLBulkOperations | Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1872238d5e017ef8b6bd3fbfb2dc185051fc3557
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="sqlbulkoperations-function"></a>Funzione SQLBulkOperations
**Conformità**  
 Introdotta: versione ODBC 3.0 aderenza: ODBC  
  
 **Riepilogo**  
 **SQLBulkOperations** esegue le operazioni di inserimento bulk e segnalibro bulk operazioni, incluso l'aggiornamento, eliminazione e il recupero dal segnalibro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
 *Operazione*  
 [Input] Operazione da eseguire:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Per ulteriori informazioni, vedere "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLBulkOperations** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di Impostato su SQL_HANDLE_STMT e *gestire* di *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLBulkOperations** e illustra ognuno nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver . Il codice restituito associato a ogni valore SQLSTATE è SQL_ERROR, se non diversamente specificato.  
  
 Per tutti questi SQLSTATE restituiti SQL_SUCCESS_WITH_INFO o SQL_ERROR (eccetto SQLSTATE 01xxx), viene restituito SQL_SUCCESS_WITH_INFO, se si verifica un errore in uno o più, ma non tutte le righe di un'operazione su più righe e viene restituito SQL_ERROR se si verifica un errore in un riga singola operazione.  
  
|SQLSTATE|Errore|Description|  
|--------------|-----------|-----------------|  
|01000|Avviso generico.|Messaggio informativo specifici del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Troncamento a destra dei dati stringa|Il *operazione* argomento è stato SQL_FETCH_BY_BOOKMARK e stringa o dati binari restituiti per una o più colonne con un tipo di dati SQL_C_CHAR o SQL_C_BINARY ha comportato il troncamento di un carattere non vuoto o dati binari non NULL.|  
|01S01|Errore alla riga|Il *operazione* argomento era SQL_ADD e si è verificato un errore in uno o più righe durante l'operazione, ma almeno una riga è stata aggiunta correttamente. (Funzione restituisce SQL_SUCCESS_WITH_INFO).<br /><br /> (Questo errore viene generato solo quando un'applicazione sta utilizzando un'API ODBC 2. *x* driver.)|  
|01S07|Troncamento frazionario.|Il *operazione* argomento era SQL_FETCH_BY_BOOKMARK, il tipo di dati del buffer di applicazione non è stata SQL_C_CHAR o SQL_C_BINARY e i dati restituiti al buffer dell'applicazione per una o più colonne è stati troncati. (Per i tipi di dati C numerici, la parte frazionaria del numero è stata troncata. Per ora, timestamp e tipi di dati di intervallo C che contengono un componente di ora, la parte frazionaria del tempo è stata troncata.)<br /><br /> (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|07006|Violazione dell'attributo del tipo di dati|Il *operazione* argomento è stato SQL_FETCH_BY_BOOKMARK e non è possibile convertire il valore di dati di una colonna nel set di risultati per tipo di dati specificato per il *TargetType* argomento nella chiamata a **SQLBindCol**.<br /><br /> Il *operazione* argomento è stato SQL_UPDATE_BY_BOOKMARK o SQL_ADD e non è possibile convertire il valore dei dati nei buffer di applicazione per il tipo di dati di una colonna nel set di risultati.|  
|07009|Indice del descrittore non valido|L'argomento *operazione* era SQL_ADD e una colonna è stata associata con un numero di colonne maggiore del numero di colonne nel set di risultati.|  
|21S02|Il grado della tabella derivata non corrisponde all'elenco di colonne|L'argomento *operazione* stato SQL_UPDATE_BY_BOOKMARK; e non le colonne aggiornabili perché sono state tutte le colonne non associate o sola lettura, o il valore nel buffer di lunghezza/indicatore associato è stato SQL_COLUMN_IGNORE.|  
|22001|Troncamento a destra dei dati stringa|L'assegnazione di un carattere o un valore binario a una colonna nel set di risultati ha restituito il troncamento di non vuoto (per i caratteri) o non null (per i dati binari) caratteri o byte.|  
|22003|Valore numerico non compreso nell'intervallo|Il *operazione* argomento è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'assegnazione di un valore numerico a una colonna nel set di risultati ha causato la parte intera (in contrapposizione frazionari) del numero da troncare.<br /><br /> L'argomento *operazione* era SQL_FETCH_BY_BOOKMARK e restituire il valore numerico per uno o più colonne associate avrebbe causato una perdita di cifre significative.|  
|22007|Formato di datetime non valido|Il *operazione* argomento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK, e l'assegnazione di un valore date o timestamp a una colonna nel set di risultati ha causato l'anno, mese o campo giorno sia compreso nell'intervallo.<br /><br /> L'argomento *operazione* era SQL_FETCH_BY_BOOKMARK e restituire il valore di date o timestamp per una o più colonne associate avrebbe causato l'anno, mese o campo giorno sia compreso nell'intervallo.|  
|22008|Overflow del campo Data/ora|Il *operazione* argomento è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e le prestazioni di datetime aritmetici sui dati inviati a una colonna nel set di risultati ha un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) il risultato che non rientrano nell'intervallo consentito di valori per il campo o non validi in base alle regole di naturale del calendario gregoriano per date e ore.<br /><br /> Il *operazione* argomento è stato SQL_FETCH_BY_BOOKMARK e le prestazioni di operazioni aritmetiche sui dati recuperati dal set di risultati datetime ha comportato un campo datetime (anno, mese, giorno, ora, minuto o secondo campo) del risultato che non rientrano nell'intervallo consentito di valori per il campo o non sono validi in base alle regole di naturale del calendario gregoriano per date e ore.|  
|22015|Overflow del campo intervallo|Il *operazione* argomento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK, e l'assegnazione di un numerico esatto o il tipo di intervallo C a un intervallo di tipo di dati SQL ha causato una perdita di cifre significative.<br /><br /> Il *operazione* argomento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; quando si assegna a un intervallo di tipo SQL, si è verificato alcuna rappresentazione del valore di tipo C nell'intervallo di tipo SQL.<br /><br /> Il *operazione* argomento è stato SQL_FETCH_BY_BOOKMARK e l'assegnazione da un numerico esatto o l'intervallo di tipo SQL a un tipo di intervallo C ha causato una perdita di cifre significative nel campo iniziale.<br /><br /> Il *operazione* argomento SQL_FETCH_BY_BOOKMARK, quando si assegna a un tipo di intervallo C, si è verificato alcun rappresentazione del valore di tipo SQL nel tipo di intervallo C.|  
|22018|Valore di carattere non valido per la specifica del cast|Il *operazione* argomento è stato SQL_FETCH_BY_BOOKMARK; il tipo C è stato un numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo SQL della colonna è un tipo di dati character; e il valore nella colonna non è valido valore letterale di tipo C associato.<br /><br /> L'argomento *operazione* era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; il tipo SQL è un numerico esatto o approssimativo, un valore datetime o un tipo di dati di intervallo; il tipo C è SQL_C_CHAR; e il valore nella colonna non è un valore letterale valido del tipo SQL associato.|  
|23000|Violazione del vincolo di integrità|Il *operazione* argomento è stato SQL_ADD, SQL_DELETE_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK e violato un vincolo di integrità.<br /><br /> Il *operazione* argomento era SQL_ADD, e una colonna che non è stata associata viene definita come non NULL e prevede alcun valore predefinito.<br /><br /> Il *operazione* SQL_ADD, la lunghezza specificata nel limite è stato argomento *StrLen_or_IndPtr* il buffer è SQL_COLUMN_IGNORE e la colonna non è un valore predefinito.|  
|24000|Stato del cursore non valido|Il *StatementHandle* è stato eseguito, ma è stato associato alcun set di risultati di *StatementHandle*.|  
|40001|Errore di serializzazione.|La transazione viene annullata a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento delle istruzioni sconosciuto|Impossibile stabilire la connessione associata durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|42000|Sintassi o violazione di accesso|Il driver è stato in grado di bloccare la riga in base alle esigenze per eseguire l'operazione richiesta nel *operazione* argomento.|  
|44000|Violazione della clausola WITH CHECK OPTION|Il *operazione* argomento è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'inserimento o aggiornamento è stato eseguito su una tabella visualizzata (o una tabella derivata dalla tabella visualizzata) che è stato creato specificando **WITH CHECK OPTION**, in modo che uno o più righe interessate dall'inserimento o aggiornamento non sarà più possibile presente nella tabella visualizzata.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. La funzione è stata chiamata e prima ha completato l'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle*. Quindi la funzione è stata chiamata nuovamente sul *StatementHandle*.<br /><br /> La funzione è stata chiamata e prima ha completato l'esecuzione, **SQLCancel** o **SQLCancelHandle** è stato chiamato sul *StatementHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza (funzione)|(DM) a cui è stata chiamata per l'handle di connessione associata a una funzione in modo asincrono in esecuzione il *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLBulkOperations** funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima che i dati sono stati recuperati per tutti i parametri con flusso.<br /><br /> (DM) specificato *StatementHandle* non è stato eseguito. La funzione è stata chiamata senza chiamare prima il metodo **SQLExecDirect**, **SQLExecute**, o una funzione di catalogo.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione (non è presente uno) di *StatementHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLSetPos** è stato chiamato per il *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima che sono stati inviati dati per tutti i parametri data-at-execution o colonne.<br /><br /> (DM) il driver non è un'API ODBC 2. *x* driver, e **SQLBulkOperations** è stato chiamato per un *StatementHandle* prima **SQLFetchScroll** o **SQLFetch**  è stato chiamato.<br /><br /> (DM) **SQLBulkOperations** è stato chiamato dopo **SQLExtendedFetch** è stato chiamato sul *StatementHandle*.|  
|HY011|Impossibile impostare l'attributo ora|(DM) il driver non è un'API ODBC 2. *x* driver e l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR è stata impostata tra le chiamate a **SQLFetch** o **SQLFetchScroll** e **SQLBulkOperations** .|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché gli oggetti di memoria sottostante non è accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza di stringa o di buffer non valida|Il *operazione* argomento è stato SQL_ADD o SQL_UPDATE_BY_BOOKMARK; un valore di dati non è un puntatore null; è stato il tipo di dati C SQL_C_BINARY o SQL_C_CHAR; e il valore di lunghezza di colonna è minore di 0, ma non uguale a SQL_DATA_AT_EXEC , SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA, o minore o uguale a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Il valore in un buffer di lunghezza/indicatore era SQL_DATA_AT_EXEC; il tipo SQL non SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo di dati specifici dell'origine dati di tipo long; e il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** è "Y".<br /><br /> Il *operazione* argomento era SQL_ADD, l'attributo di istruzione SQL_ATTR_USE_BOOKMARK è stato impostato su SQL_UB_VARIABLE e colonna 0 è stata associata a un buffer, la cui lunghezza non è uguale alla lunghezza massima per il segnalibro per questo set di risultati. (Questa lunghezza è disponibile nel campo SQL_DESC_OCTET_LENGTH di implementazione e può essere ottenuta chiamando **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY092|Identificatore di attributo non valido|(DM) il valore specificato per il *operazione* argomento non valido.<br /><br /> Il *operazione* argomento è stato SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK, e l'attributo di istruzione SQL_ATTR_CONCURRENCY era impostato su SQL_CONCUR_READ_ONLY.<br /><br /> Il *operazione* argomento è stato SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK e la colonna del segnalibro non è stata associata o l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS è stato impostato su SQL_UB_OFF.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettersi e sono consentite funzioni di sola lettura.|(DM) per ulteriori informazioni sullo stato sospeso, vedere [funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementata.|L'origine dati o driver non supporta l'operazione richiesta nel *operazione* argomento.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima che l'origine dati ha restituito il set di risultati. Il periodo di timeout viene impostato tramite **SQLSetStmtAttr** con un *attributo* argomento di SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente dell'handle restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato per l'handle per eseguire la post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
  
> [!CAUTION]  
>  Per informazioni sull'istruzione che dichiara **SQLBulkOperations** può essere chiamato in e le attività da svolgere per la compatibilità con ODBC 2. *x* applicazioni, vedere il [cursori a blocchi, i cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) sezione Appendice g: Driver le linee guida per la compatibilità con le versioni precedenti.  
  
 Un'applicazione utilizza **SQLBulkOperations** per eseguire le operazioni seguenti nella tabella di base o nella vista che corrisponde alla query corrente:  
  
-   Aggiungere nuove righe.  
  
-   Aggiornare un set di righe in cui ogni riga è identificato da un segnalibro.  
  
-   Eliminare un set di righe in cui ogni riga è identificato da un segnalibro.  
  
-   Recuperare un set di righe in cui ogni riga è identificato da un segnalibro.  
  
 Dopo una chiamata a **SQLBulkOperations**, la posizione del cursore blocco non è definita. L'applicazione deve chiamare **SQLFetchScroll** per impostare la posizione del cursore. Un'applicazione deve chiamare **SQLFetchScroll** solo con un *FetchOrientation* argomento SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK. La posizione del cursore non è definita se l'applicazione chiama **SQLFetch** o **SQLFetchScroll** con un *FetchOrientation* argomento di SQL_FETCH_PRIOR, SQL_FETCH_NEXT, o SQL_FETCH_RELATIVE.  
  
 Una colonna può essere ignorata in operazioni bulk eseguite da una chiamata a **SQLBulkOperations** impostando il buffer di lunghezza/indicatore di colonna specificato nella chiamata a **SQLBindCol**, per SQL_COLUMN_IGNORE.  
  
 Non è necessario per l'applicazione impostare l'attributo di istruzione SQL_ATTR_ROW_OPERATION_PTR quando chiama **SQLBulkOperations** perché le righe non possono essere ignorate durante l'esecuzione di operazioni bulk con questa funzione.  
  
 Il buffer a cui fa riferimento l'attributo di istruzione SQL_ATTR_ROWS_FETCHED_PTR contiene il numero di righe interessate da una chiamata a **SQLBulkOperations**.  
  
 Quando il *operazione* argomento SQL_ADD o SQL_UPDATE_BY_BOOKMARK e l'elenco select della specifica di query associata al cursore contiene più di un riferimento alla stessa colonna, è definito dal driver se l'errore viene generato o il driver ignora i riferimenti duplicati ed esegue le operazioni richieste.  
  
 Per ulteriori informazioni su come usare **SQLBulkOperations**, vedere [aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Esecuzione degli inserimenti Bulk  
 Per inserire i dati con **SQLBulkOperations**, un'applicazione esegue la sequenza di passaggi seguente:  
  
1.  Esegue una query che restituisce un set di risultati.  
  
2.  Imposta il numero di righe che desidera inserire l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE.  
  
3.  Chiamate **SQLBindCol** per associare i dati che desidera inserire. I dati vengono associati a una matrice con dimensioni pari al valore di SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  Le dimensioni della matrice a cui fa riferimento l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR devono essere maggiore o uguale a SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
4.  Chiamate **SQLBulkOperations**(*StatementHandle,* SQL_ADD) per eseguire l'inserimento.  
  
5.  Se l'applicazione ha impostato l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
 Se un'applicazione è associata la colonna 0 prima di chiamare **SQLBulkOperations** con un *operazione* argomento di SQL_ADD, il driver aggiornerà il buffer delle colonne associate 0 con i valori di segnalibro per il nuovo riga inserita. A questo scopo, l'applicazione deve avere impostare l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE prima di eseguire l'istruzione. (Questo non funziona con un'API ODBC 2. *x* driver.)  
  
 Dati di tipo Long possono aggiungere in parti SQLBulkOperations, tramite le chiamate a SQLParamData e SQLPutData. Per ulteriori informazioni, vedere "Fornendo lungo dati per Bulk istruzioni Inserts e Updates" più avanti in questo riferimento di funzione.  
  
 Non è necessario per l'applicazione chiami **SQLFetch** o **SQLFetchScroll** prima di chiamare **SQLBulkOperations** (tranne quando si passa un 2 di ODBC. *x* driver, vedere [compatibilità e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 Il comportamento è definito dal driver se **SQLBulkOperations**, con un *operazione* argomento di SQL_ADD, viene chiamato su un cursore che include colonne duplicate. Il driver può restituire un valore SQLSTATE definito dal driver, aggiungere i dati per la prima colonna che viene visualizzato nel risultato impostare o eseguono altri comportamenti definito dal driver.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Esecuzione di aggiornamenti in blocco tramite l'utilizzo di segnalibri  
 Per eseguire aggiornamenti in blocco utilizzando i segnalibri con **SQLBulkOperations**, un'applicazione esegue i passaggi seguenti in sequenza:  
  
1.  Imposta l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE.  
  
2.  Esegue una query che restituisce un set di risultati.  
  
3.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera aggiornare.  
  
4.  Chiamate **SQLBindCol** per associare i dati che desidera aggiornare. I dati vengono associati a una matrice con dimensioni pari al valore di SQL_ATTR_ROW_ARRAY_SIZE. Viene inoltre chiamato **SQLBindCol** per associare la colonna 0 (la colonna del segnalibro).  
  
5.  Copia i segnalibri per le righe interessate durante l'aggiornamento in una matrice associata alla colonna 0.  
  
6.  Aggiorna i dati nel buffer associati.  
  
    > [!NOTE]  
    >  Le dimensioni della matrice a cui fa riferimento l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR devono essere maggiore o uguale a SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
7.  Chiamate **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Se l'applicazione ha impostato l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
8.  Facoltativamente, chiama **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) per recuperare i dati nei buffer di applicazione associate per verificare che si è verificato l'aggiornamento.  
  
9. Se i dati sono stati aggiornati, il driver modifica il valore nella matrice di stato di riga per le righe appropriate in SQL_ROW_UPDATED.  
  
 Blocco aggiornamenti eseguiti da **SQLBulkOperations** possono includere dati di tipo long tramite chiamate a **SQLParamData** e **SQLPutData**. Per ulteriori informazioni, vedere "Fornendo lungo dati per Bulk istruzioni Inserts e Updates" più avanti in questo riferimento di funzione.  
  
 Se la persistenza dei segnalibri su cursori, l'applicazione non è necessario chiamare **SQLFetch** o **SQLFetchScroll** prima dell'aggiornamento per i segnalibri. È possibile utilizzare i segnalibri di cui è archiviato da un cursore precedente. Se i segnalibri non vengono conservate per i cursori, l'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** per recuperare i segnalibri.  
  
 Il comportamento è definito dal driver se **SQLBulkOperations**, con un *operazione* argomento di SQL_UPDATE_BY_BOOKMARK, viene chiamato su un cursore che include colonne duplicate. Il driver può restituire un valore SQLSTATE definito dal driver, aggiornare la prima colonna visualizzata nel set di risultati o eseguire altri comportamenti definito dal driver.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Esecuzione delle operazioni Bulk recupera l'utilizzo di segnalibri  
 Per eseguire operazioni di recupero delle operazioni bulk utilizzando i segnalibri con **SQLBulkOperations**, un'applicazione esegue i passaggi seguenti in sequenza:  
  
1.  Imposta l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE.  
  
2.  Esegue una query che restituisce un set di risultati.  
  
3.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera recuperare.  
  
4.  Chiamate **SQLBindCol** per associare i dati che desidera recuperare. I dati vengono associati a una matrice con dimensioni pari al valore di SQL_ATTR_ROW_ARRAY_SIZE. Viene inoltre chiamato **SQLBindCol** per associare la colonna 0 (la colonna del segnalibro).  
  
5.  Copia i segnalibri per le righe che è interessato il recupero di massa in una matrice associata alla colonna 0. (Ciò presuppone che l'applicazione ha già ottenuto i segnalibri separatamente).  
  
    > [!NOTE]  
    >  Le dimensioni della matrice a cui fa riferimento l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR devono essere maggiore o uguale a SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
6.  Chiamate **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Se l'applicazione ha impostato l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
 Se la persistenza dei segnalibri su cursori, l'applicazione non è necessario chiamare **SQLFetch** o **SQLFetchScroll** prima di recuperare dai segnalibri. È possibile utilizzare i segnalibri di cui è archiviato da un cursore precedente. Se i segnalibri non vengono conservate per i cursori, l'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** una volta per recuperare i segnalibri.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Esecuzione delle operazioni Bulk Elimina l'utilizzo di segnalibri  
 Per eseguire bulk eliminazioni utilizzando i segnalibri con **SQLBulkOperations**, un'applicazione esegue i passaggi seguenti in sequenza:  
  
1.  Imposta l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE.  
  
2.  Esegue una query che restituisce un set di risultati.  
  
3.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe che desidera eliminare.  
  
4.  Chiamate **SQLBindCol** per associare la colonna 0 (la colonna del segnalibro).  
  
5.  Copia i segnalibri per le righe che è interessato a eliminazione in una matrice associata alla colonna 0.  
  
    > [!NOTE]  
    >  Le dimensioni della matrice a cui fa riferimento l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR devono essere maggiore o uguale a SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR deve essere un puntatore null.  
  
6.  Chiamate **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Se l'applicazione ha impostato l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR, è possibile esaminare questa matrice per visualizzare il risultato dell'operazione.  
  
 Se la persistenza dei segnalibri su cursori, l'applicazione non è necessario chiamare **SQLFetch** o **SQLFetchScroll** prima di eliminare dai segnalibri. È possibile utilizzare i segnalibri di cui è archiviato da un cursore precedente. Se i segnalibri non vengono conservate per i cursori, l'applicazione deve chiamare **SQLFetch** o **SQLFetchScroll** una volta per recuperare i segnalibri.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Fornisce dati Long per Bulk Insert e Update  
 È possibile fornire dati Long per inserimenti bulk e aggiornamenti eseguiti tramite chiamate a **SQLBulkOperations**. Per inserire o aggiornare i dati di tipo long, un'applicazione esegue i passaggi seguenti, oltre ai passaggi descritti nelle sezioni "Esegue l'inserimento Bulk" e "Esecuzione delle operazioni Bulk Aggiorna mediante segnalibri" più indietro in questo argomento.  
  
1.  Quando associa i dati utilizzando **SQLBindCol**, viene visualizzato un valore definito dall'applicazione, ad esempio il numero di colonna, nel  *\*TargetValuePtr* buffer per data-at-execution colonne. Il valore può essere utilizzato in un secondo momento per identificare la colonna.  
  
     L'applicazione inserisce il risultato di SQL_LEN_DATA_AT_EXEC (*lunghezza*) macro di  *\*StrLen_or_IndPtr* buffer. Se il tipo di dati SQL della colonna è SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo di dati specifici dell'origine dati di tipo long e il driver restituisce "Y" per il tipo di informazioni SQL_NEED_LONG_DATA_LEN in **SQLGetInfo**, *lunghezza*  è il numero di byte di dati da inviare per il parametro; in caso contrario, deve essere un valore non negativo e viene ignorato.  
  
2.  Quando **SQLBulkOperations** viene chiamato, se sono presenti colonne data-at-execution, la funzione restituisce SQL_NEED_DATA e procede al passaggio 3, che segue. (Se non sono presenti colonne data-at-execution, il processo è completo).  
  
3.  L'applicazione chiama **SQLParamData** per recuperare l'indirizzo del  *\*TargetValuePtr* buffer per la prima colonna data-at-execution da elaborare. **SQLParamData** restituisce SQL_NEED_DATA. L'applicazione recupera il valore definito dall'applicazione di  *\*TargetValuePtr* buffer.  
  
    > [!NOTE]  
    >  Anche se i parametri data-at-execution sono simili a colonne data-at-execution, il valore restituito da **SQLParamData** è diverso per ognuno.  
  
     Le colonne data-at-execution sono colonne in un set di righe per cui i dati verranno inviati con **SQLPutData** quando una riga viene aggiornata o inserita con **SQLBulkOperations**. Sono associate con **SQLBindCol**. Il valore restituito da **SQLParamData** è l'indirizzo della riga di **TargetValuePtr* buffer che viene elaborato.  
  
4.  L'applicazione chiama **SQLPutData** una o più volte per inviare i dati per la colonna. Più di una chiamata è necessario se il valore di dati non può essere restituito nel  *\*TargetValuePtr* specificato nel buffer **SQLPutData**; più chiamate al metodo **SQLPutData** per la stessa colonna sono consentiti solo durante l'invio di dati di tipo carattere C a una colonna con un tipo di carattere, binary o dati specifici dell'origine dati o per l'invio di dati C binari a una colonna con un carattere, binario, o tipo di dati specifici dell'origine dati.  
  
5.  L'applicazione chiama **SQLParamData** per segnalare che tutti i dati è stato inviato per la colonna.  
  
    -   Se sono presenti altre colonne data-at-execution, **SQLParamData** restituisce SQL_NEED_DATA e l'indirizzo del *TargetValuePtr* buffer per la colonna data-at-execution successiva da elaborare. L'applicazione si ripete i passaggi 4 e 5.  
  
    -   Se sono presenti colonne data-at-execution non sono più presenti, il processo è stato completato. Se l'istruzione è stata eseguita correttamente, **SQLParamData** restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; se l'esecuzione non riuscita, viene restituito SQL_ERROR. A questo punto, **SQLParamData** può restituire qualsiasi SQLSTATE che può essere restituiti da **SQLBulkOperations**.  
  
 Se l'operazione viene annullata o si verifica un errore **SQLParamData** o **SQLPutData** dopo **SQLBulkOperations** restituisce SQL_NEED_DATA e prima dell'invio di dati per tutti le colonne data-at-execution, l'applicazione può chiamare solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, o **SQLPutData** per l'istruzione o la connessione associata all'istruzione. Se per la connessione associata all'istruzione o l'istruzione chiama qualsiasi altra funzione, la funzione restituisce SQL_ERROR e SQLSTATE HY010 (funzione di errore nella sequenza).  
  
 Se l'applicazione chiama **SQLCancel** mentre il driver deve comunque i dati per le colonne data-at-execution, il driver Annulla l'operazione. L'applicazione può quindi chiamare **SQLBulkOperations** nuovamente l'annullamento non influisce sullo stato del cursore o la posizione corrente del cursore.  
  
## <a name="row-status-array"></a>Matrice di stato di riga  
 La matrice di stato di riga contiene i valori di stato per ogni riga di dati nel set di righe dopo una chiamata a **SQLBulkOperations**. Il driver imposta i valori di stato di questa matrice dopo una chiamata a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, o **SQLBulkOperations** . Questa matrice viene popolata mediante una chiamata a **SQLBulkOperations** se **SQLFetch** o **SQLFetchScroll** non è stato chiamato prima di **SQLBulkOperations** . Questa matrice viene fatto riferimento tramite l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR. Il numero di elementi nelle matrici di stato di riga sia uguale al numero di righe nel set di righe (come definito dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE). Per informazioni su questa matrice di stato di riga, vedere [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente recupera 10 righe di dati in un momento dalla tabella Customers. Viene quindi richiesto all'utente di un'azione da intraprendere. Per ridurre il traffico di rete, il buffer di esempio aggiornamenti, eliminazioni e inserisce in locale in matrici associate, ma solo a offset i set di righe di dati precedenti. Quando l'utente sceglie di inviare aggiornamenti, eliminazioni e inserimenti alla origine dati, il codice imposta l'associazione in modo appropriato l'offset e chiama **SQLBulkOperations**. Per semplicità, l'utente non è possibile memorizzare nel buffer più di 10 aggiornamenti, eliminazioni o inserimenti.  
  
```  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Associazione di un buffer a una colonna in un set di risultati|[Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|L'elaborazione di istruzione di annullamento|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Recupero di un blocco di dati o di scorrimento di un risultato impostato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recupero di un singolo campo di un descrittore|[Funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Recupero di più campi di un descrittore|[Funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|L'impostazione di un singolo campo di un descrittore|[Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Impostazione dei diversi campi di un descrittore|[Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Posizionando il cursore, l'aggiornamento dei dati del set di righe o l'aggiornamento o eliminazione di dati nel set di righe|[Funzione SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
