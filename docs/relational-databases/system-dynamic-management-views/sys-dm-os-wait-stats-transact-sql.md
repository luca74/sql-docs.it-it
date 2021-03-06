---
title: sys.dm_os_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: 111
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
ms.openlocfilehash: c37a8f78d18a3315c188959f2f8403ef055c3155
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Restituisce informazioni su tutte le attese rilevate dai thread eseguiti. È possibile usare questa visualizzazione aggregata per diagnosticare problemi a livello di prestazioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e anche in query e batch specifici. [Sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) fornisce informazioni simili dalla sessione.  
  
> [!NOTE] 
> Per chiamare questo metodo dal **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**, utilizzare il nome **sys.dm_pdw_nodes_os_wait_stats**.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Nome del tipo di attesa. Per ulteriori informazioni, vedere [tipi di attesa](#WaitTypes), più avanti in questo argomento.|  
|waiting_tasks_count|**bigint**|Numero di attese del tipo specificato. Questo contatore viene incrementato all'inizio di ogni attesa.|  
|wait_time_ms|**bigint**|Tempo di attesa totale, espresso in millisecondi, per il tipo di attesa specifico. Il tempo comprende signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo di attesa massimo per il tipo di attesa specifico.|  
|signal_wait_time_ms|**bigint**|Differenza tra il momento in cui è stato rilevato il thread in attesa e quello in cui è stata avviata l'esecuzione del thread.|  
|pdw_node_id|**int**|L'identificatore per il nodo che utilizza questo tipo di distribuzione. <br/> **Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], richiede `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], richiede il `VIEW DATABASE STATE` autorizzazione per il database.   

##  <a name="WaitTypes"></a> Tipi di attesa  
 **Questo tipo di attesa** di attesa si verifica quando un thread di lavoro richiede l'accesso a una risorsa che non è disponibile perché la risorsa è in uso da un altro thread di lavoro o non è ancora disponibile. Un esempio di attesa di risorse è rappresentato da blocchi, latch e attese di I/O su rete e su disco. Le attese di blocchi e latch sono attese a livello di oggetti di sincronizzazione.  
  
**Attese di code**  
 Questo tipo di attesa si verifica quando un thread di lavoro è inattivo ed è in attesa dell'assegnazione di lavoro. Le attese di code si verificano principalmente nell'ambito di attività di sistema in background quali, ad esempio, il monitoraggio dei deadlock e le attività di pulizia dei record eliminati. Queste attività attenderanno l'inserimento delle richieste di lavoro in una coda di elaborazione. È possibile che le attese di code diventino periodicamente attive anche se non sono stati inseriti nuovi pacchetti nella coda.  
  
 **Attese esterne**  
 Questo tipo di attesa si verifica quando un thread di lavoro di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in attesa del completamento di un evento esterno, ad esempio una chiamata di stored procedure estesa o una query di server collegato. Se vengono rilevati problemi di blocco, è opportuno ricordare che le attese esterne non sempre implicano che il thread di lavoro sia inattivo in quanto è possibile che il thread di lavoro esegua attivamente codice esterno.  
  
 `sys.dm_os_wait_stats` visualizza la durata delle attese completate. Questa DMV non visualizza le attese correnti.  
  
 Un thread di lavoro di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene considerato in attesa se si verifica uno dei seguenti casi:  
  
-   Una risorsa diventa disponibile.  
  
-   Una coda non è vuota.  
  
-   Un processo esterno viene completato.  
  
 Anche se il thread non è più in attesa, la sua esecuzione non deve necessariamente essere avviata subito perché tale thread viene innanzitutto inserito nella coda dei thread di lavoro eseguibili e pertanto deve attendere un quantum per essere eseguito nell'utilità di pianificazione.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i contatori del tempo di attesa sono **bigint** valori e pertanto non sono soggetti al rollover dei contatori come i contatori equivalenti nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Tipi specifici di tempi di attesa durante l'esecuzione di query possono indicare colli di bottiglia oppure punti di stallo all'interno della query. In modo analogo, tempi di attesa o conteggi di attesa rilevanti a livello di server possono indicare colli di bottiglia o aree critiche nelle interazioni tra query all'interno dell'istanza del server. Ad esempio, le attese di blocco indicano contese a livello di dati da parte delle query, le attese di latch di I/O di pagina indicano tempi di risposta I/O bassi, mentre le attese di aggiornamento dei latch di pagina indicano layout di file errati.  
  
 Il contenuto di questa DMV può essere ripristinato mediante l'esecuzione del comando seguente:  
  
```sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
Questo comando reimposta tutti i contatori su 0.  
  
> [!NOTE]
> Queste statistiche non sono persistenti tra i vari riavvii di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tutti i dati sono cumulativi dall'ultimo ripristino delle statistiche oppure dall'ultimo avvio del server.  
  
 Nella tabella seguente sono elencati i tipi di attesa rilevati dalle attività.  

|tipo |Description| 
|-------------------------- |--------------------------| 
|ABR |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_LOAD |Si verifica durante l'accesso esclusivo al caricamento di assembly.| 
|ASYNC_DISKPOOL_LOCK |Si verifica in caso di tentativo di sincronizzazione di thread paralleli che eseguono attività quali, ad esempio, la creazione o l'inizializzazione di un file.| 
|ASYNC_IO_COMPLETION |Si verifica quando un'attività è in attesa del completamento dell'I/O.| 
|ASYNC_NETWORK_IO |Si verifica durante le operazioni di scrittura in rete quando l'attività è bloccata in rete. Verificare che il client stia elaborando dati dal server.| 
|ASYNC_OP_COMPLETION |TBD <br />**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_SOCKETDUP_IO |TBD <br />**Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AUDIT_GROUPCACHE_LOCK |Si verifica in caso di attesa su un blocco che controlla accesso a una cache speciale. La cache contiene le informazioni sui controlli usati per controllare ogni gruppo di azioni di controllo.| 
|AUDIT_LOGINCACHE_LOCK |Si verifica in caso di attesa su un blocco che controlla accesso a una cache speciale. La cache contiene le informazioni sui controlli usati per controllare i gruppi di azioni di controllo accesso.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |Si verifica in caso di attesa su un blocco usato per assicurare l'inizializzazione singola delle destinazioni degli eventi estesi relative ai controlli.| 
|AUDIT_XE_SESSION_MGR |Si verifica in caso di attesa su un blocco usato per sincronizzare l'avvio e l'arresto delle sessioni degli eventi estesi relative ai controlli.| 
|BACKUP |Si verifica quando un'attività è bloccata in quanto parte dell'elaborazione di un backup.| 
|BACKUP_OPERATOR |Si verifica quando un'attività è in attesa del montaggio del nastro. Per visualizzare lo stato del nastro, eseguire query su Sys.dm io_backup_tapes. Se un'operazione di montaggio non è in sospeso, questo tipo di attesa potrebbe indicare un problema a livello di hardware nell'unità nastro.| 
|BACKUPBUFFER |Si verifica quando un'attività di backup è in attesa di dati oppure di un buffer in cui archiviare dati. Questo tipo di attesa non è comune, tranne quando un'attività è in attesa del montaggio di un nastro.| 
|BACKUPIO |Si verifica quando un'attività di backup è in attesa di dati oppure di un buffer in cui archiviare dati. Questo tipo di attesa non è comune, tranne quando un'attività è in attesa del montaggio di un nastro.| 
|BACKUPTHREAD |Si verifica quando un'attività è in attesa del completamento di un'attività di backup. I tempi di attesa possono essere lunghi, da alcuni minuti a parecchie ore. Se l'attività per la quale si è verificata l'attesa è un processo di I/O, questo tipo di attesa non indica un problema.| 
|BAD_PAGE_PROCESS |Si verifica quando il logger in background delle pagine sospette tenta di evitare l'esecuzione con una frequenza superiore a 5 secondi. Un numero eccessivo di pagine sospette determina una frequente esecuzione del logger.| 
|BLOB_METADATA |TBD <br />**Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPALLOCATION |TBD <br />**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPBUILD |TBD <br />**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPARTITION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPLICATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BPSORT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_CONNECTION_RECEIVE_TASK |Si verifica durante l'attesa dell'accesso per la ricezione di un messaggio su un endpoint della connessione. L'accesso per la ricezione all'endpoint viene serializzato.| 
|BROKER_DISPATCHER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_ENDPOINT_STATE_MUTEX |Si verifica in caso di contesa per l'accesso allo stato di un endpoint di connessione di Service Broker. L'accesso allo stato per le modifiche viene serializzato.| 
|BROKER_EVENTHANDLER |Si verifica quando un'attività è in attesa del gestore di eventi primario di Service Broker. Questo tipo di attesa si verifica per brevissimi periodi.| 
|BROKER_FORWARDER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_INIT |Si verifica durante l'inizializzazione di Service Broker in ciascun database attivo. Questo tipo di attesa si verifica raramente.| 
|BROKER_MASTERSTART |Si verifica quando un'attività è in attesa per il gestore di eventi primario di Service Broker per avviare. Questo tipo di attesa si verifica per brevissimi periodi.| 
|BROKER_RECEIVE_WAITFOR |Si verifica quando l'istruzione RECEIVE WAITFOR è in attesa. Ciò significa che nessun messaggio è pronto per essere ricevuto nella coda o un conflitto di blocco impedisce la ricezione di messaggi dalla coda.| 
|BROKER_REGISTERALLENDPOINTS |Si verifica durante l'inizializzazione di un endpoint di connessione di Service Broker. Questo tipo di attesa si verifica per brevissimi periodi.| 
|BROKER_SERVICE |Si verifica quando l'elenco di Service Broker di destinazione associato a un servizio di destinazione viene aggiornato o riordinato.| 
|BROKER_SHUTDOWN |Si verifica in caso di chiusura pianificata di Service Broker. Questo tipo di attesa si verifica saltuariamente ed eventualmente per brevissimi periodi.| 
|BROKER_START |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_STOP |Si verifica quando il gestore di attività di coda di Service Broker tenta di chiudere l'attività. Il controllo di stato è serializzato e deve essere in uno stato di esecuzione prima dell'operazione.| 
|BROKER_TASK_SUBMIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TO_FLUSH |Si verifica quando gli oggetti di trasmissione di scaricamenti in memoria nel sistema di svuotamento lazy Service Broker per una tabella di lavoro.| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMITTER |Si verifica quando lo strumento di trasmissione di Service Broker è in attesa di lavoro.| 
|BUILTIN_HASHKEY_MUTEX |Può verificarsi dopo l'avvio dell'istanza, durante l'inizializzazione delle strutture di dati interne. Non si ripete dopo l'inizializzazione delle strutture di dati.| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_PRINT_RECORD |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|CHECK_SCANNER_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECKPOINT_QUEUE |Si verifica quando l'attività di checkpoint è in attesa della successiva richiesta di checkpoint.| 
|CHKPT |Si verifica all'avvio del server per indicare il thread di gestione dei checkpoint che è possibile avviare.| 
|CLEAR_DB |Si verifica durante le operazioni che modificano lo stato di un database, ad esempio l'apertura o la chiusura.| 
|CLR_AUTO_EVENT |Si verifica quando un'attività sta effettuando un'esecuzione CLR (Common Language Runtime) ed è in attesa dell'inizializzazione di un evento automatico specifico. In genere si verificano attese prolungate, che tuttavia non indicano un problema.| 
|CLR_CRST |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa di iniziare una parte critica dell'attività usata da un'altra attività.| 
|CLR_JOIN |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa del completamento di un'altra attività. Questo stato di attesa si verifica quando è presente un join tra attività.| 
|CLR_MANUAL_EVENT |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa dell'inizializzazione di un evento manuale specifico.| 
|CLR_MEMORY_SPY |Si verifica durante l'attesa dell'acquisizione del blocco per una struttura di dati usata per registrare tutte le allocazioni della memoria virtuale che provengono da CLR. La struttura di dati è bloccata per gestire l'integrità se l'accesso è parallelo.| 
|CLR_MONITOR |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa di acquisire un blocco per il monitoraggio.| 
|CLR_RWLOCK_READER |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa di un blocco del reader.| 
|CLR_RWLOCK_WRITER |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa di un blocco del writer.| 
|CLR_SEMAPHORE |Si verifica quando un'attività sta effettuando un'esecuzione CLR ed è in attesa di un semaforo.| 
|CLR_TASK_START |Si verifica durante l'attesa del completamento dell'avvio di un'attività CLR.| 
|CLRHOST_STATE_ACCESS |Si verifica in caso di attesa per l'acquisizione dell'accesso esclusivo alle strutture di dati di hosting CLR. Questo tipo di attesa si verifica durante la configurazione o la rimozione del runtime CLR.| 
|CMEMPARTITIONED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CMEMTHREAD |Si verifica quando un'attività è in attesa di un oggetto memoria affidabile. Il tempo di attesa potrebbe aumentare in caso di contesa causata da più attività che tentano di allocare memoria dallo stesso oggetto memoria.| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COUNTRECOVERYMGR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CREATE_DATINISERVICE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CXCONSUMER |Quando un thread consumer in attesa di un thread producer inviare righe, si verifica con i piani di query parallele. Questo è normale di esecuzione delle query parallele. <br /> **Si applica a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |Si verifica con i piani di query paralleli durante la sincronizzazione di iteratore di scambio di query processor e quando la produzione e l'utilizzo di righe. Se l'attesa è eccessiva e non è possibile ridurla ottimizzando la query (ad esempio aggiungendo indici), regolare l'opzione Cost threshold for parallelism o abbassare il grado di parallelismo.<br /> **Nota:** In [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e [!INCLUDE[ssSDS](../../includes/sssds-md.md)], CXPACKET si riferisce solo per sincronizzare l'iteratore di scambio di query processor e per la produzione di righe per i thread consumer. Thread consumer vengono registrati separatamente nel tipo di attesa CXCONSUMER.| 
|CXROWSET_SYNC |Si verifica durante un'analisi di intervalli parallela.| 
|DAC_INIT |Si verifica durante l'inizializzazione della connessione amministrativa dedicata.| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBMIRROR_DBM_EVENT |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|DBMIRROR_DBM_MUTEX |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|DBMIRROR_EVENTS_QUEUE |Si verifica quando il mirroring del database è in attesa di eventi da elaborare.| 
|DBMIRROR_SEND |Si verifica quando un'attività è in attesa della cancellazione di un backlog delle comunicazioni nel livello rete per essere in grado di inviare messaggi. Indica che nel livello comunicazioni si sta verificando un overload che può pregiudicare la velocità effettiva dei dati di mirroring del database.| 
|DBMIRROR_WORKER_QUEUE |Indica che l'attività di lavoro del mirroring del database è in attesa di ulteriore lavoro.| 
|DBMIRRORING_CMD |Si verifica quando un'attività è in attesa dello scaricamento su disco dei record di log. Questo stato di attesa viene in genere mantenuto per lunghi periodi di tempo.| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBSEEDING_OPERATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DEADLOCK_ENUM_MUTEX |Si verifica quando il monitoraggio dei deadlock e Sys.dm os_waiting_tasks cercano di garantire che SQL Server non è in esecuzione più ricerche di deadlock contemporaneamente.| 
|DEADLOCK_TASK_SEARCH |Un tempo di attesa elevato per questa risorsa indica che il server sta eseguendo query su sys.dm_os_waiting_tasks e che tali query bloccano l'esecuzione della ricerca di deadlock nell'ambito del monitoraggio dei deadlock. Questo tipo di attesa viene usato soltanto dalla funzionalità di monitoraggio dei deadlock. Le query su sys.dm_os_waiting_tasks utilizzano DEADLOCK_ENUM_MUTEX.| 
|DEBUG |Durante l'esecuzione di Transact-SQL e il debug CLR per la sincronizzazione interna.| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_POLL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_SYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISABLE_VERSIONING |Si verifica quando SQL Server esegue il polling il gestore delle transazioni di versione per verificare se il timestamp della transazione attiva meno recente è successivo rispetto al timestamp relativo quando lo stato di modifica. In questo caso, vengono completate tutte le transazioni snapshot avviate prima dell'esecuzione dell'istruzione ALTER DATABASE. Questo stato di attesa viene utilizzato quando SQL Server disabilita il controllo delle versioni tramite l'istruzione ALTER DATABASE.| 
|DISKIO_SUSPEND |Si verifica quando un'attività è in attesa di accedere a un file quando è attivo un backup esterno. Questo tipo di attesa viene segnalato per ogni processo utente in attesa. Un conteggio maggiore di 5 per processo utente può indicare che il completamento del backup esterno sta richiedendo troppo tempo.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISPATCHER_QUEUE_SEMAPHORE |Si verifica quando un thread del pool di dispatcher è in attesa di più lavori da elaborare. Si prevede che il tempo di attesa per questo tipo di attesa aumenti quando il dispatcher è inattivo.| 
|DLL_LOADING_MUTEX |Si verifica una volta durante l'attesa del caricamento della DLL del parser XML.| 
|DPT_ENTRY_LOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROPTEMP |Si verifica tra diversi tentativi di eliminare un oggetto temporaneo, se il tentativo precedente ha avuto esito negativo. La durata dell'attesa aumenta in modo esponenziale con ogni tentativo di eliminazione non riuscito.| 
|DTC |Si verifica quando un'attività è in attesa di un evento usato per gestire la transizione di stato. Questo stato i controlli quando il recupero delle transazioni Microsoft Distributed Transaction Coordinator (MS DTC) si verifica dopo che SQL Server riceve una notifica che il servizio MS DTC è diventato non disponibile.| 
|DTC_ABORT_REQUEST |Si verifica in una sessione di lavoro MS DTC quando la sessione è in attesa di acquisire la proprietà di una transazione MS DTC. Non appena MS DTC acquisisce la proprietà della transazione, la sessione può eseguire il rollback della transazione. In genere, la sessione attenderà un'altra sessione che sta utilizzando la transazione.| 
|DTC_RESOLVE |Si verifica quando un'attività di recupero è in attesa del database master in una transazione tra database in modo che l'attività possa eseguire una query sul risultato della transazione.| 
|DTC_STATE |Si verifica quando un'attività è in attesa di un evento che impedisce le modifiche all'oggetto stato globale MS DTC interno. Questo stato deve essere mantenuto per brevissimi periodi di tempo.| 
|DTC_TMDOWN_REQUEST |Si verifica in una sessione di lavoro MS DTC quando SQL Server riceve una notifica che il servizio MS DTC non è disponibile. Il thread di lavoro attenderà innanzitutto l'avvio del processo di recupero MS DTC. Il thread di lavoro attende quindi di ottenere il risultato della transazione distribuita su cui sta lavorando. Ciò potrebbe continuare finché non viene ristabilita la connessione al servizio MS DTC.| 
|DTC_WAITFOR_OUTCOME |Si verifica quando le attività di recupero attendono l'attivazione di MS DTC per consentire la risoluzione delle transazioni preparate.| 
|DTCNEW_ENLIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_PREPARE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_RECOVERY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TM |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCPNTSYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DUMP_LOG_COORDINATOR |Si verifica quando un'attività principale è in attesa che una sottoattività generi dati. In genere, questo stato non si verifica mai. Un tempo di attesa prolungato indica un blocco imprevisto. È pertanto necessario verificare la sottoattività.| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|EC |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|EE_PMOLOCK |Si verifica durante la sincronizzazione di determinati tipi di allocazioni di memoria nel corso dell'esecuzione di istruzioni.| 
|EE_SPECPROC_MAP_INIT |Si verifica durante la sincronizzazione della creazione della tabella hash delle procedure interne. Questa attesa può verificarsi solo durante l'accesso iniziale della tabella hash dopo l'avvio dell'istanza di SQL Server.| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ENABLE_VERSIONING |Si verifica quando SQL Server è in attesa per tutte le transazioni di aggiornamento in questo database, il completamento prima di dichiarare il database pronto per la transizione allo stato è consentito l'isolamento dello snapshot. Questo stato viene utilizzato quando SQL Server consente l'isolamento dello snapshot tramite l'istruzione ALTER DATABASE.| 
|ERROR_REPORTING_MANAGER |Si verifica durante la sincronizzazione delle inizializzazioni di più log degli errori simultanei.| 
|EXCHANGE |Si verifica durante la sincronizzazione nell'iteratore di scambio di Query Processor nel corso di query parallele.| 
|EXECSYNC |Si verifica durante query parallele nel corso della sincronizzazione in Query Processor in aree non correlate all'iteratore di scambio. Tali aree sono, ad esempio, bitmap, oggetti BLOB (Binary Large Object) e l'iteratore di spool. È possibile che gli oggetti BLOB utilizzino di frequente questo stato di attesa.| 
|EXECUTION_PIPE_EVENT_INTERNAL |Si verifica durante la sincronizzazione tra parti del produttore e dell'utente dell'esecuzione batch inviate tramite il contesto di connessione.| 
|EXTERNAL_RG_UPDATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] alla versione corrente.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_WAIT_ON_LAUNCHER, |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FAILPOINT |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FCB_REPLICA_READ |Si verifica quando le letture di un file sparse snapshot oppure di uno snapshot temporaneo creato da DBCC vengono sincronizzate.| 
|FCB_REPLICA_WRITE |Si verifica durante la sincronizzazione di operazioni di push o pull di una pagina in un file sparse di uno snapshot oppure di uno snapshot temporaneo creato da DBCC.| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_FIND |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_PARENT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_STATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FILEOBJECT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_TABLE_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NTFS_STORE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RECOVERY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_COMM |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_DB |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_TABLE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILE_VALIDATION_THREADS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CACHE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FCB |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILETABLE_SHUTDOWN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FOREIGN_REDO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] alla versione corrente.| 
|FORWARDER_TRANSITION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FS_FC_RWLOCK |Si verifica in caso di attesa del Garbage Collector di FILESTREAM per le seguenti operazioni:| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |Si verifica quando il Garbage Collector di FILESTREAM attende il completamento delle attività di pulizia.| 
|FS_HEADER_RWLOCK |Si verifica in caso di attesa per l'accesso all'intestazione FILESTREAM di un contenitore di dati FILESTREAM per leggere o aggiornare il contenuto nel file di intestazione (Filestream.hdr) di FILESTREAM.| 
|FS_LOGTRUNC_RWLOCK |Si verifica in caso di attesa per l'accesso al troncamento del log di FILESTREAM per le seguenti operazioni:| 
|FSA_FORCE_OWN_XACT |Si verifica quando un'operazione di I/O del file FILESTREAM deve essere associata alla transazione associata, ma la transazione appartiene attualmente a un'altra sessione.| 
|FSAGENT |Si verifica quando un'operazione di I/O del file FILESTREAM attende una risorsa dell'agente di FILESTREAM usata da un'altra operazione di I/O di file.| 
|FSTR_CONFIG_MUTEX |Si verifica in caso di attesa per il completamento di un'altra riconfigurazione di funzionalità di FILESTREAM.| 
|FSTR_CONFIG_RWLOCK |Si verifica in caso di attesa per serializzare l'accesso ai parametri di configurazione di FILESTREAM.| 
|FT_COMPROWSET_RWLOCK |Full-text è in attesa di un'operazione di metadati di frammenti. Documentato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FT_IFTS_RWLOCK |Full-text è in attesa di sincronizzazione interna. Documentato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FT_IFTS_SCHEDULER_IDLE_WAIT |Tipo di attesa sospensione dell'utilità di pianificazione full-text. L'utilità di pianificazione è inattiva.| 
|FT_IFTSHC_MUTEX |Full-text è in attesa di un'operazione di controllo fdhost. Documentato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FT_IFTSISM_MUTEX |Full-text è in attesa di un'operazione di comunicazione. Documentato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FT_MASTER_MERGE |Full-text è in attesa di un'operazione di unione nell'indice master. Documentato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_METADATA_MUTEX |Documentato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_RESTART_CRAWL |Si verifica quando è necessario riavviare una ricerca per indicizzazione full-text dall'ultimo punto valido noto per correggere un errore temporaneo. L'attesa consente alle attività di lavoro usate per il popolamento di completare il passaggio corrente o uscirne.| 
|FULLTEXT GATHERER |Si verifica durante la sincronizzazione delle operazioni full-text.| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_CREATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GUARDIAN |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|HADR_AG_MUTEX |Si verifica quando un'istruzione DDL Always On o un comando di Windows Server Failover Clustering è in attesa per l'accesso in lettura/scrittura esclusivo alla configurazione di un gruppo di disponibilità., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Si verifica quando un'istruzione DDL Always On o un comando di Windows Server Failover Clustering è in attesa per l'accesso in lettura/scrittura esclusivo allo stato di runtime della replica locale del gruppo di disponibilità associato., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_MANAGER_MUTEX |Si verifica quando l'arresto di una replica di disponibilità è in attesa del completamento dell'avvio o l'avvio di una replica di disponibilità è in attesa del completamento dell'arresto. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |Il server di pubblicazione di un evento di replica di disponibilità, ad esempio una modifica di stato o di configurazione, è in attesa dell'accesso in lettura/scrittura esclusivo all'elenco di sottoscrittori eventi. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_BULK_LOCK |Il database primario AlwaysOn ha ricevuto una richiesta di backup da un database secondario ed è in attesa per lo sfondo del thread per completare l'elaborazione della richiesta durante l'acquisizione o il rilascio del blocco BulkOp., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_QUEUE |Il thread in background di backup del database primario Always On è in attesa per una nuova richiesta di lavoro dal database secondario. (in genere, ciò si verifica quando il database primario contenente il log BulkOp ed è in attesa per il database secondario indicare che il database primario può rilasciare il blocco)., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CLUSAPI_CALL |Un thread di SQL Server è in attesa di passare dalla modalità non preemptive (pianificata da SQL Server) alla modalità preemptive (pianificata dal sistema operativo) per richiamare l'API di Clustering di Failover di Windows Server., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_COMPRESSED_CACHE_SYNC |In attesa dell'accesso alla cache di blocchi del log compresso che viene utilizzata per evitare una compressione ridondante dei blocchi di log inviati a più database secondari., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_FLOW_CONTROL |Attesa di messaggi da inviare al partner quando viene raggiunto il numero massimo di messaggi in coda. Indica che le analisi del log vengono eseguite più rapidamente degli invii di rete. Si tratta di un problema solo se invii sono più lenti del previsto., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_VERSIONING_STATE |Si verifica la modifica dello stato di controllo delle versioni di un database secondario Always On. Questo tipo di attesa strutture dati interne ed è in genere è molto breve e senza effetti diretti sull'accesso ai dati., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RESTART |In attesa di riavvio nel controllo di gruppi di disponibilità AlwaysOn del database. In condizioni normali, infatti, non un problema del cliente sono previste attese., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Una query su oggetti in un database secondario leggibile di un sempre nel gruppo di disponibilità è bloccato su versioni delle righe mentre è in attesa del commit o rollback di tutte le transazioni in transito quando la replica secondaria è stata abilitata per i carichi di lavoro di letture. Questo tipo di attesa assicura che le versioni di riga siano disponibili prima dell'esecuzione di una query con isolamento dello snapshot., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_COMMAND |In attesa per le risposte ai messaggi di conversazione a (che richiedono una risposta esplicita da altro lato, utilizzando l'infrastruttura di messaggi di conversazione Always On). Un numero di tipi di messaggi utilizza questo tipo di attesa., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_COMPLETION_SYNC |In attesa per le risposte ai messaggi di conversazione a (che richiedono una risposta esplicita da altro lato, utilizzando l'infrastruttura di messaggi di conversazione Always On). Un numero di tipi di messaggi utilizza questo tipo di attesa., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_START_SYNC |Un'istruzione DDL Always On o un comando di Windows Server Failover Clustering è in attesa dell'accesso serializzato a un database di disponibilità e il relativo stato di runtime., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER |Il server di pubblicazione di un evento di replica di disponibilità, ad esempio una modifica di stato o di configurazione, è in attesa dell'accesso in lettura/scrittura esclusivo allo stato di runtime di un sottoscrittore eventi che corrisponde a un database di disponibilità. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |Il server di pubblicazione di un evento di replica di disponibilità, ad esempio una modifica di stato o di configurazione, è in attesa dell'accesso in lettura/scrittura esclusivo all'elenco di sottoscrittori eventi che corrispondono ai database di disponibilità. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSTATECHANGE_SYNC |Attesa del controllo di concorrenza per aggiornare lo stato della replica di database interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FABRIC_CALLBACK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_BLOCK_FLUSH |La gestione del trasporto FILESTREAM Always On è in attesa fino al termine dell'elaborazione di un blocco del log., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_CLOSE |La gestione del trasporto FILESTREAM Always On è in attesa fino a quando non viene elaborato il prossimo file FILESTREAM e il relativo handle chiuso., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_REQUEST |Un Always On è in attesa della replica secondaria per la replica primaria per l'invio di tutte le richieste di FILESTREAM file durante l'annullamento., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR |La gestione del trasporto FILESTREAM Always On è in attesa di blocco di lettura/scrittura che protegge la gestione FILESTREAM sempre sui / o durante l'avvio o arresto., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |La gestione FILESTREAM sempre sui / o è in attesa di completamento i/o., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_MANAGER |La gestione del trasporto FILESTREAM Always On è in attesa del blocco di lettura/scrittura che consente di proteggere la gestione del trasporto FILESTREAM Always On durante l'avvio o arresto., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_GROUP_COMMIT |L'elaborazione del commit della transazione è in attesa di consentire un commit di gruppo in modo che sia possibile l'inserimento di più record di log del commit in un unico blocco del log. Questo tipo di attesa è una condizione prevista che consente di ottimizzare il / o di log, acquisire e operazioni di invio., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_SYNC |Controllo della concorrenza relativa all'acquisizione del log o applicazione dell'oggetto durante la creazione o l'eliminazione delle analisi. Si tratta di un'attesa prevista quando i partner modificano lo stato di connessione o di stato., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_WAIT |Attesa che diventino disponibili i record di log. Si può verificare quando si attende la generazione di nuovi record di log tramite connessioni o il completamento di I/O quando la lettura del log non viene eseguita nella cache. Si tratta di un'attesa prevista se l'analisi del log è stato aggiornato alla fine del log o viene letta dal disco., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGPROGRESS_SYNC |Attesa del controllo della concorrenza quando si aggiorna lo stato di avanzamento del log delle repliche di database., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_DEQUEUE |Un'attività in background tramite cui vengono elaborate notifiche di Windows Server Failover Clustering è in attesa della prossima notifica. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |La gestione delle repliche disponibilità Always On è in attesa dell'accesso serializzato allo stato di runtime di un'attività in background che elabora le notifiche di Windows Server Failover Clustering. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |Un'attività in background è in attesa del completamento dell'avvio di un'attività in background tramite cui vengono elaborate notifiche di Windows Server Failover Clustering. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |Un'attività in background è in attesa del completamento di un'attività in background tramite cui vengono elaborate notifiche di Windows Server Failover Clustering. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_PARTNER_SYNC |Attesa del controllo della concorrenza nell'elenco di partner., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_READ_ALL_NETWORKS |Attesa di ottenere l'accesso in lettura o scrittura all'elenco di reti WSFC. Solo per uso interno. Nota: Il motore viene mantenuto un elenco di reti WSFC che viene utilizzato nelle viste a gestione dinamica (ad esempio Sys.dm hadr_cluster_networks) o per convalidare sempre in Transact-SQL con le istruzioni che fanno riferimento a WSFC informazioni sulla rete. Questo elenco viene aggiornato all'avvio del motore, correlate a WSFC notifiche e interno AlwaysOn riavvio (ad esempio mediante perdita e recupero del quorum WSFC). Le attività verranno di solito bloccate quando è in corso un aggiornamento nell'elenco in questione. , <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |Attesa della connessione del database secondario al database primario prima dell'esecuzione del recupero. Si tratta di un'attesa prevista, che può prolungarsi se lenta per stabilire la connessione al database primario., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_UNDO |Il recupero del database è in attesa del completamento della fase di ripristino e inizializzazione da parte del database secondario che ne consente il ripristino al punto di log comune con il database primario. Si tratta di un'attesa prevista dopo i failover. Annullare sia possibile rilevare lo stato di avanzamento tramite il monitoraggio di sistema di Windows (perfmon.exe) e viste a gestione dinamica., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_REPLICAINFO_SYNC |In attesa per il controllo della concorrenza aggiornare lo stato corrente della replica., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNC_COMMIT |Attesa dell'elaborazione del commit della transazione per la finalizzazione del log da parte dei database secondari sincronizzati. Questa attesa viene inoltre riflessa dal contatore delle prestazioni Ritardo transazioni. Questo tipo di attesa è previsto per sincronizzati gruppi di disponibilità e indica il tempo di invio, scrittura e riconoscimento del log ai database secondari., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNCHRONIZING_THROTTLE |Attesa dell'elaborazione del commit della transazione per consentire l'aggiornamento da parte di un database secondario di sincronizzazione alla fine del log primario per la transazione allo stato sincronizzato. Si tratta di un'attesa prevista quando un database secondario viene aggiornato., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC |Il sistema interno AlwaysOn o il cluster WSFC richiede che i listener di avvio o l'arresto. L'elaborazione di questa richiesta è sempre asincrona ed è disponibile un meccanismo di rimozione delle richieste ridondanti. Inoltre, si possono verificare momenti in cui questa elaborazione viene sospesa a causa di modifiche di configurazione. Questo tipo di attesa viene usato da tutte le attese correlate a questo meccanismo di sincronizzazione del listener. Solo per uso interno., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |Utilizzato alla fine di un'istruzione sempre in Transact-SQL che richiede l'avvio e/o l'arresto del listener del gruppo anavailability. Dal momento che l'operazione di avvio/arresto viene eseguita in modo asincrono, il thread dell'utente verrà bloccata utilizzando questo tipo di attesa fino a quando non è nota la situazione del listener., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TIMER_TASK |Attesa per ottenere il blocco sull'oggetto attività del timer, nonché per le attese effettive tra i tempi in cui il lavoro viene effettuato. Ad esempio, per un'attività che viene eseguito ogni 10 secondi, dopo un'esecuzione, gruppi di disponibilità AlwaysOn attende circa 10 secondi, ripianificare l'attività e il tempo di attesa è incluso in questo caso., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_DBRLIST |Attesa dell'accesso all'elenco di repliche di database del livello di trasporto. Utilizzato per lo spinlock che concede l'accesso a esso., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_FLOW_CONTROL |In attesa quando il numero di messaggi in sospeso non riconosciuti Always On è supera la soglia del controllo del flusso. Si tratta di una base di replica a altra di disponibilità (non su una database a database di base)., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_SESSION |Gruppi di disponibilità AlwaysOn è in attesa durante la modifica o l'accesso allo stato di trasporto sottostante., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_POOL |Attesa del controllo della concorrenza sull'oggetto attività di lavoro in background gruppi di disponibilità AlwaysOn., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_QUEUE |Gruppi di disponibilità AlwaysOn in background thread di lavoro in attesa di un nuovo lavoro da assegnare. Si tratta di un'attesa prevista quando sono disponibili thread di lavoro pronti in attesa di un nuovo lavoro, ovvero lo stato normale., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_XRF_STACK_ACCESS |L'accesso (cercare, aggiungere ed eliminare) lo stack di fork di recupero esteso per un database di disponibilità AlwaysOn., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HCCO_CACHE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HK_RESTORE_FILEMAP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTBUILD |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTDELETE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTMEMO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREINIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREPARTITION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTTP_ENUMERATION |Si verifica all'avvio per enumerare gli endpoint HTTP per avviare HTTP.| 
|HTTP_START |Si verifica quando una connessione è in attesa che HTTP completi l'inizializzazione.| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IMPPROV_IOWAIT |Si verifica quando SQL Server in attesa di completamento dei / o di un caricamento bulk.| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|INTERNAL_TESTING |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|IO_AUDIT_MUTEX |Si verifica durante la sincronizzazione di buffer di eventi di traccia.| 
|IO_COMPLETION |Si verifica durante l'attesa del completamento di operazioni di I/O. Questo tipo di attesa rappresenta in genere operazioni di I/O su pagine non di dati. Attese di completamento dei / o di pagine di dati vengono visualizzati come PAGEIOLATCH\_ \* è in attesa.| 
|IO_QUEUE_LIMIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IO_RETRY |Si verifica quando un'operazione di I/O, quale un'operazione di lettura o scrittura sul disco, non riesce a causa di risorse insufficienti e viene ritentata l'operazione.| 
|IOAFF_RANGE_QUEUE |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|KSOURCE_WAKEUP |Viene usato dall'attività di controllo dei servizi durante l'attesa di richieste da Gestione controllo servizi. Sono previste attese prolungate, che non indicano un problema.| 
|KTM_ENLISTMENT |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|KTM_RECOVERY_MANAGER |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|KTM_RECOVERY_RESOLUTION |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|LATCH_DT |Si verifica durante l'attesa di un latch di eliminazione (DT). Non include i latch del buffer o i latch di contrassegno di transazione. Un elenco di LATCH\_ \* attese è disponibile in sys.dm os_latch_stats. Le attese sys.dm_os_latch_stats LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT sono raggruppate.| 
|LATCH_EX |Si verifica durante l'attesa di un latch esclusivo (EX). Non include i latch del buffer o i latch di contrassegno di transazione. Un elenco di LATCH\_ \* attese è disponibile in sys.dm os_latch_stats. Le attese sys.dm_os_latch_stats LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT sono raggruppate.| 
|LATCH_KP |Si verifica durante l'attesa di un latch conservativo (KP). Non include i latch del buffer o i latch di contrassegno di transazione. Un elenco di LATCH\_ \* attese è disponibile in sys.dm os_latch_stats. Le attese sys.dm_os_latch_stats LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT sono raggruppate.| 
|LATCH_NL |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|LATCH_SH |Si verifica durante l'attesa di un latch di condivisione (SH). Non include i latch del buffer o i latch di contrassegno di transazione. Un elenco di LATCH\_ \* attese è disponibile in sys.dm os_latch_stats. Le attese sys.dm_os_latch_stats LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT sono raggruppate.| 
|LATCH_UP |Si verifica durante l'attesa di un latch di aggiornamento (UP). Non include i latch del buffer o i latch di contrassegno di transazione. Un elenco di LATCH\_ \* attese è disponibile in sys.dm os_latch_stats. Le attese sys.dm_os_latch_stats LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT sono raggruppate.| 
|LAZYWRITER_SLEEP |Si verifica quando le attività Lazywriter vengono sospese. Si tratta di una misura della durata dell'attesa delle attività in background. Non considerare questo stato durante il rilevamento di stalli a livello di utente.| 
|LCK_M_BU |Si verifica quando un'attività è in attesa di acquisire un blocco aggiornamenti bulk (BU).| 
|LCK_M_BU_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco aggiornamenti bulk (BU) con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_BU_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco aggiornamenti bulk (BU) con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo condiviso (IS).| 
|LCK_M_IS_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo condiviso (IS) con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo condiviso (IS) con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo di aggiornamento (IU).| 
|LCK_M_IU_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo di aggiornamento (IU) con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo di aggiornamento (IU) con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo esclusivo (IX).| 
|LCK_M_IX_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo esclusivo (IX) con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco preventivo esclusivo (IX) con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL |Si verifica quando un'attività è in attesa di acquisire un blocco NULL per il valore di chiave corrente e un blocco di intervallo di inserimento tra la chiave corrente e quella precedente. Un blocco NULL per la chiave è un blocco a rilascio immediato.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco NULL con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo di inserimento con blocchi di interruzione tra la chiave corrente e quella precedente. Un blocco NULL per la chiave è un blocco a rilascio immediato. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco NULL con priorità bassa per il valore di chiave corrente e un blocco di intervallo di inserimento con priorità bassa tra la chiave corrente e quella precedente. Un blocco NULL per la chiave è un blocco a rilascio immediato. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso per il valore di chiave corrente e un blocco di intervallo di inserimento tra la chiave corrente e quella precedente.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo di inserimento con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con priorità bassa per il valore di chiave corrente e un blocco di intervallo di inserimento con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento per il valore di chiave corrente e un blocco di intervallo di inserimento tra la chiave corrente e quella precedente.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |L'attività è in attesa di acquisire un blocco di aggiornamento con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo di inserimento con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U_LOW_PRIORITY |L'attività è in attesa di acquisire un blocco di aggiornamento con priorità bassa per il valore di chiave corrente e un blocco di intervallo di inserimento con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo per il valore di chiave corrente e un blocco di intervallo di inserimento tra la chiave corrente e quella precedente.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo di inserimento con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo con priorità bassa per il valore di chiave corrente e un blocco di intervallo di inserimento con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso per il valore di chiave corrente e un blocco di intervallo condiviso tra la chiave corrente e quella precedente.| 
|LCK_M_RS_S_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo condiviso con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con priorità bassa per il valore di chiave corrente e un blocco di intervallo condiviso con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento per il valore di chiave corrente e un blocco di intervallo di aggiornamento tra la chiave corrente e quella precedente.| 
|LCK_M_RS_U_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo di aggiornamento con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento con priorità bassa per il valore di chiave corrente e un blocco di intervallo di aggiornamento con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso per il valore di chiave corrente e un blocco di intervallo esclusivo tra la chiave corrente e quella precedente.| 
|LCK_M_RX_S_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo esclusivo con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con priorità bassa per il valore di chiave corrente e un blocco di intervallo esclusivo con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento per il valore di chiave corrente e un blocco di intervallo esclusivo tra la chiave corrente e quella precedente.| 
|LCK_M_RX_U_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo esclusivo con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento con priorità bassa per il valore di chiave corrente e un blocco di intervallo esclusivo con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo per il valore di chiave corrente e un blocco di intervallo esclusivo tra la chiave corrente e quella precedente.| 
|LCK_M_RX_X_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo con blocchi di interruzione per il valore di chiave corrente e un blocco di intervallo esclusivo con blocchi di interruzione tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo con priorità bassa per il valore di chiave corrente e un blocco di intervallo esclusivo con priorità bassa tra la chiave corrente e quella precedente. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso.| 
|LCK_M_S_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M |Si verifica quando un'attività è in attesa di acquisire un blocco di modifica dello schema.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco di modifica dello schema con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco di modifica dello schema con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso dello schema.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco di condivisione dello schema con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco di condivisione dello schema con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso preventivo di aggiornamento.| 
|LCK_M_SIU_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso preventivo di aggiornamento con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso preventivo di aggiornamento con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso preventivo esclusivo.| 
|LCK_M_SIX_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso preventivo esclusivo con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco condiviso preventivo esclusivo con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento.| 
|LCK_M_U_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento preventivo esclusivo.| 
|LCK_M_UIX_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento preventivo esclusivo con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco di aggiornamento preventivo esclusivo con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo.| 
|LCK_M_X_ABORT_BLOCKERS |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo con blocchi di interruzione. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X_LOW_PRIORITY |Si verifica quando un'attività è in attesa di acquisire un blocco esclusivo con priorità bassa. (Correlata all'opzione di attesa per priorità bassa di ALTER TABLE e ALTER INDEX.), <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_POOL_SCAN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_RATE_GOVERNOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGBUFFER |Si verifica quando un'attività è in attesa di spazio nel buffer del log per l'archiviazione di un record di log. Valori costantemente alti possono indicare che i dispositivi di log non sono in grado di far fronte alla quantità di log generati dal server.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGGENERATION |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|LOGMGR |Si verifica quando un'attività è in attesa del completamento di qualsiasi operazione di I/O di log in sospeso prima di chiudere il log durante la chiusura del database.| 
|LOGMGR_FLUSH |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|LOGMGR_PMM_LOG |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGMGR_QUEUE |Si verifica quando l'attività di scrittura del log è in attesa di richieste di lavoro.| 
|LOGMGR_RESERVE_APPEND |Si verifica quando un'attività è in attesa di verificare se il troncamento del log libera spazio di log per consentire all'attività di scrivere un nuovo record di log. Valutare la possibilità di aumentare le dimensioni dei file di log per il database interessato allo scopo di ridurre l'attesa.| 
|LOGPOOL_CACHESIZE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMERSET |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_FREEPOOLS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_MGRSET |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOWFAIL_MEMMGR_QUEUE |Si verifica durante l'attesa di memoria disponibile per l'utilizzo.| 
|MD_AGENT_YIELD |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_ALLOCATION_EXT |Si verifica durante l'allocazione di memoria dal pool di memoria interno di SQL Server o il sistema operativo., <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_GRANT_UPDATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|MIGRATIONBUFFER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MISCELLANEOUS |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|MISCELLANEOUS |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|MSQL_DQ |Si verifica quando un'attività è in attesa del completamento di un'operazione di query distribuita. Viene usato per rilevare potenziali deadlock di applicazioni MARS (Multiple Active Result Set). L'attesa si arresta al completamento della chiamata della query distribuita.| 
|MSQL_XACT_MGR_MUTEX |Si verifica quando un'attività è in attesa di acquisire la proprietà della gestione transazioni della sessione per eseguire un'operazione di transazione a livello di sessione.| 
|MSQL_XACT_MUTEX |Si verifica durante la sincronizzazione dell'utilizzo della transazione. Per poter usare la transazione, una richiesta deve prima acquisire il mutex.| 
|MSQL_XP |Si verifica quando un'attività è in attesa del completamento di una stored procedure estesa. SQL Server utilizza questo stato di attesa per rilevare potenziali deadlock di applicazioni MARS. L'attesa si arresta al completamento della chiamata della stored procedure estesa.| 
|MSSEARCH |Si verifica durante le chiamate di ricerca full-text. L'attesa si arresta al completamento dell'operazione full-text. Non indica contesa, bensì la durata delle operazioni full-text.| 
|NET_WAITFOR_PACKET |Si verifica quando una connessione è in attesa di un pacchetto di rete durante una lettura in rete.| 
|NETWORKSXMLMGRLOAD |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |Si verifica quando SQL Server chiama il Provider SQL Server Native Client OLE DB. Questo tipo di attesa non viene usato per la sincronizzazione. Indica invece la durata delle chiamate al provider OLE DB.| 
|ONDEMAND_TASK_QUEUE |Si verifica quando un'attività in background è in attesa di richieste di attività di sistema con priorità elevata. Tempi di attesa prolungati indicano l'assenza di richieste con priorità elevata da elaborare e non costituiscono un problema.| 
|PAGEIOLATCH_DT |Si verifica quando un'attività è in attesa di un latch per un buffer in una richiesta di I/O. La richiesta di latch è in modalità di eliminazione. Attese prolungate possono indicare problemi con il sottosistema disco.| 
|PAGEIOLATCH_EX |Si verifica quando un'attività è in attesa di un latch per un buffer in una richiesta di I/O. La richiesta di latch è in modalità esclusiva. Attese prolungate possono indicare problemi con il sottosistema disco.| 
|PAGEIOLATCH_KP |Si verifica quando un'attività è in attesa di un latch per un buffer in una richiesta di I/O. La richiesta di latch è in modalità di mantenimento. Attese prolungate possono indicare problemi con il sottosistema disco.| 
|PAGEIOLATCH_NL |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PAGEIOLATCH_SH |Si verifica quando un'attività è in attesa di un latch per un buffer in una richiesta di I/O. La richiesta di latch è in modalità condivisa. Attese prolungate possono indicare problemi con il sottosistema disco.| 
|PAGEIOLATCH_UP |Si verifica quando un'attività è in attesa di un latch per un buffer in una richiesta di I/O. La richiesta di latch è in modalità di aggiornamento. Attese prolungate possono indicare problemi con il sottosistema disco.| 
|PAGELATCH_DT |Si verifica quando un'attività è in attesa di un latch per un buffer non incluso in una richiesta di I/O. La richiesta di latch è in modalità di eliminazione.| 
|PAGELATCH_EX |Si verifica quando un'attività è in attesa di un latch per un buffer non incluso in una richiesta di I/O. La richiesta di latch è in modalità esclusiva.| 
|PAGELATCH_KP |Si verifica quando un'attività è in attesa di un latch per un buffer non incluso in una richiesta di I/O. La richiesta di latch è in modalità di mantenimento.| 
|PAGELATCH_NL |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PAGELATCH_SH |Si verifica quando un'attività è in attesa di un latch per un buffer non incluso in una richiesta di I/O. La richiesta di latch è in modalità condivisa.| 
|PAGELATCH_UP |Si verifica quando un'attività è in attesa di un latch per un buffer non incluso in una richiesta di I/O. La richiesta di latch è in modalità di aggiornamento.| 
|PARALLEL_BACKUP_QUEUE |Si verifica durante la serializzazione dell'output generato da RESTORE HEADERONLY, RESTORE FILELISTONLY o RESTORE LABELONLY.| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_ABR |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Si verifica quando l'utilità di pianificazione del sistema operativo di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] (SQLOS) passa alla modalità preemptive per scrivere un evento di controllo nel registro eventi di Windows. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Si verifica quando l'utilità di pianificazione del sistema operativo di SQL Server passa alla modalità preemptive per scrivere un evento di controllo nel registro di sicurezza di Windows. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |Si verifica quando l'utilità di pianificazione del sistema operativo di SQL Server passa alla modalità preemptive per chiudere i supporti di backup.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |Si verifica quando l'utilità di pianificazione del sistema operativo di SQL Server passa alla modalità preemptive per chiudere un dispositivo di backup su nastro.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |Si verifica quando l'utilità di pianificazione del sistema operativo di SQL Server passa alla modalità preemptive per chiudere un dispositivo di backup virtuale.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Si verifica quando l'utilità di pianificazione del sistema operativo di SQL Server passa alla modalità preemptive per eseguire operazioni di cluster di failover di Windows.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |Si verifica quando l'utilità di pianificazione del sistema operativo di SQL Server passa alla modalità preemptive per creare un oggetto COM.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Gestione di gruppi di disponibilità AlwaysOn lease pianificazione per la diagnostica CSS., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PREEMPTIVE_TESTING |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|PRINT_ROLLBACK_PROGRESS |Utilizzato per l'attesa durante la conclusione di processi utente in un database in cui si è verificata una transizione tramite la clausola di terminazione ALTER DATABASE. Per ulteriori informazioni, vedere ALTER DATABASE (Transact-SQL).| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_COOP_SCAN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |Si verifica quando un'attività in background è in attesa del completamento dell'attività in background che riceve (tramite polling) notifiche di Windows Server Failover Clustering., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CLUSTER_INTEGRATION |Accodamento, sostituzione e/o rimuovere operazione è in attesa di acquisire un blocco di scrittura su un elenco interno AlwaysOn (ad esempio un elenco di reti, indirizzi di rete o listener del gruppo di disponibilità). Solo uso interno <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_JOIN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_OFFLINE_COMPLETED |Una Always On rilascio operazione gruppo di disponibilità è in attesa per il gruppo di disponibilità di destinazione non in linea prima dell'eliminazione di oggetti di Windows Server Failover Clustering., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ONLINE_COMPLETED |Creare un Always On o operazione di gruppo di disponibilità di failover è in attesa per il gruppo di disponibilità di destinazione per portare in linea., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Una Always On rilascio operazione gruppo di disponibilità è in attesa del completamento di qualsiasi attività in background pianificata come parte di un comando precedente. Ad esempio, è possibile che sia in corso la transizione al ruolo primario di database di disponibilità di un'attività in background. DROP AVAILABILITY GROUP DDL deve attendere questa attività in background terminare per evitare situazioni di race condition., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_WORKITEM_COMPLETED |Attesa interna da un thread in attesa del completamento di un'attività di lavoro asincrona. Si tratta di un'attesa prevista e per l'utilizzo di CSS., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADRSIM |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_LOGIN_STATS |Si verifica durante la sincronizzazione interna nei metadati nelle statistiche di accesso., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_RELATION_CACHE |Si verifica durante la sincronizzazione interna nei metadati nella tabella o indice., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_SERVER_CACHE |Si verifica durante la sincronizzazione interna nei metadati per i server collegati., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_UPGRADE_CONFIG |Si verifica durante la sincronizzazione interna nell'aggiornamento delle configurazioni server., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_QUEUE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BCKG_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BLOOM_FILTER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CTXS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DB_DISK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DYN_VECTOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_HOST_INIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_LOADDB |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT_DISK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_SHUTDOWN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_START |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QE_WARN_LIST_SYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QPJOB_KILL |Indica che un aggiornamento automatico asincrono delle statistiche è stato annullato da una chiamata al comando KILL all'avvio dell'esecuzione dell'aggiornamento. Il thread di interruzione viene sospeso e rimarrà in attesa dei comandi KILL. Un valore ottimale è minore di un secondo.| 
|QPJOB_WAITFOR_ABORT |Indica che un aggiornamento automatico asincrono delle statistiche è stato annullato da una chiamata al comando KILL durante l'esecuzione. L'aggiornamento è completato ma viene sospeso fino al completamento del coordinamento dei messaggi dei thread di interruzione. Questo stato è comune ma si verifica raramente e dovrebbe essere molto breve. Un valore ottimale è minore di un secondo.| 
|QRY_MEM_GRANT_INFO_MUTEX |Si verifica quando la gestione della memoria dell'esecuzione di query cerca di controllare l'accesso all'elenco di informazioni statiche sulle concessioni. Questo stato elenca le informazioni sulle richieste di memoria correnti concesse e in attesa. Questo stato rappresenta un semplice stato di controllo dell'accesso. In questo stato non si dovrebbero mai verificare attese lunghe. Se questo mutex non viene rilasciato, tutte le nuove query che utilizzano memoria non risponderanno più.| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_ERRHDL_SERVICE_DONE |Identificato solo a scopo informativo. Non supportato. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|QUERY_WAIT_ERRHDL_SERVICE |Identificato solo a scopo informativo.  Non supportato. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |Si verifica in determinati casi in cui la compilazione di indici offline viene eseguita in parallelo e i diversi thread di lavoro in cui viene eseguito l'ordinamento sincronizzano l'accesso ai file di ordinamento.| 
|QUERY_NOTIFICATION_MGR_MUTEX |Si verifica durante la sincronizzazione della coda di Garbage Collection nell'utilità di gestione delle notifiche delle query.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |Si verifica durante la sincronizzazione dello stato per le transazioni nelle notifiche delle query.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |Si verifica durante la sincronizzazione interna nell'utilità di gestione delle notifiche delle query.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |Si verifica durante la sincronizzazione della produzione di output di dati diagnostici di Query Optimizer. Questo tipo di attesa si verifica solo se sono state abilitate le impostazioni di diagnostica in direzione del supporto tecnico clienti Microsoft.| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_TRACEOUT |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|RBIO_WAIT_VLF |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RECOVER_CHANGEDB |Si verifica durante la sincronizzazione dello stato del database in modalità standby a caldo (warm standby).| 
|RECOVERY_MGR_LOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_SYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_BLOCK_IO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_CACHE_ACCESS |Si verifica durante la sincronizzazione in una cache degli articoli di replica. Durante queste attese si riscontra uno stallo nella lettura del log delle repliche e il blocco delle istruzioni DDL (Data Definition Language) per una tabella pubblicata.| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |Si verifica durante la sincronizzazione delle informazioni sulla versione dello schema di replica. Questo stato esiste quando vengono eseguite istruzioni DDL sull'oggetto replicato e quando nella lettura del log viene compilato o usato uno schema con versione basato sull'occorrenza DDL.| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPLICA_WRITES |Si verifica quando un'attività è in attesa del completamento di scritture di pagina in snapshot di database o repliche DBCC.| 
|REQUEST_DISPENSER_PAUSE |Si verifica quando un'attività è in attesa del completamento di tutte le operazioni di I/O in sospeso, per poter bloccare l'I/O in un file per il backup snapshot.| 
|REQUEST_FOR_DEADLOCK_SEARCH |Si verifica quando il monitoraggio dei deadlock è in attesa di avviare la successiva ricerca di deadlock. L'attesa tra rilevamenti di deadlock è prevista e un tempo di attesa totale prolungato per questa risorsa non indica un problema.| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESMGR_THROTTLED |Si verifica quando giunge una nuova richiesta rallentata in base all'impostazione GROUP_MAX_REQUESTS.| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESOURCE_QUEUE |Si verifica durante la sincronizzazione di diverse code di risorse interne.| 
|RESOURCE_SEMAPHORE |Si verifica quando una richiesta di memoria per una query non può essere concessa immediatamente a causa di altre query simultanee. Attese e tempi di attesa rilevanti possono indicare un numero eccessivo di query simultanee o quantità eccessive di richieste di memoria.| 
|RESOURCE_SEMAPHORE_MUTEX |Si verifica quando una query è in attesa che venga soddisfatta la richiesta di prenotazione di thread, nonché durante la sincronizzazione di richieste di compilazione di query e concessione di memoria.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |Si verifica quando il numero di compilazioni di query simultanee raggiunge un limite massimo. Attese e tempi di attesa rilevanti possono indicare una quantità eccessiva di compilazioni, ricompilazioni o piani non memorizzabili nella cache.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |Si verifica quando una richiesta di memoria per una query di dimensioni ridotte non può essere concessa immediatamente a causa di altre query simultanee. Il tempo di attesa non deve superare pochi secondi, poiché se non è in grado di concedere la memoria richiesta entro pochi secondi il server trasferisce la richiesta al pool di memoria per query principale. Attese rilevanti possono indicare un numero eccessivo di query di dimensioni ridotte simultanee mentre il pool di memoria principale è bloccato da query in attesa. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ROWGROUP_VERSION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RTDATA_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_CARGO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_DISPATCH |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_TRANSPORT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEC_DROP_TEMP_KEY |Si verifica dopo un tentativo non riuscito di eliminare una chiave di sicurezza temporanea, prima di un nuovo tentativo.| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_MUTEX |Si verifica in caso di attesa dei mutex che controllano l'accesso all'elenco globale dei provider di crittografia EKM e l'elenco con ambito sessione di sessioni EKM.| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEMPLAT_DSI_BUILD |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENCE_GENERATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENTIAL_GUID |Si verifica durante l'ottenimento di un nuovo GUID sequenziale.| 
|SERVER_IDLE_CHECK |Si verifica durante la sincronizzazione dello stato di inattività istanza di SQL Server quando un monitoraggio risorse tenta di dichiarare un'istanza di SQL Server come inattiva o durante il tentativo di attivazione.| 
|SERVER_RECONFIGURE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHUTDOWN |Si verifica quando un'istruzione di chiusura è in attesa dell'interruzione delle connessioni attive.| 
|SLEEP_BPOOL_FLUSH |Si verifica quando un checkpoint limita il rilascio di nuove operazioni di I/O per evitare il sovraccarico del sottosistema disco.| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_DBSTARTUP |Si verifica durante l'avvio di database, in attesa del recupero di tutti i database.| 
|SLEEP_DCOMSTARTUP |Si verifica una volta al massimo durante l'avvio di istanza di SQL Server, attendere il completamento dell'inizializzazione di DCOM.| 
|SLEEP_MASTERDBREADY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERMDREADY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERUPGRADED |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MSDBSTARTUP |Si verifica quando Traccia SQL è in attesa del completamento dell'avvio del database msdb.| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_SYSTEMTASK |Si verifica durante l'avvio di un'attività in background, in attesa che venga completato l'avvio di tempdb.| 
|SLEEP_TASK |Si verifica quando un'attività viene sospesa in attesa di un evento generico.| 
|SLEEP_TEMPDBSTARTUP |Si verifica quando un'attività è in attesa del completamento dell'avvio di tempdb.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLO_UPDATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SMSYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CONN_DUP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CRITICAL_SECTION |Si verifica durante la sincronizzazione interna nei componenti di rete SQL Server.| 
|SNI_HTTP_WAITFOR_0_DISCON |Si verifica durante l'arresto di SQL Server, durante l'attesa delle connessioni HTTP in sospeso uscire dall'installazione.| 
|SNI_LISTENER_ACCESS |Si verifica durante l'attesa dei nodi NUMA (Non-Uniform Memory Access) per aggiornare il cambiamento dello stato. L'accesso alla modifica dello stato è serializzato.| 
|SNI_TASK_COMPLETION |Si verifica durante l'attesa del completamento di tutte le attività durante il cambiamento di stato di un nodo NUMA.| 
|SNI_WRITE_ASYNC |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOAP_READ |Si verifica durante l'attesa del completamento di una lettura in rete HTTP.| 
|SOAP_WRITE |Si verifica durante l'attesa del completamento di una scrittura in rete HTTP.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_CALLBACK_REMOVAL |Si verifica durante l'esecuzione della sincronizzazione in un elenco di callback allo scopo di rimuovere un callback. Dopo il completamento dell'inizializzazione del server non è prevista alcuna modifica di questo contatore.| 
|SOS_DISPATCHER_MUTEX |Si verifica durante la sincronizzazione interna del pool di dispatcher e quando il pool viene modificato.| 
|SOS_LOCALALLOCATORLIST |Si verifica durante la sincronizzazione interna nel gestore della memoria di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_MEMORY_USAGE_ADJUSTMENT |Si verifica quando l'utilizzo della memoria è regolato tra i pool.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |Si verifica durante la sincronizzazione interna in pool di memoria, in caso di eliminazione di oggetti dal pool.| 
|SOS_PHYS_PAGE_CACHE |Considera il tempo che un thread attende per acquisire il mutex necessario prima che siano allocate le pagine fisiche o prima che tali pagine siano restituite al sistema operativo. Attese di questo tipo vengono visualizzati solo se l'istanza di SQL Server utilizza memoria AWE., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_PROCESS_AFFINITY_MUTEX |Si verifica durante la sincronizzazione dell'accesso a impostazioni relative all'affinità di processo.| 
|SOS_RESERVEDMEMBLOCKLIST |Si verifica durante la sincronizzazione interna nel gestore della memoria di SQL Server. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SOS_SCHEDULER_YIELD |Si verifica quando un'attività cede il controllo dell'utilità di pianificazione per consentire l'esecuzione di altre attività. Durante questa attesa, l'attività attende il rinnovo del quantum.| 
|SOS_SMALL_PAGE_ALLOC |Si verifica durante l'allocazione e la liberazione della memoria gestita da alcuni oggetti della memoria.| 
|SOS_STACKSTORE_INIT_MUTEX |Si verifica durante la sincronizzazione dell'inizializzazione dell'archivio interno.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |Si verifica quando un'attività viene avviata in modo sincrono. La maggior parte delle attività in SQL Server vengono avviate in modo asincrono, in cui controllo viene restituito per l'avvio subito dopo la richiesta di attività è stata inserita nella coda di lavoro.| 
|SOS_VIRTUALMEMORY_LOW |Si verifica quando un'allocazione di memoria è in attesa che venga liberata memoria virtuale da uno strumento di gestione delle risorse.| 
|SOSHOST_EVENT |Si verifica quando un componente hosted, ad esempio CLR, in attesa in un oggetto di sincronizzazione eventi di SQL Server.| 
|SOSHOST_INTERNAL |Si verifica durante la sincronizzazione dei callback del gestore della memoria usate da componenti hosted, ad esempio CLR.| 
|SOSHOST_MUTEX |Si verifica quando un componente hosted, ad esempio CLR, in attesa in un oggetto di sincronizzazione mutex di SQL Server.| 
|SOSHOST_RWLOCK |Si verifica quando un componente hosted, ad esempio CLR, in attesa in un oggetto di sincronizzazione di lettura / scrittura di SQL Server.| 
|SOSHOST_SEMAPHORE |Si verifica quando un componente hosted, ad esempio CLR, in attesa in un oggetto di sincronizzazione semafori di SQL Server.| 
|SOSHOST_SLEEP |Si verifica quando un'attività hosted viene sospesa in attesa di un evento generico. Le attività hosted vengono usate da componenti hosted come CLR.| 
|SOSHOST_TRACELOCK |Si verifica durante la sincronizzazione dell'accesso a flussi di traccia.| 
|SOSHOST_WAITFORDONE |Si verifica quando un componente hosted, ad esempio CLR, è in attesa del completamento di un'attività.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLCLR_APPDOMAIN |Si verifica quando CLR è in attesa che venga completato l'avvio di un dominio applicazione.| 
|SQLCLR_ASSEMBLY |Si verifica durante l'attesa dell'accesso all'elenco degli assembly caricati nel dominio applicazione.| 
|SQLCLR_DEADLOCK_DETECTION |Si verifica quando CLR è in attesa che venga completato il rilevamento dei deadlock.| 
|SQLCLR_QUANTUM_PUNISHMENT |Si verifica quando viene applicata una limitazione a un'attività CLR poiché ha superato il quantum di esecuzione. Questa limitazione ha lo scopo di ridurre l'effetto di questa attività a elevato utilizzo di risorse sulle altre attività.| 
|SQLSORT_NORMMUTEX |Si verifica durante la sincronizzazione interna, nel corso dell'inizializzazione delle strutture di ordinamento interne.| 
|SQLSORT_SORTMUTEX |Si verifica durante la sincronizzazione interna, nel corso dell'inizializzazione delle strutture di ordinamento interne.| 
|SQLTRACE_BUFFER_FLUSH |Si verifica quando un'attività è in attesa di un'attività in background per scaricare i buffer di traccia su disco ogni 4 secondi. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SQLTRACE_FILE_BUFFER |Si verifica durante la sincronizzazione in buffer di traccia durante una traccia di file., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_LOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_SHUTDOWN |Si verifica quando la chiusura della traccia è in attesa del completamento degli eventi di traccia in sospeso.| 
|SQLTRACE_WAIT_ENTRIES |Si verifica quando una coda degli eventi di Traccia SQL è in attesa di pacchetti in arrivo nella coda.| 
|SRVPROC_SHUTDOWN |Si verifica quando il processo di chiusura è in attesa del rilascio di risorse interne per essere completato correttamente.| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_BANDWIDTH_STATE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_INIT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_PROXY_CONTAINER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TEMPOBJ |Si verifica quando vengono sincronizzate le eliminazioni di oggetti temporanei. Questo tipo di attesa è raro e si verifica solo se un'attività ha richiesto l'accesso esclusivo per eliminazioni di tabelle temp.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TERMINATE_LISTENER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|THREADPOOL |Si verifica quando un'attività è in attesa di un thread di lavoro in cui essere eseguita. Può indicare che il numero massimo di thread di lavoro impostato è troppo basso oppure che le esecuzioni dei batch richiedono una quantità di tempo insolitamente elevata, riducendo così il numero dei thread di lavoro disponibili per soddisfare altri batch.| 
|TIMEPRIV_TIMEPERIOD |Si verifica durante la sincronizzazione interna del timer degli eventi estesi.| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |Si verifica quando il provider di traccia del set di righe di Traccia SQL è in attesa di un buffer libero o un buffer con eventi da elaborare.| 
|TRAN_MARKLATCH_DT |Si verifica durante l'attesa di un latch in modalità di eliminazione in un latch di contrassegno di transazione. I latch di contrassegno di transazione vengono usati per la sincronizzazione di commit con transazioni contrassegnate.| 
|TRAN_MARKLATCH_EX |Si verifica durante l'attesa di un latch in modalità esclusiva in una transazione contrassegnata. I latch di contrassegno di transazione vengono usati per la sincronizzazione di commit con transazioni contrassegnate.| 
|TRAN_MARKLATCH_KP |Si verifica durante l'attesa di un latch in modalità conservativa in una transazione contrassegnata. I latch di contrassegno di transazione vengono usati per la sincronizzazione di commit con transazioni contrassegnate.| 
|TRAN_MARKLATCH_NL |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|TRAN_MARKLATCH_SH |Si verifica durante l'attesa di un latch in modalità condivisa in una transazione contrassegnata. I latch di contrassegno di transazione vengono usati per la sincronizzazione di commit con transazioni contrassegnate.| 
|TRAN_MARKLATCH_UP |Si verifica durante l'attesa di un latch in modalità di aggiornamento in una transazione contrassegnata. I latch di contrassegno di transazione vengono usati per la sincronizzazione di commit con transazioni contrassegnate.| 
|TRANSACTION_MUTEX |Si verifica durante la sincronizzazione dell'accesso a una transazione da parte di più batch.| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MANAGER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_SESSION_REGISTRATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UTIL_PAGE_ALLOC |Si verifica quando le analisi di log delle transazioni sono in attesa di memoria disponibile in caso di numero eccessivo di richieste di memoria.| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OPERATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OTHER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VERSIONING_COMMITTING |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VIA_ACCEPT |Si verifica quando una connessione del provider VIA (Virtual Interface Adapter) viene completata durante l'avvio.| 
|VIEW_DEFINITION_MUTEX |Si verifica durante la sincronizzazione dell'accesso a definizioni delle viste memorizzate nella cache.| 
|WAIT_FOR_RESULTS |Si verifica durante l'attesa dell'attivazione di una notifica di query.| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_CLOSE |Si verifica durante l'attesa di completamento di un checkpoint., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_ENABLED |Si verifica quando il checkpoint è disabilitata e in attesa di arresto deve essere abilitata., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_STATE_LOCK |Si verifica quando la sincronizzazione del controllo dello stato del checkpoint., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **SI APPLICA A**: da [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_GUEST |Si verifica quando l'allocatore di memoria del database è necessario arrestare la ricezione delle notifiche di memoria insufficiente., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_HOST_WAIT |Si verifica quando le attese sono attivate dal motore di database e implementate dall'host., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |Si verifica quando il checkpoint offline è in attesa per il completamento i/o di leggere un log., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |Si verifica quando il checkpoint offline è in attesa di nuovi record del log da analizzare., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_PROCEDURE_ENTRY |Si verifica quando un comando drop procedure è in attesa per tutte le esecuzioni correnti della procedura per completare., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_RECOVERY |Si verifica quando il ripristino del database è in attesa per il recupero di oggetti con ottimizzazione per la memoria per terminare., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TASK_SHUTDOWN |Si verifica durante l'attesa di un thread OLTP In memoria per il completamento., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TRAN_DEPENDENCY |Si verifica durante l'attesa delle dipendenze della transazione., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR |Si verifica in seguito a un'istruzione WAITFOR Transact-SQL. La durata dell'attesa è determinata dai parametri per l'istruzione. Si tratta di un'attesa avviata dall'utente.| 
|WAITFOR_PER_QUEUE |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR_TASKSHUTDOWN |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|WAITSTAT_MUTEX |Si verifica durante la sincronizzazione dell'accesso alla raccolta di statistiche utilizzata per popolare sys.dm_os_wait_stats.| 
|WCC |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_API_CALL |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPORT_FAULT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WORKTBL_DROP |Si verifica durante la sospensione che precede un nuovo tentativo dopo un'eliminazione di tabella di lavoro non riuscita.| 
|WRITE_COMPLETION |Si verifica quando è in esecuzione un'operazione di scrittura.| 
|WRITELOG |Si verifica durante l'attesa del completamento di uno scaricamento del log. Checkpoint e commit delle transazioni costituiscono operazioni comuni che causano scaricamenti del log.| 
|XACT_OWN_TRANSACTION |Si verifica durante l'attesa dell'acquisizione della proprietà di una transazione.| 
|XACT_RECLAIM_SESSION |Si verifica durante l'attesa del rilascio della proprietà della sessione da parte del proprietario corrente.| 
|XACTLOCKINFO |Si verifica durante la sincronizzazione dell'accesso all'elenco dei blocchi per una transazione. In aggiunta alla transazione stessa, all'elenco dei blocchi accedono operazioni come il rilevamento dei deadlock e la migrazione dei blocchi durante le suddivisioni delle pagine.| 
|XACTWORKSPACE_MUTEX |Si verifica durante la sincronizzazione delle esclusioni da una transazione, nonché del numero di blocchi di database tra i membri integrati di una transazione.| 
|XDB_CONN_DUP_HASH |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_HISTORY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_SNAPSHOT |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDESTSVERMGR |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |Si verifica quando i buffer della sessione degli eventi estesi vengono scaricati nelle destinazioni. Questa attesa si verifica in un thread in background.| 
|XE_BUFFERMGR_FREEBUF_EVENT |Si verifica quando viene soddisfatta una delle condizioni seguenti:| 
|XE_CALLBACK_LIST |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_CX_FILE_READ |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |Si verifica quando una sessione degli eventi estesi che utilizza destinazioni asincrone viene avviata o arrestata. Questa attesa indica una delle due situazioni seguenti:| 
|XE_DISPATCHER_JOIN |Si verifica quando un thread in background usato per le sessioni degli eventi estesi verrà terminato.| 
|XE_DISPATCHER_WAIT |Si verifica quando un thread in background usato per le sessioni degli eventi estesi è in attesa dell'elaborazione dei buffer degli eventi.| 
|XE_FILE_TARGET_TVF |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_LIVE_TARGET_TVF |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_MODULEMGR_SYNC |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|XE_OLS_LOCK |Identificato solo a scopo informativo. Non supportato. Non è garantita la compatibilità con le versioni future.| 
|XE_PACKAGE_LOCK_BACKOFF |Identificato solo a scopo informativo. Non supportato. <br /> **Si applica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_TRUNCATION_LSN |TBD <br /> **Si applica a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_CACHE_ACCESS |Si verifica quando per l'accesso a tutti gli oggetti della cache di stored procedure compilata in modo nativo., <br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_PARTITIONED_STACK_CREATE |Si verifica quando l'allocazione in modo nativo per nodo NUMA compilato strutture cache delle stored procedure (deve essere eseguita a thread singolo) per una determinata procedura., <br /> **Si applica a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|

  
 I seguenti XEvent sono correlati alla partizione **COMMUTATORE** e ricompilazione dell'indice online. Per informazioni sulla sintassi, vedere [ALTER TABLE &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) e [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Per una matrice di compatibilità di blocchi, vedere [DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
    
 [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [Sys.dm_db_wait_stats &#40;Database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


