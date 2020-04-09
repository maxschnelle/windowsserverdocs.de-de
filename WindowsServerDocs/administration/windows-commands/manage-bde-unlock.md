---
title: "\"manage-bde Unlock\""
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e26952ca8c2b20cb0cb8efa167fca81e27b692a0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839737"
---
# <a name="manage-bde-unlock"></a>manage-bde: entsperren



Entsperrt ein durch BitLocker geschütztes Laufwerk mit einem Wiederherstellungs Kennwort oder einem Wiederherstellungs Schlüssel. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Wert|Beschreibung|
|---------|-----|-----------|
|-wiederherstellungkennwort||Gibt an, dass ein Wiederherstellungs Kennwort verwendet wird, um das Laufwerk zu entsperren. Abkürzung:-RP|
||Kennwort \<>|Stellt das Wiederherstellungs Kennwort dar, das verwendet werden kann, um das Laufwerk zu entsperren.|
|-Wiederherstellungsschlüssel||Gibt an, dass eine externe Wiederherstellungs Schlüsseldatei verwendet wird, um das Laufwerk zu entsperren. Abkürzung:-RK|
||\<Path>|Stellt die externe Wiederherstellungs Schlüsseldatei dar, die zum Entsperren des Laufwerks verwendet werden kann.|
||\<Laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-Zertifikat||Das lokale Benutzerzertifikat für ein BitLocker-Zertifikat zum deinstalcken des Volumes befindet sich im Speiche-Benutzerzertifikat Speicher. Abkürzung:-CERT|
||<-CF pathycertificatefile >|Pfad zur Zertifikatsdatei|
||< CT certifipaethumschlag-Druck >|Der Zertifikat Fingerabdruck, der optional die PIN (-PIN) enthalten kann.|
|-password||Zeigt eine Eingabeaufforderung für das Kennwort zum Entsperren des Volumes an. Abkürzung:-PW|
|-Computername||Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Abkürzung:-CN|
||\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?||Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h||Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-Unlock** " zum Entsperren von Laufwerk E mit einer Wiederherstellungs Schlüsseldatei, die in einem Sicherungsordner auf einem anderen Laufwerk gespeichert wurde.
```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)