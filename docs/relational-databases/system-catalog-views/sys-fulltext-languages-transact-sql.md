---
title: sys.fulltext_languages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb66c10f797c7951f54125c7b5b99cfc25f983ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysfulltextlanguages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  In questa vista del catalogo è contenuta una riga per ogni lingua i cui word breaker sono registrati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In ogni riga è visualizzato l'identificatore LCID e il nome della lingua. Quando si registrano i word breaker per una lingua, le altre risorse linguistiche, ovvero stemmer, parole non significative e file del thesaurus, risultano disponibili per le operazioni di indicizzazione/query full-text. Il valore di **nome** o **lcid** può essere specificato nella query full-text e dell'indice full-text [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni.  
   
|Colonna|Tipo di dati|Description|  
|------------|---------------|-----------------|  
|**lcid**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Identificatore di impostazioni locali di Windows (LCID) per la lingua.|  
|**name**|**sysname**|È il valore dell'alias in [Sys. syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) corrispondente al valore di **lcid** o rappresentazione di stringa dell'identificatore LCID numerico.|  
  
## <a name="values-returned-for-default-languages"></a>Valori restituiti per le lingue predefinite  
 Nella tabella seguente sono mostrati i valori per le lingue i cui word breaker sono registrati per impostazione predefinita.  
  
|Lingua|LCID|  
|--------------|----------|  
|Arabo|1025|  
|Bengali (India)|1093|  
|Inglese (Regno Unito)|2057|  
|Bulgaro|1026|  
|Catalano|1027|  
|Cinese (RAS di Hong Kong, Repubblica popolare cinese)|3076|  
|Cinese (Macao - R.A.S.)|5124|  
|Cinese (Singapore)|4100|  
|Croato|1050|  
|Ceco|1029|  
|Danese|1030|  
|Olandese|1043|  
|Inglese|1033|  
|Francese|1036|  
|Tedesco|1031|  
|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Greco|1032|  
|Gujarati|1095|  
|Hebrew|1037|  
|Hindi|1081|  
|Islandese|1039|  
|Indonesiano|1057|  
|Italiano|1040|  
|Giapponese|1041|  
|Kannada|1099|  
|Coreano|1042|  
|Lettone|1062|  
|Lituano|1063|  
|Malese (Malesia)|1086|  
|Malayalam|1100|  
|Marathi|1102|  
|Lingua neutra|0|  
|Norvegese (Bokmål)|1044|  
|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Polacco|1045|  
|Portoghese (Brasile)|1046|  
|Portoghese (Portogallo)|2070|  
|Punjabi|1094|  
|Romeno|1048|  
|Russo|1049|  
|Serbo (alfabeto cirillico)|3098|  
|Serbo (alfabeto latino)|2074|  
|Cinese semplificato|2052|  
|Slovacco|1051|  
|Sloveno|1060|  
|Spagnolo|3082|  
|Svedese|1053|  
|Tamil|1097|  
|Telugu|1098|  
|Thai|1054|  
|Cinese tradizionale|1028|  
|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Turco|1055|  
|Ucraino|1058|  
|Urdu|1056|  
|Vietnamita|1066|  
  
## <a name="remarks"></a>Osservazioni  
 Per aggiornare l'elenco di lingue registrate con la ricerca full-text, utilizzare [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'.  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [Configurazione e gestione di word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurare e gestire i file del Thesaurus per la ricerca Full-Text](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurare e gestire parole non significative ed elenchi per la ricerca Full-Text](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Aggiornamento della ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
