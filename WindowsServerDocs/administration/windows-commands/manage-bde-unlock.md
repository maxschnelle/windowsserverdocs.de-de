---
title: "\"manage-bde Unlock\""
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fd303116e101c8c8503d220ba382d6cdd994ad3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724064"
---
# <a name="manage-bde-unlock"></a>manage-bde: entsperren



Entsperrt ein durch BitLocker geschütztes Laufwerk mit einem Wiederherstellungs Kennwort oder einem Wiederherstellungs Schlüssel.

## <a name="syntax"></a>Syntax

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Wert|BESCHREIBUNG|
|---------|-----|-----------|
|-wiederherstellungkennwort||Gibt an, dass ein Wiederherstellungs Kennwort verwendet wird, um das Laufwerk zu entsperren. Abkürzung:-RP|
||\<Kennwort>|Stellt das Wiederherstellungs Kennwort dar, das verwendet werden kann, um das Laufwerk zu entsperren.|
|-Wiederherstellungsschlüssel||Gibt an, dass eine externe Wiederherstellungs Schlüsseldatei verwendet wird, um das Laufwerk zu entsperren. Abkürzung:-RK|
||\<"Pathdeexternalkeyfile"->|Stellt die externe Wiederherstellungs Schlüsseldatei dar, die zum Entsperren des Laufwerks verwendet werden kann.|
||\<Laufwerk>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-Zertifikat||Das lokale Benutzerzertifikat für ein BitLocker-Zertifikat zum deinstalcken des Volumes befindet sich im Speiche-Benutzerzertifikat Speicher. Abkürzung:-CERT|
||<-CF pathycertificatefile>|Pfad zur Zertifikatsdatei|
||< CT certifipaethumschlag-Druck>|Der Zertifikat Fingerabdruck, der optional die PIN (-PIN) enthalten kann.|
|-password||Zeigt eine Eingabeaufforderung für das Kennwort zum Entsperren des Volumes an. Abkürzung:-PW|
|-Computername||Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Abkürzung:-CN|
||\<Name>|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?||Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h||Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Veranschaulicht die Verwendung des Befehls " **-Unlock** " zum Entsperren von Laufwerk E mit einer Wiederherstellungs Schlüsseldatei, die in einem Sicherungsordner auf einem anderen Laufwerk gespeichert wurde.
```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)