---
title: manage-bde on
description: Referenz Artikel für den Befehl manage-bde on, der das Laufwerk verschlüsselt und BitLocker einschaltet.
ms.topic: reference
ms.assetid: f6a12814-df74-416c-a04a-62ea8512263e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9daa975a02f033efee1e9822179d7db709b3a3d5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025294"
---
# <a name="manage-bde-on"></a>manage-bde on

Verschlüsselt das Laufwerk und schaltet BitLocker ein.

## <a name="syntax"></a>Syntax

```
manage-bde –on <drive> {[-recoverypassword <numericalpassword>]|[-recoverykey <pathtoexternaldirectory>]|[-startupkey <pathtoexternalkeydirectory>]|[-certificate]|
[-tpmandpin]|[-tpmandpinandstartupkey <pathtoexternalkeydirectory>]|[-tpmandstartupkey <pathtoexternalkeydirectory>]|[-password]|[-ADaccountorgroup <domain\account>]}
[-usedspaceonly][-encryptionmethod {aes128_diffuser|aes256_diffuser|aes128|aes256}] [-skiphardwaretest] [-discoveryvolumetype <filesystemtype>] [-forceencryptiontype <type>] [-removevolumeshadowcopies][-computername <name>]
[{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -wiederherstellungkennwort | Fügt eine numerische Kennwort-Schutzvorrichtung hinzu. Sie können auch **-RP** als abgekürzte Version dieses Befehls verwenden. |
| `<numericalpassword>` | Stellt das Wiederherstellungs Kennwort dar. |
| -Wiederherstellungsschlüssel | Fügt eine externe Schlüssel Schutzvorrichtung für die Wiederherstellung hinzu. Sie können " **-RK** " auch als abgekürzte Version dieses Befehls verwenden. |
| `<pathtoexternaldirectory>` | Stellt den Verzeichnispfad zum Wiederherstellungs Schlüssel dar. |
| -startupkey | Fügt eine externe Schlüssel Schutzvorrichtung zum Starten hinzu. Sie können auch **-SK** als abgekürzte Version dieses Befehls verwenden. |
| `<pathtoexternalkeydirectory>` | Stellt den Verzeichnispfad zum Systemstart Schlüssel dar. |
| -Zertifikat | Fügt eine Schutzvorrichtung für ein öffentliches Schlüssel für ein Daten Laufwerk hinzu. Sie können auch **-CERT** als abgekürzte Version dieses Befehls verwenden. |
| -TPMAndPIN | Fügt ein Trusted Platform Module (TPM) und eine PIN-Schutzvorrichtung (Personal Identification Number) für das Betriebssystem Laufwerk hinzu. Sie können auch **-tp** als abgekürzte Version dieses Befehls verwenden. |
| -TPMAndStartupKey | Fügt ein TPM und eine Systemstart Schlüssel-Schutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-TSK** als abgekürzte Version dieses Befehls verwenden. |
| -tpmandpinandstartupkey | Fügt ein TPM, eine PIN und eine Start Schlüsselschutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-tpsk** als abgekürzte Version dieses Befehls verwenden. |
| -password | Fügt eine Kenn Wort Schlüssel-Schutzvorrichtung für das Daten Laufwerk hinzu. Sie können auch **-PW** als abgekürzte Version dieses Befehls verwenden. |
| -Adaccountorgroup | Fügt eine SID-basierte Identitäts Schutzvorrichtung für das Volume hinzu. Das Volume wird automatisch entsperrt, wenn der Benutzer oder der Computer über die richtigen Anmelde Informationen verfügt. Wenn Sie ein Computer Konto angeben, fügen **$** Sie einen an den Computernamen an, und geben Sie den **–-Dienst** an, um anzugeben, dass die Sperre im Inhalt des BitLocker-Servers anstelle des Benutzers stattfinden soll. Sie können auch **-sid** als abgekürzte Version dieses Befehls verwenden. |
| -usedspaceonly | Legt den Verschlüsselungs Modus auf "nur verwendeten Speicherplatz verschlüsseln" fest. Die Abschnitte des Volumes, die den verwendeten Speicherplatz enthalten, werden verschlüsselt, aber der freie Speicherplatz wird nicht verwendet. Wenn diese Option nicht angegeben wird, werden der gesamte verwendete Speicherplatz und der freie Speicherplatz auf dem Volume verschlüsselt. Sie können auch **-used** als abgekürzte Version dieses Befehls verwenden. |
| -verschlüsselungsmethod | Konfiguriert den Verschlüsselungsalgorithmus und die Schlüsselgröße. Sie können auch **-EM** als abgekürzte Version dieses Befehls verwenden. |
| -skiphardwaretest | Startet die Verschlüsselung ohne einen Hardware Test. Sie können auch **-s** als abgekürzte Version dieses Befehls verwenden. |
| -discoveryvolumetype | Gibt das Dateisystem an, das für das Discovery-Daten Laufwerk verwendet werden soll. Das Discovery-Daten Laufwerk ist ein verborgenes Laufwerk, das einem FAT-formatierten, BitLocker geschützten Wechsel Datenträger hinzugefügt wird, das die BitLocker To Go-Lesetool enthält. |
| -forceverschlüsseltiontype | Erzwingt, dass BitLocker Software oder Hardware Verschlüsselung verwendet. Sie können entweder **Hardware** oder **Software** als Verschlüsselungstyp angeben. Wenn der **Hardware** Parameter ausgewählt ist, das Laufwerk aber die Hardware Verschlüsselung nicht unterstützt, gibt manage-bde einen Fehler zurück. Wenn Gruppenrichtlinie Einstellungen den angegebenen Verschlüsselungstyp verbietet, gibt manage-bde einen Fehler zurück. Sie können auch **-FET** als abgekürzte Version dieses Befehls verwenden. |
| -removevolumeshadowkopien | Erzwingen Sie das Löschen von Volumeschattenkopien für das Volume. Nachdem Sie diesen Befehl ausgeführt haben, können Sie dieses Volume nicht mithilfe vorheriger System Wiederherstellungspunkte wiederherstellen. Sie können auch **-rvsc** als abgekürzte Version dieses Befehls verwenden. |
| `<filesystemtype>` | Gibt an, welche Dateisysteme mit Ermittlungs Daten Laufwerken verwendet werden können: FAT32, Standard oder None. |
| -Computername | Gibt an, dass "Manage-BDE" verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Aktivieren von BitLocker für Laufwerk C und zum Hinzufügen eines Wiederherstellungs Kennworts zum Laufwerk geben Sie Folgendes ein:

```
manage-bde –on C: -recoverypassword
```

Wenn Sie BitLocker für Laufwerk C aktivieren möchten, fügen Sie dem Laufwerk ein Wiederherstellungs Kennwort hinzu, und geben Sie Folgendes ein, um einen Wiederherstellungs Schlüssel auf Laufwerk E zu speichern:

```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```

Um BitLocker für Laufwerk C zu aktivieren, verwenden Sie eine externe Schlüssel Schutzvorrichtung (z. b. einen USB-Schlüssel), um das Betriebssystem Laufwerk zu entsperren, geben Sie Folgendes ein:

```
manage-bde -on C: -startupkey E:\
```

> [!IMPORTANT]
> Diese Methode ist erforderlich, wenn Sie BitLocker mit Computern verwenden, die nicht über ein TPM verfügen.

Zum Aktivieren von BitLocker für das Daten Laufwerk E und zum Hinzufügen einer Kenn Wort Schlüssel-Schutzvorrichtung geben Sie Folgendes ein:

```
manage-bde –on E: -pw
```

Geben Sie Folgendes ein, um BitLocker für Betriebssystem Laufwerk C zu aktivieren und hardwarebasierte Verschlüsselung zu verwenden:

```
manage-bde –on C: -fet hardware
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "manage-bde Off"](manage-bde-off.md)

- [Befehl "manage-bde Pause"](manage-bde-pause.md)

- [Befehl "manage-bde Resume"](manage-bde-resume.md)

- [Befehl "Manage-BDE"](manage-bde.md)
