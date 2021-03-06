---
title: sysschemaarticles (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa29325540bbf30c69a46990a9fa473ca6cff84b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tiene traccia degli articoli relativi solo allo schema per pubblicazioni transazionali e snapshot. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|ID dell'articolo.|  
|**creation_script**|**nvarchar(255)**|Percorso e nome di uno script di schema dell'articolo utilizzato per la creazione della tabella di destinazione.|  
|**Descrizione**|**nvarchar(255)**|Voce descrittiva per l'articolo.|  
|**dest_object**|**sysname**|Nome dell'oggetto del database di sottoscrizione se l'articolo è relativo solo allo schema, quali articoli di stored procedure, viste e funzioni definite dall'utente.|  
|**name**|**sysname**|Nome dell'articolo relativo solo allo schema in una pubblicazione.|  
|**ObjID**|**int**|Identificatore dell'oggetto di base dell'articolo. Può corrispondere all'identificatore di oggetto di una procedura, vista, vista indicizzata o funzione definita dall'utente.|  
|**pubid**|**int**|ID della pubblicazione.|  
|**pre_creation_cmd**|**tinyint**|Specifica l'azione eseguita dal sistema se nel Sottoscrittore viene rilevato un oggetto esistente avente lo stesso nome durante l'applicazione dello snapshot per l'articolo:<br /><br /> **0** = nothing.<br /><br /> **1** = eliminazione della tabella di destinazione.<br /><br /> **2** = tabella di destinazione di rilascio.<br /><br /> **3** = tabella di destinazione di troncamento.|  
|**status**|**int**|Mappa di bit utilizzata per indicare lo stato dell'articolo.|  
|**tipo**|**tinyint**|Tipo di articolo relativo solo allo schema:<br /><br /> **32** = Stored procedure.<br /><br /> **64** = vista o vista indicizzata. <br /><br /> **96** = funzione di aggregazione.<br /><br /> **128** = funzione.|  
|**schema_option**|**Binary (8)**|Maschera di bit dell'opzione di creazione dello schema per l'articolo specificato. Imposta la creazione automatica della stored procedure nel database di destinazione per ogni sintassi CALL/MCALL/XCALL e può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno dei valori seguenti:<br /><br /> **0x00** = disattiva la creazione di script tramite l'agente Snapshot e utilizza *creation_script*.<br /><br /> **0x01** = genera la creazione di oggetti (CREATE TABLE, CREATE PROCEDURE e così via). Corrisponde al valore predefinito per gli articoli di stored procedure.<br /><br /> **0x02** = genera stored procedure personalizzate per l'articolo, se definito.<br /><br /> **0x10** = genera un indice cluster corrispondente.<br /><br /> **0x20** = converte i tipi di dati definito dall'utente per i tipi di dati di base.<br /><br /> **0x40**= genera uno o più indici non cluster corrispondenti.<br /><br /> **0x80**= include l'integrità referenziale dichiarata nelle chiavi primarie.<br /><br /> **0x73** = genera l'istruzione CREATE TABLE, crea indici cluster e non cluster, converte i tipi di dati definito dall'utente in tipi di dati di base e genera gli script di stored procedure personalizzata da applicare nel Sottoscrittore. Corrisponde al valore predefinito per tutti gli articoli, tranne gli articoli di stored procedure.<br /><br /> **0x100**= i trigger utente vengono replicati in un articolo di tabella, se definito.<br /><br /> **0x200**= replica i vincoli di chiave esterni. Se la tabella con riferimenti non fa parte di una pubblicazione, i vincoli FOREIGN KEY di una tabella pubblicata non vengono replicati.<br /><br /> **0x400**= replica i vincoli check.<br /><br /> **0x800**= i valori predefiniti di replica.<br /><br /> **0x1000**= replica le regole di confronto a livello di colonna.<br /><br /> **0x2000**= replica le proprietà estese associate oggetto di origine dell'articolo pubblicato.<br /><br /> **0x4000**= replica le chiavi univoche se definite in un articolo di tabella.<br /><br /> **0x8000**= chiave primaria di replica e le chiavi univoche di un articolo di tabella come vincoli tramite istruzioni ALTER TABLE.|  
|**dest_owner**|**sysname**|Proprietario della tabella nel database di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
