---
title: "Proprietà computer Analysis Server (scheda accesso) | Documenti Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a82e0c98-efaa-4b0b-9582-3c879ee42444
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 764930102320a6a6f4b998e3de3ec6491bbb485c
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="analysis-server-properties-log-on-tab"></a>Proprietà - Analysis Server (scheda Accesso)
  Utilizzare la scheda **Accesso** della finestra di dialogo **Proprietà - Analysis Server** per specificare l'account utilizzato dal servizio [!INCLUDE[ssAS](../../includes/ssas-md.md)] e avviare e arrestare il servizio.  
  
> [!NOTE]  
>  Quando si modifica il **Nome account** utilizzato da un servizio in un'istanza cluster, il nuovo account deve essere membro del gruppo di dominio specificato durante l'installazione per il servizio in corso di modifica oppure è necessario disporre dell'autorizzazione per aggiungere membri a tale gruppo. Se non si dispone dell’autorizzazione per modificare l'appartenenza al gruppo, contattare l’amministratore di dominio.  
  
## <a name="options"></a>Opzioni  
 **Account di sistema locale**  
 Specificare un account di sistema locale che non richiede una password. Tuttavia, a seconda dei privilegi concessi, l'account di sistema locale può impedire le interazioni tra il servizio e gli altri server.  
  
 **Account seguente**  
 Specificare un account utente locale o di dominio che utilizza l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[msCoName](../../includes/msconame-md.md)]consiglia di utilizzare un account utente di dominio con diritti minimi per i servizi. Per ulteriori informazioni sulla selezione di un account, cercare l'argomento "Impostazione di account di servizio Windows" nella documentazione online.  
  
 **Nome account**  
 Specificare il nome dell'account utente locale o di dominio.  
  
 **Password**  
 Digitare la password dell'account.  
  
 **Conferma password**  
 Digitare nuovamente la password dell'account.  
  
 **Start**  
 Avviare il servizio.  
  
 **Arresta**  
 Consente di arrestare il servizio.  
  
 **Sospendi**  
 Consente di sospendere il servizio.  
  
 **Riprendi**  
 Consente di riprendere un servizio sospeso.  
  
  