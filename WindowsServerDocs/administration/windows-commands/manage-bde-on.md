---
title: Verwalten von-Bde auf
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b50cad64025e85824a8f0a27d773ffb614491fe5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841181"
---
# <a name="manage-bde-on"></a>Verwalten von-Bde: auf



Das Laufwerk verschlüsselt, und BitLocker aktiviert. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

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
|\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-recoverypassword|Fügt eine Schutzvorrichtung numerisches Kennwort hinzu. Sie können auch **- Rp** als eine verkürzte Version des mit diesem Befehl.|
|\<NumericalPassword>|Stellt die Eingabe eines Wiederherstellungskennworts dar.|
|-recoverykey|Fügt eine externe Schlüsselschutzvorrichtung für die Wiederherstellung an. Sie können auch **- Rk** als eine verkürzte Version des mit diesem Befehl.|
|\<PathToExternalDirectory>|Stellt den Verzeichnispfad für den Wiederherstellungsschlüssel dar.|
|-Startschlüssel|Fügt eine externe Schlüsselschutzvorrichtung für den Start. Sie können auch **-sk** als eine verkürzte Version des mit diesem Befehl.|
|\<PathToExternalKeyDirectory>|Stellt den Verzeichnispfad für den Schlüssel zum Systemstart dar.|
|-Zertifikat|Fügt einer öffentlichen Schlüsselschutzvorrichtung für ein Laufwerk hinzu. Sie können auch **-Cert** als eine verkürzte Version des mit diesem Befehl.|
|-tpmandpin|Fügt ein Trusted Platform Module (TPM) und das personal Identification Number (PIN)-Schutzvorrichtung für das Betriebssystemlaufwerk. Sie können auch **- Tp** als eine verkürzte Version des mit diesem Befehl.|
|-tpmandstartupkey|Fügt eine TPM- und -Systemstart-Schlüsselschutzvorrichtung für das Betriebssystemlaufwerk. Sie können auch **-tsk** als eine verkürzte Version des mit diesem Befehl.|
|-tpmandpinandstartupkey|Fügt eine TPM-PIN und Startup-Schlüsselschutzvorrichtung für das Betriebssystemlaufwerk. Sie können auch **- Tpsk** als eine verkürzte Version des mit diesem Befehl.|
|-Kennwort|Fügt eine Kennwort-Schlüsselschutzvorrichtung für das Datenlaufwerk an. Sie können auch **- kW** als eine verkürzte Version des mit diesem Befehl.|
|-ADAccountOrGroup|Fügt ein SID-basierte Identitätsschutz für das Volume an. Das Volume wird automatisch entsperrt, wenn der Benutzer oder Computer die richtigen Anmeldeinformationen verfügt. Wenn Sie ein Benutzerkonto angeben, fügen Sie eine **$** auf dem Computer ein, und geben **– Dienst** um anzugeben, dass die Sperre im Inhalt des BitLocker-Servers anstelle von geschehen soll die der Benutzer. Sie können auch **-Sid** als eine verkürzte Version des mit diesem Befehl.|
|-UsedSpaceOnly|Legt den Verschlüsselungsmodus nur verwendeten Speicherplatz Verschlüsselung fest. Die Abschnitte des verwendeten Speicherplatzes mit Volumes verschlüsselt werden, aber nicht der Fall ist des freien Speicherplatzes. Wenn diese Option nicht angegeben ist, alle verwendeter Speicherplatz und freier Speicherplatz auf dem Volume verschlüsselt werden... Sie können auch **-verwendet** als eine verkürzte Version des mit diesem Befehl.|
|-encryptionMethod|Konfiguriert die Verschlüsselung Algorithmus und Schlüssel-Größe. Sie können auch **-Em** als eine verkürzte Version des mit diesem Befehl.|
|-skiphardwaretest|Beginnt die Verschlüsselung, ohne dass ein Hardwaretest. Sie können auch **-s** als eine verkürzte Version des mit diesem Befehl.|
|-discoveryvolumetype|Gibt an, das Dateisystem für das Discovery-Datenlaufwerk zu verwenden. Das Datenlaufwerk Discovery ist ein ausgeblendetes Laufwerk hinzugefügt werden, auf einem FAT-formatierten, BitLocker-geschützte Wechseldatenträger, der die BitLocker To Go-Lesetool enthält, damit Windows Vista oder Windows XP-Betriebssystemen verwendet werden kann, um BitLocker-geschützte Laufwerke anzuzeigen.|
|-ForceEncryptionType|Erzwingt, dass BitLocker, Software oder Hardware-Verschlüsselung zu verwenden. Geben Sie entweder **Hardware** oder **Software** als Verschlüsselungstyp. Wenn die **Hardware** Parameter ausgewählt ist, aber das Laufwerk unterstützt keine Verschlüsselung, verwalten-Bde gibt einen Fehler zurück. Wenn die gruppenrichtlinieneinstellungen verbietet den angegebenen Verschlüsselungstyp an, von verwalten-Bde ein Fehler zurückgegeben. Sie können auch **-fet** als eine verkürzte Version des mit diesem Befehl.|
|-RemoveVolumeShadowCopies|Erzwingen von Volumeschattenkopien Deletikon, für das Volume an. Sie werden nicht zum Wiederherstellen dieses Volumes, die mit vorherigen Systemwiederherstellungspunkte nach dem Ausführen dieses Befehls können. Sie können auch **- Rvsc** als eine verkürzte Version des mit diesem Befehl.|
|\<FileSystemType>|Gibt an, welche Dateisysteme mit Datenlaufwerken für die Ermittlung verwendet werden können: FAT32, Standard oder none.|
|-computername|Gibt an, dass die Manage-Bde verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **-auf** Befehl zum Aktivieren von BitLocker für Laufwerk C: und fügen ein Wiederherstellungskennwort, das auf das Laufwerk.
```
manage-bde –on C: -recoverypassword
```
Das folgende Beispiel veranschaulicht die Verwendung der **-auf** Befehl zum Aktivieren von BitLocker für Laufwerk C, fügen ein Wiederherstellungskennwort, das auf das Laufwerk und speichern einen Wiederherstellungsschlüssel auf Laufwerk e:.
```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```
Das folgende Beispiel veranschaulicht die Verwendung der **-auf** Befehl zum Aktivieren von BitLocker für Laufwerk C: mit einer externen Schlüsselschutzvorrichtung (z. B. einen USB-Schlüssel) um das Betriebssystemlaufwerk zu entsperren. Diese Methode ist erforderlich, wenn Sie BitLocker mit Computern verwenden, die nicht über ein TPM verfügen.
```
manage-bde -on C: -startupkey E:\
```
Das folgende Beispiel veranschaulicht die Verwendung der **-auf** Befehl zum Aktivieren von BitLocker für Laufwerk E und Hinzufügen einer Kennwort-Schlüsselschutzvorrichtung. Verwalten von-Bde werden Sie aufgefordert, das Kennwort eingeben, nachdem dieser Befehl eingegeben wurden.
```
manage-bde –on E: -pw
```
Das folgende Beispiel veranschaulicht die Verwendung der **-auf** Befehl zum Aktivieren von BitLocker für Betriebssystem-Laufwerk C: und hardwarebasierten Verschlüsselung verwenden.
```
manage-bde –on C: -fet Hardware
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)