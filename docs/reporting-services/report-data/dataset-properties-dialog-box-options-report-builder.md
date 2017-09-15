---
title: "Finestra di dialogo Proprietà set di dati, opzioni (Generatore Report) | Documenti Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10020"
- sql13.rtp.rptdesigner.datasetproperties.options.f1
- "10130"
ms.assetid: 43e50133-45ef-47a2-b575-34dfcc28ec98
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8eea917788cfd0811750a1ffb59888fa7e2a156a
ms.contentlocale: it-it
ms.lasthandoff: 08/09/2017

---
# <a name="dataset-properties-dialog-box-options-report-builder"></a>Finestra di dialogo Proprietà set di dati, Opzioni (Generatore report)
  Selezionare **Opzioni** nella finestra di dialogo **Proprietà set di dati** per modificare le opzioni relative ai dati, ad esempio le regole di confronto e la gestione dei subtotali come dati dettaglio, per la query. Per altre informazioni sulle regole di confronto, vedere [Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md) nella [documentazione online di SQL Server](http://go.microsoft.com/fwlink/?linkid=98335).  
  
 Le opzioni relative ai dati che sono parte di una definizione del set di dati condiviso nel server di report sono valide per tutti i report in cui viene utilizzato il set di dati condiviso. È possibile ignorare le opzioni per il set di dati condiviso una volta aggiunto a un report. Queste modifiche vengono applicate solo al report nel quale sono definite.  
  
 Le opzioni relative ai dati per un set di dati incorporato sono valide solo per il report nel quale sono definite.  
  
 Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 **Confronto**  
 Consente di selezionare le impostazioni locali che determinano la sequenza di regole di confronto da utilizzare per l'ordinamento dei dati. Il valore**Default** indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se non è possibile recuperare il valore, il valore predefinito viene ottenuto in base alle impostazioni locali del computer.  
  
 **Distinzione maiuscole/minuscole**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione tra maiuscole e minuscole. Questa opzione indica se per i dati viene applicata la distinzione tra maiuscole e minuscole. È possibile impostare l'opzione **Distinzione maiuscole/minuscole** su **True**, **False**o **Auto**. Il valore predefinito **Auto**indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione tra maiuscole e minuscole, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione caratteri accentati/non accentati**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione tra caratteri accentati e non accentati. L'opzione**Distinzione caratteri accentati/non accentati** indica se per i dati viene applicata la distinzione tra caratteri accentati e non accentati e può essere impostata su **True**, **False**o **Auto**. Il valore predefinito **Auto**indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione tra caratteri accentati e non accentati, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione Kana**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione dei caratteri Kana. Questa opzione indica se per i dati viene applicata la distinzione dei caratteri Kana e può essere impostata su **True**, **False**o **Auto**. Il valore predefinito **Auto**indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione dei caratteri Kana, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Distinzione larghezza**  
 Consente di selezionare un valore per indicare la modalità di applicazione della distinzione della larghezza. Questa opzione indica se per i dati viene applicata la distinzione della larghezza e può essere impostata su **True**, **False**o **Auto**. Il valore predefinito **Auto**indica che il server di report eseguirà un tentativo di recupero del valore dal provider di dati quando si esegue il report. Se il provider di dati non supporta il tipo di distinzione della larghezza, il report viene eseguito come se il valore fosse **False**. Se si conosce il valore e si è certi che sia supportato, scegliere **True**.  
  
 **Interpretare i subtotali come righe di dettaglio**  
 Selezionare un valore per indicare se si desidera che le righe di subtotali vengano interpretate come righe di dettaglio anziché come righe di aggregazione. Il valore predefinito, **Auto**, indica che le righe di subtotali devono essere considerate come righe di dettaglio se il report non usa la funzione **Aggregate**() per accedere ai campi nel set di dati. Se si vuole che le righe di subtotali vengano interpretate come righe di aggregazione, scegliere **False**. Se si vuole che le righe di subtotali vengano interpretate come righe di dettaglio e si è certi che non usino la funzione **Aggregate**(), scegliere **True**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Funzione di aggregazione &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)   
 [Filtro, gruppo e ordinamento dei dati &#40; Generatore report e SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Report di set di dati incorporati e condivisi &#40; Generatore report e SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà set di dati, Query &#40; Generatore report &#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)  
  
  