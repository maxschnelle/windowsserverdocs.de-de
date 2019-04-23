---
title: Bitsadmin setclientcertificatebyid
description: Windows-Befehle Thema **Bitsadmin Setclientcertificatebyid** gibt den Bezeichner des Clientzertifikats für die Clientauthentifizierung in einer Anforderung von HTTPS (SSL) verwenden.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2424de18ee8aaec73b086207e8ef56d85df862fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863931"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>Bitsadmin setclientcertificatebyid



Gibt den Bezeichner des Clientzertifikats für die Clientauthentifizierung in einer Anforderung von HTTPS (SSL) verwenden.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> hexa-decimal_cert_id>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Store_location|Gibt den Standort ein Systemspeicher für das Nachschlagen des Zertifikats verwenden. Mögliche Werte:</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (SERVICES)</br>5 (BENUTZER)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Speichername|Der Name des Zertifikatspeichers. Mögliche Werte:</br>Zertifizierungsstelle (Certification Authority Zertifikate)</br>Meine (persönliche Zertifikate)</br>Stamm (Root-Zertifikate)</br>SPC (Software Publisher Certificate)|
|Hexadecimal_cert_id|Eine hexadezimale Zahl, die den Hash des Zertifikats darstellt.|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel gibt den Bezeichner des Clientzertifikats für die Verwendung für die Clientauthentifizierung in einer Anforderung HTTPS (SSL) für den Auftrag mit dem Namen *MyJob*.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByID myJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)