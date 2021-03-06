---
title: Installazione dei componenti di machine learning senza accesso a internet | Documenti Microsoft
ms.custom: 
ms.date: 03/05/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: d7d218dcb5efeddf248230abff85b46da23d389a
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2018
---
# <a name="installing-machine-learning-components-without-internet-access"></a>Installazione dei componenti di machine learning senza accesso a internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Poiché i componenti di R e Python forniti con SQL Server 2016 e SQL Server 2017 sono open source di, Microsoft non vengono installati componenti di R o Python per impostazione predefinita. Al contrario, i programmi di installazione correlate offerte e in bundle pacchetti per maggiore praticità nel Microsoft Download Center e altri siti attendibili. Deve accettare la licenza appropriata e quindi il programma di installazione di SQL Server installa i componenti di R o Python per l'utente.

In questo argomento vengono indicate le posizioni di download per i programmi di installazione e una panoramica del processo di installazione offline.

## <a name="overview-of-the-offline-installation-process"></a>Panoramica del processo di installazione offline

In genere, il programma di installazione dei componenti di computer utilizzati in SQL Server 2016 e SQL Server 2017 richiede una connessione internet. Quando viene eseguito il programma di installazione di SQL Server, se è stata selezionata una delle opzioni di apprendimento automatico, il programma di installazione verifica la presenza di Python o R i programmi di installazione, come nonché altri componenti necessari.

+ **Se il computer dispone di una connessione a internet**

    SQL Server individua e scarica i componenti per l'utente e quindi li installa durante l'installazione. Accettare le condizioni di licenza separatamente per ogni componente di origine aprire (R o Python) che si installa.

