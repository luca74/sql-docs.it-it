---
title: sp_addpublication (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e47d331f57abede1d4b0e20ebba44cced109035
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una pubblicazione snapshot o transazionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione da creare. *pubblicazione* è **sysname**, non prevede alcun valore predefinito. Il nome deve essere univoco all'interno del database.  
  
 [  **@taskid=**] *taskid*  
 Supportata per compatibilità con le versioni precedenti di sola lettura. Utilizzare [sp_addpublication_snapshot &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
 [  **@restricted=**] **'***limitato***'**  
 Supportata per compatibilità con le versioni precedenti di sola lettura. Utilizzare *default_access*.  
  
 [  **@sync_method=**] *' come sync_method***'**  
 Modalità di sincronizzazione. *sync_method* è **nvarchar(13)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**native**|Genera l'output in modalità nativa del programma per la copia bulk per tutte le tabelle. *Non supportato per il server di pubblicazione Oracle*.|  
|**carattere**|Genera l'output in modalità carattere del programma per la copia bulk per tutte le tabelle. *Per un server di pubblicazione Oracle,* **carattere** *è valido solo per la replica snapshot*.|  
|**simultanee**|Genera l'output del programma per la copia bulk in modalità nativa per tutte le tabelle, senza tuttavia bloccare le tabelle durante lo snapshot. Questo valore è supportato solo per pubblicazioni transazionali. *Non supportato per il server di pubblicazione Oracle*.|  
|**concurrent_c**|Genera l'output del programma per la copia bulk in modalità carattere per tutte le tabelle, senza tuttavia bloccare le tabelle durante lo snapshot. Questo valore è supportato solo per pubblicazioni transazionali.|  
|**snapshot del database**|Genera output del programma in modalità nativa per la copia bulk di tutte le tabelle da uno snapshot del database. Gli snapshot del database non sono disponibili in ogni edizione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**caratteri di snapshot del database**|Genera output del programma in modalità carattere per la copia bulk di tutte le tabelle da uno snapshot del database. Gli snapshot del database non sono disponibili in ogni edizione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (predefinito)|Per impostazione predefinita **nativo** per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. Per non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valori predefiniti per i server di pubblicazione **carattere** quando il valore di *repl_freq* è **Snapshot** e **concurrent_c** per tutti gli altri casi.|  
  
 [  **@repl_freq=**] **'***repl_freq***'**  
 È il tipo di frequenza della replica, *repl_freq* è **nvarchar (10)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**Continua** (impostazione predefinita)|Il server di pubblicazione genera l'output per tutte le transazioni basate su log. Per non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione, ciò richiede che *sync_method* impostare **concurrent_c**.|  
|**snapshot**|Il server di pubblicazione genera solo gli eventi di sincronizzazione pianificati. Per non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione, ciò richiede che *sync_method* impostare **carattere**.|  
  
 [  **@description=**] **'***descrizione***'**  
 Descrizione facoltativa della pubblicazione. *Descrizione* è **nvarchar (255)**, con un valore predefinito è NULL.  
  
 [  **@status=**] **'***stato***'**  
 Specifica se i dati della pubblicazione sono disponibili. *stato* è **nvarchar (8)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**Attiva**|I dati della pubblicazione risultano immediatamente disponibili per i Sottoscrittori.|  
|**inattivo** (impostazione predefinita)|I dati della pubblicazione non sono disponibili per i Sottoscrittori quando viene creata la pubblicazione (è possibile creare una sottoscrizione, che tuttavia non viene elaborata).|  
  
 *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 Specifica se per la pubblicazione è disponibile un agente di distribuzione autonomo. *independent_agent* è **nvarchar (5)**, con un valore predefinito è FALSE. Se **true**, è disponibile un agente di distribuzione autonomo per la pubblicazione. Se **false**, la pubblicazione utilizza un agente di distribuzione condiviso e ogni coppia database del server di pubblicazione/sottoscrizione di database dispone di un solo agente condiviso.  
  
 [  **@immediate_sync=**] **'***solo quando independent_agent***'**  
 Specifica se i file di sincronizzazione della pubblicazione vengono creati a ogni esecuzione dell'agente snapshot. *solo quando independent_agent* è **nvarchar (5)**, con un valore predefinito è FALSE. Se **true**, i file di sincronizzazione vengono creati o ricreati ogni volta che viene eseguito l'agente Snapshot. Se l'esecuzione dell'agente snapshot viene completata prima della creazione della sottoscrizione, i Sottoscrittori possono ricevere i file di sincronizzazione immediatamente. Le nuove sottoscrizioni ricevono i file di sottoscrizione più recenti generati dall'ultima esecuzione dell'agente snapshot. *independent_agent* deve essere **true** per *solo quando independent_agent* da **true**. Se **false**, i file di sincronizzazione vengono creati solo se esistono nuove sottoscrizioni. È necessario chiamare [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) per ogni sottoscrizione quando si aggiunge in modo incrementale un nuovo articolo a una pubblicazione esistente. I Sottoscrittori ricevono i file di sincronizzazione dopo la sottoscrizione solo se gli agenti snapshot sono stati avviati e completati.  
  
 [  **@enabled_for_internet=**] **'***enabled_for_internet***'**  
 Specifica se la pubblicazione è abilitata per Internet e determina se è possibile utilizzare FTP per il trasferimento dei file di snapshot in un Sottoscrittore. *enabled_for_internet* è **nvarchar (5)**, con un valore predefinito è FALSE. Se **true**, i file di sincronizzazione per la pubblicazione vengono inseriti nella directory C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\repldata\ftp.. La directory Ftp deve essere creata dall'utente.  
  
 [  **@allow_push=**] **'***allow_push***'**  
 Specifica se è consentito creare sottoscrizioni push per la pubblicazione specificata. *allow_push* è **nvarchar (5)**, il valore predefinito è TRUE, che consente le sottoscrizioni push per la pubblicazione.  
  
 [  **@allow_pull=**] **'***allow_pull***'**  
 Specifica se è consentito creare sottoscrizioni pull per la pubblicazione specificata. *allow_pull* è **nvarchar (5)**, con un valore predefinito è FALSE. Se **false**, per la pubblicazione non sono consentite le sottoscrizioni pull.  
  
 [  **@allow_anonymous=**] **'***allow_anonymous***'**  
 Specifica se è consentito creare sottoscrizioni anonime per la pubblicazione specificata. *allow_anonymous* è **nvarchar (5)**, con un valore predefinito è FALSE. Se **true**, *solo quando independent_agent* deve inoltre essere impostato su **true**. Se **false**, le sottoscrizioni anonime non sono consentite per la pubblicazione.  
  
 [  **@allow_sync_tran=**] **'***allow_sync_tran***'**  
 Specifica se le sottoscrizioni ad aggiornamento immediato sono consentite nella pubblicazione. *allow_sync_tran* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** è *non è supportata per server di pubblicazione Oracle*.  
  
 [  **@autogen_sync_procs=**] **'***autogen_sync_procs***'**  
 Specifica se la stored procedure di sincronizzazione per sottoscrizioni aggiornabili viene generata nel server di pubblicazione. *autogen_sync_procs* è **nvarchar (5)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**true**|Questo valore viene impostato automaticamente quando sono abilitate le sottoscrizioni aggiornabili.|  
|**false**|Questo valore viene impostato automaticamente quando non sono abilitate le sottoscrizioni aggiornabili oppure per server di pubblicazione Oracle.|  
|NULL (predefinito)|Per impostazione predefinita **true** quando è abilitato l'aggiornamento delle sottoscrizioni e per **false** quando le sottoscrizioni ad aggiornamento non è abilitato.|  
  
> [!NOTE]  
>  L'utente ha fornito il valore per *autogen_sync_procs*verrà sottoposto a override in base ai valori specificati per *allow_queued_tran* e *allow_sync_tran*.  
  
 [  **@retention=**] *conservazione*  
 Periodo di memorizzazione, espresso in ore, per le attività di sottoscrizione. *conservazione* è **int**, con un valore predefinito è 336 ore. Se una sottoscrizione non viene attivata entro il periodo di memorizzazione, scade e viene rimossa. Il valore di questo parametro può essere maggiore del periodo di memorizzazione massimo del database di distribuzione utilizzato dal server di pubblicazione. Se **0**, le sottoscrizioni note della pubblicazione non scadono mai e rimuovere l'agente.  
  
 [  **@allow_queued_tran=** ] **'***allow_queued_updating***'**  
 Abilita o disabilita l'accodamento delle modifiche nel Sottoscrittore fino a quando non è possibile applicarle nel server di pubblicazione. *allow_queued_updating* è **nvarchar (5)** con un valore predefinito è FALSE. Se **false**, le modifiche del sottoscrittore non vengono messe in coda. **true** è *non è supportata per server di pubblicazione Oracle*.  
  
 [  **@snapshot_in_defaultfolder=** ] **'***snapshot_in_default_folder***'**  
 Specifica se i file di snapshot sono archiviati nella cartella predefinita. *snapshot_in_default_folder* è **nvarchar (5)** con un valore predefinito è TRUE. Se **true**, i file di snapshot sono disponibili nella cartella predefinita. Se **false**, i file di snapshot sono stati archiviati nella posizione alternativa specificata da *alternate_snapshot_folder*. Le posizioni alternative possono essere un altro server, un'unità di rete oppure un supporto rimovibile, ad esempio un CD o un disco rimovibile. È inoltre possibile archiviare i file di snapshot in un sito FTP in modo che possano essere successivamente recuperati dal Sottoscrittore. Si noti che questo parametro può essere true e un percorso non è stato  **@alt_snapshot_folder**  parametro. Tale combinazione indica che i file di snapshot vengono archiviati sia nella posizione predefinita che in posizioni alternative.  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder***'**  
 Specifica la posizione della cartella alternativa per lo snapshot. *alternate_snapshot_folder* è **nvarchar (255)** con un valore predefinito è NULL.  
  
 [  **@pre_snapshot_script=** ] **'***pre_snapshot_script***'**  
 Specifica un puntatore a un **SQL** percorso del file. *pre_snapshot_script* è **nvarchar (255),**con un valore predefinito è NULL. L'agente di distribuzione esegue lo script pre-snapshot prima dell'esecuzione di tutti gli script di oggetti replicati durante l'applicazione di uno snapshot in un Sottoscrittore. Lo script viene eseguito nel contesto di sicurezza utilizzato dall'agente di distribuzione per la connessione al database di sottoscrizione.  
  
 [  **@post_snapshot_script=** ] **'***post_snapshot_script***'**  
 Specifica un puntatore a un **SQL** percorso del file. *post_snapshot_script* è **nvarchar (255)**, con un valore predefinito è NULL. L'agente di distribuzione esegue lo script post-snapshot dopo l'applicazione di tutti gli altri dati e script di oggetti replicati durante una sincronizzazione iniziale. Lo script viene eseguito nel contesto di sicurezza utilizzato dall'agente di distribuzione per la connessione al database di sottoscrizione.  
  
 [  **@compress_snapshot=** ] **'***compress_snapshot***'**  
 Specifica che lo snapshot viene scritto il  **@alt_snapshot_folder**  percorso è deve essere compresso nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* è **nvarchar (5)**, con un valore predefinito è FALSE. **false** specifica che non lo snapshot verrà compresso; **true** specifica che lo snapshot verrà compresso. I file di snapshot con una dimensione superiore a 2 gigabyte (GB) non possono essere compressi. I file di snapshot compressi vengono decompressi nella posizione in cui viene eseguito l'agente di distribuzione. Per le sottoscrizioni pull in genere vengono utilizzati snapshot compressi in modo che i file vengano decompressi nel Sottoscrittore. Non è possibile comprimere lo snapshot all'interno della cartella predefinita.  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 Indirizzo di rete del servizio FTP per il database di distribuzione. *ftp_address* è **sysname**, con un valore predefinito è NULL. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore. Poiché questa proprietà viene archiviata per ogni pubblicazione, ogni pubblicazione può essere un altro *ftp_address*. La pubblicazione deve supportare la propagazione di snapshot tramite FTP.  
  
 [  **@ftp_port=** ] *ftp_port*  
 Numero di porta del servizio FTP per il database di distribuzione. *ftp_port* è **int**, con un valore predefinito è 21. Specifica la posizione dei file di snapshot della pubblicazione, dove i file possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore. Poiché questa proprietà viene archiviata per ogni pubblicazione, ogni pubblicazione può avere un proprio *ftp_port*.  
  
 [  **@ftp_subdirectory =** ] **'***ftp_subdirectory***'**  
 Specifica la posizione in cui i file di snapshot possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore se la pubblicazione supporta la propagazione degli snapshot tramite FTP. *ftp_subdirectory* è **nvarchar (255)**, con un valore predefinito è NULL. Poiché questa proprietà viene archiviata per ogni pubblicazione, ogni pubblicazione può avere un proprio *ftp_subdirctory* oppure scegliere di non una sottodirectory con un valore NULL.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 Nome utente utilizzato per la connessione al servizio FTP. *ftp_login* è **sysname**, con valore predefinito è Anonymous.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 Password utente utilizzata per la connessione al servizio FTP. *ftp_password* è **sysname**, con un valore predefinito è NULL.  
  
 [  **@allow_dts =** ] **'***allow_dts***'**  
 Specifica che la pubblicazione supporta le trasformazioni di dati. Quando si crea una sottoscrizione, è possibile specificare un pacchetto DTS. *allow_transformable_subscriptions* è **nvarchar (5)** con un valore predefinito è FALSE, che non consente trasformazioni DTS. Quando *allow_dts* è true, *sync_method* deve essere impostata su **carattere** o **concurrent_c**.  
  
 **true** è *non è supportata per server di pubblicazione Oracle*.  
  
 [  **@allow_subscription_copy =** ] **'***allow_subscription_copy***'**  
 Abilita o disabilita la funzione di copia dei database di sottoscrizione che sottoscrivono la pubblicazione. *allow_subscription_copy* è**nvarchar (5)**, con un valore predefinito è FALSE.  
  
 [  **@conflict_policy =** ] **'***conflict_policy***'**  
 Specifica i criteri di risoluzione dei conflitti adottati quando viene utilizzata l'opzione per Sottoscrittori ad aggiornamento in coda. *conflict_policy* è **nvarchar (100)** con un valore predefinito è NULL, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**wins pub**|Prevale il server di pubblicazione.|  
|**sub reinit**|Reinizializzare la sottoscrizione.|  
|**Sub wins**|Prevale il Sottoscrittore.|  
|NULL (predefinito)|Se NULL e la pubblicazione è una pubblicazione snapshot, il criterio predefinito diventa **sub reinit**. Se NULL e la pubblicazione non è una pubblicazione snapshot, il valore predefinito diventa **wins pub**.|  
  
 *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@centralized_conflicts =** ] **'***centralized_conflicts***'**  
 Specifica se i record dei conflitti vengono archiviati nel server di pubblicazione. *centralized_conflicts* è **nvarchar (5)**, con un valore predefinito è TRUE. Se **true**, record con conflitti vengono archiviati nel server di pubblicazione. Se **false**, record con conflitti vengono archiviati nel server di pubblicazione e nel Sottoscrittore che ha causato il conflitto. *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 Specifica il periodo di memorizzazione dei conflitti, espresso in giorni. Si tratta del periodo di tempo durante il quale i metadati dei conflitti rimangono archiviati per la replica transazionale peer-to-peer e le sottoscrizioni ad aggiornamento in coda. *conflict_retention* è **int**, con un valore predefinito è 14. *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@queue_type =** ] **'***queue_type***'**  
 Specifica il tipo di coda da utilizzare. *queue_type* è **nvarchar (10)**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**SQL**|Consente di utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'archiviazione delle transazioni.|  
