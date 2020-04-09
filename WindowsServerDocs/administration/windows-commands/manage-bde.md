---
title: manage-bde
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 816e20152ec40ce54c1192f3075c6f4556aed3db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839693"
---
# <a name="manage-bde"></a>manage-bde



Dient zum Aktivieren oder Deaktivieren von BitLocker, zum Angeben von entsperrungs Mechanismen, zum Aktualisieren von Wiederherstellungsmethoden und zum Entsperren von mit BitLocker geschützten Daten Laufwerken. Dieses Befehlszeilen Tool kann anstelle des **BitLocker-Laufwerkverschlüsselung** System Steuerungs Elements verwendet werden. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm] 
[–SetIdentifier] [-ForceRecovery] [–changepassword] [–changepin] [–changekey] [-KeyPackage] [–upgrade] [-WipeFreeSpace] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Manage-bde: status](manage-bde-status.md)|Enthält Informationen zu allen Laufwerken auf dem Computer, unabhängig davon, ob Sie durch BitLocker geschützt sind.|
|[Manage-bde: on](manage-bde-on.md)|Verschlüsselt das Laufwerk und schaltet BitLocker ein.|
|[Manage-bde: off](manage-bde-off.md)|Entschlüsselt das Laufwerk und deaktiviert BitLocker. Alle Schlüssel Schutzvorrichtungen werden entfernt, wenn die Entschlüsselung vollständig ist.|
|[Manage-bde: pause](manage-bde-pause.md)|Hält die Verschlüsselung oder Entschlüsselung an.|
|[Manage-bde: resume](manage-bde-resume.md)|Nimmt die Verschlüsselung oder Entschlüsselung wieder auf.|
|[Manage-bde: lock](manage-bde-lock.md)|Verhindert den Zugriff auf durch BitLocker geschützte Daten.|
|[Manage-bde: unlock](manage-bde-unlock.md)|Ermöglicht den Zugriff auf durch BitLocker geschützte Daten mit einem Wiederherstellungs Kennwort oder einem Wiederherstellungs Schlüssel.|
|[Manage-bde: autounlock](manage-bde-autounlock.md)|Verwaltet das automatische Entsperren von Daten Laufwerken.|
|[Manage-bde: protectors](manage-bde-protectors.md)|Verwaltet Schutzmethoden für den Verschlüsselungsschlüssel.|
|[Manage-bde: tpm](manage-bde-tpm.md)|Konfiguriert den Trusted Platform Module des Computers (TPM). Dieser Befehl wird auf Computern, auf denen Windows 8 oder **win8_server_2**ausgeführt wird, nicht unterstützt. Um das TPM auf diesen Computern zu verwalten, verwenden Sie entweder das TPM-Verwaltungs-MMC-Snap-in oder die TPM-Verwaltungs-Cmdlets für Windows PowerShell.|
|[Manage-bde: setidentifier](manage-bde-setidentifier.md)|Legt das Feld Laufwerks-ID auf dem Laufwerk auf den Wert fest, der in der Einstellung **Geben Sie die eindeutigen Bezeichner für Ihre Organisation** Gruppenrichtlinie festgelegt ist.|
|[Manage-bde: forcerecovery](manage-bde-forcerecovery.md)|Erzwingt ein durch BitLocker geschütztes Laufwerk beim Neustart in den Wiederherstellungs Modus. Dieser Befehl löscht alle TPM-bezogenen Schlüsselschutz Vorrichtungen vom Laufwerk. Wenn der Computer neu gestartet wird, kann nur ein Wiederherstellungs Kennwort oder ein Wiederherstellungs Schlüssel verwendet werden, um das Laufwerk zu entsperren.|
|[Manage-bde: changepassword](manage-bde-changepassword.md)|Ändert das Kennwort für ein Daten Laufwerk.|
|[Manage-bde: changepin](manage-bde-changepin.md)|Ändert die PIN für ein Betriebssystem Laufwerk.|
|[Manage-bde: changekey](manage-bde-changekey.md)|Ändert den Systemstart Schlüssel für ein Betriebssystem Laufwerk.|
|[Manage-bde: KeyPackage](manage-bde-keypackage.md)|Generiert ein Schlüssel Paket für ein Laufwerk.|
|[Manage-bde: upgrade](manage-bde-upgrade.md)|Aktualisiert die BitLocker-Version.|
|[Manage-bde: wipeer FreeSpace](manage-bde-wipefreespace.md)|Löscht den freien Speicherplatz auf einem Laufwerk.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung an.|
|-Help oder-h|Zeigt die gesamte Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Im folgenden Beispiel werden die Laufwerke auf dem Computer angezeigt, und es wird ermittelt, ob Sie durch BitLocker geschützt sind, und der aktuelle Verschlüsselungs Status.
```
manage-bde -status
```
Das folgende Beispiel veranschaulicht das Aktivieren von BitLocker auf Laufwerk C mit der Option eines Wiederherstellungs Kennworts. Das Wiederherstellungs Kennwort wird von BitLocker generiert und auf dem Bildschirm angezeigt, sodass Sie es aufzeichnen können.
```
manage-bde –on C: -recoverypassword
```
Im folgenden Beispiel wird veranschaulicht, wie ein durch BitLocker geschütztes Laufwerk mithilfe eines Wiederherstellungs Kennworts entsperrt wird.
```
manage-bde –unlock E: -recoverypassword 111111-222222-333333-444444-555555-666666-777777-888888
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Aktivieren von BitLocker über die Befehlszeile](https://technet.microsoft.com/library/dd894351(v=ws.10).aspx)
