---
title: attach vdisk
description: Windows-Befehle Thema **anfügen Vdisk** -fügt (manchmal als Mounts oder Flächen) eine virtuelle Festplatte (VHD), damit es auf dem Hostcomputer als ein lokales Festplattenlaufwerk angezeigt wird.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: fb33d040ce0b2a7a9d06951a7e80251a0d0da614
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435221"
---
# <a name="attach-vdisk"></a>attach vdisk

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt an (manchmal als Mounts oder Flächen) eine virtuelle Festplatte (VHD), damit es auf dem Hostcomputer als ein lokales Festplattenlaufwerk angezeigt wird. Wenn die virtuelle Festplatte beim Anfügen bereits über eine Festplattenpartition und ein Dateisystemvolume verfügt, wird dem Volume auf der virtuellen Festplatte ein Laufwerkbuchstabe zugeordnet.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.

## <a name="syntax"></a>Syntax
```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```
### <a name="parameters"></a>Parameter

|    Parameter     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     ReadOnly     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Fügt an die virtuelle Festplatte im schreibgeschützten Modus. Alle Schreibvorgänge Vorgang gibt einen Fehler.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| sd=<SDDL string> | Legt den Benutzerfilter für die virtuelle Festplatte fest. Die Filterzeichenfolge muss im Format Security Descriptor Definition Language (SDDL) sein. Standardmäßig ermöglicht der Benutzerfilter zugreifen wie auf einem physischen Datenträger an.<br /><br />SDDL-Zeichenfolgen können komplex sein, aber in seiner einfachsten Form wird eine Sicherheitsbeschreibung, die Zugriff geschützt als eine besitzerverwaltete Zugriffssteuerungsliste (DACL) bezeichnet. Er hat folgendes Format: D: < Dacl_flags >< string_ace1 >< string_ace2 >... < String_acen ><br /><br />Allgemeine DACL-Flags sind:<br /><br />-   **Ein** Zugriff zulassen<br />-   **D** Verweigern des Zugriffs<br /><br />Allgemeine Rechte sind:<br /><br />-   **Bei allgemeiner Verfügbarkeit** Vollzugriff<br />-   **GR** Lesezugriff<br />-   **GW** Schreibzugriff<br /><br />Gewöhnliche Benutzerkonten sind:<br /><br />-   **BA** integrierte Administratoren<br />-   **AU** authentifizierte Benutzer<br />-   **CO** Ersteller-Besitzer<br />-   **WD** – alle Benutzer<br /><br />Beispiele:<br /><br />**D:P:(A;; GR;; AU** erhalten Sie Lesezugriff auf alle authentifizierten Benutzer<br /><br />**D:P:(A;; ALLGEMEIN VERFÜGBAR;; WD** ermöglicht allen Mitarbeitern volle rufen |
|    usefilesd     |                                                                                                                                                                                                                                                                                                                                                                                          Gibt an, die die Sicherheitsbeschreibung für die VHD-Datei für die virtuelle Festplatte verwendet werden soll. Wenn die **Usefilesd** Parameter nicht angegeben wird, die virtuelle Festplatte hat keine explizite Sicherheitsbeschreibung, wenn es angegeben wird, mit der **Sd** Parameter.                                                                                                                                                                                                                                                                                                                                                                                          |
|      Diskpart       |                                                                                                                                                                                                                                                                                                                                                                                                           Nur für Skripting verwendet. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.                                                                                                                                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Hinweise
- Eine virtuelle Festplatte muss ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Vdisk** Befehl aus, um die virtuelle Festplatte auswählen, und verschiebt den Fokus auf sie.
  ## <a name="BKMK_Examples"></a>Beispiele für
  Um die ausgewählte virtuelle Festplatte im schreibgeschützten Modus anzufügen, geben Sie Folgendes ein:
  ```
  attach vdisk readonly
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [compact vdisk](compact-vdisk.md)

- [detail vdisk](detail-vdisk.md)
- [Trennen Sie die virtuellen Datenträger](detach-vdisk.md)
- [Erweitern Sie die virtuellen Datenträger](expand-vdisk.md)
- [Zusammenführen von virtuellen Datenträger](merge-vdisk.md)
- [select vdisk](select-vdisk.md)
- [list_1](list_1.md)
