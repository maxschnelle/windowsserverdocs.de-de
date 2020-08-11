---
title: Verwenden von persönlichen Sitzungsdesktops mit Remotedesktopdiensten
description: Hier erfährst du, wie du personalisierte, zugewiesene Desktops über die Remotedesktopdienste freigibst.
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 10/22/2019
manager: dongill
ms.openlocfilehash: ccb8bd5a91af6e4b9a8d1a610bf22747433bf913
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946423"
---
# <a name="use-personal-session-desktops-with-remote-desktop-services"></a>Verwenden von persönlichen Sitzungsdesktops mit Remotedesktopdiensten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Mithilfe von persönlichen Sitzungsdesktops kannst du serverbasierte persönliche Desktops in einer Cloud Computing-Umgebung bereitstellen.  (In einer Cloud Computing-Umgebung besteht eine Trennung zwischen den Hyper-V-Fabricservern und den Gast-VMs wie der Microsoft Azure Cloud oder der Microsoft-Cloudplattform.) Die Funktion für persönliche Sitzungsdesktops erweitert das Szenario für die Bereitstellung sitzungsbasierter Desktops in den Remotedesktopdiensten: Es wird eine neue Art von Sitzungssammlung erstellt, in der jeder Benutzer zu einem eigenen persönlichen Sitzungshost zugewiesen wird und dafür Administratorrechte erhält.

Verwende die folgenden Informationen, um eine Sammlung persönlicher Sitzungsdesktops zu erstellen und zu verwalten.

## <a name="create-a-personal-session-desktop-collection"></a>Erstellen einer Sammlung persönlicher Sitzungsdesktops

Verwende das Cmdlet „New-RDSessionCollection“, um eine Sammlung persönlicher Sitzungsdesktops zu erstellen. Die folgenden drei Parameter stellen die Konfigurationsinformationen bereit, die für persönliche Sitzungsdesktops benötigt werden:

- **-PersonalUnmanaged**: Gibt den Typ der Sitzungssammlung an, mit dem du Benutzer einem persönlichen Sitzungshostserver zuweisen kannst. Wenn du diesen Parameter nicht angibst, wird die Sammlung als herkömmliche Remotedesktop-Sitzungshostsammlung erstellt, bei der Benutzer beim Anmelden dem nächsten verfügbaren Sitzungshost zugewiesen werden.
- **-GrantAdministrativePrivilege**: Wenn du **-PersonalUnmanaged** verwendest, gibt dieser Parameter an, dass der Benutzer, der dem Sitzungshost zugewiesen wurde, Administratorrechte erhalten soll. Wenn du diesen Parameter nicht verwendest, werden den Benutzern nur Standardbenutzerrechte erteilt.
- **-AutoAssignUser**: Wenn du **-PersonalUnmanaged** verwendest, gibt dieser Parameter an, dass neue Benutzer, die eine Verbindung über den Remotedesktop-Verbindungsbroker herstellen, automatisch einem noch nicht zugewiesenen Sitzungshost zugewiesen werden. Wenn in der Sammlung keine nicht zugewiesenen Sitzungshosts vorhanden sind, wird dem Benutzer eine Fehlermeldung angezeigt. Wenn du diesen Parameter nicht verwendest, musst du [Benutzer manuell einem Sitzungshost zuweisen](#manually-assign-a-user-to-a-personal-session-host), bevor die Benutzer sich anmelden.

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
