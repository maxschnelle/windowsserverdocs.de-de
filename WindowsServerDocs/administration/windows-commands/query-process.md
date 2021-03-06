---
title: query process
description: Referenz Artikel für den Abfrageprozess Befehl, der Informationen zu Prozessen anzeigt, die auf einem Remotedesktop-Sitzungshost Server ausgeführt werden.
ms.topic: reference
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: eb2deaeac012eba4dad06ae6084474942536adfd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639899"
---
# <a name="query-process"></a>query process

Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Prozessen an, die auf einem Remotedesktop-Sitzungshost Server ausgeführt werden. Mit diesem Befehl können Sie herausfinden, welche Programme von einem bestimmten Benutzer ausgeführt werden und welche Benutzer ein bestimmtes Programm ausführen. Dieser Befehl gibt folgende Information zurück:

- Benutzer, der den Prozess besitzt

- Sitzung, die den Prozess besitzt

- Die ID der Sitzung.

- Name des Prozesses

- ID des Prozesses

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
query process [*|<processID>|<username>|<sessionname>|/id:<nn>|<programname>] [/server:<servername>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| * | Listet die Prozesse für alle Sitzungen auf. |
| `<processID>` | Gibt die numerische ID an, die den Prozess identifiziert, den Sie Abfragen möchten. |
| `<username>` | Gibt den Namen des Benutzers an, dessen Prozesse Sie auflisten möchten. |
| `<sessionname>` | Gibt den Namen der aktiven Sitzung an, deren Prozesse Sie auflisten möchten. |
| /ID`<nn>` | Gibt die ID der Sitzung an, deren Prozesse Sie auflisten möchten. |
| `<programname>` | Gibt den Namen des Programms an, dessen Prozesse Sie Abfragen möchten. Die Erweiterung ". exe" ist erforderlich. |
| /server:`<servername>` | Gibt den Remotedesktop-Sitzungshost Server an, dessen Prozesse Sie auflisten möchten. Wenn keine Angabe erfolgt, wird der Server verwendet, auf dem Sie zurzeit angemeldet sind. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Administratoren haben Vollzugriff auf alle **Abfrageprozess** Funktionen.

- Wenn Sie die <*username*>, <*Sessionname*>, * `<nn>` /ID:*, <*Program Name*> oder *&#42;* Parameter nicht angeben, zeigt diese Abfrage nur die Prozesse an, die zum aktuellen Benutzer gehören.

- Wenn der **Abfrageprozess** Informationen zurückgibt, `(>)` wird vor jedem Prozess, der zur aktuellen Sitzung gehört, ein größer-als-Symbol angezeigt.

## <a name="examples"></a>Beispiele

Zum Anzeigen von Informationen zu den Prozessen, die von allen Sitzungen verwendet werden, geben Sie Folgendes ein:

```
query process *
```

Geben Sie Folgendes ein, um Informationen über die Prozesse anzuzeigen, die von der *Sitzungs-ID 2*verwendet werden:

```
query process /ID:2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Abfragebefehl](query.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
