---
title: Introduzione al caricamento Bulk XML (SQLXML 4.0) | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18950714bd976c224ef33627fb12528ad08b0584
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>Introduzione al caricamento bulk XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Il caricamento bulk XML è un oggetto COM autonomo che consente di caricare dati XML semistrutturati nelle tabelle di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 È possibile inserire dati XML in un database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando un'istruzione INSERT e la funzione OPENXML. L'utilità di caricamento bulk fornisce tuttavia prestazioni migliori quando è necessario inserire grandi quantità di dati XML.  
  
 Il metodo Execute del modello a oggetti il caricamento Bulk XML accetta due parametri:  
  
-   Uno schema XSD (XML Schema Definition) o uno schema XDR (XML-Data Reduced) con annotazioni. L'utilità di caricamento bulk XML interpreta questo schema di mapping e le annotazioni specificate nello schema per identificare le tabelle di SQL Server nelle quali devono essere inseriti i dati XML.  
  
-   Un documento o un frammento di documento XML (un frammento di documento è un documento privo di un singolo elemento di livello superiore). È possibile specificare un nome file o un flusso dal quale il caricamento bulk XML può leggere.  
  
 Il caricamento bulk XML interpreta lo schema di mapping e identifica le tabelle nelle quali devono essere inseriti i dati XML.  
  
 Si presuppone che l'utente abbia familiarità con le caratteristiche [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seguenti:  
  
-   Schemi XSD e XDR annotati. Per ulteriori informazioni sugli schemi XSD con annotazioni, vedere [Introduzione a schemi XSD con annotazioni &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Per informazioni sugli schemi XDR con annotazioni, vedere [schemi XDR con annotazioni &#40; deprecate in SQLXML 4.0 &#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] l'istruzione BULK insert meccanismi, ad esempio il [!INCLUDE[tsql](../../../includes/tsql-md.md)] l'istruzione BULK INSERT e l'utilità bcp. Per ulteriori informazioni, vedere [BULK INSERT &#40; Transact-SQL &#41; ](../../../t-sql/statements/bulk-insert-transact-sql.md) e [utilità bcp](../../../tools/bcp-utility.md).  
  
## <a name="streaming-of-xml-data"></a>Flusso dei dati XML  
 Poiché le dimensioni del documento XML di origine possono essere elevate, l'intero documento non viene letto in memoria per l'elaborazione del caricamento bulk. Il caricamento bulk XML interpreta invece i dati XML come un flusso e li legge. Durante la lettura dei dati, l'utilità identifica le tabelle di database, genera i record appropriati dall'origine dati XML, quindi invia i record a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per l'inserimento.  
  
 Ad esempio, il seguente documento XML di origine include  **\<cliente >** elementi e  **\<ordine >** gli elementi figlio:  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 Quando il caricamento Bulk XML legge il  **\<cliente >** elemento, genera un record per il Customertable. Quando legge il  **\</Customer. >** inserisce il caricamento Bulk XML record nella tabella di tag di fine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nello stesso modo, quando legge il  **\<ordine >** elemento, il caricamento Bulk XML genera un record per il Ordertable e quindi inserisce il record nel [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabella durante la lettura di  **\< / Order >** tag di fine.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>Operazioni di caricamento bulk XML in transazioni e non in transazioni  
 Il caricamento bulk XML può funzionare in modalità transazionale e non transazionale. Le prestazioni sono in genere ottimali se si esegue un caricamento bulk in una modalità non transazionale: ovvero, la proprietà Transaction è impostata su FALSE) e una delle seguenti condizioni è vera:  
  
-   Le tabelle nelle quali si esegue il caricamento bulk dei dati sono vuote e senza indici.  
  
-   Le tabelle includono dati e indici univoci.  
  
 L'approccio non transazionale non garantisce un rollback in caso di errore del processo di caricamento bulk, anche se possono verificarsi rollback parziali. Il caricamento bulk non transazionale è consigliabile quando il database è vuoto. In caso di errore, pertanto, è possibile eseguire una pulizia del database e riavviare il caricamento bulk XML.  
  
> [!NOTE]  
>  In modalità non transazionale il caricamento bulk XML utilizza una transazione interna predefinita e ne esegue il commit. Quando la proprietà Transaction è impostata su TRUE, il caricamento Bulk XML non chiama commit per questa transazione.  
  
 Se la proprietà della transazione è impostata su TRUE, il caricamento Bulk XML crea file temporanei, uno per ogni tabella identificata nello schema di mapping. Il caricamento bulk XML archivia innanzitutto i record del documento XML di origine in questi file temporanei. Quindi, un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT recupera tali record dai file e li archivia nelle tabelle corrispondenti. È possibile specificare il percorso di questi file temporanei utilizzando la proprietà TempFilePath. In questo caso, è necessario assicurarsi che l'account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzato con il caricamento bulk XML disponga di accesso a tale percorso. Se la proprietà TempFilePath non è specificata, il percorso predefinito specificato nella variabile di ambiente TEMP viene utilizzato per creare i file temporanei.  
  
 Se la proprietà della transazione è impostata su FALSE (impostazione predefinita), caricamento Bulk XML utilizza l'interfaccia IRowsetFastLoad di OLE DB per il caricamento bulk dei dati.  
  
 Se la proprietà ConnectionString imposta la stringa di connessione e la proprietà delle transazioni è impostata su TRUE, il caricamento Bulk XML agisce nel proprio contesto di transazione. ad esempio avvia la propria transazione ed esegue il commit o il rollback nel modo appropriato.  
  
 Se la proprietà ConnectionCommand imposta la connessione con un oggetto connessione esistente e la proprietà della transazione è impostata su TRUE, il caricamento Bulk XML non emette un'istruzione COMMIT o ROLLBACK nel caso di esito positivo o esito negativo, rispettivamente. In presenza di un errore, il caricamento bulk XML restituisce il messaggio di errore appropriato. La decisione di eseguire un'istruzione COMMIT o ROLLBACK è delegata al client che ha avviato il caricamento bulk. L'oggetto connessione utilizzato per il caricamento Bulk XML deve essere di tipo ICommand o essere un oggetto comando ADO.  
  
 In SQLXML 4.0, un ConnectionObject non può essere utilizzato con la proprietà delle transazioni impostata su FALSE. La modalità non transazionale non è supportata con un ConnectionObject perché non è possibile aprire più di un'interfaccia IRowsetFastLoad in una sessione passata.  
  
  
