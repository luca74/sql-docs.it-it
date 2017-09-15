---
title: 'Lezione 1: Creazione di un Database Sottoscrittore di esempio | Documenti Microsoft'
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4d862dc34dcbb81ce8d50cfac53d81a80f47d29c
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---

# <a name="lesson-1-creating-a-sample-subscriber-database"></a>Lezione 1: Creazione di un database di esempio del Sottoscrittore

In questa lezione dell'esercitazione [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] si crea un database "subscriber" di piccole dimensioni per archiviare dati di sottoscrizione che verranno usati in uno scenario di sottoscrizione guidata dai dati. Quando la sottoscrizione viene elaborata, il server di report recupera i dati e li usa per personalizzare l'output dei report. Ad esempio, le righe di dati includono numeri d'ordine specifici usabili per i filtri e per determinare il formato di file per la creazione dei report.  
  
In questa lezione si presuppone l'uso [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] per creare un database di SQL Server.  
  
### <a name="to-create-a-sample-subscriber-database"></a>Per creare un database di esempio del Sottoscrittore  
  
1.  Avviare [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]e stabilire una connessione a un'istanza di [!INCLUDE[ssDEnoversion_md](../includes/ssdenoversion-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse su Database, quindi scegliere **Nuovo database**.  
  
3.  Nella finestra di dialogo Nuovo database, in **Nome database**digitare *Subscribers*. 
4. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Fare clic sul pulsante **Nuova query** sulla barra degli strumenti.  
  
6.  Copiare le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] seguenti nella query vuota:  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
7.  Fare clic su **! Eseguire** sulla barra degli strumenti.  
  
8.  Utilizzare un'istruzione SELECT per verificare che siano disponibili tre righe di dati. Esempio: `select * from OrderInfo`  
  
## <a name="next-steps"></a>Passaggi successivi  
+ In tal modo sono stati creati i dati di sottoscrizione per la distribuzione dei report e per la variazione dell'output del report per ogni sottoscrittore. 
+ Sarà quindi possibile modificare le proprietà dell'origine dati del report per l'uso delle credenziali archiviate. 
+ Inoltre, verrà modificata la progettazione report per includere un parametro che verrà utilizzato dalla sottoscrizione con i dati del sottoscrittore. [Lezione 2: Modifica delle proprietà dell'origine dei dati del report](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md).  

## <a name="next-steps"></a>Passaggi successivi

[Creazione di una sottoscrizione guidata dai dati](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[Creare un database](../relational-databases/databases/create-a-database.md)  
[Creazione di un report tabella semplice](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

Ulteriori domande? [Provare a porre il forum di Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)