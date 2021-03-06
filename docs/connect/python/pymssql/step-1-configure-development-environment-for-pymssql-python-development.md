---
title: 'Passaggio 1: Configurare l''ambiente di sviluppo Python pymssql | Documenti Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: python
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 91916f56a4bbdad46c7fc391257c4575886c28dc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per pymssql sviluppo Python
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione utilizzando il Driver di Python per SQL Server.    
  
Si noti che i driver SQL Python il protocollo TDS, che è abilitato per impostazione predefinita in SQL Server e Database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime di Python e pip Gestione pacchetti**  
a. Passare a [python.org](https://www.python.org/downloads/)  
b. Fare clic sul collegamento appropriato Windows installer msi.   
c. Esegui una volta scaricato il file msi per installare il runtime di Python  
  
2. **Scaricare il modulo pymssql** da [qui](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Assicurarsi di scegliere il file whl corretto.  Ad esempio: scegliere se si usa Python 2.7 in un computer a 64 bit: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Dopo avere scaricato il file .whl inserirlo la cartella c: / Python27.  
      
3. **Aprire cmd.exe**  
  
4. **Installare il modulo pymssql**     
    Ad esempio, se si usa Python 2.7 in un computer a 64 bit:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Installare il runtime di Python e pip Gestione pacchetti** Python preinstallata sulla maggior parte delle distribuzioni di Ubuntu.  Se il computer non dispone di python installato, è possibile ottenere entrambi download tarball l'origine da [python.org](https://www.python.org/downloads/) e compilare in locale oppure è possibile utilizzare la gestione dei pacchetti:  
```  
> sudo apt-get install python   
```  
  
2.  **Aprire terminal**  
  
3.  **Installare le dipendenze e modulo pymssql**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installare il runtime di Python e pip Gestione pacchetti**  
a. Passare a [python.org](https://www.python.org/downloads/)  
b. Fare clic sul collegamento appropriato Mac installer pkg.   
c. Esegui una volta scaricato pkg per installare il runtime di Python  
  
2.  **Aprire terminal**  
  
3. **Installare Gestione pacchetti di Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Installare il modulo di disporre di FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Installare il modulo pymssql**  
```  
> sudo -H pip install pymssql  
```
