---
title: Verwalten von-Bde entsperren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a86267890449be2048221940e5955e49f30f99f3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814601"
---
# <a name="manage-bde-unlock"></a>Verwalten von-Bde: nicht entsperren



Wird ein mit BitLocker geschütztes Laufwerk mit einer Wiederherstellungskennwort oder Wiederherstellungsschlüssel entsperrt. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Wert|Beschreibung|
|---------|-----|-----------|
|-recoverypassword||Gibt an, dass ein Wiederherstellungskennwort zum Entsperren des Laufwerks verwendet werden. Abkürzung: - rp|
||\<Kennwort >|Stellt das Wiederherstellungskennwort, das zum Entsperren des Laufwerks verwendet werden kann.|
|-recoverykey||Gibt an, dass eine externe wiederherstellungsschlüsseldatei zum Entsperren des Laufwerks verwendet werden. Abbreviation: -rk|
||\<PathToExternalKeyFile>|Stellt die externen Wiederherstellungsschlüssel-Datei, die zum Entsperren des Laufwerks verwendet werden kann.|
||\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-Zertifikat||Das lokale Zertifikat für ein BitLocker-Zertifikat, das Volume unclock befindet sich im Zertifikatspeicher Locat-Benutzers. Abbreviation: -cert|
||<-Cf PathToCertificateFile >|Pfad zur Datei cerficate|
||<-ct CertificateThumbprint >|Fingerabdruck des Zertifikats, z. B. optional die PIN (-Pin).|
|-Kennwort||Stellt eine Eingabeaufforderung für das Kennwort zum Entsperren des Volumes an. Abkürzung: Pw-|
|-computername||Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Abbreviation: -cn|
||\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?||Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h||Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **-nicht entsperren** Befehl aus, um das Laufwerk E: mit einer Schlüsseldatei für die Wiederherstellung zu entsperren, die auf einem anderen Laufwerk in einen Sicherungsordner gespeichert wurde.
```
manage-bde –unlock E: -recoverykey "F:\Backupkeys\recoverykey.bek"
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)