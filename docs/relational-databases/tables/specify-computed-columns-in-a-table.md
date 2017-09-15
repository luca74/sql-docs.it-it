---
title: Specificare le colonne calcolate in una tabella | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- computed columns, define
ms.assetid: 731a4576-09c1-47f0-a8f6-edd0b55679f4
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a540a749f8682e47215f18ca022fbfc446f93e1d
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="specify-computed-columns-in-a-table"></a>Specificare le colonne calcolate in una tabella
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Una colonna calcolata è una colonna virtuale che non viene archiviata fisicamente nella tabella, a meno che non sia contrassegnata come PERSISTED. In un'espressione di colonna calcolata possono essere utilizzati dati di altre colonne per calcolare un valore per la colonna di appartenenza. È possibile specificare un'espressione per una colonna calcolata in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Limitations)  
  
     [Sicurezza](#Security)  
  
-   **Per specificare una colonna calcolata:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Limitations"></a> Limitazioni e restrizioni  
  
-   Una colonna calcolata non può essere utilizzata come definizione di vincolo DEFAULT o FOREIGN KEY o con la definizione di vincolo NOT NULL. È tuttavia possibile utilizzare una colonna calcolata come colonna chiave di un indice o come parte di un vincolo PRIMARY KEY o UNIQUE, a condizione che il valore della colonna calcolata sia definito da un'espressione deterministica e il tipo di dati del risultato sia supportato nelle colonne dell'indice. Se, ad esempio, la tabella contiene le colonne di tipo integer a e b, è possibile indicizzare la colonna calcolata a + b, ma non la colonna calcolata a+DATEPART(dd, GETDATE()), in quanto durante chiamate successive il valore potrebbe cambiare.  
  
-   Non è possibile usare una colonna calcolata in un'istruzione INSERT o UPDATE.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
###  <a name="NewColumn"></a> Per aggiungere una nuova colonna calcolata  
  
1.  In **Esplora oggetti**espandere la tabella per cui si desidera aggiungere la nuova colonna calcolata. Fare clic con il pulsante destro del mouse su **Colonne** e scegliere **Nuova colonna**.  
  
2.  Immettere il nome della colonna e accettare il tipo di dati predefinito,**nchar**(10). Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina il tipo di dati della colonna calcolata applicando le regole sulla precedenza dei tipi di dati alle espressioni specificate nella formula. Ad esempio, se la formula fa riferimento a una colonna di tipo **money** e una colonna di tipo **int**, la colonna calcolata sarà di tipo **money** perché tale tipo di dati ha precedenza maggiore. Per altre informazioni, vedere [Precedenza dei tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
3.  Nella scheda **Proprietà colonne** espandere la proprietà **Specifica della colonna calcolata** .  
  
4.  Nella proprietà figlio **(Formula)** immettere l'espressione per la colonna nella cella della griglia a destra. Ad esempio, in una colonna `SalesTotal` , la formula immessa potrebbe essere `SubTotal+TaxAmt+Freight`, che aggiunge il valore in queste colonne per ogni riga della tabella.  
  
    > [!IMPORTANT]  
    >  Quando una formula combina due espressioni di tipi di dati diversi, le regole per la precedenza dei tipi di dati specificano che i tipi con precedenza inferiore vengano convertiti nei tipi con precedenza superiore. Se la conversione non è una conversione implicita supportata, viene restituito l'errore`Error validating the formula for column column_name.`. Utilizzare la funzione CAST o CONVERT per risolvere il conflitto del tipo di dati. Ad esempio, se una colonna di tipo **nvarchar** viene combinata con una colonna di tipo **int**, il tipo integer deve essere convertito in **nvarchar** come mostrato in questa formula `('Prod'+CONVERT(nvarchar(23),ProductID))`. Per altre informazioni, vedere [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
5.  Indicare se i dati sono persistenti selezionando **Sì** oppure **No** nell'elenco a discesa della proprietà figlio **Persistente**.  
  
6.  Nel menu **File** scegliere **Salva***table name*.  
  
#### <a name="to-add-a-computed-column-definition-to-an-existing-column"></a>Per aggiungere una definizione di colonna calcolata a una colonna esistente  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella con la colonna per cui si vuole modificare ed espandere la cartella **Colonne** .  
  
2.  Fare clic con il pulsante destro del mouse sulla colonna per cui si vuole specificare una formula di colonna calcolata e scegliere **Elimina**. Scegliere **OK**.  
  
3.  Aggiungere una nuova colonna e specificare la formula della colonna calcolata attenendosi alla procedura precedente per aggiungere una nuova colonna calcolata.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-add-a-computed-column-when-creating-a-table"></a>Per aggiungere una colonna calcolata quando si crea una tabella  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio viene creata una tabella con una colonna calcolata che moltiplica il valore della colonna `QtyAvailable` per il valore della colonna `UnitPrice` .  
  
    ```  
    CREATE TABLE dbo.Products   
    (  
        ProductID int IDENTITY (1,1) NOT NULL  
      , QtyAvailable smallint  
      , UnitPrice money  
      , InventoryValue AS QtyAvailable * UnitPrice  
    );  
  
    -- Insert values into the table.  
    INSERT INTO dbo.Products (QtyAvailable, UnitPrice)  
    VALUES (25, 2.00), (10, 1.5);  
  
    -- Display the rows in the table.  
    SELECT ProductID, QtyAvailable, UnitPrice, InventoryValue  
    FROM dbo.Products;  
  
    ```  
  
#### <a name="to-add-a-new-computed-column-to-an-existing-table"></a>Per aggiungere una nuova colonna calcolata a una tabella esistente  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio seguente viene aggiunta una nuova colonna alla tabella creata nell'esempio precedente.  
  
    ```  
    ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.35);  
  
    ```  
  
#### <a name="to-change-an-existing-column-to-a-computed-column"></a>Per impostare una colonna esistente su una colonna calcolata  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Per modificare una colonna esistente in una colonna calcolata, rilasciare e ricreare la colonna calcolata. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio seguente viene modificata la colonna aggiunta nell'esempio precedente.  
  
    ```  
    ALTER TABLE dbo.Products DROP COLUMN RetailValue;  
    GO  
    ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5);  
  
    ```  
  
     Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  