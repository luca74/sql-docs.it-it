---
title: Creare e gestire cataloghi full-text | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 04ab847cd0305139aa1f7e1dc462ef77ef555bee
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="create-and-manage-full-text-catalogs"></a>Creazione e gestione dei cataloghi full-text
Un catalogo full-text è un contenitore logico per un gruppo di indici full-text. Prima di poter creare un indice full-text è necessario creare un catalogo full-text.

Un catalogo full-text è un oggetto virtuale che non appartiene ad alcun filegroup.
  
##  <a name="creating"></a> Creare un catalogo full-text  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>Creare un catalogo full-text con Transact-SQL
Usare [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md). Esempio:

```tsql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>Creare un catalogo full-text con Management Studio
1.  In Esplora oggetti espandere il server, quindi **Database**e infine il database in cui si vuole creare il catalogo full-text.  
  
2.  Espandere **Archivio**, quindi fare clic con il pulsante destro del mouse su **Cataloghi full-text**.  
  
3.  Selezionare **Nuovo catalogo full-text**.  
  
4.  Nella finestra di dialogo **Nuovo catalogo full-text** specificare le informazioni per il catalogo da creare. Per altre informazioni, vedere [Nuovo catalogo full-text &#40;pagina Generale&#41;](http://msdn.microsoft.com/library/5ed6f7cd-d9af-4439-9f33-fc935b883d91).  
  
    > [!NOTE]  
    >  Gli ID dei cataloghi full-text iniziano da 00005 e vengono incrementati di un'unità per ogni catalogo creato.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="props"></a> Ottenere le proprietà di un catalogo full-text  
Usare la funzione di [!INCLUDE[tsql](../../includes/tsql-md.md)] **FULLTEXTCATALOGPROPERTY** per ottenere il valore di varie proprietà correlate ai cataloghi full-text. Per altre info, vedere [FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).

Ad esempio, eseguire la query seguente per ottenere il conteggio degli indici nel catalogo full-text `Catalog1`.

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
Nella tabella seguente sono elencate le proprietà correlate ai cataloghi full-text. Queste informazioni possono essere utili per l'amministrazione e la risoluzione dei problemi relativi alla ricerca full-text. 
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**AccentSensitivity**|Impostazione relativa alla distinzione tra caratteri accentati e non accentati.|
|**ImportStatus**|Indica se il catalogo full-text viene importato o meno.|  
|**IndexSize**|Dimensione del catalogo full-text in megabyte (MB).| 
|**ItemCount**|Numero delle voci indicizzate incluse attualmente nel catalogo full-text.|  
|**MergeStatus**|Indica se è in corso un'unione nell'indice master.| 
|**PopulateCompletionAge**|Differenza espressa in secondi tra il completamento dell'ultimo popolamento di indici full-text e la data 01/01/1990 00:00:00.| 
|**PopulateStatus**|Stato popolamento.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|Numero di chiavi univoche nel catalogo full-text.| 

##  <a name="rebuildone"></a> Ricompilare un catalogo full-text  

Eseguire l'istruzione Transact-SQL [ALTER FULLTEXT CATALOG ... REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md) oppure eseguire le operazioni seguenti in SQL Server Management Studio (SSMS).

1.  In SSMS, in Esplora oggetti espandere il server, quindi **Database** e infine il database contenente il catalogo full-text che si vuole ricompilare.  
  
2.  Espandere **Archivio**e quindi **Cataloghi full-text**.  
  
3.  Fare clic con il pulsante destro sul nome del catalogo full-text da ricompilare e scegliere **Ricompila**.  
  
4.  Quando viene visualizzato il messaggio **Eliminare il catalogo full-text e ricompilarlo?**, fare clic su **OK**.  
  
5.  Nella finestra di dialogo **Ricompila catalogo full-text** fare clic su **Chiudi**.  
   
##  <a name="rebuildall"></a> Ricompilare tutti i cataloghi full-text per un database  

1.  In SSMS, in Esplora oggetti espandere il server, quindi **Database** e infine il database contenente i cataloghi full-text da ricompilare.  
  
2.  Espandere **Archivio**, quindi fare clic con il pulsante destro del mouse su **Cataloghi full-text**.  
  
3.  Scegliere **Ricompila tutto**.  
  
4.  Quando viene visualizzato il messaggio **Eliminare tutti i cataloghi full-text e ricompilarli?**, fare clic su **OK**.  
  
5.  Nella finestra di dialogo **Ricompila tutti i cataloghi full-text** scegliere **Chiudi**.  
  
  
  
##  <a name="removing"></a> Rimuovere un catalogo full-text da un database  

Eseguire l'istruzione Transact-SQL [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) oppure eseguire le operazioni seguenti in SQL Server Management Studio (SSMS).

1.  In SSMS, in Esplora oggetti espandere il server, quindi **Database** e infine il database contenente il catalogo full-text che si vuole rimuovere.  
  
2.  Espandere **Archivio**e quindi **Cataloghi full-text**.  
  
3.  Fare clic con il pulsante destro del mouse sul catalogo full-text da rimuovere e quindi scegliere **Elimina**.  
  
4.  Nella finestra di dialogo **Elimina oggetti** fare clic su **OK**.  

## <a name="next-step"></a>Passaggio successivo
[Creare e gestire indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md)
