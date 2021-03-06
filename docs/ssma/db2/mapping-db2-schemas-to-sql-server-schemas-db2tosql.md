---
title: DB2 schemi di mapping per gli schemi di SQL Server (DB2ToSQL) | Documenti Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b6270bf3fda2f19b6559ceca4c3385369213de3
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>DB2 schemi di mapping per gli schemi di SQL Server (DB2ToSQL)
In DB2, ogni database dispone di uno o più schemi. Per impostazione predefinita, SSMA esegue la migrazione di tutti gli oggetti in uno schema DB2 per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] denominato per lo schema di database. Tuttavia, è possibile personalizzare il mapping tra gli schemi di DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] database.  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 e schemi SQL Server  
Un database DB2 contiene gli schemi. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] contiene più database, ognuno dei quali può disporre di più schemi.  
  
Il concetto di DB2 di uno schema di mapping per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] concetto di un database e uno dei relativi schemi. Ad esempio, DB2 può avere uno schema denominato **HR**. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] potrebbe disporre di un database denominato **HR**, e all'interno del database sono gli schemi. È uno schema di **dbo** (o proprietario del database) dello schema. Per impostazione predefinita, lo schema DB2 **HR** verrà eseguito il mapping per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] database e lo schema **HR.dbo**. SSMA si intende il [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] combinazione di database e lo schema come schema.  
  
È possibile modificare il mapping tra DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] schemi.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica il Database di destinazione e lo Schema  
In SSMA, è possibile mappare un schema DB2 a eventuale [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dello schema.  
  
**Per modificare il database e lo schema**  
  
1.  Nel Visualizzatore metadati DB2, selezionare **schemi**.  
  
    Il **Mapping dello Schema** scheda è disponibile anche quando si seleziona un singolo database, il **schemi** cartella o singoli schemi. Nell'elenco di **dello Schema di Mapping** scheda personalizzata per l'oggetto selezionato.  
  
2.  Nel riquadro di destra, fare clic su di **dello Schema di Mapping** scheda.  
  
    Verrà visualizzato un elenco di tutti gli schemi di DB2, seguito da un valore di destinazione. La destinazione è identificata in una notazione di due parti (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in cui gli oggetti e dati sarà possibile eseguire la migrazione.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare e quindi fare clic su **modifica**.  
  
    Nel **scegliere lo Schema di destinazione** la finestra di dialogo, è esplorare per database di destinazione disponibili e dello schema o un tipo di database e lo schema nella casella di testo in una notazione di due parti (database.schema) e quindi fare clic su **OK**.  
  
4.  La destinazione viene modificato nel **dello Schema di Mapping** scheda.  
  
**Modalità di Mapping**  
  
-   Mapping a SQL Server  
  
È possibile mappare i database di origine a un database di destinazione. Per impostazione predefinita viene eseguito il mapping di database di origine alla destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] database a cui si è connessi con SSMA. Se il database di destinazione viene eseguito il mapping è inesistente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], quindi verrà visualizzato un messaggio **"il Database e/o schema non esiste nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadati. Viene creato durante la sincronizzazione. Si desidera continuare?"** Fare clic su Sì. Analogamente, è possibile eseguire il mapping di schema allo schema non esistente nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] database che verrà creato durante la sincronizzazione.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Ripristinando il Database predefinito e lo Schema  
Se si personalizza il mapping tra uno schema DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] dello schema, è possibile ripristinare il mapping i valori predefiniti.  
  
**Per ripristinare il database predefinito e lo schema**  
  
1.  Nella scheda mapping dello schema, selezionare una riga e fare clic su **Ripristina predefiniti** per ripristinare il database predefinito e lo schema.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera analizzare la conversione di oggetti di DB2 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oggetti, è possibile [Report di migrazione di dati (SSMA comune)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241).  
  
## <a name="see-also"></a>Vedere anche  
[La connessione a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
