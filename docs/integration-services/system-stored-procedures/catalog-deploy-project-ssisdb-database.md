---
title: catalog.deploy_project (database SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55fafb278e55a6044cd92f4c1dede3b574bd4c0a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="catalogdeployproject-ssisdb-database"></a>catalog.deploy_project (database SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Viene distribuito un progetto in una cartella del catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o viene aggiornato un progetto esistente distribuito precedentemente.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [@project_name =] project_name   
      , [@project_stream =] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [@folder_name =] *folder_name*  
 Nome della cartella in cui è distribuito il progetto. *folder_name* è di tipo **nvarchar(128)**.  
  
 [@project_name =] *project_name*  
 Nome del progetto nuovo o aggiornato nella cartella. *project_name* è di tipo **nvarchar(128)**.  
  
 [@projectstream =] *projectstream*  
 Contenuto binario di un file di distribuzione progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (estensione ispac).  
  
 È possibile utilizzare un'istruzione SELECT con la funzione OPENROWSET e il provider BULK per set di righe per recuperare il contenuto binario del file. Per un esempio, vedere [Distribuire progetti e pacchetti di Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md). Per altre informazioni su OPENROWSET, vedere [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
 *projectstream* è di tipo **varbinary(MAX)**  
  
 [@operation_id =] *operation_id*  
 Viene restituito l'identificatore univoco dell'operazione di distribuzione. *operation_id* è di tipo **bigint**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni CREATE_OBJECTS sulla cartella per distribuire un nuovo progetto o autorizzazioni MODIFY sul progetto per aggiornare un progetto  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono determinare la generazione di un errore da parte della stored procedure:  
  
-   Parametro che fa riferimento a un oggetto inesistente, parametro che tenta di creare un oggetto già esistente o parametro non valido in alcuni altri modi  
  
-   Valore del parametro *@project_name* non corrispondente al nome del progetto nel file di distribuzione  
  
-   Utente senza autorizzazioni sufficienti.  
  
## <a name="remarks"></a>Remarks  
 Durante la distribuzione o aggiornamento di un progetto, il livello di protezione dei singoli pacchetti non viene controllato dalla stored procedure.  
  
  
