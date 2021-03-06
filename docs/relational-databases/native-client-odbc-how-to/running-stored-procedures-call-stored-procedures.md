---
title: Chiamare le Stored procedure (ODBC) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e8aa0ae9c68313671e3d6e9c8ad1a71392f9524
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="running-stored-procedures---call-stored-procedures"></a>Esecuzione di Stored procedure, chiamare le Stored procedure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'esecuzione di stored procedure come stored procedure remote. L'esecuzione di una stored procedure come stored procedure remota consente al driver e al server di ottimizzare le prestazioni di esecuzione della procedura.  
  
  Quando un'istruzione SQL chiama una stored procedure utilizzando la clausola di escape ODBC CALL, tramite driver di Microsoft® SQL Server™ la stored procedure viene inviata a SQL Server utilizzando il meccanismo di chiamata RPC (Remote Procedure Call). Le richieste RPC ignorano la maggior parte dell'analisi delle istruzioni e dell'elaborazione dei parametri in SQL Server e sono più veloci rispetto a un'istruzione Transact-SQL EXECUTE.  
  
 Per un'applicazione di esempio che illustra questa funzionalità, vedere [codici restituiti di processo e i parametri di Output &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Per eseguire una procedura come RPC  
  
1.  Costruire un'istruzione SQL che utilizzi la sequenza di escape ODBC CALL. Nell'istruzione vengono utilizzati marcatori di parametro per ogni parametro di input, input/output e di output e per il valore restituito della procedura, se disponibile:  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Chiamare [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) per ogni input, input/output, parametro di output e per la procedura di valore restituito (se presente).  
  
3.  Eseguire l'istruzione con [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Se un'applicazione invia una procedura utilizzando la sintassi Transact-SQL EXECUTE, invece della sequenza di escape ODBC CALL, il driver ODBC di SQL Server passa la chiamata di procedura a SQL Server come istruzione SQL anziché come chiamata RPC. Se viene utilizzata l'istruzione Transact-SQL EXECUTE, inoltre, i parametri di output non vengono restituiti.  
  
## <a name="see-also"></a>Vedere anche  
  [Batch di chiamate di Stored Procedure](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Esecuzione di Stored procedure](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Chiamare una Stored Procedure](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedure](../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
  
