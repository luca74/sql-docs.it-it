---
title: ICommandWithParameters | Documenti Microsoft
description: Interfaccia ICommandWithParameters
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9d810ea13512537572bf39fbda938b6b59d64db7
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2018
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Miglioramenti all'inizio del motore di database con [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] consentire ICommandWithParameters:: GetParameterInfo ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati differiscano dai valori restituiti da CommandWithParameters::GetParameterInfo nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Metadata Discovery](../../oledb/features/metadata-discovery.md).  
  
 A partire dalla [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], durante la chiamata di ICommandWithParameters:: SetParameterInfo, il valore passato al *pwszName* parametro deve essere un identificatore valido. Per altre informazioni, vedere [Identificatori del database](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
