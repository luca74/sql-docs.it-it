---
title: Creare un backup crittografato | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2ee0ec30a5ec6f6fc6977d74ff4b00a35781e2ac
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="create-an-encrypted-backup"></a>Creare un backup crittografato
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento descrive i passaggi necessari per creare un backup crittografato tramite Transact-SQL.  Per un esempio dell'uso di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vedere [Creazione di un backup completo del database (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md). 
  
## <a name="backup-to-disk-with-encryption"></a>Backup su disco con crittografia  
 **Prerequisiti:**  
  
-   Accesso a un disco locale o a uno spazio di archiviazione con una quantità di spazio adeguata per creare un backup del database.  
  
-   Chiave master di un database master e certificato o chiave asimmetrica disponibile nell'istanza di SQL Server. Per le autorizzazioni e i requisiti di crittografia, vedere [Crittografia dei backup](../../relational-databases/backup-restore/backup-encryption.md).  
  
 Utilizzare i passaggi seguenti per creare un backup crittografato di un database in un disco locale. In questo esempio viene utilizzato un database utente denominato MyTestDB.  
  
1.  **Creare una chiave master del database per il database master:** scegliere una password per crittografare la copia della chiave master che verrà archiviata nel database. Connettersi al motore di database, avviare una nuova finestra Query e copiare e incollare l'esempio seguente, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **Creare un certificato di backup:** creare un certificato di backup nel database master. Copiare e incollare l'esempio seguente nella finestra Query e quindi fare clic su **Esegui**.  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **Backup del database:** specificare l'algoritmo di crittografia e il certificato da usare. Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
 Per un esempio di crittografia di un backup protetto da Extensible Key Management, vedere [Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
### <a name="backup-to-windows-azure-storage-with-encryption"></a>Backup nel servizio di archiviazione Windows Azure con crittografia  
 Se si crea un backup nel servizio di archiviazione Windows Azure usando l'opzione **Backup di SQL Server nell'URL** , i passaggi di crittografia sono gli stessi, ma è necessario usare un URL come destinazione e le credenziali di SQL per autenticare il servizio di archiviazione Windows Azure. Se si desidera configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con le opzioni di crittografia, vedere [Abilitare il backup gestito di SQL Server in Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
 **Prerequisiti:**  
  
-   Account di archiviazione di Windows con contenitore. Per altre informazioni, vedere [Lezione 1: Creare gli oggetti della risorsa di archiviazione di Windows Azure](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5).  
  
-   Chiave master di un database master e certificato o chiave asimmetrica nell'istanza di SQL Server. Per le autorizzazioni e i requisiti di crittografia, vedere [Crittografia dei backup](../../relational-databases/backup-restore/backup-encryption.md).  
  
1.  **Creare le credenziali di SQL Server:** per creare le credenziali di SQL Server, connettersi al motore di database, aprire una nuova finestra Query e copiare e incollare il seguente esempio, quindi fare clic su **Esegui**.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' – this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' – this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **Creare una chiave master del database:** scegliere una password per crittografare la copia della chiave master che verrà archiviata nel database. Connettersi al motore di database, avviare una nuova finestra Query e copiare e incollare l'esempio seguente, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **Creare un certificato di backup:** creare un certificato di backup nel database master. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **Backup del database:** specificare l'algoritmo di crittografia e il certificato da usare. Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' – this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  
