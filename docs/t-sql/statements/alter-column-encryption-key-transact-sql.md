---
title: ALTER COLUMN ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a6bc70a7cafdbf69549435b44099b903cfc60327
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Modifica una chiave di crittografia della colonna in un database, aggiungendo o eliminando un valore crittografato. Una chiave di crittografia della colonna può avere fino a due valori in moda da consentire la rotazione della chiave master della colonna corrispondente. La chiave di crittografia della colonna viene usata per crittografare le colonne tramite la funzionalità [Always Encrypted &#40;Motore di database&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Prima di aggiungere un valore per la chiave di crittografia della colonna, è necessario definire la chiave master della colonna usata per crittografare il valore tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o l'istruzione [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *key_name*  
 Chiave di crittografia della colonna che si sta modificando.  
  
 *column_master_key_name*  
 Specifica il nome della chiave master della colonna usata per crittografare la chiave di crittografia della colonna.  
  
 *algorithm_name*  
 Nome dell'algoritmo di crittografia usato per crittografare il valore. L'algoritmo per i provider di sistema deve essere **RSA_OAEP**. Questo argomento non è valido quando si elimina un valore della chiave di crittografia della colonna.  
  
 *varbinary_literal*  
 BLOB della chiave di crittografia della colonna crittografato con la chiave di crittografia master specificata. , Questo argomento non è valido quando si elimina un valore della chiave di crittografia della colonna.  
  
> [!WARNING]  
>  Non passare mai i valori della chiave di crittografia della colonna in testo non crittografato in questa istruzione, altrimenti sarà compromesso il vantaggio di questa funzionalità.  
  
## <a name="remarks"></a>Remarks  
 In genere, una chiave di crittografia della colonna viene creata con un solo valore crittografato. Quando una chiave master della colonna deve essere ruotata, vale a dire la chiave master della colonna corrente deve essere sostituita dalla nuova chiave master della colonna, è possibile aggiungere un nuovo valore della chiave di crittografia della colonna, crittografato con la nuova chiave master della colonna. In questo modo è possibile garantire alle applicazioni client l'accesso ai dati crittografati con la chiave di crittografia della colonna, mentre la nuova chiave master della colonna sarà resa disponibile alle applicazioni client. Un driver abilitato per Always Encrypted in un'applicazione client che non ha accesso alla nuova chiave master potrà usare il valore della chiave di crittografia della colonna crittografato con la vecchia chiave master della colonna per accedere ai dati sensibili. Per gli algoritmi di crittografia supportati da Always Encrypted è necessario che il valore del testo non crittografato sia di 256 bit. È necessario generare un valore crittografato tramite un provider dell'archivio chiavi in cui è incapsulato l'archivio chiavi contenente la chiave master della colonna.  
  
 Usare [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) e [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) per visualizzare le informazioni sulle chiavi di crittografia della colonna.  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessaria l'autorizzazione **ALTER ANY COLUMN ENCRYPTION KEY** per il database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-adding-a-column-encryption-key-value"></a>A. Aggiunta di un valore della chiave di crittografia della colonna  
 Nell'esempio seguente viene modificata una chiave di crittografia della colonna denominata `MyCEK`.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>B. Eliminazione di un valore della chiave di crittografia della colonna  
 Nell'esempio seguente viene modificata una chiave di crittografia della colonna denominata `MyCEK` eliminando un valore.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Always Encrypted &#40;Motore di database&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
