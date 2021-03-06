---
title: Usare i dati JSON in SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1e4e9f4a26b2d5ad3ee12975fa16d0442766f7e9
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2018
---
# <a name="json-data-in-sql-server"></a>Dati JSON in SQL Server
[!INCLUDE[appliesto-ss2016-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

JSON è un popolare formato di dati testuali usato per lo scambio di dati in applicazioni per dispositivi mobili e Web moderne. JSON viene usato anche per archiviare dati non strutturati nei file di log o nei database NoSQL come Microsoft Cosmos DB. Molti servizi Web REST restituiscono risultati formattati come testo JSON oppure accettano dati formattati come JSON. La maggior parte dei servizi di Azure, come Ricerca di Azure, Archiviazione di Azure e Azure Cosmos DB, include ad esempio endpoint REST che restituiscono o usano JSON. JSON è anche il formato principale per lo scambio di dati tra le pagine Web e i server Web tramite le chiamate AJAX. 

Le funzioni JSON in SQL Server consentono di combinare concetti NoSQL e concetti relazionali nello stesso database. È possibile combinare colonne relazionali classiche con colonne che contengono documenti formattati come testo JSON nella stessa tabella, analizzare e importare documenti JSON in strutture relazionali o formattare dati relazionali come testo JSON. Nel video seguente è possibile vedere come le funzioni JSON connettono concetti relazionali e NoSQL in SQL Server e nel database SQL di Azure:

*JSON as a bridge between NoSQL and relational worlds* (JSON come ponte tra NoSQL e gli ambienti relazionali)
> [!VIDEO https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds/player]
 
Ecco un esempio di testo JSON: 
 
```json 
[{
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
}, {
    "name": "Jane",
    "surname": "Doe"
}]
``` 
 
Usando le funzioni e gli operatori predefiniti di SQL Server, è possibile eseguire le operazioni seguenti con testo JSON: 
 
- Analizzare il testo JSON e leggere o modificare i valori.  
- Trasformare matrici di oggetti JSON in formato tabella.  
- Eseguire qualsiasi query Transact-SQL sugli oggetti JSON convertiti.  
- Formattare i risultati delle query Transact-SQL in formato JSON.  
  
![Panoramica del supporto JSON predefinito](../../relational-databases/json/media/jsonslides1overview.png "Panoramica del supporto JSON predefinito")  
  
## <a name="key-json-capabilities-of-sql-server-and-sql-database"></a>Principali funzionalità JSON di SQL Server e del database SQL
Le sezioni successive illustrano le principali funzionalità offerte da SQL Server tramite il supporto JSON predefinito. È possibile visualizzare le modalità d'uso di funzioni e operatori JSON nel video seguente:

*SQL Server 2016 and JSON Support* (SQL Server 2016 e supporto JSON)
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support/player]

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>Estrarre valori dal testo JSON e usarli nelle query
Se un testo JSON viene archiviato in tabelle di database, è possibile leggere o modificare i valori nel testo JSON usando le funzioni predefinite seguenti:  
  
-   **JSON_VALUE** estrae un valore scalare da una stringa JSON.
-   **JSON_QUERY** estrae un oggetto o una matrice da una stringa JSON.
-   **ISJSON** verifica se una stringa include contenuto JSON valido.
-   **JSON_MODIFY** modifica un valore in una stringa JSON.

**Esempio**
  
Nell'esempio seguente la query usa sia i dati relazionali sia i dati JSON (archiviati nella colonna `jsonCol`) di una tabella:  
  
```sql  
SELECT Name,Surname,
 JSON_VALUE(jsonCol,'$.info.address.PostCode') AS PostCode,
 JSON_VALUE(jsonCol,'$.info.address."Address Line 1"')+' '
  +JSON_VALUE(jsonCol,'$.info.address."Address Line 2"') AS Address,
 JSON_QUERY(jsonCol,'$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol)>0
 AND JSON_VALUE(jsonCol,'$.info.address.Town')='Belgrade'
 AND Status='Active'
ORDER BY JSON_VALUE(jsonCol,'$.info.address.PostCode')
```  
  
Strumenti e applicazioni non rilevano alcuna differenza tra i valori ricavati dalle colonne della tabella scalare e i valori ricavati dalla colonna JSON. È possibile usare i valori dal testo JSON in qualsiasi parte della query Transact-SQL (tra cui clausole WHERE, ORDER BY o GROUP BY, aggregazioni finestra e così via). Le funzioni JSON usano una sintassi di tipo JavaScript per fare riferimento ai valori all'interno del testo JSON.

Per altre informazioni, vedere [Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite (SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)e [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md).  
  
### <a name="change-json-values"></a>Modificare valori JSON
Se è necessario modificare parti di testo JSON, è possibile usare la funzione **JSON_MODIFY** per aggiornare il valore di una proprietà in una stringa JSON e restituire la stringa JSON aggiornata. L'esempio seguente aggiorna il valore di una proprietà in una variabile che include contenuto JSON:  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=JSON_MODIFY(@jsonInfo,'$.info.address[0].town','London') 
```  
  
### <a name="convert-json-collections-to-a-rowset"></a>Convertire raccolte JSON in un set di righe
Non è necessario un linguaggio di query personalizzato per eseguire query JSON in SQL Server. Per eseguire query sui dati JSON, si può usare il linguaggio T-SQL standard. Se è necessario creare una query o un report sui dati JSON, è possibile convertire facilmente i dati JSON in righe e colonne chiamando la funzione **OPENJSON** del set di righe. Per altre informazioni, vedere [Convertire dati JSON in righe e colonne con la funzione OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
Nell'esempio seguente viene chiamato **OPENJSON** che trasforma una matrice di oggetti archiviati nella variabile `@json` in un set di righe su cui è possibile eseguire una query usando l'istruzione SQL **SELECT** standard:  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =  
N'[  
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
 ]'  
   
SELECT *  
FROM OPENJSON(@json)  
  WITH (id int 'strict $.id',  
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
        age int, dateOfBirth datetime2 '$.dob')  
```  
  
**Risultati**  
  
|id|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
**OPENJSON** trasforma la matrice di oggetti JSON in una tabella in cui ogni oggetto è rappresentato come una riga e le coppie chiave-valore vengono restituite come celle. L'output osserva le regole seguenti:
- **OPENJSON** converte i valori JSON nei tipi specificati nella clausola **WITH**.
- **OPENJSON** può gestire sia coppie chiave-valore flat che gli oggetti annidati organizzati gerarchicamente.
- Non è necessario restituire tutti i campi contenuti nel testo JSON.
- Se non esistono valori JSON, **OPENJSON** restituisce valori NULL.
- È possibile specificare un percorso dopo la definizione del tipo per fare riferimento a una proprietà annidata o a una proprietà con un nome diverso.
- Il prefisso **strict** facoltativo nel percorso specifica che i valori per le proprietà specificate devono esistere nel testo JSON.

Per altre informazioni, vedere [Convertire dati JSON in righe e colonne con la funzione OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) e [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md).  
  
### <a name="convert-sql-server-data-to-json-or-export-json"></a>Convertire dati di SQL Server in formato JSON o esportare JSON
Formattare i dati SQL Server o i risultati delle query JSON in formato JSON aggiungendo la clausola **FOR JSON** a un'istruzione **SELECT** . Usare la clausola **FOR JSON** per delegare la formattazione dell'output JSON dalle applicazioni client a SQL Server. Per altre informazioni, vedere [Formattare i risultati delle query in formato JSON con FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
L'esempio seguente usa la modalità PATH con la clausola **FOR JSON**:  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
Ogni **FOR JSON** formatta i risultati SQL come testo JSON che può essere fornito a qualsiasi app che riconosce JSON. L'opzione PATH usa alias separati da punti nella clausola SELECT per annidare oggetti nei risultati della query.  
  
**Risultati**  
  
```json  
[{
    "id": 2,
    "info": {
        "name": "John",
        "surname": "Smith"
    },
    "age": 25
}, {
    "id": 5,
    "info": {
        "name": "Jane",
        "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
}] 
```  
  
Per altre informazioni, vedere [Formattare i risultati delle query in formato JSON con FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)e [Clausola FOR (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="use-cases-for-json-data-in-sql-server"></a>Casi d'uso per dati JSON in SQL Server

Il supporto di JSON in SQL Server e nel database SQL di Azure consente di combinare concetti relazionali e NoSQL. È possibile trasformare facilmente dati relazionali in dati semistrutturati e viceversa. JSON non è tuttavia una sostituzione per i modelli relazionali esistenti. Ecco alcuni casi d'uso specifici che traggono vantaggio dal supporto JSON in SQL Server e nel database SQL. Per altre info, vedere [JSON in SQL Server – Use cases](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2018/01/31/json-in-sql-server-use-cases/) (JSON in SQL Server - Casi d'uso).

### <a name="simplify-complex-data-models"></a>Semplificare modelli di dati complessi

Valutare la possibilità di denormalizzare il modello di dati con campi JSON al posto di più tabelle figlio. Per altre informazioni, vedere [Simplify data access using de-normalized models](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2018/01/24/simplify-data-access-using-de-normalized-models/) (Semplificare l'accesso ai dati con modelli denormalizzati).

### <a name="store-retail-and-e-commerce-data"></a>Archiviare dati di vendita al dettaglio e di e-commerce

Archiviare informazioni sui prodotti con un'ampia gamma di attributi variabili in un modello denormalizzato per una maggiore flessibilità. Per altre informazioni, vedere [Designing Product Catalogs in SQL Server using JSON](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/12/21/designing-product-catalogs-in-sql-server-2016-using-json/) (Progettazione di cataloghi di prodotti in SQL Server) e [Indexing data in JSON product catalogs](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/12/21/indexing-data-in-json-product-catalogs/) (Indicizzazione dei dati nei cataloghi di prodotti JSON).

### <a name="process-log-and-telemetry-data"></a>Elaborare i dati di log e di telemetria

Caricare, eseguire query e analizzare i dati di log archiviati come file JSON con tutte le potenzialità del linguaggio Transact-SQL. Per altre informazioni, vedere la sezione *Log and telemetry data analysis* (Analisi dei dati di log e di telemetria) in [JSON in SQL Server – Use cases](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2018/01/31/json-in-sql-server-use-cases/) (JSON in SQL Server - Casi d'uso).

### <a name="store-semi-structured-iot-data"></a>Archiviare dati IoT semistrutturati

Quando è necessario analizzare dati IoT in tempo reale, caricare i dati in ingresso direttamente nel database anziché in una posizione di archiviazione temporanea. Per altre informazioni, vedere [Working with Azure IoT data in Azure SQL Database](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2018/01/23/working-with-azure-iot-data-in-azure-sql-database/) (Utilizzo dei dati IoT di Azure nel database SQL di Azure).

### <a name="simplify-rest-api-development"></a>Semplificare lo sviluppo delle API REST

Trasformare facilmente i dati relazionali dal database nel formato JSON usato dalle API REST che supportano il sito Web. Per altre informazioni, vedere [Simplify REST API development for modern Single-page apps with SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2018/01/29/simplify-rest-api-development-modern-single-page-apps-sql-server/) (Semplificare lo sviluppo di API REST per app a pagina singola moderne con SQL Server).

## <a name="combine-relational-and-json-data"></a>Combinare dati relazionali e dati JSON
SQL Server fornisce un modello ibrido per l'archiviazione e l'elaborazione dei dati relazionali e JSON usando il linguaggio Transact-SQL standard. È possibile organizzare le raccolte di documenti JSON in tabelle, stabilire relazioni tra di esse, combinare colonne scalari fortemente tipizzate archiviate in tabelle con coppie chiave-valore flessibili archiviate nelle colonne JSON ed eseguire query su valori scalari e JSON in una o più tabelle usando il linguaggio Transact-SQL completo.
 
Il testo JSON è archiviato in colonne varchar o nvarchar e viene indicizzato come testo normale. Qualsiasi funzionalità o componente di SQL Server che supporta testo supporta anche JSON, quindi non esiste quasi nessun vincolo nell'interazione tra JSON e altre funzionalità di SQL Server. È possibile archiviare i dati JSON in tabelle in memoria o temporali, applicare i predicati della sicurezza a livello di riga al testo JSON e così via.

Se si hanno semplici carichi di lavoro JSON in cui si vuole usare un linguaggio di query personalizzato per l'elaborazione di documenti JSON, prendere in considerazione Microsoft Azure [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).  
  
Ecco alcuni casi d'uso che mostrano come usare il supporto JSON integrato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="store-and-index-json-data-in-sql-server"></a>Archiviare e indicizzare dati JSON in SQL Server

Per altre informazioni sulle opzioni per l'archiviazione, l'indicizzazione e l'ottimizzazione dei dati JSON in SQL Server, vedere gli articoli seguenti:
-   [Archiviare documenti JSON in SQL Server o nel database SQL](store-json-documents-in-sql-tables.md)
-   [Indicizzazione dei dati JSON](index-json-data.md)
-   [Ottimizzare l'elaborazione JSON con OLTP in memoria](optimize-json-processing-with-in-memory-oltp.md)

### <a name="load-json-files-into-sql-server"></a>Caricare file JSON in SQL Server  
È possibile formattare le informazioni archiviate nei file come JSON standard o JSON delimitato da righe. SQL Server può importare il contenuto di file JSON, analizzarlo usando le funzioni **OPENJSON** e **JSON_VALUE** e caricarlo nelle tabelle.  
  
-   Se i documenti JSON vengono archiviati in file locali, unità di rete condivise o posizioni di File di Azure accessibili da SQL Server, è possibile usare l'importazione in blocco per caricare i dati JSON in SQL Server. Per altre informazioni su questo scenario, vedere [Importing JSON files into SQL Server using OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx)(Importazione di file JSON in SQL Server usando OPENROWSET - BULK).  
  
-   Se i file JSON delimitati da righe vengono archiviati nell'archivio BLOB di Azure o nel file system di Hadoop, è possibile usare PolyBase per caricare il testo JSON, analizzarlo nel codice Transact-SQL e caricarlo nelle tabelle.  

### <a name="import-json-data-into-sql-server-tables"></a>Importare i dati JSON in tabelle di SQL Server  
Se è necessario caricare dati JSON da un servizio esterno in SQL Server, è possibile usare **OPENJSON** per importare i dati in SQL Server, invece di analizzare i dati nel livello dell'applicazione.  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX)

SET @jsonVariable = N'[  
        {  
          "Order": {  
            "Number":"SO43659",  
            "Date":"2011-05-31T00:00:00"  
          },  
          "AccountNumber":"AW29825",  
          "Item": {  
            "Price":2024.9940,  
            "Quantity":1  
          }  
        },  
        {  
          "Order": {  
            "Number":"SO43661",  
            "Date":"2011-06-01T00:00:00"  
          },  
          "AccountNumber":"AW73565",  
          "Item": {  
            "Price":2024.9940,  
            "Quantity":3  
          }  
       }  
  ]'
  
INSERT INTO SalesReport  
SELECT SalesOrderJsonData.*  
FROM OPENJSON (@jsonVariable, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData;  
```  
  
È possibile fornire il contenuto della variabile JSON tramite un servizio REST esterno, inviarlo come parametro da un framework JavaScript sul lato client o caricarlo da file esterni. È possibile inserire, aggiornare o unire facilmente i risultati dal testo JSON in una tabella di SQL Server. Per altre informazioni su questo scenario, vedere i post di blog seguenti:
-   [Import JSON data in SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/) (Importare i dati JSON in SQL Server)
-   [eseguire l'upsert dei documenti JSON in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016)
-   [Load GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/) (Caricare i dati GeoJSON in SQL Server 2016)  

## <a name="analyze-json-data-with-sql-queries"></a>Analizzare i dati JSON con query SQL  
Se è necessario filtrare o aggregare dati JSON per la creazione di report, è possibile usare **OPENJSON** per trasformare i dati JSON in formato relazionale. È quindi possibile usare le funzioni predefinite e [!INCLUDE[tsql](../../includes/tsql-md.md)] standard per preparare i report.  
  
```sql  
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date  
FROM   SalesOrderRecord AS Tab  
          CROSS APPLY  
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData  
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'  
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified  
```  
  
È possibile usare sia le colonne sia i valori della tabella standard dal testo JSON nella stessa query. È possibile aggiungere indici nell'espressione `JSON_VALUE(Tab.json, '$.Status')` per migliorare le prestazioni della query. Per altre informazioni, vedere [Indicizzazione dei dati JSON](../../relational-databases/json/index-json-data.md).
 
## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>Restituire dati da una tabella di SQL Server formattata come JSON  
Se si ha un servizio Web che preleva i dati dal livello di database e li restituisce in formato JSON oppure se si hanno framework o librerie JavaScript che accettano dati formattati come JSON, è possibile formattare l'output JSON direttamente in una query SQL. Invece di scrivere codice o includere una libreria per convertire i risultati di una query tabulare e quindi serializzare gli oggetti in formato JSON, è possibile usare **FOR JSON** per delegare la formattazione JSON a SQL Server.  
  
Ad esempio, può essere necessario generare output JSON che sia conforme alla specifica OData. Il servizio Web prevede una richiesta e una risposta nel formato seguente: 
  
-   Richiesta: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Risposta: `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
Questo URL OData rappresenta una richiesta per le colonne ProductID e ProductName per il prodotto con `id` 1. È possibile usare la clausola **FOR JSON** per formattare l'output come previsto in SQL Server.  
  
```sql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity'
 AS '@odata.context',   
 ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
```  
  
Il risultato di questa query è testo JSON interamente conforme alla specifica OData. Formattazione e sequenza di escape vengono gestite da SQL Server. SQL Server può anche formattare i risultati delle query in qualsiasi formato, ad esempio OData JSON o GeoJSON. Per altre informazioni, vedere [Returning spatial data in GeoJSON format](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1) (Restituzione di dati spaziali in formato GeoJSON).  
  
## <a name="test-drive-built-in-json-support-with-the-adventureworks-sample-database"></a>Test drive del supporto JSON integrato con il database di esempio AdventureWorks
Per ottenere il database di esempio AdventureWorks, è necessario scaricare almeno il file di database e il file di script ed esempi dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=49502). 
 
Dopo aver ripristinato il database di esempio in un'istanza di SQL Server 2016, estrarre il file degli esempi e quindi aprire il file *JSON Sample Queries procedures views and indexes.sql* dalla cartella JSON. Eseguire gli script in questo file per riformattare alcuni dati esistenti come dati JSON, eseguire test di report e query di esempio sui dati JSON, indicizzare i dati JSON e importare ed esportare JSON.  
  
Di seguito sono elencate le operazioni possibili con gli script inclusi nel file:  
  
* Denormalizzare lo schema esistente per creare colonne di dati JSON.
  
    * Archiviare informazioni dalle tabelle SalesReasons SalesOrderDetails, SalesPerson, Customer e da altre tabelle che contengono informazioni relative all'ordine di vendita nelle colonne JSON della tabella SalesOrder_json.  
  
    * Archiviare informazioni dalle tabelle EmailAddresses/PersonPhone nella tabella Person_json come matrici di oggetti JSON.  
  
* Creare procedure e viste che eseguono query sui dati JSON.  
  
* Indicizzare i dati JSON. Creare indici sulle proprietà JSON e indici full-text.  
  
* Importare ed esportare JSON. Creare ed eseguire procedure per esportare il contenuto delle tabelle Person e SalesOrder come risultati JSON, quindi importare e aggiornare le tabelle Person e SalesOrder usando input JSON.  
  
* Eseguire esempi di query. Eseguire alcune query che chiamano le stored procedure e le viste create nei passaggi 2 e 4.  
  
* Pulire gli script. Non eseguire questa parte se si vogliono conservare le stored procedure e le viste create nei passaggi 2 e 4.  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-blog-posts"></a>Post del blog Microsoft  
  
Per soluzioni specifiche, casi d'uso e indicazioni, vedere questi [post del blog sul supporto JSON integrato](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server e nel database SQL di Azure.  

### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere il video seguente:

*Using JSON in SQL Server 2016 and Azure SQL Database* (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database/player]

*Building REST API with SQL Server using JSON functions* (Compilazione di API REST con SQL Server tramite le funzioni JSON)
> [!VIDEO https://www.youtube.com/embed/0m6GXF3-5WI]

### <a name="reference-articles"></a>Articoli di riferimento  
  
-   [Clausola FOR (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
-   [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
-   [Funzioni JSON (Transact-SQL)](../../t-sql/functions/json-functions-transact-sql.md)  
    -   [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)  
    -   [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)  
    -   [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
    -   [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)  