+ **Se il computer non ha accesso a internet**

    È necessario scaricare i programmi di installazione aggiuntive prima di procedere con l'installazione. Come minimo, scaricare i programmi di installazione R o Python supportati per la versione di SQL Server che si sta installando.

    A seconda della configurazione del server, potrebbe essere necessario i componenti aggiuntivi.  Vedere [i componenti aggiuntivi](#bkmk_OtherComponents) per informazioni dettagliate.

    Dopo avere scaricato i programmi di installazione, si utilizzati durante l'installazione della funzionalità come parte del programma di installazione di SQL Server.

### <a name="step-1-obtain-additional-installers"></a>Passaggio 1. Ottenere i programmi di installazione aggiuntivi

In generale, vengono forniti programmi di installazione separati per open source e componenti proprietari. L'installazione guidata di SQL Server assicura che siano installati nell'ordine corretto. Alcune versioni, tuttavia, potrebbero aggiornare un solo set di componenti. Vedere la [tabella dei programmi di installazione](#bkmk_2017Installers) per ogni versione per informazioni dettagliate.

**Per R**

Il linguaggio R è supportato in SQL Server 2016 e versioni successive. 

+ Programmi di installazione con **SRO** nel nome di fornire i componenti di origine aperti.
+ Programmi di installazione con **SRS** nel nome contengono i componenti forniti da Microsoft, inclusi quelli per l'integrazione di database.

**Per Python**

Il linguaggio Python richiede SQL Server 2017 o versione successiva. 

+ Programmi di installazione con **Simulato** nel nome sono per aprire Python di Microsoft e fornire i componenti di origine aperti.
+ Programmi di installazione con **SPS** nel nome sono per il Server di Python di Microsoft e include i componenti forniti da Microsoft, inclusi quelli per l'integrazione di database.

**Come scaricare**

1. Scaricare i programmi di installazione dal [siti Microsoft Download Center](#installerlocs) in un computer con accesso a internet, quindi salvare il programma di installazione anziché eseguirla.
2. Copiare i file di programma di installazione (CAB) nel computer in cui si prevede di installare i componenti di machine learning.
3. In SQL Server 2016, l'installazione guidata installato inglese per impostazione predefinita. Per installare utilizzando una lingua diversa necessarie modifiche del nome del file di programma di installazione, come descritto qui: [modifiche richieste per le impostazioni locali diverse lingue](#modslocales).
    Per SQL Server 2017, lingua corretta viene identificata in base alle impostazioni locali di istanza.
4. Scaricare tutti i componenti aggiuntivi necessari, ad esempio MPI o .NET Core.
5. Facoltativamente, è possibile scaricare il codice sorgente archiviato per i componenti di origine aperti, ma ciò non è necessaria per l'installazione di SQL Server e può essere completata in qualsiasi momento. Per altre informazioni, vedere [R Server per Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows).

Per una descrizione dettagliata del processo di installazione offline per R Services in SQL Server 2016, si consiglia di articolo per la [SQL Server Customer Advisory Team](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/). l'articolo include le schermate e riguarda anche l'applicazione di patch e integrazione scenari di installazione.

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>Passaggio 2. Eseguire il programma di installazione offline utilizzando l'installazione guidata di SQL Server

1. Eseguire l'Installazione guidata di SQL Server.
2. Dopo l'installazione guidata consente di visualizzare la pagina di gestione delle licenze, fare clic su **Accept**.
3. Verrà visualizzata una finestra di dialogo che viene richiesto di specificare il **percorso di installazione** dei pacchetti necessari.
4. Fare clic su **Sfoglia** per individuare la cartella che contiene i file di programma di installazione copiato in precedenza.
5. Se vengono trovati i file corretti, fare clic su **Avanti** per indicare che i componenti sono disponibili.
6. Completare l'Installazione guidata di SQL Server.
7. Eseguire i passaggi di post-installazione necessari per assicurarsi che il servizio è abilitato.

## <a name="installerlocs"></a>Posizione in cui scaricare i componenti di machine learning

Assicurarsi di ottenere i file che corrispondano alla versione di SQL Server si sta installando.

+ [Per ottenere i componenti R per SQL Server 2016](#bkmk_2016Installers)

+ [Per ottenere i componenti di R o Python per SQL Server 2017](#bkmk_2017Installers)

Supporto per Python viene fornito a partire da SQL Server 2017 versioni da CTP 2.0. Le versioni precedenti, tra cui SQL Server 2016 non supportano Python.

### <a name="bkmk_2017Installers"></a>Download di SQL Server 2017

Versione  |Collegamento di download  |
---------|---------|
**SQL Server 2017 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 2017 CTP 1.4** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Aprire Microsoft Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python Server    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**SQL Server 2017 RC1** |
Microsoft R Open     |[SRO_3.3.3.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851503)|
Microsoft R Server     |[SRS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851498)|
Aprire Microsoft Python     |[SPO_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851499)|
Microsoft Python Server    |[SPS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851504)|
**SQL Server 2017 RC 2** |
Microsoft R Open     |[SRO_3.3.3.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851493)|
Microsoft R Server     |[SRS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851505)|
Aprire Microsoft Python     |[SPO_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851506)|
Microsoft Python Server    |[SPS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851497)|
**SQL Server 2017 RTM** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Aprire Microsoft Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Aprire Microsoft Python     |Nessuna modifica, Utilizzare precedente |
Microsoft Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server      |Nessuna modifica, Utilizzare precedente|
Aprire Microsoft Python     |Nessuna modifica, Utilizzare precedente|
Microsoft Python Server    |Nessuna modifica, Utilizzare precedente|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Aprire Microsoft Python     |Nessuna modifica, Utilizzare precedente|
Microsoft Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 2017 CU4** |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Aprire Microsoft Python     |Nessuna modifica, Utilizzare precedente|
Microsoft Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|

### <a name="bkmk_2016Installers"></a>Download di SQL Server 2016

> [!IMPORTANT]
> 
> Quando si installa SQL Server 2016 SP1 CU4 o CU5 SP1 offline, scaricare SRO_3.2.2.16000_1033.cab. Se hai scaricato SRO_3.2.2.13000_1033.cab da FWLINK 831785 come indicato nella finestra di dialogo programma di installazione, rinominare il file come SRO_3.2.2.16000_1033.cab prima di installare l'aggiornamento cumulativo.

Versione  |Collegamento di download  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server     | Nessuna modifica, Utilizzare precedente |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server     |Nessuna modifica, Utilizzare precedente|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server     |Nessuna modifica, Utilizzare precedente |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server     |Nessuna modifica, Utilizzare precedente|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server     |Nessuna modifica, Utilizzare precedente|
**GDR e SQL Server 2016 SP 1 CU4**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |Nessuna modifica, Utilizzare precedente|
Microsoft R Server    |Nessuna modifica, Utilizzare precedente |

Se si desidera visualizzare il codice sorgente per Microsoft R, è disponibile per il download come archivio in formato con estensione tar: [programmi di installazione scaricare R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Prerequisiti aggiuntivi

A seconda dell'ambiente, potrebbe essere necessario effettuare copie locali dei programmi di installazione per i prerequisiti seguenti.

Componente  |Versione
---------|---------
[Provider OLE DB Microsoft AS per SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="modslocales"></a>Installazione per diverse lingue

Se si scarica il. File CAB come parte del programma di installazione di SQL Server in un computer con accesso a internet, l'installazione guidata rileva la lingua locale e la lingua del programma di installazione viene automaticamente modificato.

Tuttavia, a seconda della versione di SQL Server, potrebbe essere necessario adottare misure aggiuntive per installare i componenti di R localizzati in un computer senza accesso a internet.

+ **Per SQL Server 2016**

   Dopo aver scaricato i programmi di installazione di R in una condivisione locale, potrebbe essere necessario modificare manualmente il nome dei file scaricati per inserire l'identificatore di lingua corretta per la lingua che si sta installando.

    Ad esempio, per installare la versione giapponese di SQL Server, si modificherebbe il nome del file da SRS_8.0.3.0_**1033**CAB a SRS_8.0.3.0_**1041**CAB.

    > [!IMPORTANT]
    > Questo problema si applica solo a versioni ed è stato corretto nelle versioni successive.
    > **Utilizzare questa soluzione solo se il programma di installazione restituisce un messaggio che è possibile installare quella desiderata.**

+ **Per SQL Server 2017**

    Scaricare la. File CAB per i componenti R o Python.
    
    La lingua è stata rilevata in base alle impostazioni locali di server. Le impostazioni locali corrette viene automaticamente installata mediante scaricato. File CAB.

## <a name="slipstream-upgrades"></a>Aggiornamenti di integrazione

L'installazione integrata si riferisce alla possibilità di applicare una patch a un'installazione di istanza non riuscita o di aggiornare tale installazione per risolvere i problemi esistenti. Il vantaggio di questo metodo è che SQL Server viene aggiornato mentre si esegue l'installazione, evitando il riavvio separato in un secondo momento.

+ Se il server non ha accesso a Internet, è necessario scaricare il programma di installazione di SQL Server e quindi scaricare le versioni dei programmi di installazione dei componenti R corrispondenti **prima** di iniziare il processo di aggiornamento.  I componenti di R non sono inclusi per impostazione predefinita con SQL Server.

+ Se si aggiungono questi componenti a un'installazione esistente, utilizzare la versione aggiornata del programma di installazione di SQL Server e la versione aggiornata corrispondente dei componenti aggiuntivi. Quando si specifica che la funzionalità di R viene installato, il programma di installazione cerca la versione corrispondente dei programmi di installazione per l'apprendimento automatico dei componenti.

## <a name="command-line-arguments-for-specifying-component-locations"></a>Argomenti della riga di comando che consente di specificare percorsi dei componenti

Quando si esegue un'installazione offline dalla riga di comando, è necessario fornire gli argomenti della riga di comando seguenti per specificare il percorso dei componenti che è stato scaricato in anticipo. Tuttavia, è necessario impostare i flag aggiuntivi per installare i componenti aggiuntivi; impostazione predefinita vengono installati automaticamente i prerequisiti, ad esempio .NET core.

**Percorso dei programmi di installazione**

- `/UPDATESOURCE` Per specificare il percorso del file locale contenente il programma di installazione di aggiornamento di SQL Server
- `/MRCACHEDIRECTORY` Per specificare la cartella contenente i file CAB del componente R
- `/MPYCACHEDIRECTORY` Per specificare la cartella contenente i file CAB del componente Python

**Componenti di R in SQL Server 2016**

- `/ADVANCEDANALYTICS` Per ottenere supporto del motore di script esterni
- `/IACCEPTROPENLICENSETERMS="True"` per accettare la R separato contratto di licenza

**Componenti di R in SQL Server 2017**

- `/ADVANCEDANALYTICS` Per ottenere supporto del motore di script esterni
- `/SQL_INST_MR` usare il linguaggio R
- `/IACCEPTROPENLICENSETERMS="True"` per accettare la R separato contratto di licenza

**Componenti di Python in SQL Server 2017**

- `/ADVANCEDANALYTICS` Per ottenere supporto del motore di script esterni
- `/SQL_INST_MPY` Per utilizzare Python
- `/IACCEPTPYTHONLICENSETERMS="True"` per accettare il Python separato contratto di licenza

> [!NOTE]
> Non è possibile modificare l'account del servizio per la finestra di avvio utilizzando i parametri nel programma di installazione di SQL Server. È consigliabile installare utilizzando l'account di servizio predefiniti e quindi modificare l'account del servizio utilizzando Gestione configurazione SQL Server. Al termine dell'operazione, assicurarsi di riavviare il servizio Launchpad.

## <a name="see-also"></a>Vedere anche

[Installare Microsoft R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows)

In questo articolo dal team di supporto di servizi R viene illustrato come eseguire un'installazione automatica o un aggiornamento di R services in SQL Server 2016: [distribuzione di R Services nei computer senza accesso a Internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).
