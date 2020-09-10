---
title: attach vdisk
description: Referenz Artikel zum Anfügen eines Vdisk-Befehls, der eine virtuelle Festplatte (manchmal auch als Bereitstellung oder Oberfläche bezeichnet) anfügt, sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird.
ms.topic: reference
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: aa94847ceaf4d978d50f0e00d9376c4f6b67691b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633365"
---
# <a name="attach-vdisk"></a>attach vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wird eine virtuelle Festplatte (auch als Bereitstellung oder Oberfläche bezeichnet) an eine virtuelle Festplatte (VHD) angefügt, sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird. Wenn die virtuelle Festplatte beim Anfügen bereits über eine Festplattenpartition und ein Dateisystemvolume verfügt, wird dem Volume auf der virtuellen Festplatte ein Laufwerkbuchstabe zugeordnet.

> [!IMPORTANT]
> Sie müssen eine VHD auswählen und trennen, damit dieser Vorgang erfolgreich ist. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.

## <a name="syntax"></a>Syntax

```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| readonly | Fügt die VHD als schreibgeschützt an. Bei jedem Schreibvorgang wird ein Fehler zurückgegeben. |
| `sd=<SDDL string>` | Legt den Benutzer Filter auf der VHD fest. Die Filter Zeichenfolge muss im SDDL-Format (Security Descriptor Definition Language) vorliegen. Standardmäßig ermöglicht der Benutzer Filter den Zugriff wie auf einem physischen Datenträger. SDDL-Zeichen folgen können komplex sein, aber in ihrer einfachsten Form wird eine Sicherheits Beschreibung, die den Zugriff schützt, als freigegebene Zugriffs Steuerungs Liste (DACL) bezeichnet. Dabei wird das folgende Format verwendet: `D:<dacl_flags><string_ace1><string_ace2>` ... `<string_acen>`<p>Allgemeine DACL-Flags sind:<ul><li>**A**. Zugriff zulassen</li><li>**D**. Zugriff verweigern</li></ul>Allgemeine Rechte:<ul><li>Allgemein **verfügbar.** Alle Zugriffe</li><li>**Gr**. Lesezugriff</li><li> **GW**. Schreibzugriff</li></ul>Allgemeine Benutzerkonten:<ul><li>**BA**. Integrierte Administratoren</li><li>**Au**. Authentifizierte Benutzer</li><li>**CO**. Ersteller-Besitzer</li><li>**WD**. Jeder</li></ul>Beispiele:<ul><li>**d:p: (A;; Gr;;; Au**. Bietet Lesezugriff für alle authentifizierten Benutzer.</li><li>**d:p: (A;; GA;;; WD**. Ermöglicht allen Benutzern Vollzugriff.</li></ul> |
| usefilesd | Gibt an, dass die Sicherheits Beschreibung der VHD-Datei auf der virtuellen Festplatte verwendet werden soll. Wenn der **usefilesd-** Parameter nicht angegeben wird, verfügt die VHD nicht über eine explizite Sicherheits Beschreibung, es sei denn, Sie wird mit dem **SD** -Parameter angegeben. |
| Noerr | Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Um die ausgewählte VHD als schreibgeschützt anzufügen, geben Sie Folgendes ein:

```
attach vdisk readonly
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [select vdisk](select-vdisk.md)

- [compact vdisk](compact-vdisk.md)

- [detail vdisk](detail-vdisk.md)

- [detach vdisk](detach-vdisk.md)

- [expand vdisk](expand-vdisk.md)

- [merge vdisk](merge-vdisk.md)

- [list](./list.md)