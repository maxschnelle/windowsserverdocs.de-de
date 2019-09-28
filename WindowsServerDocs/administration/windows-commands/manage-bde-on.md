---
title: manage-bde on
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6a12814-df74-416c-a04a-62ea8512263e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a95bbc375c0a5b62b96f7c68f7d5ab5e09371d1c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374001"
---
# <a name="manage-bde-on"></a>manage-bde: on



Verschlüsselt das Laufwerk und schaltet BitLocker ein. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde –on <Drive> {[-recoveryPassword <NumericalPassword>]|[-recoverykey <PathToExternalDirectory>]|[-startupkey <PathToExternalKeyDirectory>]|[-certificate]|
[-tpmandpin]|[-tpmandpinandstartupkey <PathToExternalKeyDirectory>]|[-tpmandstartupkey <PathToExternalKeyDirectory>]|[-password]|[-ADAccountOrGroup <Domain\Account>]}
[-UsedSpaceOnly][-encryptionmethod {aes128_diffuser|aes256_diffuser|aes128|aes256}] [-skiphardwaretest] [-discoveryvolumetype <FileSystemType>] [-ForceEncryptionType <type>] [-RemoveVolumeShadowCopies][-computername <Name>] 
[{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<laufwerk >|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-wiederherstellungkennwort|Fügt eine numerische Kennwort-Schutzvorrichtung hinzu. Sie können auch **-RP** als abgekürzte Version dieses Befehls verwenden.|
|\<numericalpassword >|Stellt das Wiederherstellungs Kennwort dar.|
|-Wiederherstellungsschlüssel|Fügt eine externe Schlüssel Schutzvorrichtung für die Wiederherstellung hinzu. Sie können " **-RK** " auch als abgekürzte Version dieses Befehls verwenden.|
|\<path>|Stellt den Verzeichnispfad zum Wiederherstellungs Schlüssel dar.|
|-startupkey|Fügt eine externe Schlüssel Schutzvorrichtung zum Starten hinzu. Sie können auch **-SK** als abgekürzte Version dieses Befehls verwenden.|
|\<path>|Stellt den Verzeichnispfad zum Systemstart Schlüssel dar.|
|-Zertifikat|Fügt eine Schutzvorrichtung für ein öffentliches Schlüssel für ein Daten Laufwerk hinzu. Sie können auch **-CERT** als abgekürzte Version dieses Befehls verwenden.|
|-TPMAndPIN|Fügt ein Trusted Platform Module (TPM) und eine PIN-Schutzvorrichtung (Personal Identification Number) für das Betriebssystem Laufwerk hinzu. Sie können auch **-tp** als abgekürzte Version dieses Befehls verwenden.|
|-TPMAndStartupKey|Fügt ein TPM und eine Systemstart Schlüssel-Schutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-TSK** als abgekürzte Version dieses Befehls verwenden.|
|-tpmandpinandstartupkey|Fügt ein TPM, eine PIN und eine Start Schlüsselschutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-tpsk** als abgekürzte Version dieses Befehls verwenden.|
|-Kennwort|Fügt eine Kenn Wort Schlüssel-Schutzvorrichtung für das Daten Laufwerk hinzu. Sie können auch **-PW** als abgekürzte Version dieses Befehls verwenden.|
|-ADAccountOrGroup|Fügt eine SID-basierte Identitäts Schutzvorrichtung für das Volume hinzu. Das Volume wird automatisch entsperrt, wenn der Benutzer oder der Computer über die richtigen Anmelde Informationen verfügt. Wenn Sie ein Computer Konto angeben, fügen Sie einen **$** an den Computernamen an, und geben Sie den **–-Dienst** an, um anzugeben, dass die Sperre im Inhalt des BitLocker-Servers anstelle des Benutzers stattfinden soll. Sie können auch **-sid** als abgekürzte Version dieses Befehls verwenden.|
|-UsedSpaceOnly|Legt den Verschlüsselungs Modus auf "nur verwendeten Speicherplatz verschlüsseln" fest. Die Abschnitte des Volumes, die den verwendeten Speicherplatz enthalten, werden verschlüsselt, aber der freie Speicherplatz wird nicht verwendet. Wenn diese Option nicht angegeben wird, werden der gesamte verwendete Speicherplatz und der freie Speicherplatz auf dem Volume verschlüsselt. Sie können auch **-used** als abgekürzte Version dieses Befehls verwenden.|
|-verschlüsselungsmethod|Konfiguriert den Verschlüsselungsalgorithmus und die Schlüsselgröße. Sie können auch **-EM** als abgekürzte Version dieses Befehls verwenden.|
|-skiphardwaretest|Startet die Verschlüsselung ohne einen Hardware Test. Sie können auch **-s** als abgekürzte Version dieses Befehls verwenden.|
|-discoveryvolumetype|Gibt das Dateisystem an, das für das Discovery-Daten Laufwerk verwendet werden soll. Das Discovery Data Drive ist ein verborgenes Laufwerk, das einem FAT-formatierten, BitLocker geschützten Wechsel Datenträger hinzugefügt wird, der die BitLocker To Go-Lesetool enthält, damit die Betriebssysteme Windows Vista oder Windows XP zum Anzeigen von BitLocker-geschützten Laufwerken verwendet werden können.|
|-Forceverschlüsseltiontype|Erzwingt, dass BitLocker Software oder Hardware Verschlüsselung verwendet. Sie können entweder **Hardware** oder **Software** als Verschlüsselungstyp angeben. Wenn der **Hardware** Parameter ausgewählt ist, das Laufwerk aber die Hardware Verschlüsselung nicht unterstützt, gibt manage-bde einen Fehler zurück. Wenn Gruppenrichtlinie Einstellungen den angegebenen Verschlüsselungstyp verbietet, gibt manage-bde einen Fehler zurück. Sie können auch **-FET** als abgekürzte Version dieses Befehls verwenden.|
|-Removevolumeshadowkopien|Erzwingen Sie das Delta der Volumeschattenkopie für das Volume. Nachdem Sie diesen Befehl ausgeführt haben, können Sie dieses Volume nicht mithilfe vorheriger System Wiederherstellungspunkte wiederherstellen. Sie können auch **-rvsc** als abgekürzte Version dieses Befehls verwenden.|
|\<filesystemtype >|Gibt an, welche Dateisysteme mit Ermittlungs Daten Laufwerken verwendet werden können: FAT32, Default oder None.|
|-Computername|Gibt an, dass "Manage-BDE" verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.|
|\<Name >|Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele

Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-on** " zum Aktivieren von BitLocker für Laufwerk C und zum Hinzufügen eines Wiederherstellungs Kennworts zum Laufwerk.
```
manage-bde –on C: -recoverypassword
```
Das folgende Beispiel veranschaulicht die Verwendung des Befehls " **-on** " zum Aktivieren von BitLocker für Laufwerk C, zum Hinzufügen eines Wiederherstellungs Kennworts zum Laufwerk und zum Speichern eines Wiederherstellungs Schlüssels auf Laufwerk E.
```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```
Das folgende Beispiel veranschaulicht die Verwendung des **-on-** Befehls zum Aktivieren von BitLocker für Laufwerk C mit einer externen Schlüssel Schutzvorrichtung (z. b. einem USB-Schlüssel) zum Entsperren des Betriebssystem Laufwerks. Diese Methode ist erforderlich, wenn Sie BitLocker mit Computern verwenden, die nicht über ein TPM verfügen.
```
manage-bde -on C: -startupkey E:\
```
Das folgende Beispiel veranschaulicht die Verwendung des **-on-** Befehls zum Aktivieren von BitLocker für das Daten Laufwerk E und zum Hinzufügen einer Kenn Wort Schlüssel-Schutzvorrichtung. Mit manage-bde werden Sie aufgefordert, das Kennwort einzugeben, nachdem dieser Befehl eingegeben wurde.
```
manage-bde –on E: -pw
```
Das folgende Beispiel veranschaulicht die Verwendung des **-on-** Befehls zum Aktivieren von BitLocker für das Betriebssystem Laufwerk C und zum Verwenden der hardwarebasierten Verschlüsselung.
```
manage-bde –on C: -fet Hardware
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)