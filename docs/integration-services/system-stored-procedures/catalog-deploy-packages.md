---
title: catalog.deploy_packages | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f44775c2852c1d89c0549f2beab7fd903d66c4d3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Distribuisce uno o più pacchetti in una cartella del catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o aggiorna un pacchetto esistente distribuito precedentemente.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @folder_name = ] *folder_name*  
 Nome della cartella. *folder_name* è di tipo **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Nome del progetto nella cartella. *project_name* è di tipo **nvarchar(128)**.  
  
 [ @packages_table = ] *packages_table*  
 Contenuto binario dei file del pacchetto (con estensione dtsx) di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. *packages_table* è di tipo **[catalog].[Package_Table_Type]**  
  
 [ @operation_id = ] *operation_id*  
 Viene restituito l'identificatore univoco dell'operazione di distribuzione. *operation_id* è di tipo **bigint**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni CREATE_OBJECTS sul progetto o autorizzazioni MODIFY sul pacchetto per aggiornare un pacchetto.  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono determinare la generazione di un errore da parte della stored procedure:  
  
-   Parametro che fa riferimento a un oggetto inesistente, parametro che tenta di creare un oggetto già esistente o parametro in altro modo non valido.  
  
-   Utente senza autorizzazioni sufficienti.  
  
  