|NULL (predefinito)|Per impostazione predefinita **sql**, che consente di utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare le transazioni.|  
  
> [!NOTE]  
>  L'utilizzo di MSMQ ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) non è più supportato. Se si specifica un valore **msmq** genererà un avviso e la replica verrà automaticamente di impostare il valore su **sql**.  
  
 *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@add_to_active_directory =** ] **'***aggiungere**_**to_active_directory***'**  
 Questo parametro è deprecato ed è supportato solo per compatibilità con gli script di versioni precedenti. Non è più possibile aggiungere informazioni di pubblicazione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
 [  **@logreader_job_name =** ] **'***logreader_agent_name***'**  
 Nome di un processo esistente dell'agente. *logreader_agent_name* è **sysname**, con un valore predefinito null. Questo parametro viene specificato solo quando l'agente di lettura log utilizzerà un processo esistente anziché uno nuovo.  
  
 [  **@qreader_job_name =** ] **'***queue_reader_agent_name***'**  
 Nome di un processo esistente dell'agente. *queue_reader_agent_name* è **sysname**, con un valore predefinito null. Questo parametro viene specificato solo quando l'agente di lettura coda utilizzerà un processo esistente anziché uno nuovo.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Specifica un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *server di pubblicazione* è **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzato durante l'aggiunta di una pubblicazione per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
 [  **@allow_initialize_from_backup =** ] **'***allow_initialize_from_backup***'**  
 Specifica se i Sottoscrittori possono inizializzare una sottoscrizione di questa pubblicazione da un backup anziché da uno snapshot iniziale. *allow_initialize_from_backup* è **nvarchar (5)**, i possibili valori sono i seguenti:  
  
