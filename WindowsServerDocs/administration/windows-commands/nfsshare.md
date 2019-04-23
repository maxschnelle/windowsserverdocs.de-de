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
ms.openlocfilehash: 50df88a3fddbceb1595f328bdd4e3c6f526e3a2c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881691"
---
# <a name="nfsshare"></a>nfsshare



Sie können **Nfsshare** Network File System (NFS teilt) steuern.

## <a name="syntax"></a>Syntax

```
nfsshare <ShareName>=<Drive:Path> [-o <Option=value>...]
nfsshare {<ShareName> | <Drive>:<Path> | * } /delete
```

## <a name="description"></a>Beschreibung

Ohne Argumente die **Nfsshare** Befehlszeilenprogramm Listet alle Network File System (NFS)-Freigaben, die vom Server für NFS exportiert. Mit *ShareName* als einziges Argument, **Nfsshare** Listet die Eigenschaften von der NFS-Freigabe identifizierte *ShareName*. Wenn *ShareName* und *Laufwerk ***:*** Pfad* zur Verfügung, **Nfsshare** exportiert den Ordner identifizierte *Laufwerk ***:*** Pfad* als *ShareName*. Wenn die **/delete** Option wird verwendet, der angegebene Ordner ist NFS-Clients nicht mehr zur Verfügung gestellt.

## <a name="options"></a>Optionen

Die **Nfsshare** Befehl akzeptiert die folgenden Optionen und Argumente:

|Begriff|Definition|
|----|----------|
|-o anon = {Yes | Keine}|Gibt an, ob anonyme (nicht zugeordneten) Benutzer das freigegebene Verzeichnis zugreifen können. Der Standardwert ist **keine**.|
|-o rw[=\<Host>[:<Host>]...]|Bietet Lese-/ Schreibzugriff auf das freigegebene Verzeichnis von Hosts oder -Client als angegebenen *Host*. Trennen Sie Host und der Gruppenname durch einen Doppelpunkt (**:**). Wenn *Host* nicht angegeben ist, alle Hosts und Clientgruppen (mit Ausnahme angegeben wird, mit der **Ro** Option) Lese-/ Schreibzugriff besitzen. Wenn weder die **Ro** noch die **Rw** -Option festgelegt ist, alle Clients haben Lese-/ Schreibzugriff auf das freigegebene Verzeichnis.|
|-o ro[=\<Host>[:<Host>]...]|Bietet schreibgeschützten Zugriff auf das freigegebene Verzeichnis von Hosts oder -Client als angegebenen *Host*. Trennen Sie Host und der Gruppenname durch einen Doppelpunkt (**:**). Wenn *Host* nicht angegeben ist, alle Clients (mit Ausnahme angegeben wird, mit der **Rw** Option) haben schreibgeschützten Zugriff. Wenn die **Ro** Option wird festgelegt, für einen oder mehrere Clients, aber die **Rw** Option nicht festgelegt ist, nur die Clients, die mit angegebenen die **Ro** Option haben Zugriff auf das freigegebene Verzeichnis.|
|-o-Codierung = {big5|euc-jp|EUC-kr|EUC-tw|gb2312-80|ksc5601|shift-jis}|Die standardcodierung für Datei- und Verzeichnisnamen verwendet und angegeben, wenn verwendet, muss auf eine der folgenden festgelegt werden:</br>-   **Big5** (Chinesisch)</br>-   **EUC-jp** (Japanisch)</br>-   **EUC-Kr** (Koreanisch)</br>-   **EUC-Tw** (Chinesisch)</br>-   **GB2312-80** (Chinesisch (vereinfacht))</br>-   **ksc5601** (Korean)</br>-   **Shift-Jis** (Japanisch)</br>Wenn diese Option ist nicht festgelegt ist, wird das Standard-Codierungsschema ist ANSI oder auf Systemen, die für die nicht englischen Gebietsschemas, die standardcodierung-Schema für das Gebietsschema konfiguriert. Im folgenden finden die Codierung des Standardschemas für die angegebenen Gebietsschemas:</br>– Japanisch: SHIFT-JIS</br>– Koreanisch: KS_C_5601-1987</br>-Chinesisch vereinfacht, Chinesisch: GB2312-80</br>Chinesisch (traditionell): BIG5|
|-o anongid=\<gid>|Gibt an, dass anonyme (nicht zugeordneten) Benutzer der Freigabe dann mit Directory zugreift, *Gid* als Gruppen-ID (GID). Der Standardwert ist-2. Die anonyme GID wird verwendet werden, wenn den Besitzer einer Datei, die im Besitz von einem nicht zugeordneten Benutzer, berichterstellung, selbst wenn der anonyme Zugriff deaktiviert ist.|
|-o  anonuid=\<uid>|Gibt an, dass anonyme (nicht zugeordneten) Benutzer der Freigabe dann mit Directory zugreift, *Uid* als Benutzer-ID (UID). Der Standardwert ist-2. Wenn den Besitzer einer Datei, die im Besitz von einem nicht zugeordneten Benutzer, gemeldet, selbst wenn der anonyme Zugriff deaktiviert ist, wird die anonyme UID verwendet werden.|
|-o root[=\<Host>[:<Host>]...]|Gewährt den Root-Zugriff auf das freigegebene Verzeichnis von Hosts oder -Client angegebenen von *Host*. Trennen Sie Host und der Gruppenname durch einen Doppelpunkt (**:**). Wenn *Host* nicht angegeben ist, alle Clients müssen Root-Zugriff. Wenn die **Stamm** Option nicht festgelegt ist, keine Clients haben den Root-Zugriff auf das freigegebene Verzeichnis.|
|/delete|Wenn *ShareName* oder *Laufwerk ***:*** Pfad* angegeben ist, löscht die angegebene Freigabe. Wenn * angegeben ist, löscht alle NFS-Freigaben.|

> [!NOTE]
> Geben Sie zum Anzeigen der vollständigen Syntax für diesen Befehl an der Eingabeaufforderung Folgendes ein:</br>> **Nfsshare /?**

##

[Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md) Siehe auch