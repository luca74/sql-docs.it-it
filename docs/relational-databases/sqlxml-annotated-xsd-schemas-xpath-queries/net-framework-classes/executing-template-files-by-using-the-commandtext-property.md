---
title: "Esecuzione di file modello tramite la proprietà CommandText | Documenti Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- executing template files [SQLXML]
- CommandText property
ms.assetid: f1b1278d-252d-4a06-836e-4ef77f338ef9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef0cc4fe9655e7ac183226f01bfba0a7a3901971
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="executing-template-files-by-using-the-commandtext-property"></a>Esecuzione di file modello mediante la proprietà CommandText
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Questo esempio viene illustrato come specificare i file modello costituiti da query SQL o XPath mediante la CommandTextproperty. Anziché specificare query SQL o XPath come valore di CommandText, è possibile specificare un nome di file come valore. Nell'esempio seguente, la proprietà CommandType è specificata come SqlXmlCommandType.TemplateFile.  
  
 L'applicazione di esempio esegue questo modello:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Si tratta dell'applicazione C# di esempio. Per testare l'applicazione, salvare il modello (TemplateFile.xml), quindi eseguire l'applicazione.  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandType = SqlXmlCommandType.TemplateFile;  
         cmd.CommandText = "TemplateFile.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
                Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
  
         return 0;        
      }  
      public static int Main(String[] args)  
      {  
         testParams();     
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>Per testare l'applicazione  
  
1.  Assicurarsi che [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework sia installato nel computer.  
  
2.  Salvare il modello XML (TemplateFile.xml) fornito in questo esempio in una cartella.  
  
3.  Salvare il codice C# (DocSample.cs) fornito in questo esempio nella stessa cartella nella quale viene archiviato lo schema. Se si archiviano i file in un'altra cartella, sarà necessario modificare il codice e specificare il percorso di directory appropriato per lo schema di mapping.  
  
4.  Compilare il codice. Per compilare il codice al prompt dei comandi, utilizzare:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Viene creato un file eseguibile (DocSample.exe).  
  
5.  Al prompt dei comandi eseguire DocSample.exe.  
  
 Se si passa un parametro a un modello, il nome del parametro deve iniziare con simbolo di chiocciola (@); ad esempio, p.Name= "@ContactID", dove p è un oggetto SqlXmlParameter.  
  
 Si tratta del modello aggiornato che accetta solo un parametro.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:header>  
     <sql:param name='ContactID'>1</sql:param>    
  </sql:header>  
  <sql:query>  
    SELECT ContactID, FirstName, LastName  
    FROM   Person.Contact  
    WHERE  ContactID=@ContactID  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Si tratta del codice aggiornato nel quale un parametro viene passato per eseguire il modello.  
  
```  
public static int testParams()  
{  
  
   Stream strm;  
   SqlXmlParameter p;  
  
   SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
   cmd.CommandType = SqlXmlCommandType.TemplateFile;  
   cmd.CommandText = "TemplateFile.xml";  
   p = cmd.CreateParameter();  
   p.Name="@ContactID";  
   p.Value = "1";  
   strm = cmd.ExecuteStream();  
   StreamReader sw = new StreamReader(strm);  
   Console.WriteLine(sw.ReadToEnd());  
   return 0;        
}  
```  
  
  