|Valore|Description|  
|-----------|-----------------|  
|**true**|Abilita l'inizializzazione da un backup.|  
|**false**|Disabilita l'inizializzazione da un backup.|  
|NULL (predefinito)|Per impostazione predefinita **true** per una pubblicazione in una topologia di replica peer-to-peer e **false** per tutte le altre pubblicazioni.|  
  
 Per altre informazioni, vedere [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!WARNING]  
>  Per evitare la mancanza di dati del Sottoscrittore, quando si utilizza **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilizzare sempre `@immediate_sync = N'true'`.  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 Indica se per la pubblicazione è supportata la replica dello schema. *replicate_ddl* è **int**, il valore predefinito è **1** per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione e **0** per non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. **1** indica che vengono replicate istruzioni di data definition language (DDL) eseguite nel server di pubblicazione, e **0** indica che le istruzioni DDL non vengono replicate. *La replica dello schema non è supportata per server di pubblicazione Oracle.* Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Il  *@replicate_ddl*  parametro viene rispettato quando un'istruzione DDL aggiunge una colonna. Il  *@replicate_ddl*  parametro viene ignorato quando un'istruzione DDL modifica o elimina una colonna per i motivi seguenti.  
  
-   Quando viene eliminata una colonna, è necessario aggiornare sysarticlecolumns per evitare che le nuove istruzioni DML, compresi la colonna eliminata che potrebbe causare l'agente di distribuzione. Il  *@replicate_ddl*  parametro verrà ignorato perché la replica deve replicare sempre la modifica dello schema.  
  
