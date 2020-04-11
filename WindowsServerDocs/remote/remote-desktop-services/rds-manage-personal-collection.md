---
title: Verwalten einer Sammlung mit persönlichen Desktopsitzungen in den Remotedesktopdiensten
description: Hier erfährst du, wie du RDSH- und RemoteApp-Programme zu deiner Remotedesktopdienste-Bereitstellung hinzufügst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 7088d164ecdd7211894b004ed580eecb33d1ba60
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861063"
---
# <a name="manage-your-personal-desktop-session-collections"></a>Verwalten deiner Sammlung mit persönlichen Desktopsitzungen

Verwende die folgenden Informationen zum Verwalten einer Sammlung mit persönlichen Desktopsitzungen in den Remotedesktopdiensten.

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>Manuelles Zuweisen eines Benutzers zu einem persönlichen Sitzungshost
Verwende das Cmdlet **Set-RDPersonalSessionDesktopAssignment**, um einen Benutzer manuell einem persönlichen Sitzungshostserver in der Sammlung zuzuweisen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<Zeichenfolge\> 

-User \<Zeichenfolge\>

-Name \<Zeichenfolge\>

- **-CollectionName**: Gibt den Namen einer Sammlung mit persönlichen Sitzungsdesktops an. Dieser Parameter ist erforderlich.
- **-ConnectionBroker**: Gibt den Server des Remotedesktop-Verbindungsbrokers für deine Remotedesktopbereitstellung an. Wenn du keinen Wert angibst, verwendet das Cmdlet den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des lokalen Computers.
- **-User**: Gibt das Benutzerkonto, das dem persönlichen Sitzungsdesktop zugeordnet werden soll, im Format „DOMAENE\Benutzer“ an. Dieser Parameter ist erforderlich.
- **-Name**: Gibt den Namen des Sitzungshostservers an. Dieser Parameter ist erforderlich. Der hier identifizierte Sitzungshost muss Mitglied der Sammlung sein, die vom Parameter **-CollectionName** angegeben wird.

Das Cmdlet **Import-RDPersonalSessionDesktopAssignment** importiert Zuordnungen zwischen Benutzerkonen und persönlichen Sitzungsdesktops aus einer Textdatei. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<Zeichenfolge\>

-Path \<Zeichenfolge>

**-Path** gibt den Pfad und den Dateinamen der Datei an, die importiert werden soll.
 
## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>Entfernen einer Benutzerzuweisung aus einem persönlichen Sitzungshost
Verwende das Cmdlet **Remove-RDPersonalSessionDesktopAssignment**, um die Zuordnung zwischen einem persönlichen Sitzungsdesktop und einem Benutzer zu entfernen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<Zeichenfolge\>

-Force

-Name \<Zeichenfolge\>

-User \<Zeichenfolge\>

**-Force** erzwingt die Ausführung des Befehls ohne Aufforderung zur Bestätigung durch den Benutzer.

## <a name="query-user-assignments"></a>Abfragen von Benutzerzuweisungen
Verwende das Cmdlet **Get-RDPersonalSessionDesktopAssignment**, um eine Liste mit persönlichen Sitzungsdesktops und den zugeordneten Benutzerkonten abzurufen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<Zeichenfolge\>

-User \<Zeichenfolge\>

-Name \<Zeichenfolge\>

Mit diesem Cmdlet kannst du Abfragen nach Sammlungsnamen, Benutzernamen oder Namen von Sitzungsdesktops ausführen. Wenn du nur den Parameter **-CollectionName** angibst, gibt das Cmdlet eine Liste mit Sitzungshosts und zugeordneten Benutzern zurück. Wenn du auch den Parameter **-User** angibst, wird der Sitzungshost zurückgegeben, der diesem Benutzer zugeordnet ist. Wenn du den Parameter **-Name** angibst, wird der Benutzer zurückgegeben, der diesem Sitzungshost zugeordnet ist. 


Das Cmdlet **Export-RDPersonalPersonalDesktopAssignment** exportiert die aktuellen Zuordnungen zwischen Benutzern und persönlichen virtuellen Desktops in eine Textdatei. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<Zeichenfolge\>

-Path \<Zeichenfolge\>


Alle neuen Cmdlets unterstützen die folgenden allgemeinen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen findest du unter [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).
