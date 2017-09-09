---
title: Definire relazioni tra attributi | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a1b74894ea54989ca409c860f8cd95126941e118
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-relationships---define"></a>Attributo relazioni - definire
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], gli attributi rappresentano l'elemento costitutivo fondamentale di una dimensione. Una dimensione contiene un set di attributi organizzato in base alle relazioni tra attributi.  
  
 Per ogni tabella inclusa in una dimensione, vi è una relazione tra attributi che mette in relazione l'attributo chiave della tabella agli altri attributi di quella tabella. Si crea questa relazione quando si crea la dimensione.  
  
 Una relazione tra attributi fornisce i vantaggi seguenti:  
  
-   Riduce la quantità di memoria necessaria per l'elaborazione della dimensione. Ciò consente di rendere più rapida l’elaborazione di dimensioni, partizioni e query.  
  
-   Aumenta le prestazioni di esecuzione delle query in quanto l'accesso all'archiviazione è più veloce ed i piani di esecuzione sono ottimizzati.  
  
-   Determina la selezione di aggregati più efficaci da parte degli algoritmi di progettazione delle aggregazioni, purché siano presenti gerarchie definite dall'utente nei percorsi delle relazioni.  
  
    > [!NOTE]  
    >  Per altre informazioni sull'importanza e le implicazioni della definizione e della configurazione di relazioni tra attributi, vedere la sezione relativa all'ottimizzazione delle prestazioni delle query nella [Guida alle prestazioni di SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="attribute-relationship-considerations"></a>Considerazioni sulle relazioni tra attributi  
 Quando i dati sottostanti lo supportano, si devono definire anche relazioni univoche tra attributi. Per definire relazioni tra attributi univoche, usare la scheda **Relazioni tra attributi** di Progettazione dimensioni.  
  
 Qualsiasi attributo che ha una relazione in uscita deve avere una chiave univoca relativa all'attributo correlato. In altre parole, un membro in un attributo di origine deve identificare un solo membro in un attributo correlato. Si consideri, ad esempio, la relazione, Città -> Stato. In questa relazione, l'attributo di origine è Città e l'attributo correlato è Stato. In una relazione molti-a-uno l'attributo di origine è il lato "molti" e l’attributo correlato è il lato "uno". La chiave per l'attributo di origine sarebbe Città + Stato. Per altre informazioni, vedere [Creare, modificare o eliminare una relazione tra attributi](../../analysis-services/multidimensional-models/attribute-relationships-create-modify-or-delete-relationship.md).  
  
 Per altre informazioni sulle proprietà di una relazione tra attributi, vedere [Configurare le proprietà della relazione tra attributi](../../analysis-services/multidimensional-models/attribute-relationships-configure-attribute-properties.md).  
  
> [!NOTE]  
>  Definire erroneamente relazioni tra attributi può produrre risultati della query non validi.  
  
## <a name="see-also"></a>Vedere anche  
 [Relazione tra attributi](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  