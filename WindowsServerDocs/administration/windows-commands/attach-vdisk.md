---
title: attach vdisk
description: Windows-Befehls Artikel zum **Anfügen von Vdisk-anfügen** (manchmal als "Bereitstellen" oder "Oberflächen" bezeichnet) eine virtuelle Festplatte (VHD), sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d29eacfc8575ec50859733612a3d58b166d9402d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382637"
---
# <a name="attach-vdisk"></a>attach vdisk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wird eine virtuelle Festplatte (auch als Bereitstellung oder Oberfläche bezeichnet) an eine virtuelle Festplatte (VHD) angefügt, sodass Sie auf dem Host Computer als lokales Festplattenlaufwerk angezeigt wird. Wenn die virtuelle Festplatte beim Anfügen bereits über eine Festplattenpartition und ein Dateisystemvolume verfügt, wird dem Volume auf der virtuellen Festplatte ein Laufwerkbuchstabe zugeordnet.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.

## <a name="syntax"></a>Syntax
```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```
### <a name="parameters"></a>Parameter

|    Parameter     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     ReadOnly     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Fügt die VHD als schreibgeschützt an. Bei jedem Schreibvorgang wird ein Fehler zurückgegeben.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| SD = <SDDL string> | Legt den Benutzer Filter auf der VHD fest. Die Filter Zeichenfolge muss im SDDL-Format (Security Descriptor Definition Language) vorliegen. Standardmäßig ermöglicht der Benutzer Filter den Zugriff wie auf einem physischen Datenträger.<br /><br />SDDL-Zeichen folgen können komplex sein, aber in ihrer einfachsten Form wird eine Sicherheits Beschreibung, die den Zugriff schützt, als freigegebene Zugriffs Steuerungs Liste (DACL) bezeichnet. Dies hat folgendes Format: D: < dacl_flags > < string_ace1 > < string_ace2 >... < string_acen ><br /><br />Allgemeine DACL-Flags sind:<br /><br />-   **A** Zugriff zulassen<br />-   **D** Zugriff verweigern<br /><br />Allgemeine Rechte:<br /><br />@no__t **-0 allgemein** verfügbar<br />-   **gr** Lesezugriff<br />-   -**GW** -Schreibzugriff<br /><br />Allgemeine Benutzerkonten:<br /><br />@no__t **-0-** Administratoren, die in Administratoren integriert sind<br />@no__t **-0 Analytics** -authentifizierte Benutzer<br />Besitzer des -   -**mitstellers**<br />-   **WD** -jeder<br /><br />Beispiele:<br /><br />**d:p: (A;; Gr;;; Au** bietet Lesezugriff auf alle authentifizierten Benutzer.<br /><br />**d:p: (A;; GA;;; WD** bietet alle vollen Zugriffs Steuerungs Listen |
|    usefilesd     |                                                                                                                                                                                                                                                                                                                                                                                          Gibt an, dass die Sicherheits Beschreibung der VHD-Datei auf der virtuellen Festplatte verwendet werden soll. Wenn der **usefilesd-** Parameter nicht angegeben wird, verfügt die VHD nicht über eine explizite Sicherheits Beschreibung, es sei denn, Sie wird mit dem **SD** -Parameter angegeben.                                                                                                                                                                                                                                                                                                                                                                                          |
|      Noerr       |                                                                                                                                                                                                                                                                                                                                                                                                           Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Hinweise
- Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.
  ## <a name="BKMK_Examples"></a>Beispiele
  Um die ausgewählte VHD als schreibgeschützt anzufügen, geben Sie Folgendes ein:
  ```
  attach vdisk readonly
  ```
  ## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Compact Vdisk](compact-vdisk.md)

- [Detail-Vdisk](detail-vdisk.md)
- [Vdisk trennen](detach-vdisk.md)
- [Erweitern von Vdisk](expand-vdisk.md)
- [Vdisk zusammenführen](merge-vdisk.md)
- [Vdisk auswählen](select-vdisk.md)
- [list_1](list_1.md)
