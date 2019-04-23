---
title: Group Managed Service Accounts Overview
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
ms.openlocfilehash: 24e3e3c15544de2f3bed4a7ef177b659e8095385
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836971"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema ändert für IT-Spezialisten das gruppenverwaltete Dienstkonto eingeführt. hierzu werden praktische Anwendungen, sich in der Microsoft-Implementierung und Hardware- und softwareanforderungen.


## <a name="BKMK_OVER"></a>Featurebeschreibung
Eine eigenständige Managed Service Account (sMSA) wird von verwalteten Domänenkonten, die automatische kennwortverwaltung, vereinfachte Dienstprinzipalnamen (SPN) für dienstverwaltung sowie die Möglichkeit, die Verwaltung an andere Administratoren delegieren bereitstellt. Diese Art von verwalteten Dienstkonto (MSA) wurde in Windows Server 2008 R2 und Windows 7 eingeführt.

Die Gruppe Managed Service Account (gMSA) bietet die gleiche Funktionalität innerhalb der Domäne, aber erweitert diese Funktion auch über mehrere Server. Bei der Verbindung an eines Diensts, gehostet in einer Serverfarm, z. B. Netzwerk-Lastenausgleich-Lösung erfordern die Authentifizierungsprotokolle mit gegenseitiger Authentifizierung an, dass alle Instanzen der Dienste den gleichen Prinzipal verwenden. Wenn ein gMSA als Dienstprinzipale verwendet wird, verwaltet das Windows-Betriebssystem das Kennwort für das Konto nicht die des Administrators das Kennwort zu verwalten.

Die Microsoft-Schlüsselverteilungsdienst \("kdssvc.dll"\) stellt den Mechanismus, um sicher zu den neuesten Schlüssel oder ein angegebener Schlüssel mit einer schlüsselkennung für ein Active Directory-Konto erhalten. Vom Schlüsselverteilungsdienst werden geheime Informationen zur Erstellung von Schlüsseln für das Konto bereitgestellt. Diese Schlüssel werden regelmäßig geändert. Für ein gruppenverwaltetes Dienstkonto berechnet der Domänencontroller das Kennwort für den Schlüssel von Key Distribution Services, zusätzlich zu anderen Attributen des gMSA bereitgestellt.  Die aktuellen und preceding Password Values erhalten-mitgliedshosts durch kontaktieren eines-Domänencontrollers.

## <a name="BKMK_APP"></a>Praktische Anwendungen
gMSAs bieten eine einzelidentitätslösung für Dienste, die in einer Serverfarm oder auf Systemen hinter einem Network Load Balancer ausgeführt. Indem Sie ein gMSA-Lösung verwenden, Dienste können so konfiguriert werden, für die neuen Gmsas Dienstprinzipal, und die kennwortverwaltung wird von Windows verarbeitet.

Verwendung eines gruppenverwalteten Dienstkontos, müssen Dienste oder Dienstadministratoren nicht die kennwortsynchronisierung zwischen Dienstinstanzen zu verwalten. Das gruppenverwaltete Dienstkonto unterstützt Hosts, die für einen längeren Zeitraum und die Verwaltung von mitgliedshosts für alle Instanzen eines Diensts offline gespeichert werden. Sie können also eine Serverfarm bereitstellen, die eine einzelne Identität unterstützt, gegenüber der sich vorhandene Clientcomputer authentifizieren können, ohne zu wissen, mit welcher Instanz des Diensts eine Verbindung hergestellt wird.

Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt werden, können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe oder gMSA oder sMSA systemeigen unterstützen.

## <a name="BKMK_SOFT"></a>Softwareanforderungen

Ein 64\--Bit-Architektur ist erforderlich, um die Windows PowerShell-Befehle ausführen, die zum Verwalten von gMSAs verwendet werden.

Ein verwaltetes Dienstkonto ist abhängig von Verschlüsselungstypen mit Kerberos-Unterstützung. Wenn sich ein Clientcomputer gegenüber einem Server per Kerberos authentifiziert, wird vom Domänencontroller ein Kerberos-Dienstticket erstellt, das mit einer Verschlüsselung geschützt ist, die sowohl vom Domänencontroller als auch vom Server unterstützt wird. Der Domänencontroller verwendet das Konto des MsDS\-SupportedEncryptionTypes-Attribut, um zu bestimmen, was das Server-Verschlüsselung unterstützt und, wenn kein Attribut vorhanden ist, es wird vorausgesetzt der Clientcomputer unterstützt keine sicherere Verschlüsselungsarten. Wenn der Host zur Unterstützung von RC4 nicht konfiguriert ist, schlägt die Authentifizierung immer fehl. Aus diesem Grund muss AES für verwaltete Dienstkonten immer explizit konfiguriert sein.

> [!NOTE]
> Ab Windows Server 2008 R2 ist DES standardmäßig deaktiviert. Weitere Informationen zu den unterstützten Verschlüsselungsarten finden Sie unter [Changes in Kerberos Authentication](https://technet.microsoft.com/library/dd560670(WS.10).aspx).

gMSAs gelten nicht für Windows-Betriebssysteme vor Windows Server 2012.

## <a name="server-manager-information"></a>Informationen zum Server-Manager
Es sind keine Konfigurationsschritte erforderlich, Implementieren von verwalteten Dienstkonten und gruppenverwaltetes Dienstkonto mithilfe von Server-Manager oder die Installation\-WindowsFeature-Cmdlets.

## <a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind Links zu weiterführenden Ressourcen im Zusammenhang mit verwalteten Dienstkonten und gruppenverwalteten Dienstkonten aufgeführt.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Neues für verwaltete Dienstkonten](what-s-new-for-managed-service-accounts.md)<br /><br />[Dokumentation zu Windows 7 und Windows Server 2008 R2 für gruppenverwaltete Dienstkonten](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[Dienstkonten Schritt\-von\-Schritt-Handbuch für](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**Planung**|Noch nicht verfügbar|
|**Bereitstellung**|Noch nicht verfügbar|
|**Betrieb**|[Verwaltete Dienstkonten in Active Directory](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Auswertung**|[Erste Schritte mit der Gruppe von verwalteten Dienstkonten](getting-started-with-group-managed-service-accounts.md)|
|**Tools und Einstellungen**|[Verwaltete Dienstkonten in Active Directory-Domänendienste](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**Communityressourcen**|[Verwaltete Dienstkonten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung](http://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**Verwandte Technologien**|[Übersicht über Active Directory-Domänendienste](active-directory-domain-services-overview.md)|