-   Quando una colonna viene modificata, è probabile che venga modificato il tipo di dati di origine o il supporto dei valori Null, di conseguenza le istruzioni DML contengono un valore che potrebbe non essere compatibile con la tabella nel Sottoscrittore. Tali istruzioni DML potrebbero determinare la mancata esecuzione dell'agente di distribuzione. Il  *@replicate_ddl*  parametro verrà ignorato perché la replica deve replicare sempre la modifica dello schema.  
  
-   Quando un'istruzione DDL aggiunge una nuova colonna, sysarticlecolumns non include la nuova colonna. Le istruzioni DML non tenteranno di replicare i dati per la nuova colonna. Il parametro viene rispettato perché la replica o la non replica di DDL è accettabile.  
  
 [  **@enabled_for_p2p =** ] **'***enabled_for_p2p***'**  
 Consente di utilizzare la pubblicazione in una topologia di replica peer-to-peer. *enabled_for_p2p* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** indica che la pubblicazione supporta la replica peer-to-peer. Quando si imposta *enabled_for_p2p* a **true**, si applicano le restrizioni seguenti:  
  
-   *allow_anonymous* deve essere **false**.  
  
-   *allow_dts* deve essere **false**.  
  
-   *allow_initialize_from_backup* deve essere **true**.  
  
