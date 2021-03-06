---
title: TDE - Bring Your Own Key (BYOK) - Azure SQL | Microsoft Docs
description: Supporto di BYOK (Bring Your Own Key) per TDE (Transparent Data Encryption) con Azure Key Vault per database e data warehouse SQL. Panoramica di TDE con BYOK, vantaggi, funzionamento, considerazioni e consigli.
keywords: ''
services: sql-database
documentationcenter: ''
author: aliceku
manager: craigg
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.devlang: na
ms.topic: article
ms.date: 04/03/2018
ms.author: aliceku
ms.openlocfilehash: e39e6f8957c1fc2c4f50603af213055cde84d0b6
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-preview-support-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption con supporto Bring Your Own Key (ANTEPRIMA) per database SQL di Azure e SQL Data Warehouse
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

Il supporto Bring Your Own Key (BYOK) per [Transparent Data Encryption (TDE)](transparent-data-encryption.md) consente di crittografare la chiave di crittografia del database (DEK) con una chiave asimmetrica chiamata protezione TDE.  La protezione TDE è memorizzata sotto il proprio controllo in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), il sistema di gestione delle chiavi esterne basato su cloud di Azure. Azure Key Vault è il primo servizio di gestione delle chiavi che offre TDE con il supporto integrato per BYOK. La chiave DEK di TDE, memorizzata nella pagina di avvio del database, viene crittografata e decrittografata dalla protezione TDE. La protezione TDE è memorizzata in Azure Key Vault e rimane sempre nell'insieme di credenziali delle chiavi. Se viene revocato l'accesso del server all'insieme di credenziali delle chiavi, non è possibile eseguire la decrittografia del database e la lettura nella memoria.  La protezione TDE è impostata a livello del server logico e viene ereditata da tutti i database associati al server. 

Con il supporto BYOK, gli utenti possono ora controllare le attività di gestione delle chiavi, tra cui le rotazioni delle chiavi, le autorizzazioni dell'insieme di credenziali delle chiavi e l'eliminazione delle chiavi, nonché abilitare il controllo e la creazione di report relativi a tutte le protezioni TDE usando la funzionalità Azure Key Vault. Key Vault consente di gestire le chiavi in modo centralizzato, usa moduli di protezione hardware accuratamente monitorati e consente la separazione delle responsabilità tra la gestione delle chiavi e quella dei dati per contribuire a soddisfare la conformità alle normative.  


TDE con BYOK offre i vantaggi seguenti:
- Maggiore trasparenza e un controllo granulare con la possibilità di gestire in autonomia la protezione TDE   
- Gestione centralizzata delle protezioni TDE (con altre chiavi e segreti usati in altri servizi di Azure), ospitate in Key Vault
- Separazione delle responsabilità di gestione delle chiavi e dei dati all'interno dell'organizzazione, per supportare la separazione delle funzioni
- Maggiore fiducia da parte dei clienti, poiché Key Vault è progettato in modo tale che Microsoft non vede né estrae chiavi di crittografia. 
- Supporto per la rotazione delle chiavi

> [!IMPORTANT]
> Per chi usa la protezione TDE gestita dal servizio e vuole iniziare a usare Key Vault, la protezione TDE rimane abilitata durante il passaggio a una protezione TDE in Key Vault. Non esistono tempi di inattività e non viene rieseguita la crittografia dei file di database. Il passaggio da una chiave gestita dal servizio a una chiave di Key Vault richiede solo l'esecuzione di una nuova crittografia della chiave di crittografia del database (DEK), che è una rapida operazione online. 
>

## <a name="how-does-tde-with-byok-support-work"></a>Come funziona TDE con il supporto BYOK?
 
