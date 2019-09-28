---
title: Verwenden von persönlichen Sitzungsdesktops mit Remotedesktopdiensten
description: Hier erfährst du, wie du personalisierte, zugewiesene Desktops über die Remotedesktopdienste freigibst.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/16/2016
manager: dongill
ms.openlocfilehash: 7429cd9cb87db310a716136c171de47cfe0892f2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387361"
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


Alle neuen Cmdlets unterstützen die folgenden allgemeinen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="hardware-accelerated-graphics"></a>Hardwarebeschleunigte Grafikfunktionen
Windows Server 2016 erweitert die RemoteFX 3D-Grafikadaptertechnologie (vGPU) auf die Unterstützung von OpenGL und unterstützt Windows Server 2016-Gast-VMs für Einzelbenutzer. Du kannst persönliche Sitzungsdesktops mit den neuen vGPU-Funktionen kombinieren, um Unterstützung für gehostete Anwendungen bereitzustellen, die beschleunigte Grafikfunktionen erfordern. Alternativ dazu kannst du persönliche Sitzungsdesktops mit der neuen Discrete Device Assignment-Funktion (DDA) kombinieren, um Unterstützung für solche gehosteten Anwendungen bereitzustellen.
