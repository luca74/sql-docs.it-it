---
title: Editor destinazione SAP BW (pagina Avanzate) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwdestination.advanced.f1
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4923bb1fb081c630b910ec5047d8aca5eafcd2fb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="sap-bw-destination-editor-advanced-page"></a>Editor destinazione SAP BW (pagina Avanzate)
  Usare la pagina **Avanzate** dell'**Editor destinazione SAP BW** per definire le impostazioni avanzate quali dimensioni del pacchetto e informazioni sul timeout.  
  
 Per altre informazioni sulla destinazione SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Destinazione SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la pagina Avanzate**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Avanzate** per aprire la pagina **Avanzate** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare la destinazione, può essere necessario consultare l'amministratore SAP.  
  
 **Dimensioni pacchetto**  
 Specificare il numero di righe di dati che verranno trasferite contemporaneamente. Il valore ottimale per questo parametro dipende dal sistema SAP Netweaver BW e dall'ulteriore elaborazione dei dati che potrebbe verificarsi. In genere, i valori compresi tra 2000 e 20000 offrono prestazioni ottimali.  
  
 **Attivazione catena di processi**  
 (Facoltativo) Specificare il nome di una catena di processi da attivare dopo il completamento del caricamento dei dati.  
  
 **Timeout attesa InfoPackage**  
 Specificare il numero massimo di secondi di attesa del completamento dell'InfoPackage da parte della destinazione.  
  
 **Attendi completamento trasferimento dati**  
 Specificare se la destinazione deve attendere il completamento del caricamento dei dati da parte del sistema SAP Netweaver BW.  
  
 **Non avviare InfoPackage - solo attesa**  
 Specificare che la destinazione non attiva un InfoPackage, ma attende semplicemente la notifica dell'avvio del caricamento dei dati da parte del sistema SAP Netweaver BW.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Editor destinazione SAP BW &#40;pagina Mapping&#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [Editor destinazione SAP BW &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
