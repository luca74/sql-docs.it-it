---
title: sp_changemergearticle (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 11/09/2015
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
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97c2b4b07b79b061b85e50cd51c4716173f073a6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spchangemergearticle-transact-sql"></a>sp_changemergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Vengono modificate le proprietà di un articolo di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione che include l'articolo. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article=**] **'***articolo***'**  
 Nome dell'articolo da modificare. *articolo* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@property=**] **'***proprietà***'**  
 Proprietà da modificare per la pubblicazione e l'articolo specificati. *proprietà* è **nvarchar (30)**, e uno dei valori elencato nella tabella.  
  
 [  **@value=**] **'***valore***'**  
 Nuovo valore della proprietà specificata. *valore* è **nvarchar (1000)**, e uno dei valori elencato nella tabella.  
  
 Nella tabella seguente vengono descritte le proprietà degli articoli e i valori corrispondenti.  
  
|Proprietà|Valori|Description|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|Abilita l'utilizzo di un sistema di risoluzione interattivo per l'articolo.|  
||**false**|Disabilita l'utilizzo di un sistema di risoluzione interattivo per l'articolo.|  
|**article_resolver**||Sistema di risoluzione personalizzato per l'articolo. Proprietà valida solo per gli articoli di tabelle.|  
|**check_permissions** (bitmap)|**0x00**|Le autorizzazioni a livello di tabella non vengono controllate.|  
||**0x10**|Le autorizzazioni a livello di tabella vengono controllate nel server di pubblicazione prima dell'applicazione nel server di pubblicazione delle istruzioni INSERT eseguite nel Sottoscrittore.|  
||**0x20**|Le autorizzazioni a livello di tabella vengono controllate nel server di pubblicazione prima dell'applicazione nel server di pubblicazione delle istruzioni UPDATE eseguite nel Sottoscrittore.|  
||**0x40**|Le autorizzazioni a livello di tabella vengono controllate nel server di pubblicazione prima dell'applicazione nel server di pubblicazione delle istruzioni DELETE eseguite nel Sottoscrittore.|  
|**column_tracking**|**true**|Attiva il rilevamento a livello di colonna. Proprietà valida solo per gli articoli di tabelle.<br /><br /> Nota: Rilevamento a livello di colonna non può essere utilizzato durante la pubblicazione di tabelle con più di 246 colonne.|  
||**false**|Disattiva il rilevamento a livello di colonna e mantiene il rilevamento dei conflitti a livello di riga. Proprietà valida solo per gli articoli di tabelle.|  
|**compensate_for_errors**|**true**|Vengono eseguite azioni di compensazione quando si verificano errori durante la sincronizzazione. Per ulteriori informazioni, vedere [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
||**false**|Non vengono eseguite azioni di compensazione, situazione corrispondente al funzionamento predefinito. Per ulteriori informazioni, vedere [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).<br /><br /> **\*\*Importante \* \***  anche se i dati nelle righe interessate potrebbero sembrare non convergenti, non appena si risolvere gli eventuali errori, è possibile applicare modifiche e si otterrà la convergenza dei dati. Se la tabella di origine per un articolo è già pubblicata in un'altra pubblicazione, il valore di *compensate_for_errors* deve essere lo stesso per entrambi gli articoli.|  
|**creation_script**||Percorso e nome di uno script di schema dell'articolo facoltativo utilizzato per la creazione dell'articolo nel database di sottoscrizione.|  
|**delete_tracking**|**true**|Le istruzioni DELETE vengono replicate, situazione corrispondente al funzionamento predefinito.|  
||**false**|Le istruzioni DELETE non vengono replicate.<br /><br /> **\*\*Importante \* \***  impostazione **delete_tracking** a **false** i risultati in convergenza ed eliminate le righe devono essere rimossi manualmente.|  
|**Descrizione**||Voce descrittiva per l'articolo.|  
|**destination_owner**||Nome del proprietario dell'oggetto nel database di sottoscrizione, se non **dbo**.|  
|**identity_range**||**bigint** che specifica le dimensioni dell'intervallo da utilizzare per l'assegnazione di nuovi valori identity se l'articolo include **identityrangemanagementoption** impostato su **auto** o **auto_identity_ intervallo** impostato su **true**. Proprietà valida solo per gli articoli di tabelle. Per ulteriori informazioni, vedere la sezione "Replica di tipo Merge" di [replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identityrangemanagementoption**|**Manuale**|Disabilita la gestione automatica degli intervalli di valori Identity. Contrassegna le colonne Identity con NOT FOR REPLICATION per consentire la gestione manuale degli intervalli di valori Identity. Per altre informazioni, vedere [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
||**Nessuno**|Disabilita tutti i tipi di gestione degli intervalli di valori Identity.|  
|**logical_record_level_conflict_detection**|**true**|Viene rilevato un conflitto in presenza di modifiche apportate in qualsiasi posizione del record logico. È necessario che **logical_record_level_conflict_resolution** impostare **true**.|  
||**false**|Viene utilizzato il rilevamento dei conflitti predefinito come specificato da **column_tracking**.|  
|**logical_record_level_conflict_resolution**|**true**|L'intero record logico prevalente sovrascrive il record logico perdente.|  
||**false**|Le righe prevalenti non sono vincolate al record logico.|  
|**partition_options**|**0**|Il filtro applicato all'articolo è statico oppure non restituisce un subset di dati univoco per ogni partizione, ovvero si creano partizioni sovrapposte.|  
||**1**|Le partizioni sono sovrapposte e gli aggiornamenti DML eseguiti nel Sottoscrittore non possono modificare la partizione a cui appartiene una riga.|  
||**2**|Il filtro applicato all'articolo restituisce partizioni non sovrapposte, ma più Sottoscrittori possono ricevere la stessa partizione.|  
||**3**|Il filtro applicato all'articolo restituisce partizioni non sovrapposte univoche per ogni sottoscrizione.<br /><br /> Nota: Se si specifica un valore di **3** per **partition_options**, può essere presente una sola sottoscrizione per ogni partizione di dati dell'articolo. Se si crea una seconda sottoscrizione nella quale il criterio di filtro porta alla restituzione della stessa partizione della sottoscrizione esistente, quest'ultima viene eliminata.|  
|**pre_creation_command**|**Nessuno**|Se la tabella esiste già nel Sottoscrittore, non viene eseguita alcuna azione.|  
||**eliminare**|Esegue un'operazione di eliminazione in base alla clausola WHERE del filtro di subset.|  
||**eliminare**|Elimina la tabella prima di ricrearla.|  
||**troncare**|Tronca la tabella di destinazione.|  
|**processing_order**||**int** che indica l'ordine di elaborazione degli articoli in una pubblicazione di tipo merge.|  
|**pub_identity_range**||**bigint** che specifica le dimensioni dell'intervallo allocata a un sottoscrittore con una sottoscrizione server se l'articolo include **identityrangemanagementoption** impostato su **auto** o **automatico _identity_range** impostato su **true**. L'intervallo di valori Identity è riservato al Sottoscrittore di ripubblicazione per l'assegnazione ai propri Sottoscrittori. Proprietà valida solo per gli articoli di tabelle. Per ulteriori informazioni, vedere la sezione "Replica di tipo Merge" di [replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**published_in_tran_pub**|**true**|L'articolo è pubblicato anche in una pubblicazione transazionale.|  
||**false**|L'articolo non è pubblicato anche in una pubblicazione transazionale.|  
|**resolver_info**||Specifica le informazioni aggiuntive necessarie per un sistema di risoluzione personalizzato. Alcuni sistemi di risoluzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] richiedono una colonna come input. **resolver_info** è **nvarchar (255)**, con un valore predefinito è NULL. Per altre informazioni, vedere [Sistemi di risoluzione dei conflitti basati su Microsoft COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).|  
|**schema_option** (bitmap)||Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.|  
||**0x00**|Disabilita la creazione di script tramite l'agente Snapshot e utilizza lo script fornito in **creation_script**.|  
||**0x01**|Genera lo script per la creazione di oggetti (CREATE TABLE, CREATE PROCEDURE e così via).|  
||**0x10**|Genera un indice cluster corrispondente.|  
||**0x20**|Converte i tipi di dati definiti dall'utente in tipi di dati di base nel Sottoscrittore. Questa opzione non può essere utilizzata quando è presente un vincolo CHECK o DEFAULT su una colonna con tipo definito dall'utente (UDT), se una colonna UDT è inclusa nella chiave primaria o se una colonna calcolata fa riferimento a una colonna UDT.|  
||**0x40**|Genera indici non cluster corrispondenti.|  
||**0x80**|include i vincoli di integrità referenziale dichiarati nelle chiavi primarie.|  
||**0x100**|Replica gli eventuali trigger dell'utente di un articolo di tabella.|  
||**0x200**|Replica i vincoli FOREIGN KEY. Se la tabella con riferimenti non fa parte di una pubblicazione, tutti i vincoli FOREIGN KEY in una tabella pubblicata non vengono replicati.|  
||**0x400**|Replica i vincoli CHECK.|  
||**0x800**|Replica i valori predefiniti.|  
||**0x1000**|Replica le regole di confronto a livello di colonna.|  
||**0x2000**|Replica le proprietà estese associate all'oggetto di origine dell'articolo pubblicato.|  
||**0x4000**|Replica le eventuali chiavi univoche definite in un articolo di tabella.|  
||**0x8000**|Genera istruzioni ALTER TABLE per la creazione di script dei vincoli.|  
||**0x10000.**|Replica i vincoli CHECK come NOT FOR REPLICATION in modo che i vincoli non vengono imposti durante la sincronizzazione.|  
||**0x20000**|Replica i vincoli FOREIGN KEY come NOT FOR REPLICATION in modo che i vincoli non vengono imposti durante la sincronizzazione.|  
||**0x40000**|Replica i filegroup associati a una tabella o un indice partizionato.|  
||**0x80000**|Replica lo schema di partizione per una tabella partizionata.|  
||**0x100000**|Replica lo schema di partizione per un indice partizionato.|  
||**0x200000**|Replica le statistiche della tabella.|  
||**0x400000**|Replica le associazioni predefinite.|  
||**0x800000**|Replica le associazioni di regole.|  
||**0x1000000**|Replica l'indice full-text.|  
||**0x2000000**|Raccolte di XML schema associata a **xml** colonne non vengono replicate.|  
||**0x4000000**|Replica gli indici su **xml** colonne.|  
||**0x8000000**|Crea gli schemi non ancora presenti nel Sottoscrittore.|  
||**0x10000000**|Converte **xml** colonne **ntext** nel Sottoscrittore.|  
||**0x20000000**|Tipi di dati dell'oggetto converte di grandi dimensioni (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) che sono stati introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ai tipi di dati supportati in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
||**0x40000000**|Replica le autorizzazioni.|  
||**0x80000000**|Tenta di eliminare le dipendenze da tutti gli oggetti che non fanno parte della pubblicazione.|  
||**0x100000000**|Utilizzare questa opzione per replicare l'attributo FILESTREAM se viene specificato in **varbinary (max)** colonne. Non specificare questa opzione se si stanno replicando tabelle nei Sottoscrittori [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. La replica di tabelle con colonne FILESTREAM in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] sottoscrittori non è supportata, indipendentemente dall'impostazione di questa opzione dello schema. Vedere l'opzione correlata **0x800000000**.|  
||**0x200000000**|Converte i tipi di dati data e ora (**data**, **ora**, **datetimeoffset**, e **datetime2**) che vengono introdotti [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] per i tipi di dati supportati nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0x400000000**|Replica l'opzione di compressione per dati e indici. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0x800000000**|Impostare questa opzione per archiviare i dati FILESTREAM nel relativo filegroup nel Sottoscrittore. Se questa opzione non è impostata, i dati FILESTREAM vengono archiviati nel filegroup predefinito. Tramite la replica non vengono creati filegroup, pertanto, se si imposta questa opzione, è necessario creare il filegroup prima di applicare lo snapshot nel Sottoscrittore. Per ulteriori informazioni su come creare gli oggetti prima di applicare lo snapshot, vedere [eseguire script prima e dopo l'applicazione dello Snapshot](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Vedere l'opzione correlata **0x100000000**.|  
||**0x1000000000**|Converte i tipi common language runtime (CLR) definito dall'utente (UDT) in **varbinary (max)** in modo che le colonne di tipo definito dall'utente possono essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x2000000000**|Converte il **hierarchyid** tipo di dati **varbinary (max)** in modo che le colonne di tipo **hierarchyid** possano essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per ulteriori informazioni su come usare **hierarchyid** colonne nelle tabelle replicate, vedere [hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Replica gli eventuali indici filtrati sulla tabella. Per ulteriori informazioni sugli indici filtrati, vedere [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Converte il **geography** e **geometry** tipi di dati di **varbinary (max)** in modo che le colonne di questi tipi possono essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|Replica gli indici su colonne di tipo **geography** e **geometry**.|  
||NULL|Il sistema genera automaticamente un'opzione di schema valida per l'articolo.|  
|**status**|**Attiva**|Viene eseguito lo script di elaborazione iniziale per la pubblicazione della tabella.|  
||**unsynced**|Lo script di elaborazione iniziale per la pubblicazione della tabella viene eseguito in occasione della successiva esecuzione dell'agente snapshot.|  
|**stream_blob_columns**|**true**|Viene utilizzata l'ottimizzazione del flusso di dati per la replica di colonne BLOB. Tuttavia, alcune funzionalità della replica di tipo merge, come i record logici, potrebbero impedire l'utilizzo dell'ottimizzazione del flusso. *stream_blob_columns* è impostata su true se FILESTREAM è abilitato. In questo modo, la replica dei dati FILESTREAM può essere eseguita in maniera ottimale e si riduce l'utilizzo della memoria. Per forzare gli articoli di tabella FILESTREAM non vengano utilizzati flussi blob, impostare *stream_blob_columns* su false.<br /><br /> **\*\*Importante \* \***  l'abilitazione di questa ottimizzazione della memoria può ridurre le prestazioni dell'agente di Merge durante la sincronizzazione. È consigliabile utilizzare questa opzione solo se vengono replicate colonne contenenti più megabyte di dati.|  
||**false**|Non viene utilizzata l'ottimizzazione per la replica di colonne BLOB.|  
|**subscriber_upload_options**|**0**|Nessuna restrizione per gli aggiornamenti eseguiti in un Sottoscrittore con una sottoscrizione client. Le modifiche vengono caricate nel server di pubblicazione. La modifica di questa proprietà potrebbe richiedere la reinizializzazione dei Sottoscrittori esistenti.|  
||**1**|Sono consentite modifiche in un Sottoscrittore con una sottoscrizione client, ma tali modifiche non vengono caricate nel server di pubblicazione.|  
||**2**|Non sono consentite modifiche in un Sottoscrittore con una sottoscrizione client.|  
|**subset_filterclause**||Clausola WHERE che specifica il filtro orizzontale. Proprietà valida solo per gli articoli di tabelle.<br /><br /> **\*\*Importante \* \***  per motivi di prestazioni, è consigliabile non applicare funzioni ai nomi di colonna nelle clausole di filtro di riga con parametri, ad esempio `LEFT([MyColumn]) = SUSER_SNAME()`. Se si utilizza [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) in una clausola di filtro e si sostituisce il valore di HOST_NAME, potrebbe essere necessario convertire i tipi di dati tramite [CONVERTIRE](../../t-sql/functions/cast-and-convert-transact-sql.md). Per ulteriori informazioni sulle procedure consigliate in questo caso, vedere la sezione "Si esegue l'override del valore di HOST_NAME ()" in [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
|**soglia**||Valore percentuale utilizzato per i sottoscrittori che eseguono [!INCLUDE[ssEW](../../includes/ssew-md.md)] o versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **soglia** determina quando l'agente di Merge assegna un nuovo intervallo di valori identity. Quando viene utilizzata la percentuale di valori specificata in threshold, l'agente di merge crea un nuovo intervallo di valori Identity. Utilizzato quando **identityrangemanagementoption** è impostato su **auto** o **auto_identity_range** è impostato su **true**. Proprietà valida solo per gli articoli di tabelle. Per ulteriori informazioni, vedere la sezione "Replica di tipo Merge" di [replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**1**|La firma digitale di un sistema di risoluzione personalizzato viene verificata per stabilire se l'origine è attendibile.|  
||**0**|La firma digitale di un sistema di risoluzione personalizzato non viene verificata per stabilire se l'origine è attendibile.|  
|NULL (predefinito)||Restituisce l'elenco di valori supportati per *proprietà*.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo di merge non invalidano lo snapshot. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** significa che le modifiche apportate all'articolo di merge potrebbero invalidare lo snapshot potrebbe non essere valido e se sono disponibili sottoscrizioni che richiedono un nuovo snapshot, consente lo snapshot esistente deve essere contrassegnato come obsoleto e di generarne uno nuovo.  
  
 Per informazioni sulle proprietà che richiedono la generazione di un nuovo snapshot quando vengono modificate, vedere la sezione Osservazioni.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Segnala che l'azione eseguita dalla stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit**, il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo di merge non causano la reinizializzazione della sottoscrizione. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni esistenti, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** indica che le modifiche apportate all'articolo di merge causano reinizializzazione delle sottoscrizioni esistenti e concede l'autorizzazione per la reinizializzazione della sottoscrizione.  
  
 Per ulteriori informazioni sulle proprietà che richiedono la reinizializzazione di tutte le sottoscrizioni esistenti in caso di modifica, vedere la sezione Osservazioni.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_changemergearticle** viene utilizzata nella replica di tipo merge.  
  
 Poiché **sp_changemergearticle** viene utilizzata per modificare le proprietà degli articoli specificate inizialmente tramite [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), fare riferimento a [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Per ulteriori informazioni su queste proprietà.  
  
 Modifica delle proprietà seguenti richiede la generazione di un nuovo snapshot, ed è necessario specificare un valore di **1** per il *force_invalidate_snapshot* parametro:  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 Modifica delle proprietà seguenti richiede esistenti reinizializzazione delle sottoscrizioni ed è necessario specificare un valore di **1** per il *force_reinit_subscription* parametro:  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 Quando si specifica un valore pari a 3 per **partition_options**, i metadati vengono puliti ogni volta che viene eseguito l'agente di Merge e lo snapshot partizionato scade più rapidamente. Quando si utilizza questa opzione è consigliabile prendere in considerazione l'abilitazione di snapshot partizionati richiesti dal Sottoscrittore. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Quando si imposta la **column_tracking** proprietà, se la tabella è già pubblicata in altre pubblicazioni di tipo merge, la colonna di rilevamento deve essere lo stesso come il valore viene utilizzato dagli articoli esistenti basati su questa tabella. Questo parametro è disponibile solo per gli articoli di tabelle.  
  
 Se più pubblicazioni pubblicano articoli basati sulla stessa tabella sottostante, la modifica di **delete_tracking** proprietà o **compensate_for_errors** proprietà per un articolo causa la stessa modifica a eseguire ad altri articoli che sono basati sulla stessa tabella.  
  
 Se l'account di accesso o l'account utente del server di pubblicazione utilizzato per il processo di merge non dispone delle autorizzazioni corrette per le tabelle, le modifiche non valide vengono registrate come conflitti.  
  
 Quando si modifica il valore di **schema_option**, il sistema non esegue un aggiornamento bit per bit. Ciò significa che quando si imposta **schema_option** utilizzando **sp_changemergearticle**esistente, le impostazioni di bit possono essere disattivate. Per mantenere le impostazioni esistenti, è necessario eseguire [& (AND bit per bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md) tra il valore da impostare e il valore corrente di *schema_option*, che è possibile determinare eseguendo [sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md).  
  
> [!CAUTION]  
>  Quando è molti (fino a raggiungere centinaia) degli articoli in una pubblicazione e di eseguire **sp_changemergearticle** per uno degli articoli, potrebbe richiedere molto tempo per completare l'esecuzione.  
  
## <a name="valid-schema-option-table"></a>Tabella delle opzioni di schema valide  
 La tabella seguente descrive consentiti *schema_option*valori, in base al tipo di articolo.  
  
|Tipo di articolo|Valori delle opzioni di schema|  
|------------------|--------------------------|  
|**Func schema solo**|**0x01** e **0x2000**|  
|**solo schema della vista indicizzata**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, e **0x200000**|  
|**proc schema solo**|**0x01** e **0x2000**|  
|**table**|Tutte le opzioni.|  
|**solo schema della vista**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, e **0x200000**|  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_changemergearticle**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà di articolo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
