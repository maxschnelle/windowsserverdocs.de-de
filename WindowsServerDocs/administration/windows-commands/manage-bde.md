---
title: manage-bde
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8923177b03f378f8252c532ec386f1808e516e1e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874501"
---
# <a name="manage-bde"></a>manage-bde



Geben Sie zum Aktivieren oder Deaktivieren von BitLocker verwendet, Mechanismen zum Entsperren, Wiederherstellungsmethoden zu aktualisieren und BitLocker-geschützte Laufwerke zu entsperren. Dieses Befehlszeilentool kann verwendet werden, anstelle von der **BitLocker Drive Encryption** Control Panel-Element. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm] 
[–SetIdentifier] [-ForceRecovery] [–changepassword] [–changepin] [–changekey] [-KeyPackage] [–upgrade] [-WipeFreeSpace] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Verwalten von-Bde: Status](manage-bde-status.md)|Erläutert alle Laufwerke auf dem Computer, und zwar unabhängig davon, ob sie BitLocker geschützt sind.|
|[Verwalten von-Bde: auf](manage-bde-on.md)|Das Laufwerk verschlüsselt, und BitLocker aktiviert.|
|[Verwalten von-Bde: deaktiviert](manage-bde-off.md)|Das Laufwerk entschlüsselt und BitLocker deaktiviert. Alle Schlüsselschutzvorrichtungen werden entfernt, wenn die Entschlüsselung abgeschlossen ist.|
|[Verwalten von-Bde: anhalten](manage-bde-pause.md)|Hält die Verschlüsselung oder Entschlüsselung.|
|[Verwalten von-Bde: fortsetzen](manage-bde-resume.md)|Setzt die Verschlüsselung oder Entschlüsselung.|
|[Verwalten von-Bde: Sperren](manage-bde-lock.md)|Verhindert den Zugriff auf BitLocker-geschützte Daten.|
|[Verwalten von-Bde: nicht entsperren](manage-bde-unlock.md)|Ermöglicht den Zugriff auf BitLocker-geschützte Daten mit einer Wiederherstellungskennwort oder einen Wiederherstellungsschlüssel.|
|[Verwalten von-Bde: automatisches Entsperren](manage-bde-autounlock.md)|Verwaltet das automatische Entsperren von Datenträgern.|
|[Verwalten von-Bde: IRM-Schutz](manage-bde-protectors.md)|Verwaltet Schutzmethoden für den Verschlüsselungsschlüssel an.|
|[Verwalten von-Bde: Tpm](manage-bde-tpm.md)|Konfiguriert den Computer Trusted Platform Module (TPM). Mit diesem Befehl wird auf Computern mit Windows 8 nicht unterstützt oder **win8_server_2**. Um das TPM auf diesen Computern zu verwalten, verwenden Sie das TPM Management MMC-Snap-in oder den TPM-Verwaltungs-Cmdlets für Windows PowerShell.|
|[Verwalten von-Bde: Setidentifier](manage-bde-setidentifier.md)|Legt das Bezeichnerfeld Laufwerk auf dem Laufwerk, auf die im angegebenen Wert der **Geben Sie die eindeutigen Bezeichner für Ihre Organisation** gruppenrichtlinieneinstellung.|
|[Verwalten von-Bde: ForceRecovery](manage-bde-forcerecovery.md)|Erzwingt, dass ein mit BitLocker geschütztes Laufwerk in den Wiederherstellungsmodus beim Neustart. Dieser Befehl löscht alle TPM-bezogenen Schlüsselschutzvorrichtungen aus dem Laufwerk. Wenn der Computer neu gestartet wird, kann nur ein Wiederherstellungskennwort oder Wiederherstellungsschlüssel zum Entsperren des Laufwerks verwendet werden.|
|[Verwalten von-Bde: Changepassword](manage-bde-changepassword.md)|Ändert das Kennwort für ein Laufwerk an.|
|[Verwalten von-Bde: "changepin" werden](manage-bde-changepin.md)|Ändert die PIN für ein Betriebssystemlaufwerk.|
|[Verwalten von-Bde: Changekey](manage-bde-changekey.md)|Ändert den Systemstartschlüssel für ein Betriebssystemlaufwerk.|
|[Verwalten von-Bde: KeyPackage](manage-bde-keypackage.md)|Generiert ein Schlüsselpaket für ein Laufwerk an.|
|[Verwalten von-Bde: Aktualisieren](manage-bde-upgrade.md)|Die BitLocker-Version aktualisiert.|
|[Verwalten von-Bde: WipeFreeSpace](manage-bde-wipefreespace.md)|Setzt den freien Speicherplatz auf einem Laufwerk zurück.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel zeigt die Laufwerke auf dem Computer, und identifiziert, ob sie BitLocker geschützt sind und den aktuellen Verschlüsselungsstatus.
```
manage-bde -status
```
Das folgende Beispiel veranschaulicht das Aktivieren von BitLocker auf Laufwerk C mit der Option ein Wiederherstellungskennwort. Die Eingabe eines Wiederherstellungskennworts durch BitLocker generiert und auf dem Bildschirm angezeigt werden, sodass Sie diese erfassen können.
```
manage-bde –on C: -recoverypassword
```
Das folgende Beispiel veranschaulicht ein mit BitLocker geschütztes Laufwerk mit einer Wiederherstellungskennwort entsperren.
```
manage-bde –unlock E: -recoverypassword 111111-222222-333333-444444-555555-666666-777777-888888
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Aktivieren von BitLocker über die Befehlszeile](https://technet.microsoft.com/library/dd894351(v=ws.10).aspx)
