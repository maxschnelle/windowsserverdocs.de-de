---
title: manage-bde
description: Referenz Artikel zum Befehl "Manage-BDE", mit dem BitLocker eingeschaltet oder deaktiviert wird, das Entsperren von Mechanismen, das Aktualisieren von Wiederherstellungsmethoden und das Aufheben der Sperre von BitLocker-geschützten Daten Laufwerken.
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1d910f9787d2a952a5e844c4aedb3d4c5ca53fa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886565"
---
# <a name="manage-bde"></a>manage-bde

Schaltet BitLocker ein oder aus, gibt die entsperrungs Mechanismen an, aktualisiert Wiederherstellungsmethoden und entsperrt BitLocker-geschützte Daten Laufwerke.

> [!NOTE]
> Dieses Befehlszeilen Tool kann anstelle des **BitLocker-Laufwerkverschlüsselung** System Steuerungs Elements verwendet werden.

## <a name="syntax"></a>Syntax

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm]
[–setidentifier] [-forcerecovery] [–changepassword] [–changepin] [–changekey] [-keypackage] [–upgrade] [-wipefreespace] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- |------------ |
| [manage-bde-Status](manage-bde-status.md) | Enthält Informationen zu allen Laufwerken auf dem Computer, unabhängig davon, ob Sie durch BitLocker geschützt sind. |
| [manage-bde on](manage-bde-on.md) | Verschlüsselt das Laufwerk und schaltet BitLocker ein. |
| [manage-bde Off](manage-bde-off.md) | Entschlüsselt das Laufwerk und deaktiviert BitLocker. Alle Schlüssel Schutzvorrichtungen werden entfernt, wenn die Entschlüsselung vollständig ist. |
| [manage-bde Pause](manage-bde-pause.md) | Hält die Verschlüsselung oder Entschlüsselung an. |
| [manage-bde Resume](manage-bde-resume.md) | Nimmt die Verschlüsselung oder Entschlüsselung wieder auf. |
| [manage-bde-Sperre](manage-bde-lock.md) | Verhindert den Zugriff auf durch BitLocker geschützte Daten. |
| ["manage-bde Unlock"](manage-bde-unlock.md) | Ermöglicht den Zugriff auf durch BitLocker geschützte Daten mit einem Wiederherstellungs Kennwort oder einem Wiederherstellungs Schlüssel. |
| [manage-bde Entsperrens](manage-bde-autounlock.md) | Verwaltet das automatische Entsperren von Daten Laufwerken. |
| [manage-bde-Schutzvorrichtungen](manage-bde-protectors.md) | Verwaltet Schutzmethoden für den Verschlüsselungsschlüssel. |
| [manage-bde TPM](manage-bde-tpm.md) | Konfiguriert den Trusted Platform Module des Computers (TPM). Dieser Befehl wird nicht auf Computern unterstützt, auf denen Windows 8 oder **win8_server_2**ausgeführt wird. Um das TPM auf diesen Computern zu verwalten, verwenden Sie entweder das TPM-Verwaltungs-MMC-Snap-in oder die TPM-Verwaltungs-Cmdlets für Windows PowerShell. |
| [manage-bde-Spezifizierer](manage-bde-setidentifier.md)   | Legt das Feld Laufwerks-ID auf dem Laufwerk auf den Wert fest, der in der Einstellung **Geben Sie die eindeutigen Bezeichner für Ihre Organisation** Gruppenrichtlinie festgelegt ist. |
| [manage-bde forcerecovery](manage-bde-forcerecovery.md) | Erzwingt ein durch BitLocker geschütztes Laufwerk beim Neustart in den Wiederherstellungs Modus. Dieser Befehl löscht alle TPM-bezogenen Schlüsselschutz Vorrichtungen vom Laufwerk. Wenn der Computer neu gestartet wird, kann nur ein Wiederherstellungs Kennwort oder ein Wiederherstellungs Schlüssel verwendet werden, um das Laufwerk zu entsperren. |
| [manage-bde ChangePassword](manage-bde-changepassword.md) | Ändert das Kennwort für ein Daten Laufwerk. |
| [manage-bde changepin](manage-bde-changepin.md) | Ändert die PIN für ein Betriebssystem Laufwerk. |
| [manage-bde ChangeKey](manage-bde-changekey.md) | Ändert den Systemstart Schlüssel für ein Betriebssystem Laufwerk. |
| [manage-bde KeyPackage](manage-bde-keypackage.md) | Generiert ein Schlüssel Paket für ein Laufwerk. |
| [manage-bde-Upgrade](manage-bde-upgrade.md) | Aktualisiert die BitLocker-Version. |
| [manage-bde wipeer FreeSpace](manage-bde-wipefreespace.md) | Löscht den freien Speicherplatz auf einem Laufwerk. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Aktivieren von BitLocker über die Befehlszeile](/previous-versions/windows/it-pro/windows-7/dd894351(v=ws.10))
