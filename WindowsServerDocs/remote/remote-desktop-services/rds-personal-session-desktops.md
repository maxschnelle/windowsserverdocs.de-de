---
title: Verwenden Sie persönliche sitzungsdesktops mit Remote Desktop Services
description: Erfahren Sie, wie personalisierten, Freigeben von zugewiesenen Desktops mittels RDS.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/16/2016
manager: dongill
ms.openlocfilehash: 41f6a28c1b754a5277a0966a87dae08a6aa34e08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875951"
---
# <a name="use-personal-session-desktops-with-remote-desktop-services"></a>Verwenden Sie persönliche sitzungsdesktops mit Remote Desktop Services

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können Server-basierten persönliche Desktops in einer Cloud-computing-Umgebung mithilfe von persönlichen sitzungsdesktops bereitstellen.  (Eine Cloud-computing-Umgebung weist eine Trennung zwischen den Hyper-V-fabricservern und den virtuellen Gastcomputern bereitstellen, z. B. Microsoft Azure-Cloud oder der Microsoft-Cloud-Plattform.) Die persönlichen Sitzung-desktop-Funktion erweitert das sitzungsbasierte desktopbereitstellung-Szenario in Remote Desktop Services, um eine neue Art von sitzungssammlung zu erstellen, wird jeder Benutzer ihre eigenen persönlichen Sitzungshost mit Administratorrechten zugewiesen. 

Verwenden Sie die folgende Informationen zum Erstellen und Verwalten einer persönlichen desktop sitzungssammlung.

## <a name="create-a-personal-session-desktop-collection"></a>Erstellen einer persönlichen desktop sitzungssammlung

Verwenden Sie das Cmdlet "New-RDSessionCollection", um einen persönlichen desktop sitzungssammlung erstellen. Die folgenden drei Parameter geben die Konfigurationsinformationen für persönliche sitzungsdesktops benötigt:

- **-PersonalUnmanaged** -gibt der Typ der sitzungssammlung, der Ihnen ermöglicht eine persönliche Sitzungshostserver Benutzer zuweisen. Wenn Sie diesen Parameter nicht angeben, wird als eine herkömmliche RD-Sitzungshost-Auflistung, die Sammlung erstellt, in denen Benutzer den nächsten verfügbaren Sitzungshost zugewiesen sind, bei der Anmeldung.
- **-GrantAdministrativePrivilege** : bei Verwendung von **- PersonalUnmanaged**, gibt an, dass der Benutzer, die dem Sitzungshost zugewiesen Administratorrechte zugewiesen werden. Wenn Sie diesen Parameter nicht verwenden, erhalten Benutzer nur Berechtigungen für Standardbenutzer.
- **-AutoAssignUser** : bei Verwendung von **- PersonalUnmanaged**, gibt an, dass neue Benutzer, die eine Verbindung über den Remotedesktop-Verbindungsbroker automatisch auf einem Sitzungshost nicht zugewiesene zugewiesen werden. Wenn keine nicht zugewiesenen Sitzungshosts in der Auflistung vorhanden sind, wird der Benutzer eine Fehlermeldung angezeigt. Wenn Sie diesen Parameter nicht verwenden, müssen Sie [manuell zuweisen von Benutzern zu einem Host für Remotedesktopsitzungen](#manually-assign-a-user-to-a-personal-session-host) , bevor sie sich anmelden.

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>Weisen Sie einen Benutzer manuell zu einer persönlichen Sitzungshost
Verwenden der **Set-RDPersonalSessionDesktopAssignment** Cmdlet, um eine persönliche Sitzungshostserver in der Auflistung einen Benutzer manuell zuweisen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<string\> 

-Benutzer \<Zeichenfolge\>

--Name \<Zeichenfolge\>

- **– CollectionName** -gibt den Namen des persönlichen desktop sitzungssammlung. Dieser Parameter ist erforderlich.
- **– ConnectionBroker** -gibt den Remotedesktop-Verbindungsbroker (RD-Verbindungsbroker)-Server für die Bereitstellung von Remotedesktop. Wenn Sie keinen Wert angeben, verwendet das Cmdlet den vollqualifizierten Domänennamen (FQDN) des lokalen Computers.
- **– Benutzer** -gibt das Benutzerkonto an, die persönliche Sitzung Desktop, im Format "Domäne\Benutzer" zugeordnet werden soll. Dieser Parameter ist erforderlich.
- **– Name** -gibt den Namen des Sitzungshostservers. Dieser Parameter ist erforderlich. Die hier identifizierte Sitzungshost muss ein Member der Auflistung, die **- CollectionName** angegeben wird.

Die **Import-RDPersonalSessionDesktopAssignment** Cmdlet werden die Zuordnungen zwischen Benutzerkonten und persönliche sitzungsdesktops aus einer Textdatei importiert. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<string\>

-Path \<Zeichenfolge >

**– Pfad** gibt an, der Pfad und Dateiname einer Datei importieren.
 
## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>Entfernen eine aus einer persönlichen Sitzungshost
Verwenden der **Remove-RDPersonalSessionDesktopAssignment** Cmdlet, um die Zuordnung zwischen einem Desktop persönliche Sitzung und ein Benutzer zu entfernen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<string\>

-Force

--Name \<Zeichenfolge\>

-Benutzer \<Zeichenfolge\>

**– Erzwingen** erzwingt, dass den Befehl ohne Aufforderung zur Bestätigung des Benutzers ausgeführt.

## <a name="query-user-assignments"></a>Abfrage von Benutzerrechten
Verwenden der **Get-RDPersonalSessionDesktopAssignment** -Cmdlet zum Abrufen einer Liste von persönlichen sitzungsdesktops und zugeordnete Benutzerkonten. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<string\>

-Benutzer \<Zeichenfolge\>

--Name \<Zeichenfolge\>

Sie können das Cmdlet Sammlungsname, den Benutzernamen ein, oder vom desktop Sitzungsname auf Abfrage ausführen. Wenn Sie nur angeben, die **– CollectionName** -Parameter mit dem-Cmdlet gibt eine Liste von Sitzungshosts und zugeordneten Benutzern. Wenn Sie auch angeben, die **– Benutzer** Parameter, der mit diesem Benutzer verknüpfte Sitzungshost wird zurückgegeben. Wenn Sie angeben, die **– Name** Parameter der Benutzer verknüpft ist, mit dem Sitzungshost wird zurückgegeben. 


Die **Export-RDPersonalPersonalDesktopAssignment** Cmdlet exportiert die aktuellen Zuordnungen zwischen Benutzern und persönliche virtuelle Desktops in einer Textdatei gespeichert. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<string\>

-Path \<Zeichenfolge\>


Alle neuen-Cmdlets unterstützt diese gängigen Parameter:-Verbose,-Debug, - ErrorAction, -ErrorVariable,-OutBuffer und - OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="hardware-accelerated-graphics"></a>Beschleunigter Grafikfunktionen von Hardware
Windows Server 2016 erweitert die RemoteFX 3D Graphics Adapter (vGPU)-Technologie zur Unterstützung von OpenGL und Einzelbenutzer-Windows Server 2016-Gast-VMs unterstützt. Sie können persönliche sitzungsdesktops kombinieren, mit den neuen vGPU-Funktionen, um Unterstützung für gehostete Anwendungen bereitzustellen, die beschleunigte Grafikfunktionen erfordern. Alternativ können Sie persönliche sitzungsdesktops kombinieren, mit der neue diskrete Gerät Zuweisung (DDA)-Funktion, die auch für gehostete Anwendungen unterstützen, die beschleunigte Grafikfunktionen erfordern.
