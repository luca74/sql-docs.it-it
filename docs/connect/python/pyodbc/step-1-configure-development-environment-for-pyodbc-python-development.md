---
title: 'Passaggio 1: Configurare l''ambiente di sviluppo Python pyodbc | Documenti Microsoft'
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: python
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: "2"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 886cf420228b622fb9c269423ce9a71c2c25ecaa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per pyodbc sviluppo Python

## <a name="windows"></a>Windows  
Connettersi al Database SQL tramite Python - pyodbc in Windows:
  
1. **Download programma di installazione di Python**  
  Se il computer non ha Python installarlo. Passare il [pagina di download di Python](https://www.python.org/downloads/windows/) e scaricare il programma di installazione appropriato. Per esempio, se si utilizza un computer a 64 bit, scaricare il programma di installazione di Python 2.7 o 3.5 (x64).  
  
2. **Installare Python** una volta scaricato il programma di installazione, eseguire le operazioni seguenti: una. Fare doppio clic sul file per avviare il programma di installazione. b. Selezionare la lingua e accettare le condizioni. c. Seguire le istruzioni sullo schermo e Python deve essere installato nel computer in uso. d. È possibile verificare che è Python è installato, passare a C:\Python27 o C:\Python35 ed eseguire python - v o py - v (per 3. x) 
      
3. [**Installare il Driver ODBC di Microsoft**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **Aprire cmd.exe come amministratore**     

5. **Installare pyodbc uso di pip - Python package manager**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Connettersi al Database SQL tramite Python - pyodbc Ubuntu e RedHat:
  
1. **Aprire terminal**  

2. **Installare Microsoft ODBC Driver 13 per Linux** per Ubuntu 15.04 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  Per RedHat 6,7 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **Installare pyodbc**  
```  
> sudo -H pip install pyodbc
```
