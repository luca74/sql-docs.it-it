---
title: Funzioni definite dall'utente | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: udf
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
ms.openlocfilehash: 03521903614a187ca0af708dd318bbc9b3ae599d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="user-defined-functions"></a>Funzioni definite dall'utente
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
In modo analogo alle funzioni dei linguaggi di programmazione, le funzioni definite dall'utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono routine che accettano parametri, eseguono un'azione (ad esempio un calcolo complesso) e restituiscono il risultato dell'azione sotto forma di valore. Il valore restituito può essere un valore scalare singolo o un set di risultati.  
   
##  <a name="Benefits"></a> Funzioni definite dall'utente  
Perché usarle? 
  
-   Consentono la programmazione modulare.  
  
     È possibile creare la funzione una sola volta, archiviarla nel database e richiamarla nel programma tutte le volte che si desidera. Le funzioni definite dall'utente possono essere modificate in maniera indipendente dal codice sorgente del programma.  
  
-   Consentono tempi di esecuzione più rapidi.  
  
     In maniera simile alle stored procedure, le funzioni definite dall'utente in [!INCLUDE[tsql](../../includes/tsql-md.md)] riducono le risorse necessarie per la compilazione di codice [!INCLUDE[tsql](../../includes/tsql-md.md)] memorizzando nella cache e riutilizzando i piani per esecuzioni ripetute. Ciò significa che una funzione definita dall'utente non deve essere analizzata e ottimizzata nuovamente ogni volta che viene utilizzata, con una conseguente e sensibile riduzione dei tempi di esecuzione.  
  
     Le funzioni CLR offrono un significativo vantaggio nelle prestazioni rispetto alle funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] per le attività di calcolo, modifica delle stringhe e logiche di business. Le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] sono più adatte per logica intensiva di accesso ai dati.  
  
-   Consentono di ridurre il traffico di rete.  
  
     È possibile esprimere in una funzione un'operazione che filtra i dati sulla base di un vincolo complesso che non è possibile esprimere in una singola espressione scalare. È quindi possibile richiamare la funzione nella clausola WHERE per ridurre il numero delle righe inviate al client.  
  
> [!NOTE]
> [!INCLUDE[tsql](../../includes/tsql-md.md)] le funzioni definite dall'utente nelle query possono essere eseguite su un solo thread (piano di esecuzione seriale).  
  