-   *allow_queued_tran* deve essere **false**.  
  
-   *allow_sync_tran* deve essere **false**.  
  
-   *conflict_policy* deve essere **false**.  
  
-   *independent_agent* deve essere **true**.  
  
-   *repl_freq* deve essere **continua**.  
  
-   *replicate_ddl* deve essere **1**.  
  
 Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [  **@publish_local_changes_only =** ] **'***publish_local_changes_only***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@enabled_for_het_sub=** ] **'***enabled_for_het_sub***'**  
 Abilita il supporto dei Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella pubblicazione. *enabled_for_het_sub* è **nvarchar (5)** con valore predefinito è false. Il valore **true** significa che supporta la pubblicazione non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i sottoscrittori. Quando *enabled_for_het_sub* è **true**, si applicano le restrizioni seguenti:  
  
-   *allow_initialize_from_backup* deve essere **false**.  
  
-   *allow_push* deve essere **true**.  
  
-   *allow_queued_tran* deve essere **false**.  
  
-   *allow_subscription_copy* deve essere **false**.  
  
-   *allow_sync_tran* deve essere **false**.  
  
-   *autogen_sync_procs* deve essere **false**.  
  
-   *conflict_policy* deve essere NULL.  
  
-   *enabled_for_internet* deve essere **false**.  
  
