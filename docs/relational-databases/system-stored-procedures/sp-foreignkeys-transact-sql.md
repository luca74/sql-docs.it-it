---
title: sp_foreignkeys (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 248113fe68932f385203b067d77afad506fabbdf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spforeignkeys-transact-sql"></a>sp_foreignkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le chiavi esterne che fanno riferimento alle chiavi primarie nella tabella del server collegato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@table_server =** ] **'***table_server***'**  
 Nome del server collegato di cui si desidera ottenere informazioni di tabella. *table_server* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@pktab_name =** ] **'***pktab_name***'**  
 Nome della tabella contenente una chiave primaria. *pktab_name* è **sysname**, con un valore predefinito è NULL.  
  
 [  **@pktab_schema =** ] **'***pktab_schema***'**  
 Nome dello schema contenente una chiave primaria. *pktab_schema*è **sysname**, con un valore predefinito è NULL. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene il nome del proprietario.  
  
 [  **@pktab_catalog =** ] **'***pktab_catalog***'**  
 Nome del catalogo contenente una chiave primaria. *pktab_catalog*è **sysname**, con un valore predefinito è NULL. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene il nome del database.  
  
 [  **@fktab_name =** ] **'***fktab_name***'**  
 Nome della tabella contenente una chiave esterna. *fktab_name*è **sysname**, con un valore predefinito è NULL.  
  
 [  **@fktab_schema =** ] **'***fktab_schema***'**  
 Nome dello schema contenente una chiave esterna. *fktab_schema*è **sysname**, con un valore predefinito è NULL.  
  
 [  **@fktab_catalog =** ] **'***fktab_catalog***'**  
 Nome del catalogo contenente una chiave esterna. *fktab_catalog*è **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuno  
  
## <a name="result-sets"></a>Set di risultati  
 Vari prodotti DBMS supportano nomi in tre parti per le tabelle (*catalogo***.** *schema***.** *tabella*), adottati nel set di risultati.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|Catalogo della tabella contenente la chiave primaria.|  
|**PKTABLE_SCHEM**|**sysname**|Schema della tabella contenente la chiave primaria.|  
|**PKTABLE_NAME**|**sysname**|Nome della tabella contenente la chiave primaria. Questo campo restituisce sempre un valore.|  
|**PKCOLUMN_NAME**|**sysname**|Nome della colonna chiave primaria o delle colonne, per ogni colonna del **TABLE_NAME** restituito. Questo campo restituisce sempre un valore.|  
|**FKTABLE_CAT**|**sysname**|Catalogo della tabella contenente la chiave esterna.|  
|**FKTABLE_SCHEM**|**sysname**|Schema della tabella contenente la chiave esterna.|  
|**FKTABLE_NAME**|**sysname**|Nome della tabella contenente una chiave esterna. Questo campo restituisce sempre un valore.|  
|**FKCOLUMN_NAME**|**sysname**|Nome delle colonne chiavi esterne, per ogni colonna della tabella TABLE_NAME restituita. Questo campo restituisce sempre un valore.|  
|**KEY_SEQ**|**smallint**|Numero sequenziale della colonna in una chiave primaria a più colonne. Questo campo restituisce sempre un valore.|  
|**UPDATE_RULE**|**smallint**|Azione applicata alla chiave esterna quando l'operazione SQL è un aggiornamento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce 0, 1 o 2 per queste colonne:<br /><br /> 0 = modifiche di tipo CASCADE alla chiave esterna.<br /><br /> 1 = modifiche di tipo NO ACTION se la chiave esterna è presente.<br /><br /> 2 = SET_NULL; la chiave esterna viene impostata su NULL.|  
|**DELETE_RULE**|**smallint**|Azione applicata alla chiave esterna quando l'operazione SQL è un'operazione di eliminazione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce 0, 1 o 2 per queste colonne:<br /><br /> 0 = modifiche di tipo CASCADE alla chiave esterna.<br /><br /> 1 = modifiche di tipo NO ACTION se la chiave esterna è presente.<br /><br /> 2 = SET_NULL; la chiave esterna viene impostata su NULL.|  
|**FK_NAME**|**sysname**|Identificatore della chiave esterna. NULL se non è applicabile all'origine dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce il nome del vincolo FOREIGN KEY.|  
|**PK_NAME**|**sysname**|Identificatore della chiave primaria. NULL se non è applicabile all'origine dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce il nome del vincolo PRIMARY KEY.|  
|**DEFERRABILITY**|**smallint**|Indica se è possibile posticipare il controllo dei vincoli.|  
  
 Nel set di risultati le colonne FK_NAME e PK_NAME restituiscono sempre NULL.  
  
## <a name="remarks"></a>Osservazioni  
 **sp_foreignkeys** nel set di righe di una query di **IDBSchemaRowset** interfaccia del provider OLE DB che corrisponde a *table_server*. Il *table_name*, *table_schema*, *table_catalog*, e *colonna* i parametri vengono passati a questa interfaccia per limitare le righe restituito.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni relative alla chiave esterna per la tabella `Department` del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] presente nel server collegato `Seattle1`.  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
