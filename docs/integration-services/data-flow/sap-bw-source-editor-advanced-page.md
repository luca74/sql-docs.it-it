---
title: Editor origine SAP BW (pagina avanzate) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ac7757987c169f803f3b0adda7f27c94f090d7db
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-source-editor-advanced-page"></a>Editor origine SAP BW (pagina Avanzate)
  Usare la pagina **Avanzate** dell' **Editor origine SAP BW** per specificare la regola per la conversione di stringhe e il periodo di timeout, nonché per reimpostare lo stato di un ID richiesta specifico.  
  
 Per sapere di più sul componente di origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 **Per aprire la pagina Gestione connessione**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Avanzate** per aprire la pagina **Avanzate** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare l'origine, può essere necessario consultare l'amministratore SAP.  
  
 **Conversione stringhe**  
 Specificare la regola da applicare per la conversione di stringhe.  
  
|Opzione|Description|  
|------------|-----------------|  
|**Conversione automatica stringhe**|Convertire tutte le stringhe in **nvarchar** quando il sistema SAP Netweaver BW è un sistema Unicode. In caso contrario, convertire tutte le stringhe in **varchar**.|  
|**Converti stringhe in varchar**|Convertire tutte le stringhe in **varchar**.|  
|**Converti stringhe in nvarchar**|Convertire tutte le stringhe in **nvarchar**.|  
  
 **Timeout (secondi)**  
 Specificare il numero massimo di secondi di attesa da parte dell'origine.  
  
> [!NOTE]  
>  Questa opzione è valida solo se è stato selezionato **W - Attesa notifica** come valore di **Modalità di esecuzione** nella pagina **Gestione connessione** dell'editor. Per altre informazioni, vedere [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md).  
  
 **ID richiesta**  
 Specificare l'ID richiesta di cui reimpostare lo stato su "G - Green" quando si fa clic su **Reimposta**.  
  
 **Reimposta**  
 Consente di reimpostare lo stato dell'ID richiesta specificato su "G - Green", dopo la richiesta di conferma. Ciò risulta utile quando si verifica un problema e il sistema SAP Netweaver BW contrassegna la richiesta con uno stato giallo o rosso.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Editor origine SAP BW &#40; Pagina colonne &#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Editor origine SAP BW &#40; Pagina Output degli errori &#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Guida (F1) di Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  