![Autenticazione del server per Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Quando TDE viene configurato per la prima volta per l'uso di una protezione TDE da Key Vault, il server invia la chiave DEK di ogni database abilitato per TDE a Key Vault per una richiesta di wrapping della chiave. Key Vault restituisce la chiave di crittografia del database crittografato, che è archiviata nel database utente.  

>[!IMPORTANT]
>È importante notare che **dopo essere stata memorizzata in Azure Key Vault, la protezione TDE viene mantenuta in Azure Key Vault**. Il server logico può solo inviare richieste di operazioni relative alla chiave al materiale della chiave di protezione TDE all'interno di Key Vault e **non accedere mai o memorizzare nella cache la protezione TDE**. L'amministratore di Key Vault ha il diritto di revocare le autorizzazioni di Key Vault del server in qualsiasi momento. In tal caso, tutte le connessioni al server vengono interrotte. 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>Linee guida per la configurazione di TDE con BYOK

### <a name="general-guidelines"></a>Linee guida generali
- Assicurarsi che Azure Key Vault e il database SQL di Azure si trovino nello stesso tenant.  Le interazioni dell'insieme di credenziali delle chiavi e del server tra tenant **non sono supportate**.
- Definire le sottoscrizioni da usare per le risorse necessarie poiché se il server viene spostato successivamente in un'altra sottoscrizione sarà necessario eseguire una nuova impostazione di TDE con BYOK.
- Quando si configura TDE con BYOK è importante valutare il carico che le ripetute operazioni di wrapping e annullamento del wrapping determinano sull'insieme di credenziali delle chiavi. Ad esempio, poiché tutti i database associati a un server logico usano la stessa protezione TDE, un failover del server attiverà un numero di operazioni sull'insieme di credenziali delle chiavi equivalente al numero di database presenti nel server. In base all'esperienza e ai [limiti del servizio Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits) documentati, è consigliabile associare al massimo 500 database Standard o 200 database Premium a un'istanza di Azure Key Vault in una sottoscrizione singola al fine di garantire una disponibilità costantemente elevata durante l'accesso alla protezione TDE nell'insieme di credenziali. 
- Consigliato: conservare una copia della protezione TDE in locale.  A tale scopo, è necessario che un modulo di protezione hardware crei una protezione TDE locale e che un sistema di deposito delle chiavi memorizzi una copia locale della protezione TDE.


### <a name="guidelines-for-configuring-azure-key-vault"></a>Linee guida per la configurazione di Azure Key Vault

- Usare un insieme di credenziali delle chiavi con [eliminazione temporanea](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) abilitata per evitare la perdita di dati in caso di eliminazione accidentale della chiave o dell'insieme di credenziali delle chiavi:  
  - Le risorse eliminate temporaneamente vengono conservate per un periodo di tempo di 90 giorni, a meno che non vengano recuperate o ripulite.
  - Alle azioni di **recupero** e **pulizia** sono associate autorizzazioni specifiche nei criteri di accesso dell'insieme di credenziali delle chiavi. 
- Concedere al server logico l'accesso all'insieme di credenziali delle chiavi usando la relativa identità di Azure Active Directory (Azure AD).  Quando viene usata l'interfaccia utente del portale, l'identità Azure AD creata automaticamente e le autorizzazioni di accesso all'insieme di credenziali delle chiavi vengono concesse al server.  Se si usa PowerShell per configurare TDE con BYOK, è necessario creare l'identità Azure AD e verificare il completamento. Per istruzioni passo passo dettagliate per l'uso di PowerShell, vedere [Configurare TDE con BYOK](transparent-data-encryption-byok-azure-sql-configure.md).

  >[!NOTE]
  >Se l'identità Azure AD **viene eliminata per errore o se vengono revocate le autorizzazioni del server** usando i criteri di accesso dell'insieme di credenziali delle chiavi, il server perde l'accesso all'insieme di credenziali delle chiavi.
  >
  
- Abilitare il controllo e la creazione di report per tutte le chiavi di crittografia: Key Vault offre log che possono essere facilmente inseriti in altri strumenti di informazioni di sicurezza e gestione degli eventi (SIEM). [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) di Operations Management Suite (OMS) è un esempio di servizio già integrato.
- Per garantire la disponibilità elevata dei database crittografati, configurare ogni server logico con due Azure Key Vault che risiedono in aree diverse.


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>Linee guida per la configurazione della protezione TDE (chiave asimmetrica) memorizzata in Azure Key Vault

- Creare la chiave di crittografia in locale in un dispositivo HSM locale. Verificare che si tratti di una chiave RSA 2048 asimmetrica memorizzabile in Azure Key Vault.
- Depositare la chiave in un sistema di deposito delle chiavi.  
- Importare il file della chiave di crittografia (PFX, BYOK o BACKUP) in Azure Key Vault. 
    

>[!NOTE] 
    >A scopo di test, è possibile creare una chiave con Azure Key Vault, ma la chiave non potrà essere depositata poiché la chiave privata deve rimanere nell'insieme di credenziali delle chiavi.  Eseguire sempre il backup e il deposito delle chiavi usate per crittografare i dati di produzione poiché la perdita della chiave (eliminazione accidentale nell'insieme di credenziali delle chiavi, scadenza, ecc.) causa la perdita permanente dei dati.
    >
    
