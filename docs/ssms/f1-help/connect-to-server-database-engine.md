---
title: Connetti al server (Motore di database) | Microsoft Docs
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-f1
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: "6"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c2a0a98011192659703c444b75cae144dc1303af
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="connect-to-server-database-engine"></a>Connetti al server (Motore di database)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Usare questa finestra di dialogo per visualizzare o specificare le opzioni per la connessione a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]. Nella maggior parte dei casi è possibile connettersi specificando il nome del computer del server di database nella casella **Nome server** e facendo clic su **Connetti**. Se si sta eseguendo la connessione a un'istanza denominata, usare il nome del computer seguito da una barra rovesciata e dal nome dell'istanza. Ad esempio, `mycomputer\myinstance`. Se ci si connette a [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], usare il nome del computer seguito da **\sqlexpress**.  
  
Molti fattori possono incidere sulla possibilità di connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Per informazioni, vedere le risorse seguenti:  
- [Esercitazione - Lezione 1: Connessione al motore di base](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [Risolvere i problemi di connessione al motore di database di SQL Server](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [Solving Connectivity errors to SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server) (Risoluzione di errori di connettività a SQL Server)   
  
## <a name="options"></a>Opzioni  
**Tipo server**  
Per la registrazione di un server da Esplora oggetti, selezionare il tipo di server a cui connettersi, ovvero [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]. Nelle altre parti della finestra di dialogo vengono visualizzate solo le opzioni applicabili al tipo di server selezionato. Durante la registrazione di un server da Server registrati, la casella **Tipo server** è di sola lettura e corrisponde al tipo di server visualizzato nel componente Server registrati. Per registrare un tipo diverso di server, selezionare [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)], [!INCLUDE[ssEW](../../includes/ssew_md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] sulla barra degli strumenti Server registrati prima di iniziare a registrare un nuovo server.  
  
**Nome server**  
Consente di selezionare l'istanza del server a cui connettersi. Per impostazione predefinita verrà visualizzata l'ultima istanza del server a cui è stata effettuata la connessione.  
  
> [!NOTE]  
> Per connettersi a un'istanza utente attiva di [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], eseguire la connessione tramite il protocollo Named Pipes specificando il nome della pipe, ad esempio `np:\\.\pipe\3C3DF6B1-2262-47\tsql\query`. Per altre informazioni, vedere la documentazione di [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].  
  
**Autenticazione**  
La versione corrente di SSMS offre cinque modalità di autenticazione quando si esegue la connessione a un'istanza di [!INCLUDE[ssDE](../../includes/ssde_md.md)]. Se la finestra di dialogo Autenticazione non corrisponde all'elenco seguente, scaricare la versione più recente di SSMS da [Scaricare SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md).  

  
  > **Autenticazione di Windows**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Tale modalità consente di connettersi tramite un account utente di Windows.  
  
  > **autenticazione di SQL Server**  
  > Quando un utente si connette con un nome account di accesso e una password specifici da una connessione non affidabile, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esegue l'autenticazione verificando che sia impostato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e che la password specificata corrisponda a quella registrata in precedenza. Se non è stato impostato alcun account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , l'autenticazione non viene completata e viene segnalato un errore all'utente. Quando possibile, usare l'autenticazione di Windows o l'autenticazione della password Active Directory.  

  > **Active Directory - Universale con supporto MFA**  
Active Directory - Universale con supporto MFA è un flusso di lavoro interattivo che supporta Azure Multi-Factor Authentication (MFA). Azure MFA consente di salvaguardare l'accesso a dati e applicazioni soddisfacendo l'aspettativa dell'utente all'uso di un processo di accesso semplice. Offre autenticazione avanzata con una gamma di opzioni di verifica semplice, ad esempio telefonate, SMS, smart card con pin o notifiche di app mobili, consentendo agli utenti di scegliere il metodo preferito. Quando l'account utente è configurato per MFA il flusso di lavoro di autenticazione interattiva richiede intervento aggiuntivo dell'utente in finestre di dialogo popup, nell'uso di smart card e così via. Quando l'account utente è configurato per MFA, l'utente deve selezionare Autenticazione universale di Azure per la connessione. Se l'account utente non richiede MFA, l'utente può comunque usare le altre due opzioni di autenticazione di Azure Active Directory. Per altre informazioni, vedere [Supporto di SQL Server Management Studio (SSMS) per l'autenticazione MFA di Azure AD con database SQL e SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Se necessario, è possibile modificare il dominio che esegue l'autenticazione dell'accesso facendo clic su **Opzioni**, selezionando la scheda **Proprietà connessione** e quindi completando la casella **ID tenant o nome di dominio AD**.  

  > **Active Directory - Password**  
L'autenticazione di Azure Active Directory è un meccanismo di connessione a [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] tramite identità in Azure Active Directory (Azure AD).  Usare questo metodo per la connessione a [!INCLUDE[ssSDS](../../includes/sssds_md.md)] se si è connessi a Windows con le credenziali da un dominio che non è federato con Azure o se si usa l'autenticazione di Azure AD tramite Azure AD basata sul dominio iniziale o client. Per altre informazioni, vedere [Connessione al database SQL oppure a SQL Data Warehouse con l'autenticazione di Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
  > **Active Directory - Integrata**  
L'autenticazione di Azure Active Directory è un meccanismo di connessione a [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] tramite identità in Azure Active Directory (Azure AD). Usare questo metodo per la connessione a [!INCLUDE[ssSDS](../../includes/sssds_md.md)] se si è connessi a Windows con le credenziali di Azure Active Directory da un dominio federato. Per altre informazioni, vedere [Connessione al database SQL oppure a SQL Data Warehouse con l'autenticazione di Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**User name**  
Nome utente Windows per la connessione. Questa opzione è disponibile solo se si è scelto di connettersi tramite **Autenticazione della password Active Directory**. È di sola lettura quando si seleziona **Autenticazione di Windows** o l'autenticazione **Active Directory - Integrata**.  
  
**Account di accesso**  
Immettere l'account di accesso da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di connettersi tramite Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Autenticazione della password di Active Directory.  
  
**Password**  
Immettere la password per l'account di accesso. Questa opzione è modificabile solo se si è scelto di connettersi tramite Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Autenticazione della password di Active Directory.  
  
**Connect**  
Fare clic per connettersi al server.  
  
**Opzioni**  
Fare clic per visualizzare le schede **Proprietà connessione** e **Parametri aggiuntivi per la connessione**.  
  
