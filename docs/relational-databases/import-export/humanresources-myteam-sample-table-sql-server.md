---
title: Tabella di esempio HumanResources.myTeam (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10cb06809859e67b4c8eadd9aceec41f60a71041
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>Tabella di esempio HumanResources.myTeam (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Molti degli esempi di codice inclusi nell'argomento relativo all' [importazione ed esportazione di dati bulk](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) richiedono una tabella di prova speciale denominata **myTeam**. Prima che sia possibile eseguire gli esempi, è necessario creare la tabella **myTeam** nello schema **HumanResources** del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] è uno dei database di esempio disponibili in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Nella tabella **myTeam** sono incluse le colonne seguenti.  
  
|colonna|Tipo di dati|Supporto di valori Null|Description|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|**smallint**|Non Null|Chiave primaria per le righe. ID dipendente di un membro del team.|  
|**Nome**|**nvarchar(50)**|Non Null|Nome di un membro del team.|  
|**Title**|**nvarchar(50)**|Ammette valori Null|Titolo professionale del dipendente nel team.|  
|**Background**|**nvarchar(50)**|Non Null|Data e ora dell'ultimo aggiornamento della riga. Valore predefinito.|  
  
**Per creare HumanResources.myTeam**  
  
-   Utilizzare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
    ```sql
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
**Per popolare HumanResources.myTeam**  
  
-   Eseguire le istruzioni `INSERT` seguenti per popolare la tabella con due righe:  
  
    ```sql
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  Queste istruzioni ignorano la quarta colonna, `Background`, che ha un valore predefinito. Ignorando la colonna, l'istruzione `INSERT` lascia la colonna vuota.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sull'importazione ed esportazione bulk di dati &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
