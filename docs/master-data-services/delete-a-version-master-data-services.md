---
title: Eliminare una versione (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fecbaf5df8943cc52d0745d86b606a23d2d508a5
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
---
# <a name="delete-a-version-master-data-services"></a>Eliminare una versione (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eliminare una versione quando si è certi che non sono più necessari i dati master a essa associati. Dopo avere eliminato una versione, non è possibile recuperare i dati master associati.  
  
> [!WARNING]  
>  Se un modello presenta una sola versione e la si elimina, il modello diventa inutilizzabile.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre delle autorizzazioni per visualizzare la vista mdm.viw_SYSTEM_SCHEMA_VERSION ed eseguire la stored procedure mds.udpVersionDelete nel database di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Per altre informazioni, vedere [Sicurezza di oggetti di database &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-delete-a-version"></a>Per eliminare una versione  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e connettersi all'istanza [!INCLUDE[ssDE](../includes/ssde-md.md)] per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Aprire la vista mdm.viw_SYSTEM_SCHEMA_VERSION.  
  
3.  Trovare la versione del modello che si vuole eliminare e copiare il valore nel campo **ID** .  
  
4.  Creare una nuova query.  
  
5.  Digitare il testo seguente, sostituendo *version_ID* con il valore copiato nel passaggio 2.  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  Consente di eseguire la query.  
  
    > [!NOTE]  
    >  Può essere necessario attendere alcuni minuti prima che l'applicazione Web rifletta la modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Versioni &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Copiare una versione &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
  
