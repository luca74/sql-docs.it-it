---
title: Creazione, modifica e rimozione di regole | Documenti Microsoft
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4e0a96280d38f7447a10decb6c99187b925f646
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2018
---
# <a name="creating-altering-and-removing-rules"></a>Creazione, modifica e rimozione di regole
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In SMO le regole sono rappresentate dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Rule>. La regola è definita dalla proprietà <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A>, ovvero una stringa di testo contenente un'espressione della condizione che utilizza operatori o predicati, ad esempio IN, LIKE o BETWEEN. Una regola non può fare riferimento a colonne o ad altri oggetti di database. È possibile includere funzioni predefinite che non fanno riferimento a oggetti di database.  
  
 La definizione nella proprietà <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> deve contenere una variabile che fa riferimento al valore di dati immesso. Quando si crea la regola, è possibile utilizzare qualsiasi nome o simbolo per rappresentare il valore, ma il primo carattere deve essere il simbolo di chiocciola (@).  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per ulteriori informazioni, vedere [crea un Visual C &#35; Progetto SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Creazione, modifica e rimozione di una regola in Visual Basic  
 In questo esempio di codice viene illustrato come creare una regola, collegarla a una colonna, modificare le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Rule>, scollegarla dalla colonna e infine eliminarla.  
  
 Il **Dim** istruzione per il <xref:Microsoft.SqlServer.Management.Smo.Rule> oggetto è specificato con il percorso completo dell'assembly per evitare ambiguità con un <xref:Microsoft.SqlServer.Management.Smo.Rule> oggetto nell'assembly System. Data.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Creazione, modifica e rimozione di una regola in Visual C#  
 In questo esempio di codice viene illustrato come creare una regola, collegarla a una colonna, modificare le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Rule>, scollegarla dalla colonna e infine eliminarla.  
  
 Il **Dim** istruzione per il <xref:Microsoft.SqlServer.Management.Smo.Rule> oggetto è specificato con il percorso completo dell'assembly per evitare ambiguità con un <xref:Microsoft.SqlServer.Management.Smo.Rule> oggetto nell'assembly System. Data.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>Creazione, modifica e rimozione di una regola in PowerShell  
 In questo esempio di codice viene illustrato come creare una regola, collegarla a una colonna, modificare le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Rule>, scollegarla dalla colonna e infine eliminarla.  
  
 Il **Dim** istruzione per il <xref:Microsoft.SqlServer.Management.Smo.Rule> oggetto è specificato con il percorso completo dell'assembly per evitare ambiguità con un <xref:Microsoft.SqlServer.Management.Smo.Rule> oggetto nell'assembly System. Data.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
