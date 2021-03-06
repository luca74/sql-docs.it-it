---
title: Impostazioni (Mapping dei tipi) del progetto (SybaseToSQL) | Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 411cb12d17399e43ebdc454f5f55a5c5595972a2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2018
---
# <a name="project-settings-type-mapping-sybasetosql"></a>Impostazioni (Mapping dei tipi) del progetto (SybaseToSQL)
La pagina Mapping dei tipi del **impostazioni progetto** la finestra di dialogo contiene le impostazioni che consentono di personalizzare la modalità di conversione di tipi di dati Sybase Adaptive Server Enterprise (ASE) in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipi di dati.  
  
La pagina Mapping dei tipi è disponibile nel **impostazioni progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Per specificare le impostazioni di mapping del tipo per tutti i progetti futuri di SSMA, il **strumenti** dal menu **impostazioni di progetto predefinite**, selezionare il tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificati da **versione di destinazione della migrazione** elenco a discesa e quindi selezionare **Mapping dei tipi** nella parte inferiore del riquadro a sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu **impostazioni progetto**e quindi selezionare **del mapping dei tipi** nella parte inferiore del riquadro a sinistra.  
  
## <a name="options"></a>Opzioni  
**Tipo origine**  
Il tipo di dati ASE mappato.  
  
**Tipo di destinazione**  
La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] il tipo di dati per il tipo di dati di base specificato.  
  
Vedere la tabella nella sezione seguente per il valore predefinito SSMA per Sybase mapping del tipo.  
  
**Aggiungi**  
Fare clic per aggiungere un tipo di dati nell'elenco di mapping.  
  
**Modifica**  
Fare clic per modificare il tipo di dati selezionato nell'elenco di mapping.  
  
**Rimuovi**  
Fare clic per rimuovere il mapping dei tipi di dati selezionato dall'elenco di mapping.  
  
**Ripristina predefiniti**  
Fare clic per reimpostare l'elenco di mapping del tipo di SSMA predefinite.  
  
## <a name="default-type-mapping"></a>Mapping dei tipi predefiniti  
Nella tabella seguente contiene il mapping dei tipi predefiniti tra ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipi di dati.  
  
|Tipo di dati di base|Tipo di dati di SQL Server|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary[\*..8000]**|**binary[\*]**|  
|**binario [8001...\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**Char varying [\*... 8000]**|**varchar [\*]**|  
|**Char varying [8001...\*]**|**ntext**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**ntext**|  
|**character**|**char**|  
|**caratteri diversi**|**varchar**|  
|**variabile di tipo carattere [\*... 8000]**|**varchar [\*]**|  
|**variabile di tipo carattere [8001...\*]**|**ntext**|  
|**caratteri [\*... 8000]**|**char[\*]**|  
|**caratteri [8001...\*]**|**ntext**|  
|**data**|**data**|  
|**datetime**|**datetime2 [3]**|  
|**dec**|**decimal**|  
|**DEC [\*... \*]**|**decimal[\*]**|  
|**DEC [\*... \*][\*.. \*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimale [\*... \*]**|**decimal[\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**valore a precisione doppia**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float [16 Outlook\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**char nazionali**|**nchar**|  
|**char National [\*... 4000]**|**nchar[\*]**|  
|**char National variabile**|**nvarchar**|  
|**char National varying [\*... 4000]**|**nvarchar [\*]**|  
|**char National varying [4001...\*]**|**nvarchar(max)**|  
|**char National [4001...\*]**|**nvarchar(max)**|  
|**caratteri nazionali**|**nchar**|  
|**caratteri nazionali [\*... 4000]**|**nchar[\*]**|  
|**caratteri nazionali [4001...\*]**|**nvarchar(max)**|  
|**variabile di caratteri nazionali**|**nvarchar**|  
|**variabile di caratteri nazionali [\*... 4000]**|**nvarchar [\*]**|  
|**variabile di caratteri nazionali [4001...\*]**|**nvarchar(max)**|  
|**varchar nazionali**|**nvarchar**|  
|**varchar National [\*... 4000]**|**nvarchar [\*]**|  
|**varchar National [4001...\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar varying**|**nvarchar**|  
|**nchar varying [\*... 4000]**|**nvarchar [\*]**|  
|**nchar varying [4001...\*]**|**nvarchar(max)**|  
|**nchar [\*... 4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numerico [\*... \*]**|**numerico [\*]**|  
|**numerico [\*... \*][\*.. \*]**|**numerico [\*] [\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*... 4000]**|**nvarchar [\*]**|  
|**nvarchar [4001...\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**UNICHAR varying**|**nvarchar**|  
|**UNICHAR varying [\*... 4000]**|**nvarchar [\*]**|  
|**UNICHAR varying [4001...\*]**|**nvarchar(max)**|  
|**UNICHAR [\*... 4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*... 4000]**|**nvarchar [\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**bigint senza segno**|**numerico [20] [0]**|  
|**int senza segno**|**bigint**|  
|**smallint senza segno**|**int**|  
|**tinyint senza segno**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*... 8000]**|**varbinary[\*]**|  
|**varbinary [8001...\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [\*... 8000]**|**varchar [\*]**|  
|**varchar [8001...\*]**|**ntext**|  
  
