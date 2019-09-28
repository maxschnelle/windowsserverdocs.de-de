---
title: BI-admin setclientcertificatebyid
description: Windows-Befehls Thema für **bizadmin setclientcertificatebyid** gibt den Bezeichner des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung verwendet werden soll.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53b6fa4c65397cf710d0497fbae889afd31ec136
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380728"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>BI-admin setclientcertificatebyid



Gibt den Bezeichner des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS-Anforderung (SSL) verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> hexa-decimal_cert_id>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Store_location|Gibt den Speicherort eines Systemspeicher an, der zum Nachschlagen des Zertifikats verwendet werden soll. Mögliche Werte:</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (DIENSTE)</br>5 (BENUTZER)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Store_name|Der Name des Zertifikat Speicher. Mögliche Werte:</br>CA (Zertifizierungsstellen Zertifikate)</br>Meine (persönliche Zertifikate)</br>Root (Stamm Zertifikate)</br>SPC (Software Herausgeber Zertifikat)|
|Hexadecimal_cert_id|Eine hexadezimale Zahl, die den Hash des Zertifikats darstellt.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Bezeichner des Client Zertifikats angegeben, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung für den Auftrag mit dem Namen *MyJob*verwendet werden soll.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByID myJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)