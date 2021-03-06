---
title: DROP VIEW (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ed2dc16e20179981985cc52812c8dbc44c0624b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Rimuove una o più viste dal database corrente. È possibile eseguire l'istruzione DROP VIEW su viste indicizzate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *IF EXISTS*  
 **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] alla [versione corrente](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).|  
  
 Rimuove in modo condizionale la vista solo se esiste già.  
  
 *schema_name*  
 Nome dello schema a cui appartiene la vista.  
  
 *view_name*  
 Nome della vista da rimuovere.  
  
## <a name="remarks"></a>Remarks  
 Quando si rimuove una vista, dal catalogo di sistema vengono eliminate la definizione e altre informazioni della vista. Vengono inoltre eliminate tutte le autorizzazioni per la vista.  
  
 Qualsiasi vista di una tabella che viene eliminata tramite DROP TABLE deve essere eliminata in modo esplicito con DROP VIEW.  
  
 Quando viene eseguita su una vista indicizzata, l'istruzione DROP VIEW elimina automaticamente tutti gli indici della vista. Per visualizzare tutti gli indici di una vista, usare [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 Quando si esegue una query tramite una vista, [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica che tutti gli oggetti di database a cui viene fatto riferimento nell'istruzione esistano e siano validi nel contesto dell'istruzione. Inoltre, verifica che le istruzioni di modifica dei dati non violino le regole di integrità dei dati. Se la verifica ha esito negativo, viene visualizzato un messaggio di errore. In caso contrario, l'azione viene convertita automaticamente in un'operazione sulla tabella o sulle tabelle sottostanti. Se le tabelle o viste sottostanti sono state modificate dopo la creazione della vista, può risultare utile eliminare e ricreare la vista.  
  
 Per altre informazioni sulla determinazione delle dipendenze per una vista specifica, vedere [sys.sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 Per altre informazioni sulla visualizzazione del testo della vista, vedere [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Sono necessarie l'autorizzazione **CONTROL** per la vista, l'autorizzazione **ALTER** per lo schema contenente la vista o l'appartenenza al ruolo predefinito del server **db_ddladmin**.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-drop-a-view"></a>A. Eliminare una vista  
 Nell'esempio seguente si rimuove la vista `Reorder`.  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 
