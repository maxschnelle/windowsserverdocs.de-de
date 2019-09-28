---
title: bizadmin setclientcertificatebyname
description: 'Windows-Befehls Thema für **bizadmin setclientcertificatebyname** : gibt den Antragsteller Namen des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung verwendet werden soll.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de2e84401673848ecc8823bb6dd3f91224d9a87e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380671"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bizadmin setclientcertificatebyname



Gibt den Antragsteller Namen des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS-Anforderung (SSL) verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> <subject_name>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Store_location|Gibt den Speicherort eines Systemspeicher an, der zum Nachschlagen des Zertifikats verwendet werden soll. Mögliche Werte:</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (DIENSTE)</br>5 (BENUTZER)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Store_name|Der Name des Zertifikat Speicher. Mögliche Werte:</br>CA (Zertifizierungsstellen Zertifikate)</br>Meine (persönliche Zertifikate)</br>Root (Stamm Zertifikate)</br>SPC (Software Herausgeber Zertifikat)|
|Subject_name|Name des Zertifikats|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Name des Client *Zertifikats, das* für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung für den Auftrag *MyJob*verwendet werden soll, angegeben.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByName myJob 1 MY myCertificate 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)