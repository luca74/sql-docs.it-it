---
title: Esempi di accesso bulk ai dati nell&quot;archiviazione BLOB di Azure | Microsoft Docs
ms.custom: 
ms.date: 01/04/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
caps.latest.revision: 2
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f1e6d604647070e6789fd9a49a7825a3ae3c7e1b
ms.lasthandoff: 04/11/2017

---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Esempi di accesso bulk ai dati nell'archiviazione BLOB di Azure
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Le istruzioni `BULK INSERT` e `OPENROWSET` consentono di accedere direttamente a un file nell'archiviazione BLOB di Azure. Gli esempi seguenti usano dati da un file CSV (con valori delimitati da virgola) denominato `inv-2017-01-19.csv`, archiviato in un contenitore denominato `Week3` e archiviato in un account di archiviazione denominato `newinvoices`. È possibile usare il percorso al file di formato, ma non è incluso in questi esempi. 

Per l'accesso bulk all'archiviazione BLOB di Azure da SQL Server è necessario almeno [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.

## <a name="create-the-credential"></a>Creare le credenziali   
   
Per tutti gli esempi seguenti sono necessarie credenziali con ambito database che fanno riferimento a una firma di accesso condiviso.   

>  [!IMPORTANT]
>  L'origine dati esterna deve essere creata con credenziali con ambito database che usano l'identità `SHARED ACCESS SIGNATURE`. Per creare una firma di accesso condiviso per l'account di archiviazione, vedere la proprietà **Firma di accesso condiviso** nella pagine delle proprietà dell'account di archiviazione, nel portale di Azure. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Per altre informazioni sulle credenziali, vedere [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
 
Creare credenziali con ambito database usando `IDENTITY` che deve essere `SHARED ACCESS SIGNATURE`. Usare il segreto dal portale di Azure. Esempio:  

```tsql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```


## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Accesso ai dati in un file CSV che fa riferimento a un percorso di archiviazione BLOB di Azure   
L'esempio seguente usa un'origine dati esterna che punta a un account di archiviazione di Azure denominato `newinvoices`.   
```tsql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net', 
        CREDENTIAL = UploadInvoices  
    );
```   

L'istruzione `OPENROWSET` aggiunge quindi il nome del contenitore (`week3`) alla descrizione del file. Il file è denominato `inv-2017-01-19.csv`.
```tsql     
SELECT * FROM OPENROWSET(
   BULK  'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```

Con `BULK INSERT`, usare il contenitore e la descrizione del file:

```tsql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV'); 
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>Accesso ai dati in un file CSV che fa riferimento a un contenitore in un percorso di archiviazione BLOB di Azure   

L'esempio seguente usa un'origine dati esterna che punta a un contenitore denominato `week3` in un account di archiviazione di Azure.   
```tsql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3', 
        CREDENTIAL = UploadInvoices  
    );
```  
  
L'istruzione `OPENROWSET` non include il nome del contenitore nella descrizione del file.
```tsql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   SINGLE_CLOB) AS DataFile;
```   

Con `BULKINSERT`, non usare il nome del contenitore nella descrizione del file: 

```tsql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV'); 
```

## <a name="see-also"></a>Vedere anche   

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)   
[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)   
[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)   