- Usare una chiave senza data di scadenza e non impostare mai una data di scadenza per una chiave già in uso: **dopo la scadenza della chiave, i database crittografati perdono l'accesso alla protezione TDE e vengono eliminati entro 24 ore**.
- Verificare che la chiave sia abilitata e abbia le autorizzazioni per eseguire le operazioni *get*, *wrap key* e *unwrap key*.
- Creare un backup della chiave di Azure Key Vault prima di usare la chiave in Azure Key Vault per la prima volta. Altre informazioni sul comando [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) .
- Creare un nuovo backup ogni volta che vengono apportate modifiche alla chiave, ad esempio si aggiungono elenchi di controllo di accesso, tag o attributi della chiave.
- **Mantenere le versioni precedenti** della chiave nell'insieme di credenziali delle chiavi quando viene eseguita la rotazione delle chiavi in modo che si possano ripristinare i backup meno recenti dei database. Quando la protezione TDE viene modificata per un database, i backup precedenti del database **non vengono aggiornati** in modo da usare la protezione TDE più recente.  In fase di ripristino ogni backup richiede la protezione TDE con cui è stato creato. Le rotazioni delle chiavi possono essere eseguite seguendo le istruzioni in [Ruotare la protezione Transparent Data Encryption (TDE) con PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- Mantenere tutte le chiavi usate in precedenza in Azure Key Vault dopo il ripristino delle chiavi gestite dal servizio.  Ciò garantisce la possibilità di ripristinare i backup dei database con le protezioni TDE memorizzate in Azure Key Vault.  Le protezioni TDE create con Azure Key Vault devono essere mantenute fino a quando non vengono creati tutti i backup memorizzati con le chiavi gestite dal servizio.  
- Creare copie di backup recuperabili delle chiavi usando [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1).
- Per rimuovere una chiave potenzialmente compromessa durante un evento imprevisto per la sicurezza senza il rischio di perdita di dati, eseguire la procedura descritta in [Rimuovere una protezione Transparent Data Encryption (TDE) con PowerShell](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md).


## <a name="high-availability-geo-replication-and-backup--restore"></a>Disponibilità elevata, replica geografica e backup/ripristino

### <a name="high-availability-and-disaster-recovery"></a>Disponibilità elevata e ripristino di emergenza

La modalità di configurazione della disponibilità elevata con Azure Key Vault varia a seconda della configurazione del database e del server logico. Di seguito sono descritte le configurazioni consigliate per due casi distinti.  Il primo caso riguarda un database autonomo o un server logico per il quale non è stata configurata alcuna ridondanza geografica.  Il secondo caso riguarda un database o un server logico configurato con gruppi di failover o ridondanza geografica in cui è necessario assicurare che ogni copia con ridondanza geografica abbia un Azure Key Vault locale all'interno del gruppo di failover per garantire il funzionamento dei failover geografici. Nel primo caso, se si richiede la disponibilità elevata di un database e di un server logico per il quale non è stata configurata alcuna ridondanza geografica, è consigliabile configurare il server in modo che usi due insiemi di credenziali delle chiavi diversi in due aree diverse con lo stesso materiale delle chiavi.  Questo risultato può essere ottenuto creando una protezione TDE tramite l'insieme di credenziali delle chiavi primario che si trova nella stessa area del server e clonando la chiave in un insieme di credenziali delle chiavi in un'area di Azure diversa in modo che il server abbia accesso a un secondo insieme di credenziali delle chiavi nel caso in cui si verifichi un'interruzione nell'insieme di credenziali delle chiavi primario mentre il database è in esecuzione. Usare il cmdlet Backup-AzureKeyVaultKey per recuperare la chiave in formato crittografato dall'insieme di credenziali delle chiavi primario e quindi usare il cmdlet Restore-AzureKeyVaultKey e specificare un insieme di credenziali delle chiavi nella seconda area.


