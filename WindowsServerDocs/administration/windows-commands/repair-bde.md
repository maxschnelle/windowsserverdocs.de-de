---
title: repair-bde
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e2bce0c0a0f12a3a171c161a669c903044e8b4b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813541"
---
# <a name="repair-bde"></a>repair-bde



Greift auf verschlüsselte Daten auf einer schwer beschädigten Festplatte aus, wenn das Laufwerk mit BitLocker verschlüsselt wurde. Mit Repair-bde können wichtige Laufwerksbereiche wiederhergestellt und wiederherstellbare Daten repariert werden, vorausgesetzt ein gültiges Wiederherstellungskennwort oder ein gültiger Wiederherstellungsschlüssel wird zum Entschlüsseln der Daten verwendet. Wenn die BitLocker-Metadaten auf dem Laufwerk beschädigt sind, muss neben einem Wiederherstellungskennwort oder Wiederherstellungsschlüssel ein Sicherungsschlüsselpaket angegeben werden. Dieses Schlüsselpaket wird in den Active Directory-Domänendiensten (AD DS) gesichert, wenn Sie die Standardeinstellung für die AD DS-Sicherung verwendet haben. Mit diesem Schlüsselpaket dem Wiederherstellungskennwort oder Wiederherstellungsschlüssel können Sie Teile eines mit BitLocker geschützten Laufwerks entschlüsseln, wenn die Festplatte beschädigt ist. Jeder Schlüsselpaket funktioniert nur für ein Laufwerk mit der entsprechenden Laufwerkskennung. Sie können die [BitLocker-Wiederherstellungskennwort-Viewers für Active Directory](https://technet.microsoft.com/library/dd875531(v=ws.10).aspx) dieses Schlüsselpaket aus AD DS abrufen.

> [!NOTE]
> Die BitLocker-Wiederherstellungskennwort-Viewer ist als eines der Features optionale Verwaltungs-installierbare mit Server verwalten, auf Windows Server 2012 enthalten.

Die folgenden Einschränkungen gelten für das Befehlszeilentool Repair-Bde:
-   Repair-Bde kann kein Laufwerk repariert werden, die während des-Verschlüsselung oder Entschlüsselung ist fehlgeschlagen.
-   Repair-Bde wird davon ausgegangen, dass wenn das Laufwerk Verschlüsselung verfügt, klicken Sie dann das Laufwerk vollständig verschlüsselt ist.

Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
repair-bde <InputVolume> <OutputVolumeorImage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<InputVolume>|Gibt den Laufwerkbuchstaben des Laufwerks mit BitLocker verschlüsselte, die Sie reparieren möchten. Der Buchstabe des Laufwerks muss einen Doppelpunkt enthalten. Zum Beispiel: **C:**.|
|\<OutputVolumeorImage>|Identifiziert das Laufwerk auf dem den Inhalt des Laufwerks reparierten gespeichert. Alle Informationen auf dem Laufwerk für die Ausgabe wird überschrieben.|
|-ZS|Identifiziert den Speicherort des Wiederherstellungsschlüssels, die verwendet werden soll, um das Volume zu entsperren. Dieser Befehl kann auch angegeben werden, als **- Recoverykey**.|
|-rp|Identifiziert das numerische Wiederherstellungskennwort, das zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch angegeben werden, als **- Recoverypassword**.|
|-pw|Gibt das Kennwort, das zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch angegeben werden, als **-Kennwort**|
|-kp|Identifiziert das wiederherstellungsschlüsselpaket, das verwendet werden kann, um das Volume zu entsperren. Dieser Befehl kann auch angegeben werden, als **- Keypackage**.|
|-lf|Gibt den Pfad zur Datei, die Fehler, Warn- und informationsmeldungen von Repair-Bde gespeichert werden. Dieser Befehl kann auch angegeben werden, als **- Protokolldatei**.|
|-f|Erzwingt, dass ein Volume, deren Bereitstellung aufgehoben werden, auch wenn es nicht gesperrt werden kann. Dieser Befehl kann auch angegeben werden, als **-erzwingen**.|
|-? oder /?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Wenn der Pfad zu einem Schlüsselpaket nicht angegeben ist, **Repair-Bde** wird das Laufwerk nach einem Schlüsselpaket durchsucht. Jedoch, wenn die Festplatte beschädigt wurde, **Repair-Bde** möglicherweise nicht um das Paket zu finden und werden Sie aufgefordert, den Pfad angeben.

## <a name="BKMK_Examples"></a>Beispiele für

Im folgenden Beispiel wird versucht, reparieren Sie Laufwerk C, und geben Sie den Inhalt von Laufwerk C: auf Laufwerk D mit die wiederherstellungsschlüsseldatei (RecoveryKey.bek), der auf Laufwerk F gespeichert und schreibt die Ergebnisse von dieser Versuch in die Log-Datei (log.txt) auf dem Laufwerk Z.
```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```
Im folgenden Beispiel wird versucht, reparieren Sie Laufwerk C, und geben Sie den Inhalt auf Laufwerk C: auf Laufwerk D mit dem 48-stelligen Wiederherstellungskennworts Kennwort angegeben. Die Eingabe eines Wiederherstellungskennworts sollte durch einen Bindestrich getrennt jeder Block in den acht Blöcken sechs Ziffern eingegeben werden.
```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```
Im folgenden Beispiel erzwingt, dass Laufwerk C, deren Bereitstellung aufgehoben werden und versucht anschließend, reparieren Sie Laufwerk C, und geben Sie den Inhalt auf Laufwerk C: auf Laufwerk D mit dem wiederherstellungsschlüsselpaket und wiederherstellungsschlüsseldatei (RecoveryKey.bek) auf Laufwerk F. gespeichert
```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```
Im folgenden Beispiel wird versucht, reparieren Laufwerk C, und geben Sie den Inhalt von Laufwerk C: auf Laufwerk D, und geben Sie ein Kennwort zum Entsperren des Laufwerks "c:", wenn Sie aufgefordert werden:
```
repair-bde C: D: -pw
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)