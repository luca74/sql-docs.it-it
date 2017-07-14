---
title: Metodo CreateSSLCertificateBinding (MSReportServer_ConfigurationSetting WMI) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1d9a797922bc8d7b39e7b7c43897d4ae5ee5bd28
ms.contentlocale: it-it
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-method---createsslcertificatebinding"></a>Metodo ConfigurationSetting - createsslcertificatebinding-metodo
  Crea un'associazione certificato SSL.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Applicazione*  
 Nome dell'applicazione per la quale l'associazione certificato deve essere creata.  
  
 *CertificateHash*  
 Hash per il certificato.  
  
 *IPAddress*  
 Indirizzo IP per l'applicazione.  
  
 *Porta*  
 Porta SSL associata all'associazione.  
  
 *LCID*  
 Impostazioni locali da utilizzare per i messaggi di errore restituiti.  
  
 *Errore*  
 [out] Descrizione degli errori che si sono verificati.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo aggiunge un'associazione a rsreportserver.config per l'applicazione. Se in HTTP.SYS non esiste già un'associazione, questa viene creata.  
  
 Prima di creare l'associazione, la chiamata al metodo esamina le prenotazioni dell'URL affinché l'applicazione specificata determini se l'associazione certificato SSL è valida.  
  
 Le condizioni seguenti vengono convalidate e possono causare errori:  
  
1.  Il certificato non esiste.  
  
2.  Il valore IPAddress specificato non corrisponde al valore IPAddress di questo computer.  
  
3.  Il valore IPAddress specificato è un IPAddress DHCP (che cambia periodicamente). Utilizzare invece l'indirizzo IP con caratteri jolly (0.0.0.0).  
  
4.  Il valore IPAddress specificato non corrisponde all'indirizzo IP di una prenotazione URL E non esiste né un carattere jolly né la prenotazione URL del nome host.  
  
5.  Esiste una prenotazione URL che specifica un nome host, ma il nome host non corrisponde al nome host del certificato.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  