##  <a name="FunctionTypes"></a> Tipi di funzioni  
**Funzioni scalari**  
 Le funzioni scalari definite dall'utente restituiscono un singolo valore di dati del tipo definito nella clausola RETURNS. Per una funzione scalare inline, non è disponibile alcun corpo della funzione. Il valore scalare corrisponde al risultato di una singola istruzione. Per una funzione scalare con istruzioni multiple, il corpo della funzione, definito in un blocco BEGIN...END, include una serie di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che restituiscono un solo valore. Il tipo restituito può essere qualsiasi tipo di dati ad eccezione di **text**, **ntext**, **image**, **cursor**e **timestamp**. 
 **[Esempi.](https://msdn.microsoft.com/library/bb386973(v=vs.110).aspx)**
  
**Funzioni con valori di tabella**  
 Le funzioni con valori di tabella definite dall'utente restituiscono un tipo di dati **table**. Per una funzione inline con valori di tabella non è disponibile alcun corpo della funzione. La tabella corrisponde al set di risultati di una singola istruzione SELECT. **[Esempi.](https://msdn.microsoft.com/library/bb386954(v=vs.110).aspx)**
  
**Funzioni di sistema**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre molte funzioni di sistema che consentono di eseguire diverse operazioni. Tali funzioni non possono essere modificate. Per altre informazioni, vedere [Funzioni predefinite &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md), [Funzioni archiviate di sistema &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-for-transact-sql.md), and [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
##  <a name="Guidelines"></a> Linee guida  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] gli errori che causano l'annullamento di un'istruzione e l'esecuzione dell'istruzione successiva nel modulo (ad esempio trigger o stored procedure) vengono trattati in modo diverso all'interno di una funzione. Nelle funzioni tali errori arrestano l'esecuzione della funzione, che a sua volta comporta l'interruzione dell'istruzione che ha richiamato la funzione.  
  
 Le istruzioni in un blocco BEGIN...END non possono avere effetti collaterali. Gli effetti collaterali di una funzione sono le modifiche permanenti allo stato di una risorsa il cui ambito è al di fuori della funzione, ad esempio la modifica di una tabella di database. Le uniche modifiche che possono essere apportate dalle istruzioni nella funzione sono le modifiche agli oggetti locali rispetto alla funzione, ad esempio variabili o cursori locali. Modifiche a tabelle di database, operazioni su cursori che non sono locali rispetto alla funzione, invio di messaggi di posta elettronica, tentativi di modifica del catalogo e generazione di un set di risultati da restituire all'utente sono esempi di azioni che non possono essere eseguite in una funzione.  
  
> [!NOTE]
> Se un'istruzione CREATE FUNCTION produce effetti collaterali su risorse che non esistono quando l'istruzione CREATE FUNCTION viene eseguita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'istruzione. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esegue la funzione quando viene richiamata.  
  
 Il numero di volte in cui viene effettivamente eseguita una funzione specificata in una query varia in base ai piani di esecuzione compilati da Query Optimizer. Si consideri ad esempio una funzione richiamata da una sottoquery in una clausola WHERE. Il numero di volte in cui la sottoquery e la relativa funzione vengono eseguite varia in base ai diversi percorsi di accesso scelti da Query Optimizer.  
  
##  <a name="ValidStatements"></a> Istruzioni valide in una funzione  
I tipi di istruzioni valide in una funzione sono i seguenti:  
  
-   Istruzioni DECLARE che definiscono variabili di dati e cursori locali rispetto alla funzione.  
  
-   Assegnazioni di valori a oggetti locali rispetto alla funzione, ad esempio utilizzando SET per assegnare valori a variabili locali scalari e di tabella.  
  
-   Operazioni su cursori che fanno riferimento a cursori locali dichiarati, aperti, chiusi e deallocati nella funzione. Non sono consentite istruzioni FETCH che restituiscono dati al client. Sono consentite solo istruzioni FETCH che assegnano valori a variabili locali mediante la clausola INTO.  
  
-   Istruzioni per il controllo di flusso, ad eccezione delle istruzioni TRY...CATCH.  
  
-   Istruzioni SELECT che includono elenchi di selezione con espressioni che assegnano valori a variabili locali rispetto alla funzione.  
  
-   Istruzioni INSERT, UPDATE e DELETE che modificano le variabili di tabella locali rispetto alla funzione.  
  
-   Istruzioni EXECUTE che chiamano stored procedure estese.  
  
### <a name="built-in-system-functions"></a>Funzioni di sistema predefinite  
 Le funzioni predefinite non deterministiche seguenti possono essere utilizzate nelle funzioni Transact-SQL definite dall'utente.  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 Le funzioni predefinite non deterministiche seguenti **non possono** essere usate in funzioni Transact-SQL definite dall'utente.  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 Per un elenco delle funzioni di sistema predefinite deterministiche e non deterministiche, vedere [Funzioni deterministiche e non deterministiche](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
##  <a name="SchemaBound"></a> Funzioni associate a schema  
 L'istruzione CREATE FUNCTION supporta la clausola SCHEMABINDING che associa la funzione allo schema degli oggetti a cui fa riferimento, ad esempio tabelle, viste e altre funzioni definite dall'utente. I tentativi di modifica o eliminazione degli oggetti a cui fa riferimento una funzione associata a schema hanno esito negativo.  
  
 Per includere la clausola SCHEMABINDING in un'istruzione [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) devono essere soddisfatte le condizioni seguenti:  
  
-   Tutte le viste e le funzioni definite dall'utente a cui la funzione fa riferimento devono essere associate a uno schema.  
  
-   Tutti gli oggetti a cui fa riferimento la funzione devono essere inclusi nello stesso database in cui si trova la funzione. Per fare riferimento agli oggetti utilizzare nomi in una parte o in due parti.  
  
-   È necessario disporre di autorizzazione REFERENCES per tutti gli oggetti (tabelle, viste e funzioni definite dall'utente) a cui la funzione fa riferimento.  
  
 È possibile utilizzare l'istruzione ALTER FUNCTION per eliminare l'associazione allo schema. L'istruzione ALTER FUNCTION deve ridefinire la funzione senza specificare WITH SCHEMABINDING.  
  
##  <a name="Parameters"></a> Specifica dei parametri  
 Le funzioni definite dall'utente accettano zero o più parametri di input e restituiscono tabelle o valori scalari. Una funzione può avere al massimo 1024 parametri di input. Quando a un parametro della funzione è associato un valore predefinito, quando si chiama la funzione è necessario specificare la parola chiave DEFAULT per ottenere il valore predefinito. Questa funzionalità risulta diversa per i parametri con valore predefinito nelle stored procedure definite dall'utente in cui l'omissione del parametro implica l'utilizzo del valore predefinito. Le funzioni definite dall'utente non supportano parametri di output.  
  
##  <a name="Tasks"></a> Altri esempi  
  
|||  
|-|-|  
|**Descrizione dell'attività**|**Argomento**|  
|Viene descritto come creare una funzione Transact-SQL definita dall'utente.|[Creare funzioni definite dall'utente &#40;motore di database&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|Viene descritto come creare una funzione CLR.|[Creare funzioni CLR](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|Viene descritto come creare una funzione di aggregazione definita dall'utente.|[Creare funzioni di aggregazione definite dall'utente](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|Viene descritto come modificare una funzione Transact-SQL definita dall'utente.|[Modificare funzioni definite dall'utente](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|Viene descritto come eliminare una funzione definita dall'utente.|[Eliminare funzioni definite dall'utente](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|Viene descritto come eseguire una funzione definita dall'utente.|[Eseguire funzioni definite dall'utente](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|Viene descritto come rinominare una funzione definita dall'utente.|[Rinominare funzioni definite dall'utente](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|Viene descritto come visualizzare la definizione di una funzione definita dall'utente.|[Visualizzare funzioni definite dall'utente](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  
