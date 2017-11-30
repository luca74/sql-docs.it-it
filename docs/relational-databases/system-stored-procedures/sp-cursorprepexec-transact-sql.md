---
title: sp_cursorprepexec (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs: TSQL
helpviewer_keywords: sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5264e1c645cf1716d01e352f2b248b3b80a038d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spcursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compila un piano per il batch o l'istruzione di cursore inviata, quindi crea e popola il cursore. sp_cursorprepexec combina le funzioni di sp_cursorprepare e sp_cursorexecute. Questa routine viene richiamata specificando ID = 5 in un pacchetto del flusso TDS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *handle preparato*  
 È un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generato preparato *gestire* identificatore. *handle preparato* è obbligatorio e restituisce **int**.  
  
 *cursor*  
 Identificatore del cursore generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *cursore* è un parametro obbligatorio che deve essere fornito su tutte le routine successive che agiscono su questo cursore, ad esempio sp_cursorfetch.  
  
 *params*  
 Identifica le istruzioni con parametri. Il *params* definizione delle variabili viene sostituita per i marcatori di parametro nell'istruzione. *params* è un parametro obbligatorio che richiede un **ntext**, **nchar**, o **nvarchar** valore di input.  
  
> [!NOTE]  
>  Utilizzare un **ntext** stringa come input quando *stmt* è con parametri e *scrollopt* valore PARAMETERIZED_STMT è impostata su ON.  
  
 *istruzione*  
 Definisce il set di risultati del cursore. Il *istruzione* parametro è obbligatorio e richiede un **ntext**, **nchar** o **nvarchar** valore di input.  
  
> [!NOTE]  
>  Le regole per la specifica del valore stmt sono le stesse di quelle per sp_cursoropen, con l'eccezione che il *stmt* deve essere di tipo di dati string **ntext**.  
  
 *Opzioni*  
 Parametro facoltativo tramite cui viene restituita una descrizione delle colonne dei set di risultati del cursore. *opzioni* richiede le seguenti condizioni **int** valore di input.  
  
|Valore|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Opzione di scorrimento. *scrollopt* è un parametro facoltativo che richiede uno dei seguenti **int** valori di input.  
  
|Valore|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 A causa della possibilità che l'opzione richiesta non è appropriato per il cursore definito da  *\<stmt >*, questo parametro funge sia da input e output. In casi di questo tipo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegna un tipo appropriato e modifica questo valore.  
  
 *ccopt*  
 Opzioni del controllo della concorrenza. *ccopt* è un parametro facoltativo che richiede uno dei seguenti **int** valori di input.  
  
|Valore|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (precedentemente noto come LOCKCC)|  
|0x0004|**OTTIMISTICA** (precedentemente noto come OPTCC)|  
|0x0008|OPTIMISTIC (precedentemente noto come OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Come con *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile assegnare un valore diverso da quello richiesto.  
  
 *conteggio delle righe*  
 Parametro facoltativo che indica il numero di righe del buffer di recupero da utilizzare con AUTO_FETCH. Il valore predefinito è 20 righe. *conteggio delle righe* si comporta in modo diverso quando assegnato come valore di input rispetto a un valore restituito.  
  
|Come valore di input|Come valore restituito|  
|--------------------|---------------------|  
|Quando in cui viene specificato AUTO_FETCH con i cursori FAST_FORWARD *rowcount* rappresenta il numero di righe da inserire nel buffer di recupero.|Rappresenta il numero di righe nel set di risultati. Quando il *scrollopt* viene specificato il valore AUTO_FETCH, *rowcount* restituisce il numero di righe recuperate nel buffer di recupero.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 Se *params* restituisce un valore NULL, quindi l'istruzione non è con parametri.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursoropen &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  