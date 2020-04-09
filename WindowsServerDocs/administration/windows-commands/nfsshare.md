---
title: nfsshare
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 032baaf3013d2658b1040345da3a35cb6a1631f2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838903"
---
# <a name="nfsshare"></a>nfsshare



Sie können **nfsshare** verwenden, um NFS-Freigaben (Network File System) zu steuern.

## <a name="syntax"></a>Syntax

```
nfsshare <ShareName>=<Drive:Path> [-o <Option=value>...]
nfsshare {<ShareName> | <Drive>:<Path> | * } /delete
```

## <a name="description"></a>Beschreibung

Ohne Argumente listet das Befehlszeilen-Hilfsprogramm **nfsshare** alle von Server für NFS exportierten NFS-Freigaben (Network File System) auf. Mit *ShareName* als einziges Argument listet **nfsshare** die Eigenschaften der von *ShareName*identifizierten NFS-Freigabe auf. Wenn *ShareName* und <em>Laufwerk</em> **:** <em>path</em> bereitgestellt werden, exportiert **nfsshare** den von <em>Laufwerk</em> **:** <em>path</em> identifizierten Ordner als *ShareName*. Wenn die **/Delete** -Option verwendet wird, wird der angegebene Ordner nicht mehr für NFS-Clients zur Verfügung gestellt.

## <a name="options"></a>Optionen

Der Befehl **nfsshare** akzeptiert die folgenden Optionen und Argumente:


|             Begriff              |                                                                                                                                                                                                                      Definition                                                                                                                                                                                                                       |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         -o anon = {ja          |                                                                                                                                                                                                                          gar                                                                                                                                                                                                                          |
|  -o RW [=\<Host > [:<Host>]...]  |                       Bietet Lese-/Schreibzugriff auf das freigegebene Verzeichnis durch die Hosts oder Client Gruppen, die vom *Host*angegeben werden. Trennen Sie Host-und Gruppennamen mit einem Doppelpunkt ( **:** ). Wenn kein *Host* angegeben ist, haben alle Hosts und Client Gruppen (außer den mit der Option **RO** angegebenen) Lese-/Schreibzugriff. Wenn weder die **RO** -noch die **RW** -Option festgelegt ist, haben alle Clients Lese-/Schreibzugriff auf das freigegebene Verzeichnis.                       |
|  -o RO [=\<Host > [:<Host>]...]  | Bietet schreibgeschützten Zugriff auf das freigegebene Verzeichnis durch die Hosts oder Client Gruppen, die vom *Host*angegeben werden. Trennen Sie Host-und Gruppennamen mit einem Doppelpunkt ( **:** ). Wenn kein *Host* angegeben ist, haben alle Clients (außer den mit der Option **RW** angegebenen) schreibgeschützten Zugriff. Wenn die Option " **RO** " für mindestens einen Client festgelegt ist, die Option " **RW** " jedoch nicht festgelegt ist, haben nur die mit der Option " **RO** " angegebenen Clients Zugriff auf das freigegebene Verzeichnis. |
|       -o Encoding = {Big5       |                                                                                                                                                                                                                        EUC-JP                                                                                                                                                                                                                         |
|       -o anongid =\<gid >       |                                                                                     Gibt an, dass anonyme (nicht zugeordnete) Benutzer auf das Freigabe Verzeichnis mithilfe von *gid* als Gruppen Bezeichner (GID) zugreifen. Der Standardwert ist-2. Die anonyme gid wird verwendet, wenn der Besitzer einer Datei, die im Besitz eines nicht zugeordneten Benutzers ist, gemeldet wird, auch wenn der anonyme Zugriff deaktiviert ist.                                                                                      |
|      -o anonuid =\<UID >       |                                                                                      Gibt an, dass anonyme (nicht zugeordnete) Benutzer auf das Freigabe Verzeichnis mithilfe von *UID* als Benutzer-ID (UID) zugreifen. Der Standardwert ist-2. Die anonyme UID wird verwendet, wenn der Besitzer einer Datei, die im Besitz eines nicht zugeordneten Benutzers ist, gemeldet wird, auch wenn der anonyme Zugriff deaktiviert ist.                                                                                      |
| -o root [=\<Host > [:<Host>]...] |                                                                         Ermöglicht den Stamm Zugriff auf das freigegebene Verzeichnis durch die Hosts oder Client Gruppen, die durch den *Host*angegeben werden. Trennen Sie Host-und Gruppennamen mit einem Doppelpunkt ( **:** ). Wenn kein *Host* angegeben ist, haben alle Clients root-Zugriff. Wenn die **root** -Option nicht festgelegt ist, haben keine Clients Stamm Zugriff auf das freigegebene Verzeichnis.                                                                         |
|            /delete            |                                                                                                                                                       Wenn *ShareName* oder <em>Laufwerk</em> **:** <em>path</em> angegeben ist, wird die angegebene Freigabe von gelöscht. Wenn \* angegeben wird, löscht alle NFS-Freigaben.                                                                                                                                                       |

> [!NOTE]
> Geben Sie zum Anzeigen der vollständigen Syntax für diesen Befehl an der Eingabeaufforderung Folgendes ein:</br>> **nfsshare/?**

## <a name="see-also"></a>Siehe auch

[Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)