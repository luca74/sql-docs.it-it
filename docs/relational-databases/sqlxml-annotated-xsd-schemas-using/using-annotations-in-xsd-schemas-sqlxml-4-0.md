---
title: Utilizzo delle annotazioni negli schemi XSD (SQLXML 4.0) | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c124bb466416e06768444ac7040c47a6267ae0d6
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>Utilizzo delle annotazioni negli schemi XSD (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 il linguaggio dello schema XSD supporta le annotazioni in una modalità analoga a quella delle annotazioni introdotte con il linguaggio dello schema XDR (XML-Data Reduced). In XSD sono state introdotte alcune annotazioni aggiuntive che non sono supportate in XDR.  
  
 Queste annotazioni possono essere utilizzate all'interno dello schema XSD per specificare un mapping tra dati XML e dati relazionali, incluso un mapping tra elementi e attributi nello schema XSD e tabelle (viste) e colonne nei database.  
  
 Se non si specificano le annotazioni, viene eseguito il mapping predefinito. Per impostazione predefinita, un elemento XSD con un tipo complesso viene mappato a un nome di tabella (vista) nel database specificato e un elemento o attributo con un tipo semplice viene mappato alla colonna che riporta lo stesso nome dell'elemento o dell'attributo.  
  
 Queste annotazioni possono essere utilizzate anche per specificare le relazioni gerarchiche in XML e in questo caso rappresentano le relazioni nel database in quanto uno schema XSD è semplicemente una vista XML dei dati relazionali.  
  
 In questa sezione vengono descritte le annotazioni che è possibile utilizzare con schemi XSD ed esempi pratici del loro utilizzo.  
  
> [!NOTE]  
>  In tutti gli esempi di questa sezione sono specificate query XPath semplici sullo schema XSD con annotazioni descritto in ogni esempio. Si presuppone che l'utente abbia già acquisito familiarità con il linguaggio XPath.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Annotazioni XSD &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 Vengono elencate le annotazioni che è possibile utilizzare con gli schemi XSD, le relative descrizioni e le annotazioni equivalenti per XDR.  
  
 [Mapping predefinito di attributi ed elementi XSD a tabelle e colonne &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 Viene illustrato il mapping predefinito e vengono forniti esempi di attività relative al mapping predefinito.  
  
 [Mapping esplicito di attributi ed elementi XSD a tabelle e colonne &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 Viene illustrato il mapping esplicito con il **SQL: relation** e **SQL: field** annotazioni e vengono forniti esempi.  
  
 [Specifica di relazioni tramite SQL: Relationship &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **SQL: Relationship** annotazione.  
  
 [Specifica l'attributo SQL: inverse in SQL: Relationship &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 Viene descritto il **inverse** annotazione.  
  
 [Creazione di elementi costanti tramite sql: costante è &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **sql: costante è** annotazione.  
  
 [Esclusione di elementi dello Schema dal documento XML risultante tramite sql: il mapping &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 Descrive e fornisce esempi del **sql: il mapping** annotazione.  
  
 [Filtrare valori tramite SQL: limit-field e SQL: limit-value &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **SQL: limit-campo** e **SQL: limit-valore** annotazioni.  
  
 [Identificazione di colonne chiave mediante SQL: Key-campi &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **SQL: Key-campi** annotazione.  
  
 [Specifica destinazione Namespace mediante l'attributo targetNamespace &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **targetNamespace** attributo.  
  
 [Creazione di prefix valido ID, IDREF e gli attributi di tipo IDREFS usando &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **prefix** annotazione.  
  
 [Coercizioni dei tipi di dati e l'annotazione SQL: DataType &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **SQL: DataType** annotazione.  
  
 [Mapping dei tipi di dati XSD a tipi di dati XPath &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 Viene fornita una tabella in cui i tipi di dati XSD, XDR e XPath vengono messi a confronto e le relative conversioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono elencate.  
  
 [Creazione di sezioni CDATA mediante SQL: use-cdata &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **SQL: Use-dati** annotazione.  
  
 [Richiesta di riferimenti URL a dati BLOB utilizzando sql: codificare &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **sql: codificare** annotazione.  
  
 [Il recupero dei dati non utilizzati tramite SQL: overflow-campo &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 Descrive e fornisce esempi del **SQL: overflow-campo** annotazione.  
  
 [Nascondere gli elementi e gli attributi usando sql:hide](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 Descrive e fornisce esempi del **SQL: hide** annotazione.  
  
 [Uso delle annotazioni sql:identity e sql:guid](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 Descrive e fornisce esempi del **: Identity** e **SQL: GUID** annotazioni.  
  
 [Specifica del livello di nidificazione nelle relazioni ricorsive con sql:max-depth](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 Descrive e fornisce esempi del **SQL: max-depth** annotazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza di Schema con annotazioni &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
