---
title: "Proprietà SQL Server (scheda parametri di avvio) | Documenti Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16942624-5374-446c-8de4-ee6ed34d6e94
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c845f8c174f96ba2e0dd5595d49721ae800777e2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sql-server-properties-startup-parameters-tab"></a>Proprietà di SQL Server (scheda Parametri di avvio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Utilizzare questa finestra di dialogo per aggiungere o rimuovere parametri di avvio per [!INCLUDE[ssDE](../../includes/ssde-md.md)]. I parametri di avvio possono avere un effetto significativo sulle prestazioni di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Prima di aggiungere o modificare i parametri di avvio, vedere l'argomento "Utilizzo delle opzioni di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opzioni  
 **Specificare un parametro di avvio**  
 Per aggiungere un parametro, digitarlo e quindi fare clic su **Aggiungi**.  
  
 Per modificare uno dei parametri obbligatori, selezionare il parametro nella casella **Parametri esistenti** , modificare i valori nella casella **Specificare un parametro di avvio** e quindi fare clic su **Aggiorna**.  
  
 **Parametri esistenti**  
 Per rimuovere un parametro, selezionarlo e quindi fare clic su **Rimuovi**.  
  
## <a name="parameter-format"></a>Formato dei parametri  
 Non inserire un separatore tra parametri. Il separatore viene aggiunto automaticamente in Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager consente di applicare i seguenti requisiti di parametro.  
  
-   Spazi iniziali e finali vengono tagliati da qualsiasi parametro di avvio.  
  
-   Tutti i parametri di avvio iniziano con un - (trattino) e il secondo valore è una lettera.  
  
## <a name="required-parameters"></a>Parametri obbligatori  
 I parametri seguenti sono obbligatori. Possono essere modificati ma non rimossi.  
  
-   -d è il percorso del file **master.mdf** (il file di dati del database master).  
  
-   -l è il percorso del file **master.ldf** (il file di log del database master).  
  
-   -e è il percorso dei file di log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  Se i parametri del percorso del file non sono corretti, è possibile che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non venga avviato.  
  
 Per altre informazioni su come spostare il database master, vedere l'argomento "Spostamento dei database di sistema" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="optional-parameters"></a>Parametri facoltativi  
 Tutti i parametri di avvio supportati sono descritti nell'argomento "Utilizzo delle opzioni di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un parametro di avvio -T*trace#* indica che deve essere avviata un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con uno specifico flag di traccia (*trace#*) attivo. I flag di traccia vengono utilizzati per avviare il server con un funzionamento non standard. Per altre informazioni sui flag di traccia, vedere l'argomento "Flag di traccia ([!INCLUDE[tsql](../../includes/tsql-md.md)])" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  Su Internet è possibile che siano descritti parametri di avvio e flag di traccia aggiuntivi non documentati. I parametri di avvio e i flag di traccia non documentati vengono creati per risolvere problemi non comuni o per forzare determinate condizioni richieste per il test. L'utilizzo di parametri di avvio non documentati può causare risultati imprevisti. Utilizzare parametri non documentati solo se indicato dal Servizio Supporto Tecnico Clienti Microsoft.  
  
 Nell'elenco seguente vengono descritti alcuni parametri facoltativi comuni.  
  
|Parametro|Breve descrizione|  
|---------------|-----------------------|  
|-m|Avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo.|  
|-T1204|Restituisce le risorse e i tipi di blocco coinvolti in un deadlock nonché il comando corrente interessato.|  
|-T1224|Disabilita l'escalation di blocchi in base al numero di blocchi.|  
|-T3608|Impedisce l'avvio e il recupero automatico dei database ad eccezione del database master in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|-T7806|Abilita una connessione amministrativa dedicata (DAC, Dedicated Administrator Connection) in [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].|  
  
> [!CAUTION]  
>  Alcuni parametri facoltativi possono modificare il comportamento del server e incidere sulle prestazioni.  
  
## <a name="permissions"></a>Permissions  
 L'utilizzo di questa pagina è limitato a utenti che possono modificare le voci correlate nel Registro di sistema. Sono inclusi gli utenti indicati di seguito.  
  
-   Membri del gruppo Administrators locale.  
  
-   Account di dominio utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] è configurato per essere in esecuzione in un account di dominio.  
  
## <a name="books-online-references"></a>Riferimenti della documentazione online  
 Per informazioni aggiuntive sui parametri di avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere "Procedura: Configurazione delle opzioni di avvio del server (Gestione configurazione[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
