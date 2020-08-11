---
title: Verwalten einer Sammlung mit persönlichen Desktopsitzungen in den Remotedesktopdiensten
description: Hier erfährst du, wie du RDSH- und RemoteApp-Programme zu deiner Remotedesktopdienste-Bereitstellung hinzufügst.
ms.author: elizapo
ms.date: 11/08/2016
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: bd6c91b7f022e60e488c90776e0981523da7bccb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961654"
---
# <a name="manage-your-personal-desktop-session-collections"></a>Verwalten deiner Sammlung mit persönlichen Desktopsitzungen

Verwende die folgenden Informationen zum Verwalten einer Sammlung mit persönlichen Desktopsitzungen in den Remotedesktopdiensten.

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>Manuelles Zuweisen eines Benutzers zu einem persönlichen Sitzungshost
Verwende das Cmdlet **Set-RDPersonalSessionDesktopAssignment**, um einen Benutzer manuell einem persönlichen Sitzungshostserver in der Sammlung zuzuweisen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<string\>

-ConnectionBroker \<string\>

-User \<string\>

-Name \<string\>

- **-CollectionName**: Gibt den Namen einer Sammlung mit persönlichen Sitzungsdesktops an. Dieser Parameter ist erforderlich.
- **-ConnectionBroker**: Gibt den Server des Remotedesktop-Verbindungsbrokers für deine Remotedesktopbereitstellung an. Wenn du keinen Wert angibst, verwendet das Cmdlet den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des lokalen Computers.
- **-User**: Gibt das Benutzerkonto, das dem persönlichen Sitzungsdesktop zugeordnet werden soll, im Format „DOMAENE\Benutzer“ an. Dieser Parameter ist erforderlich.
- **-Name**: Gibt den Namen des Sitzungshostservers an. Dieser Parameter ist erforderlich. Der hier identifizierte Sitzungshost muss Mitglied der Sammlung sein, die vom Parameter **-CollectionName** angegeben wird.

Das Cmdlet **Import-RDPersonalSessionDesktopAssignment** importiert Zuordnungen zwischen Benutzerkonen und persönlichen Sitzungsdesktops aus einer Textdatei. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string>

**-Path** gibt den Pfad und den Dateinamen der Datei an, die importiert werden soll.

## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>Entfernen einer Benutzerzuweisung aus einem persönlichen Sitzungshost
Verwende das Cmdlet **Remove-RDPersonalSessionDesktopAssignment**, um die Zuordnung zwischen einem persönlichen Sitzungsdesktop und einem Benutzer zu entfernen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Force

-Name \<string\>

-User \<string\>

**-Force** erzwingt die Ausführung des Befehls ohne Aufforderung zur Bestätigung durch den Benutzer.

## <a name="query-user-assignments"></a>Abfragen von Benutzerzuweisungen
Verwende das Cmdlet **Get-RDPersonalSessionDesktopAssignment**, um eine Liste mit persönlichen Sitzungsdesktops und den zugeordneten Benutzerkonten abzurufen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<string\>

-ConnectionBroker \<string\>

-User \<string\>

-Name \<string\>

Mit diesem Cmdlet kannst du Abfragen nach Sammlungsnamen, Benutzernamen oder Namen von Sitzungsdesktops ausführen. Wenn du nur den Parameter **-CollectionName** angibst, gibt das Cmdlet eine Liste mit Sitzungshosts und zugeordneten Benutzern zurück. Wenn du auch den Parameter **-User** angibst, wird der Sitzungshost zurückgegeben, der diesem Benutzer zugeordnet ist. Wenn du den Parameter **-Name** angibst, wird der Benutzer zurückgegeben, der diesem Sitzungshost zugeordnet ist.


Das Cmdlet **Export-RDPersonalPersonalDesktopAssignment** exportiert die aktuellen Zuordnungen zwischen Benutzern und persönlichen virtuellen Desktops in eine Textdatei. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string\>


Alle neuen Cmdlets unterstützen die folgenden allgemeinen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen findest du unter [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).
