---
title: Trasformazione Conversione dati | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 314175a9f3a90c54a90b149cce91be885d5ef597
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="data-conversion-transformation"></a>Conversione dati - trasformazione
  La trasformazione Conversione dati converte i dati in una colonna di input in un tipo di dati diverso e quindi li copia in una nuova colonna di output. Un pacchetto può ad esempio estrarre dati da più origini e quindi utilizzare questa trasformazione per convertire le colonne nel tipo di dati richiesto dall'archivio dati di destinazione. È possibile applicare più conversioni a una singola colonna di input.  
  
 Tramite questa trasformazione un pacchetto può eseguire i tipi di conversioni dei dati seguenti:  
  
-   Modifica del tipo di dati. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
    > [!NOTE]  
    >  Se i dati da convertire hanno tipo di dati date o datetime, per la data nella colonna di output verrà utilizzato il formato ISO anche se le impostazioni locali specificano un formato diverso.  
  
-   Impostazione della lunghezza di colonna dei dati stringa, nonché della scala e della precisione dei dati numerici. Per altre informazioni, vedere [Precisione, scala e lunghezza &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
-   Impostazione di una tabella codici. Per altre informazioni, vedere [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
    > [!NOTE]  
    >  È possibile copiare dati tra colonne con un tipo di dati string solo se le due colonne utilizzano la stessa tabella codici.  
  
 Se la lunghezza di una colonna di output con dati di tipo string è minore di quella della colonna di input corrispondente, i dati di output verranno troncati. Per altre informazioni, vedere [Gestione degli errori nei dati](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Questa trasformazione include un input, un output e un output degli errori.  
  
## <a name="related-tasks"></a>Related Tasks  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice. Per informazioni sull'uso della trasformazione Conversione dati in Progettazione SSIS, vedere [Convertire i dati in un tipo di dati diverso tramite la trasformazione Conversione dati](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md). Per informazioni sull'impostazione delle proprietà di questa trasformazione a livello di programmazione, vedere [Proprietà comuni](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) e [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog sul [confronto delle prestazioni tra le tecniche di conversione dei tipi di dati in SSIS 2008](http://go.microsoft.com/fwlink/?LinkId=220823)su blogs.msdn.com.  
  
## <a name="data-conversion-transformation-editor"></a>Editor trasformazione Conversione dati
  Usare la finestra di dialogo **Editor trasformazione Conversione dati** per selezionare le colonne da convertire e i tipi di dati in cui convertire la colonna e impostare gli attributi di conversione.  
  
> [!NOTE]  
>  La proprietà **FastParse** delle colonne di output della trasformazione Conversione dati non è disponibile nell' **Editor trasformazione Conversione dati**ma può essere impostata tramite l' **Editor avanzato**. Per altre informazioni su questa proprietà, vedere la sezione relativa alla trasformazione Conversione dati in [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di selezionare le colonne da convertire utilizzando le caselle di controllo. Le selezioni effettuate determinano l'aggiunta delle colonne di input nella tabella sottostante.  
  
 **Colonna di input**  
 Consente di selezionare le colonne da convertire nell'elenco delle colonne di input disponibili. Le selezioni effettuate vengono riflesse nelle selezioni delle caselle di controllo descritte in precedenza.  
  
 **Alias di output**  
 Consente di digitare un alias per ogni nuova colonna. L'impostazione predefinita è **Copia di** seguita dal nome della colonna di input.  È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Tipo di dati**  
 Consente di selezionare un tipo di dati disponibile nell'elenco. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Length**  
 Consente di selezionare la lunghezza della colonna per dati di tipo stringa.  
  
 **Precisione**  
 Consente di impostare la precisione per dati numerici.  
  
 **Scala**  
 Consente di impostare la scala per dati numerici.  
  
 **Tabella codici**  
 Consente di selezionare la tabella codici appropriata per le colonne di tipo DT_STR.  
  
 **Configura output errori**  
 Consente di indicare come gestire gli errori tramite la finestra di dialogo [Configura output errori](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi veloce](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
