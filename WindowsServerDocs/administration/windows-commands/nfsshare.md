---
title: nfsshare
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc77825d63875861839ecdb22bee5a62375aaa13
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437038"
---
# <a name="nfsshare"></a>nfsshare



Sie können **Nfsshare** Network File System (NFS teilt) steuern.

## <a name="syntax"></a>Syntax

```
nfsshare <ShareName>=<Drive:Path> [-o <Option=value>...]
nfsshare {<ShareName> | <Drive>:<Path> | * } /delete
```

## <a name="description"></a>Beschreibung

Ohne Argumente die **Nfsshare** Befehlszeilenprogramm Listet alle Network File System (NFS)-Freigaben, die vom Server für NFS exportiert. Mit *ShareName* als einziges Argument, **Nfsshare** Listet die Eigenschaften von der NFS-Freigabe identifizierte *ShareName*. Wenn *ShareName* und <em>Laufwerk</em> **:** <em>Pfad</em> zur Verfügung, **Nfsshare** exportiert den Ordner identifizierte <em>Laufwerk</em> **:** <em>Pfad</em> als *ShareName*. Wenn die **/delete** Option wird verwendet, der angegebene Ordner ist NFS-Clients nicht mehr zur Verfügung gestellt.

## <a name="options"></a>Optionen

Die **Nfsshare** Befehl akzeptiert die folgenden Optionen und Argumente:


|             Begriff              |                                                                                                                                                                                                                      Definition                                                                                                                                                                                                                       |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         -o anon = {Yes          |                                                                                                                                                                                                                          Keine}                                                                                                                                                                                                                          |
|  -o rw[=\<Host>[:<Host>]...]  |                       Bietet Lese-/ Schreibzugriff auf das freigegebene Verzeichnis von Hosts oder -Client als angegebenen *Host*. Trennen Sie Host und der Gruppenname durch einen Doppelpunkt ( **:** ). Wenn *Host* nicht angegeben ist, alle Hosts und Clientgruppen (mit Ausnahme angegeben wird, mit der **Ro** Option) Lese-/ Schreibzugriff besitzen. Wenn weder die **Ro** noch die **Rw** -Option festgelegt ist, alle Clients haben Lese-/ Schreibzugriff auf das freigegebene Verzeichnis.                       |
|  -o ro[=\<Host>[:<Host>]...]  | Bietet schreibgeschützten Zugriff auf das freigegebene Verzeichnis von Hosts oder -Client als angegebenen *Host*. Trennen Sie Host und der Gruppenname durch einen Doppelpunkt ( **:** ). Wenn *Host* nicht angegeben ist, alle Clients (mit Ausnahme angegeben wird, mit der **Rw** Option) haben schreibgeschützten Zugriff. Wenn die **Ro** Option wird festgelegt, für einen oder mehrere Clients, aber die **Rw** Option nicht festgelegt ist, nur die Clients, die mit angegebenen die **Ro** Option haben Zugriff auf das freigegebene Verzeichnis. |
|       -o-Codierung = {big5       |                                                                                                                                                                                                                        euc-jp                                                                                                                                                                                                                         |
|       -o anongid=\<gid>       |                                                                                     Gibt an, dass anonyme (nicht zugeordneten) Benutzer der Freigabe dann mit Directory zugreift, *Gid* als Gruppen-ID (GID). Der Standardwert ist-2. Die anonyme GID wird verwendet werden, wenn den Besitzer einer Datei, die im Besitz von einem nicht zugeordneten Benutzer, berichterstellung, selbst wenn der anonyme Zugriff deaktiviert ist.                                                                                      |
|      -o  anonuid=\<uid>       |                                                                                      Gibt an, dass anonyme (nicht zugeordneten) Benutzer der Freigabe dann mit Directory zugreift, *Uid* als Benutzer-ID (UID). Der Standardwert ist-2. Wenn den Besitzer einer Datei, die im Besitz von einem nicht zugeordneten Benutzer, gemeldet, selbst wenn der anonyme Zugriff deaktiviert ist, wird die anonyme UID verwendet werden.                                                                                      |
| -o root[=\<Host>[:<Host>]...] |                                                                         Gewährt den Root-Zugriff auf das freigegebene Verzeichnis von Hosts oder -Client angegebenen von *Host*. Trennen Sie Host und der Gruppenname durch einen Doppelpunkt ( **:** ). Wenn *Host* nicht angegeben ist, alle Clients müssen Root-Zugriff. Wenn die **Stamm** Option nicht festgelegt ist, keine Clients haben den Root-Zugriff auf das freigegebene Verzeichnis.                                                                         |
|            /delete            |                                                                                                                                                       Wenn *ShareName* oder <em>Laufwerk</em> **:** <em>Pfad</em> angegeben ist, löscht die angegebene Freigabe. Wenn \* angegeben ist, löscht alle NFS-Freigaben.                                                                                                                                                       |

> [!NOTE]
> Geben Sie zum Anzeigen der vollständigen Syntax für diesen Befehl an der Eingabeaufforderung Folgendes ein:</br>> **Nfsshare /?**

# #

[Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md) Siehe auch