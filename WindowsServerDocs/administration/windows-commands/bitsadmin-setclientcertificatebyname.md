---
title: bizadmin setclientcertificatebyname
description: Windows-Befehls Thema für bizadmin setclientcertificatebyname, das den Antragsteller Namen des Client Zertifikats angibt, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung verwendet werden soll.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08ec6fd8c941234de36f14cd71ffa51c3b428acb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849653"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bizadmin setclientcertificatebyname

Gibt den Antragsteller Namen des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS-Anforderung (SSL) verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Store_location|Gibt den Speicherort eines Systemspeicher an, der zum Nachschlagen des Zertifikats verwendet werden soll. Mögliche Werte:</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (Dienste)</br>5 (Benutzer)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Store_name|Der Name des Zertifikatspeichers. Mögliche Werte:</br>CA (Zertifizierungsstellen Zertifikate)</br>Meine (persönliche Zertifikate)</br>Root (Stamm Zertifikate)</br>SPC (Software Herausgeber Zertifikat)|
|Subject_name|Name des Zertifikats|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Name des Client *Zertifikats, das* für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung für den Auftrag *MyJob*verwendet werden soll, angegeben.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByName myJob 1 MY myCertificate 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)