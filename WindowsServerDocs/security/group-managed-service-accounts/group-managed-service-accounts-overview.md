---
title: Group Managed Service Accounts Overview
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 09405b940e9fd862372fe80c4a5194caa205e5ea
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991502"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten wird das Gruppen verwaltete Dienst Konto eingeführt. hierzu werden praktische Anwendungen, Änderungen in der Implementierung von Microsoft sowie Hardware-und Softwareanforderungen beschrieben.


## <a name="feature-description"></a><a name="BKMK_OVER"></a>Featurebeschreibung
Ein eigenständiges verwaltetes Dienst Konto (Managed Service Account, SMSA) ist ein verwaltetes Domänen Konto, das die automatische Kenn Wort Verwaltung, vereinfachte Dienst Prinzipal Namen-Verwaltung (Service Principal Name, SPN) und die Möglichkeit zum Delegieren der Verwaltung Diese Art von verwaltetem Dienstkonto (Managed Service Account, MSA) wurde in Windows Server 2008 R2 und Windows 7 eingeführt.

Das Gruppen verwaltete Dienst Konto (Group Managed Service Account, GMSA) bietet die gleiche Funktionalität innerhalb der Domäne, erweitert diese Funktionalität aber auch auf mehrere Server. Beim Herstellen einer Verbindung mit einem auf einer Serverfarm gehosteten Dienst, wie z. b. der Lösung für Netzwerk Lastenausgleich, erfordern die Authentifizierungsprotokolle, die gegenseitige Authentifizierung unterstützen, dass alle Instanzen der Dienste denselben Prinzipal Wenn ein GMSA als Dienst Prinzipale verwendet wird, verwaltet das Windows-Betriebssystem das Kennwort für das Konto, anstatt sich auf den Administrator zu verlassen, um das Kennwort zu verwalten.

Der Microsoft-Schlüssel Verteilungsdienst \(kdssvc.dll\) bietet den Mechanismus zum sicheren Abrufen des aktuellen Schlüssels oder eines bestimmten Schlüssels mit einer Schlüssel Kennung für ein Active Directory Konto. Vom Schlüsselverteilungsdienst werden geheime Informationen zur Erstellung von Schlüsseln für das Konto bereitgestellt. Diese Schlüssel werden regelmäßig geändert. Bei einem GMSA berechnet der Domänen Controller das Kennwort für den Schlüssel, der von den Schlüssel Verteilungs Diensten bereitgestellt wird, zusätzlich zu anderen Attributen des GMSA.  Mitglieder Hosts können die aktuellen und vorangehenden Kenn Wort Werte abrufen, indem Sie einen Domänen Controller kontaktieren.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
gmsas bieten eine einzelne Identitäts Lösung für Dienste, die in einer Serverfarm oder auf Systemen hinter Netzwerk Load Balancer ausgeführt werden. Durch die Bereitstellung einer GMSA-Lösung können Dienste für den neuen GMSA-Prinzipal konfiguriert werden, und die Kenn Wort Verwaltung wird von Windows verarbeitet.

Durch die Verwendung eines GMSA müssen Dienste oder Dienst Administratoren die Kenn Wort Synchronisierung zwischen Dienst Instanzen nicht verwalten. Das GMSA unterstützt Hosts, die über einen längeren Zeitraum offline gehalten werden, sowie die Verwaltung von Mitglieds Hosts für alle Instanzen eines Diensts. Sie können also eine Serverfarm bereitstellen, die eine einzelne Identität unterstützt, gegenüber der sich vorhandene Clientcomputer authentifizieren können, ohne zu wissen, mit welcher Instanz des Diensts eine Verbindung hergestellt wird.

Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt werden, können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe oder gMSA oder sMSA systemeigen unterstützen.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen

\-Zum Ausführen der Windows PowerShell-Befehle, die zur Verwaltung von gmsas verwendet werden, ist eine 64-Bit-Architektur erforderlich.

Ein verwaltetes Dienstkonto ist abhängig von Verschlüsselungstypen mit Kerberos-Unterstützung. Wenn sich ein Clientcomputer gegenüber einem Server per Kerberos authentifiziert, wird vom Domänencontroller ein Kerberos-Dienstticket erstellt, das mit einer Verschlüsselung geschützt ist, die sowohl vom Domänencontroller als auch vom Server unterstützt wird. Der Domänen Controller verwendet das msDS \- supportedencryptiontypes-Attribut des Kontos, um zu bestimmen, welche Verschlüsselung der Server unterstützt. Wenn kein Attribut vorhanden ist, wird davon ausgegangen, dass der Client Computer stärkere Verschlüsselungstypen nicht unterstützt. Wenn der Host so konfiguriert ist, dass RC4 nicht unterstützt wird, tritt bei der Authentifizierung immer ein Fehler auf. Aus diesem Grund muss AES für verwaltete Dienstkonten immer explizit konfiguriert sein.

> [!NOTE]
> Ab Windows Server 2008 R2 ist DES standardmäßig deaktiviert. Weitere Informationen zu den unterstützten Verschlüsselungsarten finden Sie unter [Changes in Kerberos Authentication](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560670(v=ws.10)).

gmsas gelten nicht für Windows-Betriebssysteme vor Windows Server 2012.

## <a name="server-manager-information"></a>Informationen zum Server-Manager
Es sind keine Konfigurationsschritte erforderlich, um MSA und GMSA mithilfe von Server-Manager oder mit dem \- Cmdlet Install Windows Feature zu implementieren.

## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind Links zu weiterführenden Ressourcen im Zusammenhang mit verwalteten Dienstkonten und gruppenverwalteten Dienstkonten aufgeführt.

|Inhaltstyp|Referenzen|
|--------|-------|
|**Produktbewertung**|[What's New for Managed Service Accounts](what-s-new-for-managed-service-accounts.md)<p>[Dokumentation zu verwalteten Dienstkonten für Windows 7 und Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff641731(v=ws.10))<p>[Schritt- \- für-Schritt-Anleitung für Dienst Konten \-](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548356(v=ws.10))|
|**Planung**|Noch nicht verfügbar|
|**Bereitstellung**|Noch nicht verfügbar|
|**Vorgänge**|[Verwaltete Dienstkonten in Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd378925(v=ws.10))|
|**Problembehandlung**|Noch nicht verfügbar|
|**Auswertung**|[Die ersten Schritte mit Gruppen verwalteten Dienst Konten](getting-started-with-group-managed-service-accounts.md)|
|**Tools und Einstellungen**|[Verwaltete Dienstkonten in Active Directory-Domänendiensten](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd378925(v=ws.10))|
|**Communityressourcen**|[Verwaltete Dienstkonten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung](/archive/blogs/askds/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting)|
|**Verwandte Technologien**|[Übersicht über die Active Directory Domain Services](active-directory-domain-services-overview.md)|