-   *enabled_for_p2p* deve essere **false**.  
  
-   *ftp_address* deve essere NULL.  
  
-   *ftp_subdirectory* deve essere NULL.  
  
-   *ftp_password* deve essere NULL.  
  
-   *pre_snapshot_script* deve essere NULL.  
  
-   *post_snapshot_script* deve essere NULL.  
  
-   *replicate_ddl* deve essere 0.  
  
-   *qreader_job_name* deve essere NULL.  
  
-   *queue_type* deve essere NULL.  
  
-   *sync_method* non può essere **nativo** o **simultanee**.  
  
 Per altre informazioni, vedere [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 [  **@p2p_conflictdetection=** ] **'***p2p_conflictdetection***'**  
 Consente il rilevamento dei conflitti da parte dell'agente di distribuzione se la pubblicazione è abilitata per la replica peer-to-peer. *p2p_conflictdetection* è **nvarchar (5)** con valore predefinito è true. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@p2p_originator_id=** ] *p2p_originator_id*  
 Specifica un ID per un nodo in una topologia peer-to-peer. *p2p_originator_id* è **int**, con un valore predefinito è NULL. Questo ID viene utilizzato per il rilevamento dei conflitti se *p2p_conflictdetection* è impostata su TRUE. Specificare un ID positivo diverso da zero che non sia mai stato utilizzato nella topologia. Per un elenco di ID che sono già stati utilizzati, eseguire [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
 [  **@p2p_continue_onconflict=** ] **'***p2p_continue_onconflict***'**  
 Determina se l'agente di distribuzione continua a elaborare le modifiche dopo che è stato rilevato un conflitto. *p2p_continue_onconflict* è **nvarchar (5)** con valore predefinito è false.  
  
> [!CAUTION]  
>  È consigliabile utilizzare il valore predefinito FALSE. Quando questa opzione è impostata su TRUE, l'agente di distribuzione tenta di garantire la convergenza dei dati nella topologia applicando la riga in conflitto dal nodo con ID di origine maggiore. Questo metodo non garantisce la convergenza. Dopo il rilevamento di un conflitto, è necessario assicurarsi che la topologia sia coerente. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@allow_partition_switch=** ] **'***allow_partition_switch***'**  
 Specifica se le istruzioni ALTER TABLE...SWITCH possono essere eseguite sul database pubblicato. *allow_partition_switch* è **nvarchar (5)** con valore predefinito è false. Per altre informazioni, vedere [Replicare tabelle e indici partizionati](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
 [  **@replicate_partition_switch=** ] **'***replicate_partition_switch***'**  
 Specifica se le istruzioni ALTER TABLE...SWITCH eseguite sul database pubblicato devono essere replicate ai Sottoscrittori. *replicate_partition_switch* è **nvarchar (5)** con valore predefinito è false. Questa opzione è valida solo se *allow_partition_switch* è impostata su TRUE.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_addpublication** viene utilizzata nella replica snapshot e transazionale.  
  
 Se esistono più pubblicazioni che pubblicano lo stesso oggetto di database, solo per le pubblicazioni con un *replicate_ddl* valore **1** replicherà ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION e Istruzioni ALTER TRIGGER DDL. Una istruzione ALTER TABLE DROP COLUMN DDL verrà tuttavia replicata da tutte le pubblicazioni che stanno pubblicando la colonna eliminata.  
  
 Con abilitata la replica DDL (*replicate_ddl* = **1**) per una pubblicazione, per rendere DDL da non replicare le modifiche alla pubblicazione, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) devono essere eseguiti prima per impostare *replicate_ddl* a **0**. Dopo le istruzioni DDL non di replica sono stati emessi, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) può essere eseguito nuovamente per riattivare la replica DDL.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_addpublication**. Gli account di accesso con autenticazione di Windows devono disporre di un account utente nel database che rappresenta il proprio account utente di Windows. Un account utente che rappresenta un gruppo di Windows non è sufficiente.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addlogreader_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
