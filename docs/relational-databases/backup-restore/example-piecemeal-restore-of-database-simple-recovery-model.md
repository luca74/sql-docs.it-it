---
title: 'Esempio: Ripristino a fasi di un database (modello di recupero con registrazione minima) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aaa83db092b00caec1a9a25bf70de97614562363
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>Esempio: Ripristino a fasi di un database (modello di recupero con registrazione minima)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Una sequenza di ripristino a fasi consente di ripristinare e recuperare un database in varie fasi a livello di filegroup, a partire dal filegroup primario e tutti i filegroup secondari di lettura/scrittura.  
  
 In questo esempio il database `adb` viene ripristinato in un nuovo computer dopo un'emergenza. Per il database è in uso il modello di recupero con registrazione minima. Prima dell'emergenza, tutti i filegroup erano online. I filegroup `A` e `C` sono di lettura/scrittura, mentre il filegroup `B` è di sola lettura. Il filegroup `B` è diventato di sola lettura prima del backup parziale più recente, che include il filegroup primario e i filegroup secondari di lettura/scrittura `A` e `C`. Dopo che il filegroup `B` è diventato di sola lettura, è stato eseguito un backup di file separato per il filegroup `B` .  
  
## <a name="restore-sequences"></a>Sequenze di ripristino  
  
1.  Eseguire un ripristino parziale del filegroup primario e dei filegroup `A` e `C`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     A questo punto il filegroup primario e i filegroup `A` e `C` sono online. Il recupero di tutti i file nel filegroup `B` è in sospeso e questo filegroup è offline.  
  
2.  Eseguire un ripristino online del filegroup `B`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     In questa fase tutti i filegroup sono online.  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
  
-   [Esempio: Ripristino a fasi di filegroup selezionati &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di un database &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di un numero limitato di filegroup &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di lettura/scrittura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  