---
title: sp_OACreate (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5b36d46482582d877241d5ec621896d8aa4206fa
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un'istanza di un oggetto OLE.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>Argomenti  
 *ProgID*  
 ProgID dell'oggetto OLE da creare. Questa stringa di caratteri descrive la classe dell'oggetto OLE e ha il formato: **'***OLEComponent***.** *Oggetto***'**  
  
 *OLEComponent* è il nome del componente del server di automazione OLE, e *oggetto* è il nome dell'oggetto OLE. L'oggetto OLE specificato deve essere valido e deve supportare il **IDispatch** interfaccia.  
  
 Ad esempio, SQLDMO. SQL Server è il valore ProgID dell'oggetto SQL-DMO **SQLServer** oggetto. SQL-DMO è SQLDMO, un nome componente il **SQLServer** oggetto sia valido e (ad esempio SQL-DMO tutti gli oggetti) di **SQLServer** supporta **IDispatch**.  
  
 *CLSID*  
 CLSID dell'oggetto OLE da creare. Questa stringa di caratteri descrive la classe dell'oggetto OLE e ha il formato: **' {***nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn***}'**. L'oggetto OLE specificato deve essere valido e deve supportare il **IDispatch** interfaccia.  
  
 Ad esempio, {00026BA1-0000-0000-C000-000000000046} è il valore CLSID dell'oggetto SQL-DMO **SQLServer** oggetto.  
  
 *vengono restituite le* **OUTPUT**  
 È il token di oggetto restituito, e deve essere una variabile locale di tipo di dati **int**. Questo token, che identifica l'oggetto OLE creato, viene utilizzato nelle chiamate alle altre stored procedure di automazione OLE.  
  
 *contesto*  
 Specifica il contesto di esecuzione in cui viene eseguito il nuovo oggetto OLE. I possibili valori sono i seguenti:  
  
 **1** = solo un server OLE in-process (DLL).  
  
 **4** = locale (.exe) OLE solo server.  
  
 **5** = server OLE locale e in-process consentito  
  
 Se non specificato, il valore predefinito è **5**. Questo valore viene passato come il *dwClsContext* parametro della chiamata a **CoCreateInstance**.  
  
 Se è consentito un server OLE in-process (utilizzando un valore di contesto **1** o **5** oppure non specificare un valore di contesto), che disponga dell'accesso alla memoria e altre risorse di proprietà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un server OLE in-process può danneggiare la memoria o le risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], con conseguenti risultati imprevisti, ad esempio un errore di violazione di accesso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando si specifica un valore di contesto **4**, un server OLE locale non ha accesso a qualsiasi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] risorse e non può danneggiare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memoria o risorse.  
  
> [!NOTE]  
>  I parametri di questa stored procedure vengono specificati in base alla posizione, non in base al nome.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o un numero diverso da zero (esito negativo) corrispondente al valore intero del codice HRESULT restituito dall'oggetto di automazione OLE.  
  
 Per ulteriori informazioni sui codici restituiti HRESULT, vedere [OLE Automation codici restituiti e informazioni sull'errore](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Osservazioni  
 Se OLE automation procedures è abilitata, una chiamata a **sp_OACreate** verrà avviato l'ambiente di esecuzione condiviso di automazione OLE. Per ulteriori informazioni sull'abilitazione di automazione OLE, vedere [Ole Automation procedure opzione di configurazione Server](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md).  
  
 L'oggetto OLE creato viene distrutto automaticamente al termine del batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-progid"></a>A. Utilizzo di un valore ProgID  
 L'esempio seguente crea un SQL-DMO **SQLServer** oggetto utilizzando il ProgID.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>B. Utilizzo di un valore CLSID  
 L'esempio seguente crea un SQL-DMO **SQLServer** oggetto tramite relativo CLSID.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Automazione OLE Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Opzione di configurazione Server OLE Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [Script di automazione OLE di esempio](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
