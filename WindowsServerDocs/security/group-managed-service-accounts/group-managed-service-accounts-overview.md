---
title: 'Gruppe verwaltete Dienstkonten: Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4912ae273e603b4a3362c4984da710f780c3e8b3
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/12/2018
---
# <a name="group-managed-service-accounts-overview"></a>Gruppe verwaltete Dienstkonten: Übersicht

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema Änderungen für IT-Experten die Group-Managed Service Account eingeführt, mit der Beschreibung praktische Anwendungsfälle, in der Microsoft Implementierung und Anforderungen an Hardware und Software.


## <a name="BKMK_OVER"></a>Featurebeschreibung
Eigenständige verwaltete Dienstkonten, die in Windows Server 2008 R2 und Windows 7 eingeführt wurden, sind verwaltete Domänenkonten, die automatische kennwortverwaltung und vereinfachte Dienstprinzipalnamen-Verwaltung, einschließlich Delegierung der Verwaltung an andere Administratoren bereitstellen.

Die Gruppe Managed Service Account bietet die gleiche Funktionalität innerhalb der Domäne, aber auch, dass eine Funktion erstreckt sich über mehrere Server. Beim Verbinden mit einem Dienst in einer Serverfarm, z.B. Netzwerklastenausgleich, müssen die gegenseitige Authentifizierung unterstützende Authentifizierungsprotokolle alle Instanzen der Dienste den gleichen Prinzipal verwenden. Wenn Group Managed Service Account als Dienstprinzipale verwendet werden, verwaltet der Windows-Betriebssystem das Kennwort für das Konto anstelle des Administrator das Kennwort verwalten.

Die Microsoft-Schlüsselverteilungsdienst-\(kdssvc.dll\) stellt den Mechanismus zum sicheren des aktuellen Schlüssels oder eines bestimmten Schlüssels mit einer Schlüssel-ID für ein Active Directory-Konto zu erhalten. Die Key Distribution Service stellt geheime Informationen die zum Erstellen von Schlüsseln für das Konto verwendet wird. Diese Schlüssel werden regelmäßig geändert. Für eine Gruppe Managed Service Account berechnet der Domänencontroller das Kennwort für den Schlüssel, die von den Key Distribution Services darüber hinaus für andere Attribute des Gruppenverwalteten Dienstkontos bereitgestellt.  Mitgliedhosts können die aktuellen und vorherigen Kennwortwerte erhalten, wenden Sie sich an einem Domänencontroller.

## <a name="BKMK_APP"></a>In der Praxis
Gruppenverwaltete Dienstkonten bieten eine einzelidentitätslösung für Dienste, die unter einer Serverfarm oder auf Systemen hinter Netzwerklastausgleich. Durch die Bereitstellung einer Gruppe MSA-Lösung, Dienste für die neue Gruppe MSA-Prinzipal konfiguriert werden, und die Verwaltung von Windows übernommen wird.

Eine Gruppe mit müssen verwaltetes Dienstkonto, Dienste oder Dienstadministratoren nicht kennwortsynchronisierung zwischen Dienstinstanzen zu verwalten. Die Gruppe Gruppenverwaltete Dienstkonto unterstützt Hosts, die für einen längeren Zeitraum und die Verwaltung von mitgliedshosts für alle Instanzen eines Diensts offline sind. Dies bedeutet, dass Sie eine Serverfarm bereitstellen können, die eine einzelne Identität unterstützt, auf die vorhandene Clientcomputer authentifizieren können, ohne zu wissen, die Instanz des Dienstes, der eine Verbindung hergestellt werden.

Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe sind oder gMSA oder sMSA systemeigen zu unterstützen.

## <a name="BKMK_SOFT"></a>Anforderungen der Clientsoftware

Eine 64-Bit-Architektur ist erforderlich, um Windows PowerShell-Befehle ausführen, die zum Verwalten von Gruppenverwalteten Dienstkonten verwendet werden.

Ein verwaltetes Dienstkonto ist abhängig von Verschlüsselungstypen für Kerberos unterstützt. Wenn ein Clientcomputer authentifiziert, auf einem Server per Kerberos des Domänencontrollers erstellt ein Kerberos-Dienstticket durch Verschlüsselung geschützt der Domänencontroller und Server unterstützt. Der Domänencontroller verwendet MsDS\-SupportedEncryptionTypes-Attributs des Kontos um zu bestimmen, welche die Server-Verschlüsselung unterstützt und, wenn kein Attribut vorhanden ist, es wird vorausgesetzt der Client-Computer unterstützt keine sichereren Verschlüsselungsarten. Wenn der Host zur Unterstützung von RC4 nicht konfiguriert ist, schlägt die Authentifizierung immer fehl. Aus diesem Grund muss AES immer explizit für verwaltete Dienstkonten konfiguriert werden.

> [!NOTE]
> Ab Windows Server2008 R2, ist DES standardmäßig deaktiviert. Weitere Informationen zu unterstützten Verschlüsselungsarten finden Sie unter [Changes in Kerberos Authentication](https://technet.microsoft.com/library/dd560670(WS.10).aspx).

Gruppenverwaltete Dienstkonten gelten nicht für Windows-Betriebssysteme vor Windows Server2012.

## <a name="server-manager-information"></a>Server-Manager-Informationen
Es sind keine Konfigurationsschritte erforderlich, um die Implementierung von Microsoft-Konto und Gruppen-MSA mit Server-Manager oder dem Cmdlet Get-WindowsFeature Install\.

## <a name="BKMK_LINKS"></a>Siehe auch
Die folgende Tabelle enthält Links zu zusätzlichen Ressourcen, die im Zusammenhang mit verwalteten Dienstkonten und Gruppenverwaltete Dienstkonten.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Neues für verwaltete Dienstkonten](what-s-new-for-managed-service-accounts.md)<br /><br />[Dokumentation für Windows 7 und Windows Server 2008 R2 zu verwalteten Dienstkonten](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[Step\-Bereichen-Schritt-Anleitung zu Dienstkonten](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**Planen der**|Noch nicht verfügbar|
|**Bereitstellung**|Noch nicht verfügbar|
|**Vorgänge**|[Verwaltete Dienstkonten in Active Directory](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Bewertung**|[Erste Schrittemit Gruppe von verwalteten Dienstkonten](getting-started-with-group-managed-service-accounts.md)|
|**Tools und Einstellungen**|[Verwaltete Dienstkonten in Active Directory-Domänendienste](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**Community-Ressourcen**|[Verwaltete Dienstkonten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung](http://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**Verwandte Technologien**|[Übersicht über Active Directory-Domänendienste](active-directory-domain-services-overview.md)|


