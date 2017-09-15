---
title: "Proprietà database (pagina File) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 96e789d47140459475bdd3b6f36500d0d24492ce
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="database-properties-files-page"></a>Proprietà database (pagina File)
  Utilizzare questa pagina per creare un nuovo database oppure per visualizzare o modificare le proprietà del database selezionato. Questo argomento si applica a **Proprietà database (pagina File)** per i database esistenti e a **Nuovo database (pagina Generale)**.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Nome database**  
 È possibile aggiungere o visualizzare il nome del database.  
  
 **Proprietario**  
 È possibile specificare il proprietario del database selezionandolo nell'elenco.  
  
 **Usa indicizzazione full-text**  
 Questa casella di controllo è selezionata e disabilitata perché l'indicizzazione full-text è sempre abilitata in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Ricerca full-text](../../relational-databases/search/full-text-search.md).  
  
 **File di database**  
 È possibile aggiungere, visualizzare, modificare o rimuovere file del database associato. I file di database dispongono delle proprietà seguenti:  
  
 **Nome logico**  
 È possibile immettere o modificare il nome del file.  
  
 **Tipo di file**  
 È possibile selezionare il tipo di file nell'elenco. Il tipo di file può essere **Dati**, **Log**o **Dati FILESTREAM**. Non è possibile modificare il tipo di file di un file esistente.  
  
 Selezionare **Dati FILESTREAM** se si aggiungono file (contenitori) a un filegroup con ottimizzazione per la memoria.  
  
 Per aggiungere file (contenitori) a un filegroup di dati FILESTREAM, FILESTREAM deve essere abilitato. È possibile abilitare FILESTREAM usando la finestra di dialogo [Proprietà server (pagina Avanzate)](../../database-engine/configure-windows/server-properties-advanced-page.md) .  
  
 **Filegroup**  
 È possibile selezionare il filegroup per il file nell'elenco. Per impostazione predefinita, il filegroup è PRIMARY. È possibile creare un nuovo filegroup selezionando **\<nuovo filegroup>** e immettendo informazioni sul filegroup nella finestra di dialogo **Nuovo filegroup**. Anche nella pagina **Filegroup** è possibile creare un nuovo filegroup. Non è possibile modificare il filegroup di un file esistente.  
  
 Quando si aggiungono file (contenitori) a un filegroup con ottimizzazione per la memoria, il campo **Filegroup** viene popolato con il nome del filegroup con ottimizzazione per la memoria del database.  
  
 **Dimensioni iniziali**  
 È possibile immettere o modificare le dimensioni iniziali in megabyte del file. Per impostazione predefinita, questo valore corrisponde a quello del database **model** .  
  
 Questo campo non è valido per i file FILESTREAM.  
  
 Per i file nei filegroup con ottimizzazione per la memoria, questo campo non può essere modificato.  
  
 **Aumento automatico**  
 È possibile selezionare o visualizzare le proprietà dell'aumento automatico per il file. Queste proprietà controllano l'espansione del file al raggiungimento delle dimensioni massime. Per modificare i valori di aumento automatico fare clic sul pulsante di modifica accanto alle proprietà di aumento automatico relative al file desiderato e modificare i valori nella finestra di dialogo **Cambia aumento automatico dimensioni** . Per impostazione predefinita, questi valori corrispondono a quelli del database **model** .  
  
 Questo campo non è valido per i file FILESTREAM.  
  
 Per i file nei filegroup con ottimizzazione per la memoria, questo campo deve essere **Senza limiti**.  
  
 **Percorso**  
 È possibile visualizzare il percorso del file selezionato. Per specificare il percorso di un nuovo file fare clic sul pulsante di modifica accanto al percorso del file e passare alla cartella di destinazione. Non è possibile modificare il percorso di un file esistente.  
  
 Per i file FILESTREAM, il percorso è una cartella. Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creerà i file sottostanti in questa cartella.  
  
 **Nome file**  
 È possibile visualizzare il nome del file.  
  
 Questo campo non è valido per i file FILESTREAM, inclusi i file nei filegroup con ottimizzazione per la memoria.  
  
 **Aggiungi**  
 È possibile aggiungere un nuovo file al database.  
  
 **Rimuovi**  
 È possibile eliminare il file selezionato dal database. È possibile eliminare solo file vuoti. Non è possibile eliminare i file di dati e di log primari.  
  
 Per altre informazioni sui file, vedere [Filegroup e file di database](../../relational-databases/databases/database-files-and-filegroups.md).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  