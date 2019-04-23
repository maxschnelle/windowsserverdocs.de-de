---
title: Verwalten einer persönlichen desktop sitzungssammlung in RDS
description: Erfahren Sie, wie hinzugefügt und RDSH und RemoteApp-Programme für Ihre RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 286c7ba4bd4428669d135c35c825033d22b8f40e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865721"
---
## <a name="manage-your-personal-desktop-session-collections"></a>Verwalten Sie Ihre persönliche Remotedesktop-Sitzungshost-Sammlungen

Verwenden Sie die folgende Informationen, um einen persönlichen desktop sitzungssammlung in Remote Desktop Services zu verwalten.

### <a name="manually-assign-a-user-to-a-personal-session-host"></a>Weisen Sie einen Benutzer manuell zu einer persönlichen Sitzungshost
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
 
### <a name="removing-a-user-assignment-from-a-personal-session-host"></a>Entfernen eine aus einer persönlichen Sitzungshost
Verwenden der **Remove-RDPersonalSessionDesktopAssignment** Cmdlet, um die Zuordnung zwischen einem Desktop persönliche Sitzung und ein Benutzer zu entfernen. Das Cmdlet unterstützt die folgenden Parameter:

-CollectionName \<Zeichenfolge\>

-ConnectionBroker \<string\>

-Force

--Name \<Zeichenfolge\>

-Benutzer \<Zeichenfolge\>

**– Erzwingen** erzwingt, dass den Befehl ohne Aufforderung zur Bestätigung des Benutzers ausgeführt.

### <a name="query-user-assignments"></a>Abfrage von Benutzerrechten
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
