---
title: Verwalten einer Sammlung mit persönlichen Desktopsitzungen in den Remotedesktopdiensten
description: Hier erfährst du, wie du RDSH- und RemoteApp-Programme zu deiner Remotedesktopdienste-Bereitstellung hinzufügst.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 6bf0ad3a2cd35c9794fd13631ed29df94725685c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387407"
---
## <a name="manage-your-personal-desktop-session-collections"></a>Verwalten deiner Sammlung mit persönlichen Desktopsitzungen

Verwende die folgenden Informationen zum Verwalten einer Sammlung mit persönlichen Desktopsitzungen in den Remotedesktopdiensten.

### <a name="manually-assign-a-user-to-a-personal-session-host"></a>Manuelles Zuweisen eines Benutzers zu einem persönlichen Sitzungshost
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
 
### <a name="removing-a-user-assignment-from-a-personal-session-host"></a>Entfernen einer Benutzerzuweisung aus einem persönlichen Sitzungshost
Verwende das Cmdlet **Remove-RDPersonalSessionDesktopAssignment**, um die Zuordnung zwischen einem persönlichen Sitzungsdesktop und einem Benutzer zu entfernen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<Zeichenfolge\>

-Force

-Name \<Zeichenfolge\>

-User \<Zeichenfolge\>

**-Force** erzwingt die Ausführung des Befehls ohne Aufforderung zur Bestätigung durch den Benutzer.

### <a name="query-user-assignments"></a>Abfragen von Benutzerzuweisungen
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


Alle neuen Cmdlets unterstützen die folgenden allgemeinen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).
