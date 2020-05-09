---
title: Dfsdiag Testsites
description: Referenz Thema für Dfsdiag Testsites, das die Konfiguration der Active Directory-Domänen Dienste-Standorte (AD DS) überprüft, indem überprüft wird, ob Server, die als Namespace Server oder Ordner (Verknüpfungs Ziele) fungieren, auf allen Domänen Controllern über die gleichen Standort Zuordnungen verfügen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54eb7c7ec44d7cd4872960ca29cd3146b710f472
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992852"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag Testsites

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit wird die Konfiguration der Active Directory-Domänen Dienste (AD DS) überprüft, indem überprüft wird, ob Server, die als Namespace Server oder Ordner (Verknüpfungs Ziele) fungieren, auf allen Domänen Controllern über dieselben Standort Zuordnungen verfügen.

## <a name="syntax"></a>Syntax

```
dfsdiag /testsites </machine:<server name>| /DFSpath:<namespace root or DFS folder> [/recurse]> [/full]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/machine:<server name>` | Der Name des Servers, auf dem die Standort Zuordnung überprüft werden soll. |
| `/DFSpath:<namespace root or DFS folder>` | Der Namespace Stamm oder verteiltes Dateisystem Ordner (DFS) (Link) mit Zielen, für die die Standort Zuordnung überprüft werden soll. |
| /recurse | Listet die Site Zuordnungen für alle Ordner Ziele unter dem angegebenen Namespace Stamm auf und überprüft sie. |
| /full | Überprüft, ob AD DS und die Registrierung des-Servers dieselben Standort Zuordnungs Informationen enthalten. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Standort Zuordnungen auf *machine\myserver*zu überprüfen:

```
dfsdiag /testsites /machine:MyServer
```

Wenn Sie einen verteiltes Dateisystem Ordner (DFS) überprüfen möchten, um die Standort Zuordnung zu überprüfen, und überprüfen, ob AD DS und die Registrierung des Servers dieselben Standort Zuordnungs Informationen enthalten, geben Sie Folgendes ein:

```
dfsdiag /TestSites /DFSpath:\\contoso.com\namespace1\folder1 /full
```

Um einen Namespace Stamm zum Überprüfen der Standort Zuordnung zu überprüfen und die Standort Zuordnungen für alle Ordner Ziele unter dem angegebenen Namespace Stamm aufzulisten und zu überprüfen, geben Sie Folgendes ein, um zu überprüfen, ob AD DS und die Registrierung des Servers dieselben Standort Zuordnungs Informationen enthalten:

```
dfsdiag /testsites /DFSpath:\\contoso.com\namespace2 /recurse /full
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dfsdiag-Befehl](dfsdiag.md)
