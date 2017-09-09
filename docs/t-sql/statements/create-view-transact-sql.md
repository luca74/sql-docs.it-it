---
title: CREATE VIEW (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
caps.latest.revision: 85
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9c47fbc342ac911cba103f34ccebafd84af8432a
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="create-view-transact-sql"></a>CREATE VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea una tabella virtuale il cui contenuto (colonne e righe) è definito da una query. Utilizzare questa istruzione per creare una vista dei dati in una o più tabelle nel database. Ad esempio, è possibile utilizzare una vista per gli scopi seguenti:  
  
-   Per analizzare, semplificare e personalizzare la visualizzazione del database per ogni utente.  
  
-   Come meccanismo di sicurezza grazie al quale è possibile consentire agli utenti di accedere ai dati tramite una vista, senza concedere loro le autorizzazioni di accesso alle tabelle di base sottostanti.  
  
-   Per fornire un'interfaccia compatibile con le versioni precedenti con cui emulare una tabella il cui schema è stato modificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] VIEW [ schema_name . ] view_name [ (column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ]   
[ ; ]  
  
<view_attribute> ::=   
{  
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE VIEW [ schema_name . ] view_name [  ( column_name [ ,...n ] ) ]   
AS <select_statement>   
[;]  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argomenti
O ALTER  
 **Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).   
  
 Consente di modificare la visualizzazione in modo condizionale solo se esiste già. 
 
 *schema_name*  
 Nome dello schema a cui appartiene la vista.  
  
 *view_name*  
 Nome della vista. I nomi di vista devono essere conformi alle regole per gli identificatori. Il nome del proprietario della vista è facoltativo.  
  
 *colonna*  
 Nome da assegnare a una colonna della vista. Il nome della colonna è necessario solo quando una colonna deriva da un'espressione aritmetica, una funzione o una costante, quando due o più colonne potrebbero altrimenti avere lo stesso nome (in genere a causa di un join) oppure quando a una colonna di una vista viene assegnato un nome diverso rispetto alla colonna da cui deriva. È inoltre possibile assegnare nomi di colonna nell'istruzione SELECT.  
  
 Se *colonna* non viene specificato, le colonne della vista acquisiscono gli stessi nomi delle colonne nell'istruzione SELECT.  
  
> [!NOTE]  
>  Nelle colonne di una vista, le autorizzazioni assegnate per un nome di colonna rimangono valide tra istruzioni CREATE VIEW e ALTER VIEW, indipendentemente dall'origine dei dati sottostanti. Ad esempio, se vengono concesse autorizzazioni per il **SalesOrderID** colonna in un'istruzione CREATE VIEW, un'istruzione ALTER VIEW può assegnare un nome di **SalesOrderID** colonna con un nome di colonna diversi, ad esempio **OrderRef**e mantenere comunque le autorizzazioni associate alla vista che utilizza **SalesOrderID**.  
  
 AS  
 Specifica le operazioni che la vista deve eseguire.  
  
 *select_statement*  
 Istruzione SELECT che definisce la vista. Nell'istruzione è possibile specificare più di una tabella e altre viste. Per selezionare gli oggetti a cui viene fatto riferimento nella clausola SELECT della vista creata è necessario disporre di autorizzazioni appropriate.  
  
 Non è necessario che una vista sia un semplice subset delle righe e delle colonne di una tabella specifica. È possibile creare una vista che utilizza più tabelle o altre viste tramite una clausola SELECT del grado di complessità desiderato.  
  
 In una definizione di vista indicizzata l'istruzione SELECT deve essere riferita a una sola tabella oppure includere un JOIN tra più tabelle con aggregazioni facoltative.  
  
 Le clausole SELECT utilizzate in una definizione di vista non possono includere gli elementi seguenti:  
  
-   Una clausola ORDER BY, a meno che nell'elenco di selezione dell'istruzione SELECT non sia presente anche una clausola TOP  
  
    > [!IMPORTANT]  
    >  La clausola ORDER BY viene utilizzata esclusivamente per determinare le righe restituite dalla clausola TOP oppure OFFSET nella definizione della vista. La clausola ORDER BY non garantisce risultati ordinati in caso di query sulla vista, a meno che tale clausola non venga specificata anche nella query.  
  
-   Parola chiave INTO  
  
-   Clausola OPTION  
  
-   Un riferimento a una tabella temporanea o a una variabile di tabella  
  
 Poiché *select_statement* utilizza l'istruzione SELECT, è possibile utilizzare \<join_hint > e \<table_hint > hint come specificato nella clausola FROM. Per ulteriori informazioni, vedere [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md) e [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md). 
  
 Funzioni e più istruzioni SELECT separate dall'operatore UNION o UNION ALL possono essere utilizzate *select_statement*.  
  
 CHECK OPTION  
 Impone a tutte le istruzioni di modifica dei dati eseguite sulla vista di soddisfare i criteri impostati nel *select_statement*. Quando una riga viene modificata tramite una vista, la clausola WITH CHECK OPTION assicura che i dati rimangano visibili nella vista dopo il commit della modifica.  
  
> [!NOTE]  
>  Tutti gli aggiornamenti eseguiti direttamente sulle tabelle sottostanti di una vista non vengono verificati in base alla vista, anche se la clausola CHECK OPTION è specificata.  
  
 ENCRYPTION  
 **Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Crittografa le voci nella [Sys. syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) che contengono il testo dell'istruzione CREATE VIEW. Se si utilizza WITH ENCRYPTION, la vista non viene pubblicata nell'ambito della replica di SQL Server.  
  
 SCHEMABINDING  
 Associa la vista allo schema della tabella o delle tabelle sottostanti. Quando la clausola SCHEMABINDING viene specificata, non è possibile apportare alla tabella o alle tabelle di base modifiche che hanno effetto sulla definizione della vista. È necessario prima modificare o eliminare la definizione della vista per rimuovere le dipendenze dalla tabella da modificare. Quando si utilizza SCHEMABINDING, il *select_statement* deve includere i nomi di due parti (*schema***.** *oggetto*) di tabelle, viste o funzioni definite dall'utente a cui fa riferimento. Tutti gli oggetti a cui viene fatto riferimento devono essere presenti nello stesso database.  
  
 Le viste o le tabelle che fanno parte di una vista creata con la clausola SCHEMABINDING non possono essere eliminate, a meno che la vista non venga eliminata o modificata in modo che non sia più associata a uno schema. In caso contrario, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene generato un errore. Inoltre, l'esecuzione di istruzioni ALTER TABLE su tabelle che fanno parte di viste associate a schema ha esito negativo se tali istruzioni modificano la definizione della vista.  
  
 VIEW_METADATA  
 Specifica che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dovrà restituire alle API DB-Library, ODBC e OLE DB le informazioni sui metadati relativi alla vista anziché alla tabella o alle tabelle di base quando vengono richiesti metadati in modalità browse per una query che fa riferimento alla vista. I metadati in modalità browse sono metadati aggiuntivi che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce a queste API sul lato client. Questi metadati consentono alle API sul lato client di implementare cursori sul lato client aggiornabili. I metadati in modalità browse includono informazioni sulla tabella di base a cui appartengono le colonne del set di risultati.  
  
 Per le viste create con VIEW_METADATA, i metadati in modalità browse restituiscono il nome della vista anziché i nomi delle tabelle di base nella descrizione delle colonne della vista nel set di risultati.  
  
 Quando viene creata una vista con WITH VIEW_METADATA, tutte le relative colonne, tranne una **timestamp** , sono aggiornabili se la vista dispone di INSTEAD OF INSERT o i trigger INSTEAD OF UPDATE. Per ulteriori informazioni sulle viste aggiornabili, vedere la sezione Osservazioni.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile creare una vista solo nel database corrente. CREATE VIEW deve essere la prima istruzione di un batch di query. Una vista può includere al massimo 1.024 colonne.  
  
 Quando si esegue una query tramite una vista, [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica che tutti gli oggetti di database a cui viene fatto riferimento nell'istruzione esistano e siano validi nel contesto dell'istruzione e che le istruzioni di modifica dei dati non violino le regole di integrità dei dati. Se la verifica ha esito negativo, viene visualizzato un messaggio di errore. In caso contrario, l'azione viene convertita automaticamente in un'operazione sulla tabella o sulle tabelle sottostanti.  
  
 Se si tenta di utilizzare una vista che dipende da una tabella o una vista eliminata, [!INCLUDE[ssDE](../../includes/ssde-md.md)] visualizza un messaggio di errore. Se viene creata una nuova tabella o vista per sostituire quella eliminata e la struttura della nuova tabella non è diversa rispetto alla tabella di base precedente, la vista risulta di nuovo utilizzabile. Se la struttura della nuova tabella o vista è diversa, la vista deve essere eliminata e ricreata.  
  
 Se non è possibile creare una vista con la clausola SCHEMABINDING, [sp_refreshview](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md) deve essere eseguito quando vengono apportate modifiche agli oggetti sottostanti la vista che influiscono sulla definizione della vista. In caso contrario, le query sulla vista possono generare risultati imprevisti.  
  
 Quando viene creata una vista, informazioni sulla visualizzazione vengono archiviate nelle viste del catalogo seguenti: [Sys. Views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md), [Columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), e [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md). Il testo dell'istruzione CREATE VIEW viene archiviato nel [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista del catalogo.  
  
 Una query che utilizza un indice su una vista definita con **numerico** o **float** espressioni possono generare un risultato diverso da una query simile che non utilizza l'indice sulla vista. Tale differenza può essere dovuta a errori di arrotondamento generati durante l'esecuzione di operazioni INSERT, DELETE o UPDATE sulle tabelle sottostanti.  
  
 In [!INCLUDE[ssDE](../../includes/ssde-md.md)] le impostazioni delle opzioni SET QUOTED_IDENTIFIER e SET ANSI_NULLS vengono salvate in fase di creazione di una vista. Queste impostazioni originali vengono utilizzate per analizzare la vista quando viene utilizzata. Pertanto, tutte le impostazioni di sessione del client per SET QUOTED_IDENTIFIER e SET ANSI_NULLS non hanno effetto sulla definizione della vista durante l'accesso alla vista.  
  
## <a name="updatable-views"></a>Viste aggiornabili  
 È possibile modificare i dati di una tabella di base sottostante tramite una vista solo se vengono soddisfatti i requisiti seguenti:  
  
-   Tutte le modifiche, incluse le istruzioni UPDATE, INSERT e DELETE, devono fare riferimento a colonne di una sola tabella di base.  
  
-   Le colonne modificate nella vista devono fare riferimento direttamente ai dati sottostanti nelle colonne della tabella. Le colonne non possono essere derivate in altro modo, ad esempio tramite:  
  
    -   Una funzione di aggregazione: AVG, COUNT, SUM, MIN, MAX, GROUPING, STDEV, STDEVP, VAR e VARP.  
  
    -   Un calcolo. La colonna non può essere calcolata tramite un'espressione che utilizza altre colonne. Le colonne create mediante gli operatori sui set UNION, UNION ALL, CROSSJOIN, EXCEPT e INTERSECT sono considerate un calcolo e non sono aggiornabili.  
  
-   Le colonne da modificare non sono interessate da clausole GROUP BY, HAVING o DISTINCT.  
  
-   Clausola TOP non viene utilizzata in un punto qualsiasi nel *select_statement* della vista in combinazione con la clausola WITH CHECK OPTION.  
  
 Le restrizioni sopra indicate sono valide sia per qualsiasi sottoquery nella clausola FROM della vista sia per la vista stessa. In genere, [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve essere in grado di tracciare senza ambiguità le modifiche dalla definizione della vista a una tabella di base. Per ulteriori informazioni, vedere [modificare dati tramite una vista](../../relational-databases/views/modify-data-through-a-view.md).  
  
 Se le restrizioni sopra indicate non consentono di modificare i dati direttamente tramite una vista, è possibile ricorrere alle soluzioni seguenti:  
  
-   **Trigger INSTEAD OF**  
  
     È possibile creare trigger INSTEAD OF per una vista in modo da renderla aggiornabile. Questo trigger viene eseguito in sostituzione dell'istruzione di modifica dei dati in cui è definito e consente all'utente di specificare il set di azioni che devono essere eseguite per elaborare l'istruzione di modifica dei dati. Pertanto, se è disponibile un trigger INSTEAD OF per una vista in un'istruzione di modifica dei dati specifica (INSERT, UPDATE o DELETE), la vista corrispondente risulta aggiornabile tramite l'istruzione. Per ulteriori informazioni sui trigger INSTEAD OF, vedere [trigger DML](../../relational-databases/triggers/dml-triggers.md).  
  
-   **Viste partizionate**  
  
     Se la vista è partizionata, è aggiornabile ma con particolari restrizioni. Quando necessario, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] effettua una distinzione tra viste partizionate locali, ovvero le viste nelle quali tutte le tabelle coinvolte e la vista stessa si trovano nella stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e viste partizionate distribuite, ovvero le viste nelle quali almeno una tabella della vista risiede in un server diverso o remoto.  
  
## <a name="partitioned-views"></a>Viste partizionate  
 Una vista partizionata è una vista definita tramite un'istruzione UNION ALL eseguita su tabelle membro con la stessa struttura, ma archiviate separatamente sotto forma di più tabelle nello stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure in un gruppo di istanze autonome di server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominato federazione di server di database.  
  
> [!NOTE]  
>  Il metodo consigliato per il partizionamento locale dei dati in un server prevede l'utilizzo di tabelle partizionate. Per altre informazioni, vedere [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Durante la progettazione di uno schema di partizione, è necessario individuare con chiarezza i dati appartenenti a ogni partizione. Ad esempio, i dati della tabella `Customers` vengono distribuiti in tre tabelle membro su tre server: `Customers_33` su `Server1`, `Customers_66` su `Server2` e `Customers_99` su `Server3`.  
  
 Una vista partizionata in `Server1` viene definita nel modo seguente:  
  
```  
--Partitioned view as defined on Server1  
CREATE VIEW Customers  
AS  
--Select from local member table.  
SELECT *  
FROM CompanyData.dbo.Customers_33  
UNION ALL  
--Select from member table on Server2.  
SELECT *  
FROM Server2.CompanyData.dbo.Customers_66  
UNION ALL  
--Select from mmeber table on Server3.  
SELECT *  
FROM Server3.CompanyData.dbo.Customers_99;  
```  
  
 In generale, una vista viene definita partizionata se utilizza il formato seguente:  
  
```  
SELECT <select_list1>  
FROM T1  
UNION ALL  
SELECT <select_list2>  
FROM T2  
UNION ALL  
...  
SELECT <select_listn>  
FROM Tn;  
```  
  
## <a name="conditions-for-creating-partitioned-views"></a>Requisiti per la creazione di viste partizionate  
  
1.  Elenchi di selezione (select `list`)  
  
    -   Tutte le colonne delle tabelle membro devono essere incluse nell'elenco di colonne della definizione della vista.  
  
    -   Alle colonne che si trovano nella stessa posizione ordinale in ogni `select list` deve essere associato lo stesso tipo, incluse le regole di confronto. Non è sufficiente che il tipo di dati delle colonne supporti la conversione implicita, come nel caso di operazioni UNION.  
  
         Inoltre, è necessario che almeno una colonna, ad esempio `<col>`, sia presente in tutti gli elenchi di selezione nella stessa posizione ordinale. La colonna `<col>` deve essere definita in modo che le tabelle membro `T1, ..., Tn` includano rispettivamente i vincoli CHECK `C1, ..., Cn` in `<col>`.  
  
         Il vincolo `C1` definito nella tabella `T1` deve avere il formato seguente:  
  
        ```  
        C1 ::= < simple_interval > [ OR < simple_interval > OR ...]  
        < simple_interval > :: =   
        < col > { < | > | \<= | >= | = < value >}   
        | < col > BETWEEN < value1 > AND < value2 >  
        | < col > IN ( value_list )  
        | < col > { > | >= } < value1 > AND  
        < col > { < | <= } < value2 >  
        ```  
  
    -   I vincoli devono essere tali per cui qualsiasi valore specificato di `<col>` può soddisfare al massimo uno dei vincoli `C1, ..., Cn` e devono quindi costituire un set di intervalli disgiunti o non sovrapposti. La colonna `<col>` in cui sono definiti i vincoli disgiunti è denominata colonna di partizionamento. Si noti che nelle tabelle sottostanti tale colonna può avere nomi diversi. Per soddisfare i requisiti della colonna di partizionamento sopra descritti, i vincoli devono essere abilitati e attendibili. Se i vincoli sono disabilitati, abilitare di nuovo vincolo controllo mediante il vincolo CHECK *constraint_name* opzione ALTER TABLE e si utilizza l'opzione WITH CHECK convalidarli.  
  
         Negli esempi seguenti vengono illustrati alcuni set di vincoli validi:  
  
        ```  
        { [col < 10], [col between 11 and 20] , [col > 20] }  
        { [col between 11 and 20], [col between 21 and 30], [col between 31 and 100] }  
        ```  
  
    -   Nell'elenco di selezione non è consentito utilizzare più volte la stessa colonna.  
  
2.  Colonna di partizionamento  
  
    -   Deve fare parte della colonna PRIMARY KEY della tabella.  
  
    -   Non può essere una calcolata, identity, predefinita o **timestamp** colonna.  
  
    -   Se una colonna di una tabella membro ha più vincoli, vengono ignorati tutti i vincoli, anche quando è necessario determinare se la vista è partizionata. Per soddisfare i requisiti per la creazione di viste partizionate, è necessario che la colonna di partizionamento includa un solo vincolo di partizionamento.  
  
    -   Non sono previste restrizioni per quanto concerne l'aggiornabilità della colonna di partizionamento.  
  
3.  Tabelle membro o tabelle sottostanti `T1, ..., Tn`  
  
    -   Possono essere tabelle locali o tabelle presenti in altri computer che eseguono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui viene fatto riferimento tramite un nome composto da quattro parti oppure un nome basato su OPENDATASOURCE o OPENROWSET. La sintassi di OPENDATASOURCE e OPENROWSET consente di specificare un nome di tabella, ma non una query pass-through. Per ulteriori informazioni, vedere [OPENDATASOURCE &#40; Transact-SQL &#41; ](../../t-sql/functions/opendatasource-transact-sql.md) e [OPENROWSET &#40; Transact-SQL &#41; ](../../t-sql/functions/openrowset-transact-sql.md).  
  
         Se una o più tabelle membro sono remote, la vista viene definita vista partizionata distribuita ed è necessario rispettare alcuni ulteriori requisiti descritti di seguito in questa sezione.  
  
    -   Non è possibile inserire una stessa tabella due volte nel set di tabelle combinate tramite l'istruzione UNION ALL.  
  
    -   Le tabelle membro non possono includere indici creati su colonne calcolate della tabella.  
  
    -   Tutti i vincoli PRIMARY KEY delle tabelle membro devono riguardare lo stesso numero di colonne.  
  
    -   L'impostazione per lo riempimento ANSI deve essere la stessa per tutte le tabelle membro della vista. Può essere impostata utilizzando il **opzioni utente** opzione **sp_configure** o l'istruzione SET.  
  
## <a name="conditions-for-modifying-data-in-partitioned-views"></a>Requisiti per la modifica dei dati in viste partizionate  
 Le istruzioni che modificano i dati in viste partizionate sono soggette alle restrizioni seguenti:  
  
-   L'istruzione INSERT deve fornire valori per tutte le colonne della vista, anche se le tabelle membro sottostanti includono un vincolo DEFAULT per tali colonne o ammettono valori Null. Per le colonne delle tabelle membro che includono definizioni DEFAULT, nelle istruzioni non è consentito specificare la parola chiave DEFAULT in modo esplicito.  
  
-   Il valore inserito nella colonna di partizionamento deve soddisfare almeno uno dei vincoli sottostanti. In caso contrario, l'operazione di inserimento provoca una violazione di vincolo e ha esito negativo.  
  
-   Nelle istruzioni UPDATE non è possibile specificare la parola chiave DEFAULT come valore nella clausola SET, anche se alla colonna è associato un valore DEFAULT definito nella tabella membro corrispondente.  
  
-   Le colonne Identity della vista incluse in una o più tabelle membro non possono essere modificate tramite un'istruzione INSERT o UPDATE.  
  
-   Se una delle tabelle membro include un **timestamp** colonna, i dati non possono essere modificati tramite un'istruzione INSERT o UPDATE.  
  
-   Se una delle tabelle membro include un trigger oppure un vincolo ON UPDATE CASCADE/SET NULL/SET DEFAULT o ON DELETE CASCADE/SET NULL/SET DEFAULT, la vista non può essere modificata.  
  
-   Le operazioni INSERT, UPDATE e DELETE eseguite su una vista partizionata non sono consentite se includono un self join con tale vista o con una delle tabelle membro.  
  
-   Importazione bulk di dati in una vista partizionata non è supportata da **bcp** o BULK INSERT e INSERT... SELECT * FROM OPENROWSET(BULK...). Tuttavia, è possibile inserire più righe in una vista partizionata utilizzando la [inserire](../../t-sql/statements/insert-transact-sql.md) istruzione.  
  
    > [!NOTE]  
    >  Per aggiornare una vista partizionata, l'utente deve disporre delle autorizzazioni INSERT, UPDATE e DELETE per le tabelle membro.  
  
## <a name="additional-conditions-for-distributed-partitioned-views"></a>Requisiti aggiuntivi per le viste partizionate distribuite  
 Per le viste partizionate distribuite, ovvero le viste nelle quali una o più tabelle membro sono remote, devono essere soddisfatti i requisiti aggiuntivi seguenti:  
  
-   Per garantire l'atomicità in tutti i nodi interessati dall'aggiornamento, viene avviata una transazione distribuita.  
  
-   Per consentire il corretto funzionamento delle istruzioni INSERT, UPDATE o DELETE, è necessario impostare l'opzione XACT_ABORT SET su ON.  
  
-   Tutte le colonne delle tabelle remote di tipo **smallmoney** cui viene fatto riferimento in una vista partizionata vengono mappate come **money**. Pertanto, le colonne corrispondenti (nella stessa posizione ordinale nell'elenco di selezione) tabelle locali inoltre devono essere di tipo **money**.  
  
-   Nel database livello di compatibilità 110 e versioni successiva, tutte le colonne delle tabelle remote di tipo **smalldatetime** cui viene fatto riferimento in una vista partizionata vengono mappate come **smalldatetime**. Le colonne corrispondenti (nella stessa posizione ordinale nell'elenco di selezione) tabelle locali devono essere **smalldatetime**. Si tratta di una modifica nel comportamento delle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui tutte le colonne delle tabelle remote di tipo **smalldatetime** cui viene fatto riferimento in una vista partizionata vengono mappate come **datetime** e le colonne corrispondenti nelle tabelle locale devono essere di tipo **datetime**. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
-   Qualsiasi server collegato nella vista partizionata non può essere di tipo loopback, ovvero non deve puntare alla stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 L'impostazione dell'opzione SET ROWCOUNT viene ignorata per le operazioni INSERT, UPDATE e DELETE che coinvolgono viste partizionate aggiornabili e tabelle remote.  
  
 Quando sono disponibili le tabelle membro e la definizione della vista partizionata, nell'utilità Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono compilati automaticamente piani appropriati in cui le query vengono utilizzate in modo efficiente per l'accesso ai dati di tabelle membro. Con le definizioni di vincoli CHECK, in Query Processor viene eseguito il mapping della distribuzione dei valori chiave nelle tabelle membro. Quando un utente inoltra una query, viene eseguito un confronto tra il mapping e i valori specificati nella clausola WHERE, quindi viene compilato un piano di esecuzione che comporta il trasferimento di una quantità minima di dati tra i server membri. Sebbene sia possibile che alcune tabelle membro si trovino in server remoti, le query distribuite vengono risolte dall'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modo che la quantità di dati distribuiti da trasferire sia minima.  
  
## <a name="considerations-for-replication"></a>Requisiti per la replica  
 Per creare viste partizionate di tabelle membro coinvolte nella replica, devono essere soddisfatti i requisiti seguenti:  
  
-   Se le tabelle sottostanti sono coinvolte nella replica di tipo merge o transazionale con sottoscrizioni aggiornabili, il **uniqueidentifier** colonna deve essere incluso anche nell'elenco di selezione.  
  
     Operazioni INSERT nella vista partizionata devono fornire un valore NEWID () per il **uniqueidentifier** colonna. Le operazioni UPDATE eseguite il **uniqueidentifier** colonna deve fornire NEWID () come valore perché non è possibile utilizzare la parola chiave DEFAULT.  
  
-   La replica di aggiornamenti tramite la vista equivale alla replica di tabelle in due database distinti, ovvero le tabelle vengono gestite da agenti di replica diversi e l'ordine degli aggiornamenti non è prevedibile.  
  
## <a name="permissions"></a>Permissions  
 Sono richieste l'autorizzazione CREATE VIEW per il database e l'autorizzazione ALTER per lo schema in cui viene creata la vista.  
  
## <a name="examples"></a>Esempi  

L'esempio seguente usa il database AdventureWorks 2012 o AdventureWorksDW.  

### <a name="a-using-a-simple-create-view"></a>A. Utilizzo di un'istruzione CREATE VIEW semplice  
 Nell'esempio seguente viene creata una vista tramite l'utilizzo di un'istruzione `SELECT` semplice. Una vista semplice risulta utile quando vengono eseguite query frequenti su una combinazione di colonne. I dati di questa vista derivano dalle tabelle `HumanResources.Employee` e `Person.Person` del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. I dati contengono informazioni sul nome e la data di assunzione dei dipendenti di [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]. È possibile creare la vista per la persona incaricata di tenere traccia del periodo di assunzione dei dipendenti, senza però consentire a tale utente di accedere a tutti i dati di queste tabelle.  
  
```  
CREATE VIEW hiredate_view  
AS   
SELECT p.FirstName, p.LastName, e.BusinessEntityID, e.HireDate  
FROM HumanResources.Employee e   
JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
### <a name="b-using-with-encryption"></a>B. Utilizzo della clausola WITH ENCRYPTION  
 Nell'esempio seguente viene utilizzata l'opzione `WITH ENCRYPTION` e vengono illustrate colonne calcolate, colonne rinominate e più colonne.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
CREATE VIEW Purchasing.PurchaseOrderReject  
WITH ENCRYPTION  
AS  
SELECT PurchaseOrderID, ReceivedQty, RejectedQty,   
    RejectedQty / ReceivedQty AS RejectRatio, DueDate  
FROM Purchasing.PurchaseOrderDetail  
WHERE RejectedQty / ReceivedQty > 0  
AND DueDate > CONVERT(DATETIME,'20010630',101) ;  
GO  
  
```  
  
### <a name="c-using-with-check-option"></a>C. Utilizzo della clausola WITH CHECK OPTION  
 Nell'esempio seguente viene illustrata una vista denominata `SeattleOnly` che fa riferimento a cinque tabelle e consente di applicare modifiche ai dati solo per i dipendenti che risiedono a Seattle.  
  
```  
CREATE VIEW dbo.SeattleOnly  
AS  
SELECT p.LastName, p.FirstName, e.JobTitle, a.City, sp.StateProvinceCode  
FROM HumanResources.Employee e  
INNER JOIN Person.Person p  
ON p.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN Person.BusinessEntityAddress bea   
    ON bea.BusinessEntityID = e.BusinessEntityID   
    INNER JOIN Person.Address a   
    ON a.AddressID = bea.AddressID  
    INNER JOIN Person.StateProvince sp   
    ON sp.StateProvinceID = a.StateProvinceID  
WHERE a.City = 'Seattle'  
WITH CHECK OPTION ;  
GO  
```  
  
### <a name="d-using-built-in-functions-within-a-view"></a>D. Utilizzo di funzioni predefinite in una vista  
 Nell'esempio seguente viene illustrata una definizione di vista che include una funzione predefinita. Quando si utilizzano le funzioni, è necessario specificare un nome di colonna per la colonna derivata.  
  
```  
CREATE VIEW Sales.SalesPersonPerform  
AS  
SELECT TOP (100) SalesPersonID, SUM(TotalDue) AS TotalSales  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > CONVERT(DATETIME,'20001231',101)  
GROUP BY SalesPersonID;  
GO  

```  
  
### <a name="e-using-partitioned-data"></a>E. Utilizzo di dati partizionati  
 Nell'esempio seguente vengono utilizzate le tabelle denominate `SUPPLY1`, `SUPPLY2`, `SUPPLY3` e `SUPPLY4`, corrispondenti alle tabelle dei fornitori di quattro uffici dislocati in aree geografiche diverse.  
  
```  
--Create the tables and insert the values.  
CREATE TABLE dbo.SUPPLY1 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 1 and 150),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY2 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 151 and 300),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY3 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 301 and 450),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY4 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 451 and 600),  
supplier CHAR(50)  
);  
GO  
INSERT dbo.SUPPLY1 VALUES ('1', 'CaliforniaCorp'), ('5', 'BraziliaLtd')  
, ('231', 'FarEast'), ('280', 'NZ')  
, ('321', 'EuroGroup'), ('442', 'UKArchip')  
, ('475', 'India'), ('521', 'Afrique');  
GO  
--Create the view that combines all supplier tables.  
CREATE VIEW dbo.all_supplier_view  
WITH SCHEMABINDING  
AS  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY1  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY2  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY3  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY4;  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-creating-a-simple-view"></a>F. Creazione di una visualizzazione semplice  
 L'esempio seguente crea una visualizzazione selezionando solo alcune colonne della tabella di origine.  
  
```  
CREATE VIEW DimEmployeeBirthDates AS  
SELECT FirstName, LastName, BirthDate   
FROM DimEmployee;  
```  
  
### <a name="g-create-a-view-by-joining-two-tables"></a>G. Creare una vista unendo in join due tabelle  
 Nell'esempio seguente crea una visualizzazione utilizzando un `SELECT` istruzione con un `OUTER JOIN`. I risultati della query join popolano la vista.  
  
```  
CREATE VIEW view1  
AS 
SELECT fis.CustomerKey, fis.ProductKey, fis.OrderDateKey, 
  fis.SalesTerritoryKey, dst.SalesTerritoryRegion  
FROM FactInternetSales AS fis   
LEFT OUTER JOIN DimSalesTerritory AS dst   
ON (fis.SalesTerritoryKey=dst.SalesTerritoryKey);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP VIEW &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Creazione di una stored procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_refreshview &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Sys. Views &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

