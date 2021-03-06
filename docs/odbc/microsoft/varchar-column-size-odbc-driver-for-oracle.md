---
title: Dimensioni della colonna VARCHAR (Driver ODBC per Oracle) | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6002a906b2796cbc2f9f50519c11e846455b3ce9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Dimensioni della colonna VARCHAR (Driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, utilizzare il driver ODBC fornito da Oracle.  
  
 In Oracle8, le dimensioni massime di una colonna VARCHAR sono aumentato da 2000 a 4000 byte. Il software client di Oracle 7.3.x non è possibile associare un valore di parametro superiore a 2000 byte. Pertanto, se si crea una tabella con una colonna VARCHAR di dimensioni superiori a 2000 byte, non sarà possibile eseguire query su di esso con i dati che superano il limite di 2000-byte del software client, gli aggiornamenti, eliminazioni e inserimenti con parametri. Poiché sia il Driver ODBC per Oracle e il Provider OLE DB per Oracle è possibile utilizzare le query, gli aggiornamenti, eliminazioni e inserimenti con parametri, questi verranno segnalati gli errori di ORA 01026 in questo caso. Dati che si trova all'interno di limiti per il software client Oracle funzionerà. Per evitare questo limite di 2000 byte, è necessario aggiornare il software client a Oracle8 (8.0.4.1.1c o versione successiva).
