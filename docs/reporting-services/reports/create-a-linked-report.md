---
title: Creare un Report collegato | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 232e24ef08c24d5c6a2c9799094fc492305eea46
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-linked-report"></a>Creare un report collegato
  Un report collegato è un elemento del server di report che fornisce un punto di accesso a un report esistente. Tale elemento è concettualmente simile al collegamento a un programma utilizzato per l'esecuzione di un programma o per l'apertura di un file.  
  
 Un report collegato viene derivato da un report esistente e mantiene la definizione del report originale. Un report collegato, inoltre, eredita sempre il layout del report e le proprietà dell'origine dati del report originale. Tutte le altre proprietà e impostazioni, ad esempio sicurezza, parametri, percorso, sottoscrizioni e pianificazioni, possono essere diverse da quelle del report originale.  
  
 È possibile creare un report collegato quando si desidera creare versioni aggiuntive di un report esistente. Un singolo report delle vendite regionali può essere utilizzato, ad esempio, per creare report specifici di una regione per tutti i territori di vendita.  
  
 I report collegati sono in genere basati su report con parametri, sebbene questa condizione non costituisca un requisito. È possibile creare report collegati ogni volta che si desidera distribuire un report esistente con impostazioni diverse.  
  
### <a name="to-create-a-linked-report"></a>Per creare un report collegato  
  
1.  In Gestione report, passare alla cartella che contiene il report per il quale si vuole creare un collegamento, quindi aprire il menu delle opzioni e fare clic su **Crea report collegato**.  
  
2.  Digitare un nome per il nuovo report collegato. Se lo si desidera, digitare una descrizione.  
  
3.  Per selezionare una cartella diversa per il report, fare clic su **Cambia percorso**. Selezionare la cartella che si vuole usare o digitare il nome della cartella nella casella **Percorso** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]Se non si seleziona una cartella diversa, il report collegato viene creato nella cartella corrente (in cui è archiviato il report su che è basato).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]Apre il report collegato.  
  
     L'icona di un report collegato è diversa da quella di altri elementi gestiti da un server di report. L'icona seguente indica un report collegato:  
  
     ![Icona di report collegato](../../reporting-services/report-server/media/hlp-16linked.gif "Icona di report collegato")  
  
## <a name="see-also"></a>Vedere anche  
 [Apertura e chiusura di un Report &#40; Gestione report &#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Pagina Nuovo Report collegato &#40; Gestione report &#41;](http://msdn.microsoft.com/library/fefb46e8-6901-4d50-a3f8-7c49ad72e7b1)   
 [Scegliere l'elemento percorso pagina &#40; Gestione report &#41;](http://msdn.microsoft.com/library/4a53a1a8-d1e1-47ef-b1fc-63352ece7d3c)   
 [Pagina delle proprietà generale, report &#40; Gestione report &#41;](http://msdn.microsoft.com/library/66c99d28-ab41-45f0-bf02-ed560293595d)   
 [Reporting Services concetti &#40; SSRS &#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Gestione report &#40; Modalità nativa SSRS &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  