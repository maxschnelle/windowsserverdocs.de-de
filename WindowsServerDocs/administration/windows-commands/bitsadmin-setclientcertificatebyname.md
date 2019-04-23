---
title: Bitsadmin setclientcertificatebyname
description: Windows-Befehle Thema **Bitsadmin Setclientcertificatebyname** -gibt den Antragstellernamen des Clientzertifikats für die Clientauthentifizierung in einer Anforderung von HTTPS (SSL) verwenden.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 76150ccb34693eb692d27efbd6538f5363ba1c26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871311"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>Bitsadmin setclientcertificatebyname



Gibt den Antragstellernamen des Clientzertifikats für die Clientauthentifizierung in einer Anforderung von HTTPS (SSL) verwenden.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> <subject_name>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Store_location|Gibt den Standort ein Systemspeicher für das Nachschlagen des Zertifikats verwenden. Mögliche Werte:</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (SERVICES)</br>5 (BENUTZER)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Speichername|Der Name des Zertifikatspeichers. Mögliche Werte:</br>Zertifizierungsstelle (Certification Authority Zertifikate)</br>Meine (persönliche Zertifikate)</br>Stamm (Root-Zertifikate)</br>SPC (Software Publisher Certificate)|
|Subject_name|Name des Zertifikats|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel gibt den Namen des Zertifikats für den Client *MyCertificate* für die Verwendung für die Clientauthentifizierung in einer Anforderung HTTPS (SSL) für den Auftrag mit dem Namen *MyJob*.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByName myJob 1 MY myCertificate 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)