![Disponibilità elevata di server singolo senza ripristino di emergenza geografico](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

## <a name="how-to-configure-geo-dr-with-azure-key-vault"></a>Come configurare il ripristino di emergenza geografico con Azure Key Vault

Per mantenere la disponibilità elevata delle protezioni TDE per i database crittografati, è necessario configurare gli Azure Key Vault ridondanti in base ai gruppi di failover del database SQL esistenti o desiderati o alle istanze di replica geografica attive.  Ogni server con replica geografica richiede un insieme di credenziali delle chiavi separato, che deve trovarsi nella stessa area di Azure del server. Se un database primario diventa inaccessibile a causa di un'interruzione in un'area e viene attivato un failover, il database secondario può sostituirlo usando l'insieme di credenziali delle chiavi secondario. 
 
Per i database SQL di Azure con replica geografica, è necessaria la configurazione di Azure Key Vault seguente:
- Un database primario con un insieme di credenziali delle chiavi nell'area e un database secondario con un insieme di credenziali delle chiavi nell'area. 
- Almeno un database secondario è obbligatorio, ne sono supportati fino a quattro. 
- Database secondari di database secondari (concatenamento) non sono supportati.

La sezione seguente descrive i passaggi di installazione e configurazione in modo più dettagliato. 

### <a name="azure-key-vault-configuration-steps"></a>Procedura di configurazione di Azure Key Vault

- Installare [PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0) 
- Creare due Azure Key Vault in due aree diverse usando [PowerShell per abilitare la proprietà di "eliminazione temporanea"](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) per gli insiemi di credenziali delle chiavi. Questa opzione non è ancora disponibile nel portale di Azure Key Vault, ma è richiesta da SQL 
- Creare una nuova chiave nel primo insieme di credenziali delle chiavi:  
  - Chiave RSA/RSA-HSA 2048 
  - Nessuna data di scadenza 
  - La chiave è abilitata e ha le autorizzazioni per eseguire operazioni get, wrap key e unwrap key 
- Eseguire il backup della chiave primaria e ripristinare la chiave nel secondo insieme di credenziali delle chiavi.  Vedere [BackupAzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) e [Restore-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-5.5.0). 

### <a name="azure-sql-database-configuration-steps"></a>Procedura di configurazione del database SQL di Azure

La procedura di configurazione seguente è diversa a seconda che si inizi con una nuova distribuzione di SQL o che si usi una distribuzione di ripristino di emergenza geografico di SQL già esistente.  Viene prima descritta la procedura di configurazione per una nuova distribuzione e quindi viene spiegato come assegnare protezioni TDE archiviate in Azure Key Vault a una distribuzione esistente per cui è già stabilito un collegamento di ripristino di emergenza geografico. 

Procedura per una nuova distribuzione:
- Creare i due server SQL logici nelle stesse due aree degli insiemi di credenziali delle chiavi creati in precedenza. 
- Selezionare il riquadro TDE dei server logici e per ognuno dei server SQL logici:  
   - Selezionare l'Azure Key Vault che si trova nella stessa area 
   - Selezionare la chiave da usare come protezione TDE. Ogni server userà la copia locale della protezione TDE. 
   - Se si esegue questa operazione nel portale, viene creato un [AppID](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview) per il server SQL logico, che consente di assegnare le autorizzazioni di SQL Server logico per accedere all'insieme di credenziali delle chiavi. Non eliminare questa identità.  L'accesso può essere revocato rimuovendo invece le autorizzazioni in Azure Key Vault. per il server SQL logico, che consente di assegnare le autorizzazioni di SQL Server logico per accedere all'insieme di credenziali delle chiavi. Non eliminare questa identità.  L'accesso può essere revocato rimuovendo invece le autorizzazioni in Azure Key Vault. 
- Creare il database primario. 
- Seguire il [materiale sussidiario per la replica geografica attiva](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview) per completare questo scenario. Questo passaggio creerà il database secondario.

![Gruppi di failover e ripristino di emergenza geografico](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

>[!NOTE]
>È importante assicurarsi che le stesse protezioni TDE siano presenti in entrambi gli insiemi di credenziali delle chiavi prima di stabilire il collegamento di replica geografica tra i database.
>

Procedura per un database SQL esistente con distribuzione di ripristino di emergenza geografico:

Poiché i server SQL logici esistono già e i database primario e secondario sono già stati assegnati, i passaggi per la configurazione di Azure Key Vault devono essere eseguiti nell'ordine seguente: 
- Iniziare con il server SQL logico che ospita il database secondario: 
   - Assegnare l'insieme di credenziali delle chiavi che si trova nella stessa area 
   - Assegnare la protezione TDE 
- Passare al server SQL logico che ospita il database primario: 
   - Selezionare la stessa protezione TDE usata per il database secondario
   
![Gruppi di failover e ripristino di emergenza geografico](./media/transparent-data-encryption-byok-azure-sql/geo_DR_ex_config.PNG)

>[!NOTE]
>Quando si assegna l'insieme di credenziali delle chiavi al server, è importante iniziare dal server secondario.  Nel secondo passaggio, assegnare l'insieme di credenziali delle chiavi al server primario e aggiornare la protezione TDE. Il collegamento di ripristino di emergenza geografico continuerà a funzionare perché a questo punto la protezione TDE usata dal database replicato è disponibile per entrambi i server.
>

Prima di abilitare TDE con chiavi gestite dal cliente in Azure Key Vault per uno scenario di emergenza geografico di un database SQL, è importante creare e gestire due Azure Key Vault con contenuto identico nelle stesse aree che verranno usate per la replica geografica del database SQL.  "Contenuto identico" significa specificamente che entrambi gli insiemi di credenziali delle chiavi devono contenere copie della stessa o delle stesse protezioni TDE, in modo che entrambi i server abbiano accesso alle protezioni TDE per l'uso da parte di tutti i database.  Andando avanti, è necessario mantenere sincronizzati entrambi gli insiemi di credenziali delle chiavi. Ciò significa che questi devono contenere le stesse copie delle protezioni TDE dopo la rotazione delle chiavi e mantenere le versioni precedenti delle chiavi usate per i file di log o i backup. Oltre a ciò, le protezioni TDE devono mantenere le stesse proprietà delle chiavi e gli insiemi di credenziali delle chiavi devono mantenere le stesse autorizzazioni di accesso per SQL.  
 
Seguire i passaggi descritti in [Panoramica della replica geografica attiva](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) per testare e attivare un failover. Questa operazione deve essere eseguita con regolarità per confermare che le autorizzazioni di accesso per SQL a entrambi gli insiemi di credenziali delle chiavi sono state mantenute. 


### <a name="backup-and-restore"></a>Backup e ripristino

Se un database viene crittografato con TDE usando una chiave di Key Vault, vengono crittografati con la stessa protezione TDE anche gli eventuali backup generati.

Per ripristinare un backup crittografato con una protezione TDE di Key Vault, verificare che il materiale della chiave sia ancora nell'insieme di credenziali originale con il nome originale della chiave. Quando la protezione TDE viene modificata per un database, i backup più datati del database **non** vengono aggiornati in modo da usare la protezione TDE più recente. È quindi consigliabile mantenere tutte le versioni precedenti della protezione TDE in Key Vault in modo che sia possibile ripristinare i backup del database. 

Se una chiave che potrebbe essere necessaria per ripristinare un backup non è più nell'insieme di credenziali delle chiavi originale, un messaggio di errore indica che il server di destinazione <Servername> non ha accesso a tutti gli URI AKV creati tra <Timestamp #1> e <Timestamp #2>. e che è possibile ritentare l'operazione dopo il ripristino di tutti gli URI AKV.

Per evitare questo problema, eseguire il cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) per restituire l'elenco delle chiavi di Key Vault aggiunte al server (a meno che non siano state eliminate da un utente). Per garantire che tutti i backup possano essere ripristinati, verificare che il server di destinazione per il backup abbia accesso a tutte queste chiavi.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Per altre informazioni sul ripristino dei backup per il database SQL, vedere [Ripristinare un database SQL di Azure mediante i backup automatici del database](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Per altre informazioni sul ripristino dei backup per il data warehouse SQL, vedere [Ripristino di SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).


Altra considerazione per i file di log sottoposti a backup: i file di log sottoposti a backup rimangono crittografati con il componente di crittografia TDE originale, anche se è stata eseguita la rotazione della protezione TDE e il database ora usa una nuova protezione TDE.  Al momento del ripristino, saranno necessarie entrambe le chiavi per ripristinare il database.  Se il file di log usa una protezione TDE archiviata in Azure Key Vault, al momento del ripristino sarà necessaria questa chiave, anche se nel frattempo il database è stato modificato in modo che usi la crittografia TDE gestita dal servizio.


