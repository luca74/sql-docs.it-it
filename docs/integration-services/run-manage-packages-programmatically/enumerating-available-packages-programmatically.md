---
title: Enumerazione dei pacchetti disponibili a livello di programmazione | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programmatically enumerate packages [SSIS]
- existence testing [Integration Services]
- enumerating packages [Integration Services]
ms.assetid: 254ec7ee-d3ff-4361-8995-46e9b9c4dc95
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2498be2192787418c87d5fd8f7983c4d2fa216e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="enumerating-available-packages-programmatically"></a>Enumerazione dei pacchetti disponibili a livello di codice
  <a name="top"></a> Quando si usano i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione, può essere necessario determinare se esiste un singolo pacchetto o cartella o enumerare i pacchetti salvati disponibili per il caricamento e l'esecuzione. La classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> dello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> fornisce un'ampia varietà di metodi e classi per soddisfare questi requisiti.    
    
##  <a name="exists"></a> Verifica dell'esistenza di un pacchetto o di una cartella    
 Per determinare a livello di codice se un pacchetto salvato esiste, chiamare uno dei metodi seguenti prima di tentare di caricarlo ed eseguirlo:    
    
|Percorso di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Per determinare a livello di codice se una cartella esiste prima di tentare di elencare i pacchetti archiviati al suo interno, chiamare uno dei metodi seguenti:    
    
|Percorso di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Torna all'inizio](#top)    
    
##  <a name="listing"></a> Enumerazione dei pacchetti disponibili    
 Per ottenere a livello di codice un elenco dei pacchetti salvati, chiamare uno dei metodi seguenti:    
    
|Percorso di archiviazione|Metodo da chiamare|    
|----------------------|--------------------|    
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerPackageInfos%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageInfos%2A>|    
    
 Gli esempi seguenti sono applicazioni console che dimostrano l'utilizzo di questi metodi.    
    
###  <a name="listing_store"></a> Esempio (archivio pacchetti SSIS)    
 Utilizzare il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerPackageInfos%2A> per elencare i pacchetti archiviati nell'archivio pacchetti SSIS. I percorsi di archiviazione predefiniti gestiti dall'archivio pacchetti SSIS sono File system e MSDB. In questi percorsi è possibile creare altre cartelle logiche.    
    
```vb    
Imports Microsoft.SqlServer.Dts.Runtime    
    
Module Module1    
    
  Sub Main()    
    
    Dim sqlFolder As String    
    Dim sqlServer As String    
    
    Dim ssisApplication As Application    
    Dim sqlPackages As PackageInfos    
    Dim sqlPackage As PackageInfo    
    
    sqlServer = "."    
    
    ssisApplication = New Application()    
    
    ' Get packages stored in MSDB.    
    sqlFolder = "MSDB"    
    sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer)    
    If sqlPackages.Count > 0 Then    
      Console.WriteLine("Packages stored in MSDB:")    
      For Each sqlPackage In sqlPackages    
        Console.WriteLine(sqlPackage.Name)    
      Next    
      Console.WriteLine()    
    End If    
    
    ' Get packages stored in the File System.    
    sqlFolder = "File System"    
    sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer)    
    If sqlPackages.Count > 0 Then    
      Console.WriteLine("Packages stored in the File System:")    
      For Each sqlPackage In sqlPackages    
        Console.WriteLine(sqlPackage.Name)    
      Next    
    End If    
    
    Console.Read()    
    
  End Sub    
    
End Module    
```    
    
```csharp    
using System;    
using Microsoft.SqlServer.Dts.Runtime;    
    
namespace EnumeratePackagesSSIS_CS    
{    
  class Program    
  {    
    static void Main(string[] args)    
    {    
    
      string sqlFolder;    
      string sqlServer;    
    
      Application ssisApplication;    
      PackageInfos sqlPackages;    
    
      sqlServer = ".";    
    
      ssisApplication = new Application();    
    
      // Get packages stored in MSDB.    
      sqlFolder = "MSDB";    
      sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer);    
      if (sqlPackages.Count > 0)    
      {    
        Console.WriteLine("Packages stored in MSDB:");    
        foreach (PackageInfo sqlPackage in sqlPackages)    
        {    
          Console.WriteLine(sqlPackage.Name);    
        }    
        Console.WriteLine();    
      }    
    
      // Get packages stored in the File System.    
      sqlFolder = "File System";    
      sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer);    
      if (sqlPackages.Count > 0)    
      {    
        Console.WriteLine("Packages stored in the File System:");    
        foreach (PackageInfo sqlPackage in sqlPackages)    
        {    
          Console.WriteLine(sqlPackage.Name);    
        }    
      }    
    
      Console.Read();    
    
    }    
    
  }    
    
}    
```    
    
 [Torna all'inizio](#top)    
    
###  <a name="listing_sql"></a> Esempio (SQL Server)    
 Utilizzare il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageInfos%2A> per elencare i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] archiviati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
```vb    
Imports Microsoft.SqlServer.Dts.Runtime    
    
Module Module1    
    
  Sub Main()    
    
    Dim sqlFolder As String    
    Dim sqlServer As String    
    Dim sqlUser As String    
    Dim sqlPassword As String    
    
    Dim ssisApplication As Application    
    Dim sqlPackages As PackageInfos    
    Dim sqlPackage As PackageInfo    
    
    sqlFolder = String.Empty    
    sqlServer = "(local)"    
    sqlUser = String.Empty    
    sqlPassword = String.Empty    
    
    ssisApplication = New Application()    
    
    sqlPackages = ssisApplication.GetPackageInfos(sqlFolder, sqlServer, sqlUser, sqlPassword)    
    
    For Each sqlPackage In sqlPackages    
      Console.WriteLine(sqlPackage.Name)    
    Next    
    
    Console.Read()    
    
  End Sub    
    
End Module    
```    
    
```csharp    
using System;    
using Microsoft.SqlServer.Dts.Runtime;    
    
namespace EnumeratePackagesSql_CS    
{    
  class Program    
  {    
    static void Main(string[] args)    
    {    
    
      string sqlFolder;    
      string sqlServer;    
      string sqlUser;    
      string sqlPassword;    
    
      Application ssisApplication;    
      PackageInfos sqlPackages;    
    
      sqlFolder = String.Empty;    
      sqlServer = "(local)";    
      sqlUser = String.Empty;    
      sqlPassword = String.Empty;    
    
      ssisApplication = new Application();    
    
      sqlPackages = ssisApplication.GetPackageInfos(sqlFolder, sqlServer, sqlUser, sqlPassword);    
    
      foreach (PackageInfo sqlPackage in sqlPackages)    
      {    
        Console.WriteLine(sqlPackage.Name);    
      }    
    
      Console.Read();    
    
    }    
  }    
}    
```    
    
 [Torna all'inizio](#top)    
   
## <a name="see-also"></a>Vedere anche    
 [Gestione dei pacchetti &#40;servizio SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)    
    
  
