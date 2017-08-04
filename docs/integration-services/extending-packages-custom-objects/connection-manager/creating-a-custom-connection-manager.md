---
title: Creazione di una gestione connessione personalizzata | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom connection managers [Integration Services], creating
ms.assetid: e83f8e02-ace4-42e0-b979-2f6be1460985
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c617741134c19c012f487bc00263c2e4b071810
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-connection-manager"></a>Creazione di una gestione connessione personalizzata
  I passaggi che è necessario effettuare per creare una gestione connessione personalizzata sono simili ai passaggi necessari per la creazione di qualsiasi altro oggetto personalizzato per [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Creare una nuova classe che eredita dalla classe di base. Per una gestione connessione, la classe di base è <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>.  
  
-   Applicare alla classe l'attributo che identifica il tipo di oggetto. Per una gestione connessione, l'attributo è <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>.  
  
-   Eseguire l'override dell'implementazione dei metodi e delle proprietà della classe di base. Per una gestione connessione, questi includono la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> e i metodi <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>.  
  
-   Se si desidera, sviluppare un'interfaccia utente personalizzata. Per una gestione connessione, è richiesta una classe tramite cui venga implementata l'interfaccia <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>.  
  
> [!NOTE]  
>  La maggior parte delle attività, delle origini e delle destinazioni incluse in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] funziona solo con tipi specifici di gestioni connessioni predefinite. Questi esempi, pertanto, non possono essere testati con le attività e i componenti predefiniti.  
  
## <a name="getting-started-with-a-custom-connection-manager"></a>Introduzione alle gestioni connessioni personalizzate  
  
### <a name="creating-projects-and-classes"></a>Creazione di progetti e classi  
 Poiché tutte le gestioni connessioni derivano dalla classe di base <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>, il primo passaggio da completare quando si crea una gestione connessione personalizzata consiste nel creare un progetto di libreria di classi nel linguaggio di programmazione gestito preferito e creare una classe che eredita dalla classe di base. In questa classe derivata si eseguirà l'override dei metodi e delle proprietà della classe di base per implementare la funzionalità personalizzata.  
  
 Nella stessa soluzione creare un secondo progetto di libreria di classi per l'interfaccia utente personalizzata. Per semplificare lo sviluppo, si consiglia di utilizzare un assembly distinto per l'interfaccia utente, perché in questo modo è possibile e ridistribuire la gestione connessione o la relativa interfaccia utente in modo indipendente.  
  
 Configurare entrambi i progetti per firmare gli assembly che verranno generati durante la compilazione utilizzando un file di chiave con nome sicuro.  
  
### <a name="applying-the-dtsconnection-attribute"></a>Applicazione dell'attributo DtsConnection  
 Applicare l'attributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> alla classe creata per identificarla come gestione connessione. Questo attributo fornisce informazioni in fase di progettazione, ad esempio il nome, la descrizione e il tipo di connessione della gestione connessione. Il <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.ConnectionType%2A> e **descrizione** le proprietà corrispondenti al **tipo** e **descrizione** le colonne visualizzate nel **Aggiungi gestione connessione SSIS** nella finestra di dialogo viene visualizzata quando si configurano le connessioni per un pacchetto in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 Utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> per collegare la gestione connessione alla relativa interfaccia utente personalizzata. Per ottenere il token di chiave pubblica che è necessario per questa proprietà, è possibile utilizzare **sn.exe -t** per visualizzare il token di chiave pubblica dal file di coppia di chiavi (con estensione snk) che si intende utilizzare per firmare l'assembly dell'interfaccia utente.  
  
```vb  
<DtsConnection(ConnectionType:="SQLVB", _  
  DisplayName:="SqlConnectionManager (VB)", _  
  Description:="Connection manager for Sql Server", _  
  UITypeName:="SqlConnMgrUIVB.SqlConnMgrUIVB,SqlConnMgrUIVB,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")> _  
Public Class SqlConnMgrVB  
  Inherits ConnectionManagerBase  
  . . .  
End Class  
```  
  
```csharp  
[DtsConnection(ConnectionType = "SQLCS",  
  DisplayName = "SqlConnectionManager (CS)",  
  Description = "Connection manager for Sql Server",  
  UITypeName = "SqlConnMgrUICS.SqlConnMgrUICS,SqlConnMgrUICS,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")]  
public class SqlConnMgrCS :  
ConnectionManagerBase  
{  
  . . .  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-connection-manager"></a>Compilazione, distribuzione e debug di una gestione connessione personalizzata  
 I passaggi per la compilazione, la distribuzione e il debug di una gestione connessione personalizzata in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sono simili a quelli richiesti per altri tipi di oggetti personalizzati. Per ulteriori informazioni, vedere [compilazione, distribuzione e debug di oggetti personalizzati](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).    
  
## <a name="see-also"></a>Vedere anche  
 [Codifica una gestione connessione personalizzata](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)   
 [Sviluppo di un'interfaccia utente per una gestione connessione personalizzata](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  