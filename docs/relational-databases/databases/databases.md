---
title: Database | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 05f9976284e6207a1057f1b7308e7276d833daae
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="databases"></a>Database
  Un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituito da una raccolta di tabelle in cui è archiviato un set specifico di dati strutturati. Una tabella contiene una raccolta di righe, definite anche record o tuple, e colonne, definite anche attributi. Ogni colonna nella tabella è progettata per contenere un tipo di informazioni specifico, ad esempio date, nomi, importi in valuta e numeri.  
  
## <a name="basic-information-about-databases"></a>Informazioni di base sui database  
 Un computer può disporre di una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può contenere uno o più database.  All'interno di un database sono presenti uno o più gruppi di proprietà di oggetti denominati schemi. All'interno di ogni schema sono presenti oggetti di database quali tabelle, viste e stored procedure. Alcuni oggetti quali certificati e chiavi asimmetriche sono contenuti all'interno del database, ma non all'interno di uno schema. Per altre informazioni sulla creazione delle tabelle, vedere [Tabelle](../../relational-databases/tables/tables.md).  
  
 I database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono archiviati in file del file system. I file possono essere raggruppati in filegroup. Per altre informazioni su file e filegroup, vedere [Filegroup e file di database](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Quando un utente accede a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene identificato come account di accesso. Quando un utente accede a un database viene identificato come utente di database. Un utente di database può essere basato su un account di accesso. Se sono abilitati i database indipendenti, è possibile creare un utente di database non basato su un account di accesso. Per altre informazioni sugli utenti, vedere [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
 A un utente che dispone di accesso a un database può essere fornita l'autorizzazione per accedere agli oggetti nel database. Sebbene sia possibile concedere autorizzazioni a singoli utenti, si consiglia di creare ruoli del database, aggiungere gli utenti del database ai ruoli, quindi concedere l'autorizzazione di accesso ai ruoli. La concessione di autorizzazioni ai ruoli anziché agli utenti agevola la coerenza e la comprensibilità delle autorizzazioni man mano che il numero di utenti aumenta e si modifica. Per altre informazioni sulle autorizzazioni per i ruoli, vedere [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md) ed [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
## <a name="working-with-databases"></a>Utilizzo dei database  
 La maggior parte degli utenti che operano con i database utilizza lo strumento [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Lo strumento [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dispone di un'interfaccia utente grafica per la creazione di database e degli oggetti nei database. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] usa anche un editor di query per interagire con i database scrivendo istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. È possibile installare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dal disco dell'installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o scaricandolo da MSDN.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|||  
|-|-|  
|[Database di sistema.](../../relational-databases/databases/system-databases.md)|[Eliminare file di dati o file di log da un database](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)|  
|[Database indipendenti](../../relational-databases/databases/contained-databases.md)|[Visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)|  
|[File di dati di SQL Server in Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|[Aumentare le dimensioni di un database](../../relational-databases/databases/increase-the-size-of-a-database.md)|  
|[Filegroup e file di database](../../relational-databases/databases/database-files-and-filegroups.md)|[Rinominare un database](../../relational-databases/databases/rename-a-database.md)|  
|[Stati del database](../../relational-databases/databases/database-states.md)|[Impostare un database in modalità utente singolo](../../relational-databases/databases/set-a-database-to-single-user-mode.md)|  
|[Stati dei file](../../relational-databases/databases/file-states.md)|[Compattare un database](../../relational-databases/databases/shrink-a-database.md)|  
|[Stimare le dimensioni di un database](../../relational-databases/databases/estimate-the-size-of-a-database.md)|[Compattare un file](../../relational-databases/databases/shrink-a-file.md)|  
|[Copiare database in altri server](../../relational-databases/databases/copy-databases-to-other-servers.md)|[Visualizzare o modificare le proprietà di un database](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)|  
|[Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)|[Visualizzare un elenco di database in un'istanza di SQL Server](../../relational-databases/databases/view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[Aggiungere file di dati o file di log a un database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)|[Visualizzare o modificare il livello di compatibilità di un database](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)|  
|[Modificare le impostazioni di configurazione per un database](../../relational-databases/databases/change-the-configuration-settings-for-a-database.md)|[Utilizzare la Creazione guidata piano di manutenzione](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[Creare un database](../../relational-databases/databases/create-a-database.md)|[Creare un alias del tipo di dati definito dall'utente](../../relational-databases/databases/create-a-user-defined-data-type-alias.md)|  
|[Eliminare un database](../../relational-databases/databases/delete-a-database.md)|[Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Indici](../../relational-databases/indexes/indexes.md)  
  
 [Viste](../../relational-databases/views/views.md)  
  
 [Stored procedure &#40;motore di database&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  